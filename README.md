# Smart Recomposition
> NOW SOPT 7차 세미나 `성능 최적화` 실습입니다. (2024.5.25)

## ✨ Smart Recomposition이란?

- 성능 향상을 위해 **변경된 부분만 다시 그리는 과정**을 의미합니다.
- 이는 Compose는 **Stability 시스템**을 통해 **매개변수의 변경 여부**를 판단하며, 필요한 경우에만 리컴포지션을 수행합니다.


## 🛠️ 문제 상황 및 해결 방법

- 현재 `HomeScreen`에서는 Column 내에 리스트 상단에 컴포저블이 추가되면, 모든 컴포저블의 위치가 변경되면서 전체 리컴포지션이 발생할 수 있습니다.
- 하지만 `Layout Key`를 사용하여 각 아이템에 고유한 키를 부여하면 Compose가 **아이디 기반으로 컴포저블을 비교**하여, 변경된 아이템만 리컴포지션합니다.


```Kotlin
@Composable
fun ColumnScope.MemoList(memoList: SnapshotStateList<Memo>) {
    LazyColumn(
      ...
    ) {
        items(
            items = memoList,
            key = { memo -> memo.id } // Layout Key 추가!
        ) { memo ->
            ...
        }
    }
}
```
