## 1.  MutableList
- 요소를 추가, 제거, 변경 작업 수행 가능

- 배열 기반 or 링크드 리스트 등 다양한 방식 구현 가능

```

val mutableList: MutableList<Int> = mutableListOf(1, 2, 3, 4, 5)
mutableList.add(6) // 요소 추가
mutableList[2] = 10 //요소 수정
mutableList.removeAt(0) // 요소 제거

```

</br>

- 특정한 위치에 값 추가

```

val values = mutableListOf(4, 6, 8)
val item = 2
 
values.add(0, item)         //index, element
 
println(values)             // [2, 4, 6, 8]

```

</br>

## 2. ArrayList 

- 요소를 추가나 제거할 때 자동으로 크기 조정

- MustableList 중 ArrayList가 포함

```

val arrayList: ArrayList<Int> = arrayListOf(1, 2, 3, 4, 5)
arrayList.add(6) // 요소 추가
arrayList[2] = 10 //요소 수정
arrayList.removeAt(0) // 요소 제거

```

</br>

## 3. IntArray 

- int로 이루어진 배열, 크기 변경 X

- 요소 추가, 제거 변경 불가능

- 배열의 크기 변경할 필요 없고 요소를 읽기만 하는 간단한 작업에서 사용

```

val intArray: IntArray = intArrayOf(1, 2, 3, 4, 5)
val element = intArray[0]   // 요소 읽기
intArray.add(6)             // 컴파일 오류, 크기 변경 불가능


println(intArray.contentToString()) // 해시코드 -> 문자열 변환 출력

```

</br>

#### 확장 함수 plus()
- 요소 추가 X
- 새로운 배열 생성

```

var intArray = intArrayOf()

// intArray에 5를 추가한 새로운 IntArray 생성 (원래의 intArray 변경 X)
intArray = intArray.plus(5)

```

</br>

## 기타 : 유용한 메소드

#### reversedArray() : 배열 뒤집기

```

var numList:IntArray = intArrayOf(1, 2, 5, 5, 7)
println(numList.reversedArray().contentToString())

```