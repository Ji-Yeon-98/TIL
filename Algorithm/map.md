## 1. Map

- map : 각 원소를 원하는 형태로 변환해서 새 컬렉션 만듦 (원소의 개수는 같고 원소의 값은 변환)

```

 val numbers = setOf(1, 2, 3)
 println(numbers.map{it*3}) //[3, 6, 9]

```


</br>

 - mapIndexed() : 인덱스와 값 둘 다 이용하여 조건을 주거나 새로운 값 생성

 ```
 
 val numbers = setOf(1, 2, 3)
 println(numbers.mapIndexed{idx, value -> value * idx}) //[0, 2, 6]

 ```

 </br>

 - mapNotNull(), mapIndexedNotNull() : null인 원소들은 포함하지 않는다.

 ```
 
 val numbers = setOf(1, 2, 3)
println(numbers.mapNotNull{if (it == 2) null else it * 3}) //[3, 9]
println(numbers.mapIndexedNotNull { idx, value -> if (idx == 0) null else value * idx }) //[2, 6]
 
 ```


 </br>

 #### Map 자료형 : mapKeys(), mapValues()

 - mapKeys() : 키 값 변경, value 유지
 - mapValues() : value 값 변경, key 유지

 ```

 val numbersMap = mapOf("key1" to 1, "key2" to 2, "key3" to 3, "key11" to 11)
 
println(numbersMap.mapKeys { it.key.uppercase() }) //uppercase() : 대문자로 바꾸기
//{KEY1=1, KEY2=2, KEY3=3, KEY11=11}

println(numbersMap.mapValues { it.value + it.key.length })
//{key1=5, key2=6, key3=7, key11=16}

 ```