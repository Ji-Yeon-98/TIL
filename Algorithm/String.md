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
</br>

## 3. 문자열 자르기, 나누기, 분할

### substring

```

var my_string = "Hello World!"

println(my_string.substring(2)) //llo World!
println(my_string.substring(0,3)) //Hel

```
</br>

### split
```

var my_string = "Hello/World!/String*Split"

val split1 = my_string.split("/")                   //[Hello, World!, String*Split]
val split2 = my_string.split("/", "*")              //[Hello, World!, String, Split]
val split3 = my_string.split("/", limit = 2)        //[Hello, World!/String*Split]

```

</br>

### chunked
```

var my_string = "HelloWorld!"

val chunked1 = my_string.chunked(3) //[Hel, loW, orl, d!]
val chunked2 = my_string.chunked(4) //[Hell, oWor, ld!]

```