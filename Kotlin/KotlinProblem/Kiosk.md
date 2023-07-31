//수정
- padding = " " repeat (가장 긴 이름의 길이 - name 길이)

- 번호 입력 받는 함수 따로 만듦 -> 예외처리 한번에

- let 함수 (null일 때와 null아닐 때 자동 구분)

- Food는 Menu 클래스 상속받아 자신만의 프로퍼티 만들고 Menu로 관리

- idx 값 넣어서 관리 : comparion object로 고유값 만듦

</br>

- fun isMaintainance() : Pair<Boolean, LocalDateTime> = 리턴 값 2개인 함수 사용

</br>

## Fold, Reduce 함수
### fold () 
- 리스트에 있는 값을 누적해서 더할 수 있음 (초기값 : 있음, 반환 값 : 초기값의 자료형)
- 빈 컬렉션에서 사용하면 오류 발생 X

### reduce ()
- 리스트에 있는 값을 누적해서 더할 수 있음 (초기값 없이 첫번째 요소부터 시작)
- total은 첫번째 element로 사용, num은 두번째 element로 사용
- 빈 컬렉션에서 사용하면 오류 발생 O

</br>

```

val numbers = listOf(7, 4, 8, 1, 9)

val sum = numbers.reduce { total, num -> total + num }
println("reduced: $sum") // reduced: 29

// total의 초기값은 10으로 시작한다.
val sumFromTen = numbers.fold(10) { total, num -> total + num }
println("folded: $sumFromTen") // folded: 39

```

</br>

- reduce : total은 첫번째 element로 사용, num은 두번째 element로 사용

```

val numbers = listOf(5, 2, 10, 4)

val doubledSum = numbers.reduce { total, num -> total + num * 2 }
println("reduced: $doubledSum") // reduced: 37 -> 원래는 42가 나와야 한다!!

val doubledSumFromZero = numbers.fold(0) { total, num -> total + num * 2 }
println("folded: $doubledSumFromZero") // folded: 42

```

</br>

- reduce : 빈 컬렉션에서 사용하면 오류 발생 O

```

val numbers = emptyList<Int>()

val sumFromTen = numbers.fold(10) { total, num -> total + num }
println("folded: $sumFromTen") // folded: 10

val sum = numbers.reduce { total, num -> total + num }
println("reduced: $sum") //UnsupportedOperationException

```

