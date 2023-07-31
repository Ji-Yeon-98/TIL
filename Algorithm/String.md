## 1. 문자열 -> 배열

### toCharArray()
- String -> CharArray 변환
- 각 문자를 문자 배열로 변환하여 반환

```

val my_string = "Hello!"
var answer = ""


//foEach : 각 문자를 반복하면서 람다식 실행
my_string.toCharArray().forEach { i ->
    answer = i + answer
}

```

</br>

## 2. 리스트 -> 문자열

### joinToString

- 리스트의 원소들을 하나의 문자열로 만들기

```

val str = "ABC"
val ml = str.toMutableList()
println("ml.joinToString("")")                      //ABC
println(ml.joinToString("->", "start ", " end"))    //start A->B->C end

```

</br>
