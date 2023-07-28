## 1. 날짜 세팅

#### 

- LocalDate (LocalDate 자료형)

```

val date: LocalDate = LocalDate.of(2021, 1, 26)

//문자열 입력
val dateParse: LocalDate = LocalDate.parse("2023-07-28")

//문자열, format 형식
val dateParseWithFormatter: LocalDate = LocalDate.parse("2023-07-28", formatter)

```

</br>

- 현재 날짜 가져오기 

```

val todayDate: LocalDate = LocalDate.now()
println(todayDate) //yyyy-MM-dd

val todaytime = LocalDatetime.now()
println(todaytime) //yyyy-MM-ddTHH:mm:ss.sss

```

</br>

- 값 읽기

```

val date: LocalDate = LocalDate.of(2023, 7, 28)

val year:Int = date.getYear()

val monthInstance:Month = date.getMonth()   //July
val month:Int = monthInstance.getValue()    //7

val day:Int = date.getDayOfMonth()

```

</br>

- 표기 형식 변경 (String 자료형)

```

//원하는 날짜 형식을 지정하여 해당 표기형식으로 날짜 변경
val formatter = DateTimeFormatter.ofPattern("yyyyMMdd")

//current 상수 날짜 표기형식을 yyyyMMdd으로 바꿈
val today: String = current.format(formatter)
println(today) //20230721

```

</br>

- 입력받은 날짜 가져오기 (LocalDate 자료형)

```

val inputCheckInDate = readLine()

//원하는 날짜 형식을 지정하여 해당 표기형식으로 날짜 변경
val formatter = DateTimeFormatter.ofPattern("yyyyMMdd")
val checkInDate: LocalDate = LocalDate.parse(inputCheckInDate, formatter)

```

</br>
</br>

## 2. 날짜 비교 (LocalDate 자료형)

- is After
```

if (checkInDate.isAfter(current)) {
    println("${chekcInDate}가 ${current} 보다 날짜가 더 미래입니다.")
} else {
    println("${chekcInDate}가 ${current} 보다 날짜가 더 과거입니다.")
}

```

</br>

- is Before

```

if (checkInDate.isBefore(current)) {
    println("${chekcInDate}가 ${current} 보다 날짜가 더 과거입니다.")
} else {
    println("${chekcInDate}가 ${current} 보다 날짜가 더 미래입니다.")
}

```

</br>

- is Equal

```

if (checkInDate.isEqual(current)) {
    println("${chekcInDate}가 ${current}와 날짜가 같습니다.")
} else {
    println("${chekcInDate}가 ${current}와 날짜가 같지않습니다.")
}

```

</br>
</br>

## 3. 시간 세팅

- LocalTime
```

val time: LocalTime = LocalTime.of(2023, 07, 28)
val timeParse: LocalTime = LocalTime.parse("19:30:20")
val timeParseWithFormatter: LocalTime = LocalDate.parse("19:30:20", formatter)

```

</br>

- 현재 날짜 가져오기 

```

val timeNow: LocalTime = LocalTime.now()

```

</br>

- 값 읽기

```

val time: LocalTime = LocalTime.of(19, 30, 20)

val hour:Int = time.getHour()
val minute:Int = time.getMinute()
val second:Int = time.getSecond()

```