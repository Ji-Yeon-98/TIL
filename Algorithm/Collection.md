## 1. 매핑 함수

### forEach()
- 컬렉션의 모든 요소 반복하며 특정 작업 수행
- 반복 실행만!

```

//List
val numbersList = listOf(1, 2, 3, 4, 5)

numbersList.forEach { number ->
    println(number * 2)
}

```

</br>

### map() 
- 각 원소를 원하는 형태로 변환해서 새 컬렉션 만듦 
- 원소의 개수는 같고 원소의 값은 변환
- 반복 실행 후 결과 값 반환


```

// List
val list = listOf(1, 2, 3, 4, 5)
val mappedList = list.map { it * 2 }
println(mappedList) // [2, 4, 6, 8, 10]

```

```

// MAP
val map = mapOf("a" to 1, "b" to 2, "c" to 3)
val mappedMap = map.map { it.key to (it.value * 10) }.toMap()
println(mappedMap) // {a=10, b=20, c=30}

```

```

// 배열
val array = arrayOf(1, 2, 3, 4, 5)
val mappedArray = array.map { it + 1 }
println(mappedArray.toList()) // [2, 3, 4, 5, 6]

```


</br>

 ### mapIndexed() 

 - 인덱스와 값 둘 다 이용하여 조건을 주거나 새로운 값 생성

 ```
 
 // Set
 val numbers = setOf(1, 2, 3)
 println(numbers.mapIndexed{idx, value -> value * idx}) //[0, 2, 6]

 ```

 ```
 
// Map
 val map = mapOf("a" to 1, "b" to 2, "c" to 3)
val mappedMap = map.mapIndexed { idx, entry -> "${entry.key}*$idx" to (entry.value * idx) }.toMap()
println(mappedMap) // {a*0=0, b*1=2, c*2=6}
 
 ```

 </br>

 ### mapNotNull(), mapIndexedNotNull()

- 컬렉션의 각 요소 변환하여 새로운 컬렉션을 생성하지만 변환값 중에 null 제외 

 ```
 
 val numbers = setOf(1, 2, 3)
println(numbers.mapNotNull{if (it == 2) null else it * 3}) //[3, 9]
println(numbers.mapIndexedNotNull { idx, value -> if (idx == 0) null else value * idx }) //[2, 6]
 
 ```

</br>
</br>

 ## 2. 요소 함수

 ### contains()

- 컬렉션 타입의 데이터 중에 특정 데이터가 있는지 판단하는 함수 (true, false 반환)

```

val result = listOf(2, 5, 10, 8).contains(7)
println("contains test : $result") //contains test : false

```

 </br>
 </br>

 ## 3. 정렬함수

 ### reserved()
 - 데이터의 순서를 거꾸로 바꿀 때 사용

 ```

 listOf(1, 5, 2).reserved().forEach { println(it) } //2, 5, 1

 ```

 </br>

### sorted(), sortedDescending()
- 정렬을 목적으로 사용

```

listOf(1, 5, 2).sorted().forEach { println(it) } //1, 2, 5

```

</br>

### sortedBy(), sortedDescendingBy()

- 람다 함술르 대입할 수 있고 람다 함수의 결과 값을 대상으로 정렬

```

listOf(1, 3, 2).sortedBy { it % 3 }.forEach { println(it) } //3, 1, 2

```

</br>
</br>

## 4. 필터링 함수

### filter()
- 컬렉션 타입의 데이터 중 특정 조건에 만족한 데이터들을 반환
```

val map = mapOf<String, Int>("one" to 15, "two" to 5)
val result = map.filter { entry -> entry.value > 10 }.forEach{ println(it) } //one=15

```