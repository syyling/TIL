### 시나리오: 상품 업데이트 후 캐시 무효화

```typescript
interface UpdateProductRequest {
  productId: string;
  name: string;
  price: number;
}

export const useUpdateProduct = (options?: MutationOptions<unknown, UpdateProductRequest>) => {
  return useMutation(updateProduct, options); // API 요청 처리
};
```
- useUpdateProduct 훅은 상품 업데이트 API 요청만 처리하는 기본적인 mutation 훅

```typescript
interface UseUpdateProductWithInvalidationParams {
  productId: string;
  name: string;
  price: number;
  onSuccess?: () => void;
  onError?: () => void;
}

export const useUpdateProductWithInvalidation = ({
  productId,
  name,
  price,
  onSuccess,
  onError,
}: UseUpdateProductWithInvalidationParams) => {
  const queryClient = useQueryClient();
  const { mutate: updateProductMutate, isPending } = useUpdateProduct();

  const updateProductHandler = (): void => {
    updateProductMutate(
      { productId, name, price },
      {
        onSuccess: () => {
          // 상품 정보 업데이트 후 캐시 무효화
          queryClient.invalidateQueries({ queryKey: ['product', productId] });

          // 성공 시 후속 작업 처리
          if (isFunction(onSuccess)) onSuccess();
        },
        onError: () => {
          // 실패 시 후속 작업 처리
          if (isFunction(onError)) onError();
        },
      }
    );
  };

  return { mutate: updateProductHandler, isPending };
};
```
- useUpdateProductWithInvalidation 훅은 상품을 업데이트한 후, 해당 상품에 대한 캐시 무효화를 담당
  캐시 무효화 후에는 성공/실패 콜백을 컴포넌트에서 전달받아 후속 작업을 처리
```typescript
const UpdateProductButton = ({ productId }: { productId: string }) => {
  const { mutate, isPending } = useUpdateProductWithInvalidation({
    productId,
    name: "새로운 상품 이름",
    price: 10000,
    onSuccess: () => {
      console.log("✅ 상품 정보 업데이트 성공!");
    },
    onError: () => {
      console.error("❌ 상품 정보 업데이트 실패...");
    },
  });

  return (
    <button onClick={mutate} disabled={isPending}>
      {isPending ? "업데이트 중..." : "상품 업데이트"}
    </button>
  );
};
```
- 컴포넌트에서는 useUpdateProductWithInvalidation 훅을 사용해서, 상품 업데이트 버튼을 클릭할 때 상품 정보가 업데이트되고,
그 후에 성공 시와 실패 시 처리할 로직을 onSuccess, onError를 통해 넘겨줌
- 후속 작업을 컴포넌트에서 쉽게 처리할

### 흐름
1. useMutation을 사용하여 기본 API 요청을 처리
2. mutationWithInvalidate 같은 커스텀 훅을 만들어 후처리 로직을 외부로 위임
3. onSuccess와 onError 콜백을 사용하여 후속 작업을 컴포넌트에서 처리
4. 쿼리 무효화, 캐시 관리와 같은 추가적인 작업은 커스텀 훅 내에서 처리
5. 책임 분리로 코드가 깔끔하고 유지보수가 쉬워짐

### 효과
- 책임 분리: API 요청과 후속 작업(예: 캐시 무효화, 콜백 처리)을 분리하여 각 부분이 명확한 역할을 담당
- 유지보수성 향상: 후속 작업을 컴포넌트에서 유연하게 처리할 수 있어 코드 변경이나 확장이 용이
- 가독성 향상: 코드가 간결하고 이해하기 쉽게 분리되어 있어 유지보수가 쉬움
- 재사용성 향상: mutation 훅을 여러 컴포넌트에서 재사용할 수 있어 코드 중복을 줄일 수 있음
- 확장성 향상: 후속 작업 로직을 쉽게 확장할 수 있어 기능 추가가 용이
- 일관된 에러 처리: onSuccess와 onError 콜백을 사용해 에러 처리를 일관되게 관리
- 테스트 용이성: 각 로직이 분리되어 있어 단위 테스트가 용이
- 데이터 일관성 유지: 쿼리 무효화
