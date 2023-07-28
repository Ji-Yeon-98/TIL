## 1. Map 컬렉션

### map.entries
- 주어진 map 항목을 Set<Map.Entry> 형태로 반환
- 키-쌍을 나타내는 인터페이스, 키와 값을 각각 가져옴
```

val myMap = mapOf("apple" to 1, "banana" to 2, "orange" to 3)

// key와 value를 사용하여 맵의 각 항목에 접근하여 처리
for ((key, value) in myMap.entries) {
    entry.setValue(entry.value * 2)
}

//조건에 따라 filtering
val filteredEntries = myMap.entries.filter { it.value > 1 }
println(filteredEntries) // 출력: [banana=2, orange=3]

```

</br>

### 요소 확인 : containsKey(key), containsValue(value) 
```

val map = mapOf("a" to 1, "b" to 2, "c" to 3)

// 키 "a"가 Map에 있는지 확인
val containsKey = map.contains("a")
println(containsKey) // true

// 값 2가 Map에 있는지 확인
val containsValue = map.containsValue(2)
println(containsValue) // true

// in 연산자를 이용하여 키 "c"가 Map에 있는지 확인
val keyExists = "c" in map
println(keyExists) // true

```

</br>
 
 ### 요소 변경 : mapKeys(), mapValues()

 - mapKeys() : 키 값 변경, value 유지
 - mapValues() : value 값 변경, key 유지

 ```

 val numbersMap = mapOf("key1" to 1, "key2" to 2, "key3" to 3, "key11" to 11)
 
println(numbersMap.mapKeys { it.key.uppercase() }) //uppercase() : 대문자로 바꾸기
//{KEY1=1, KEY2=2, KEY3=3, KEY11=11}

println(numbersMap.mapValues { it.value + it.key.length })
//{key1=5, key2=6, key3=7, key11=16}

 ```

</br>

 ### 최대값

 ```

 var maxValue: Int = Collections.max(map.values)

 //만약 map이 비어있다면 null 반환
 val maxEntry = myMap.maxByOrNull { it.value }
 
 ```

