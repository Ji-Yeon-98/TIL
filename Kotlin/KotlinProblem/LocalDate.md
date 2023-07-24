## 1. 날짜 세팅

#### 


- 현재 날짜 가져오기 (LocalDate 자료형)

```

val todayDate = LocalDate.now()
println(todayDate) //yyyy-MM-dd

val todaytime = LocalDatetime.now()
println(todaytime) //yyyy-MM-ddTHH:mm:ss.sss

```

</br>

- String 자료형으로 변환

```

//원하는 날짜 형식을 지정하여 해당 표기형식으로 날짜 변경
val formatter = DateTimeFormatter.ofPattern("yyyyMMdd")

//current 상수 날짜 표기형식을 yyyyMMdd으로 바꿈
val today = current.format(formatter)
println(today) //20230721

```

</br>

- 입력받은 날짜 가져오기 (LocalDate 자료형)

```

val inputCheckInDate = readLine()

//원하는 날짜 형식을 지정하여 해당 표기형식으로 날짜 변경
val formatter = DateTimeFormatter.ofPattern("yyyyMMdd")
checkInDate = LocalDate.parse(inputCheckInDate, formatter)

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