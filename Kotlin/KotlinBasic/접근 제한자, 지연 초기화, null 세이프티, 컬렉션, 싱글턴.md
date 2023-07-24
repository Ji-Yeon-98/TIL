## 1. 접근 제한자

### 1) 정의

- 접근 :  객체를 이용해서 변수나 메소드를 호출할 수 있는 지의 여부
- 프로젝트 : 최상단 개념 <모듈, 패키지, 클래스>
- 모듈 : <패키지, 클래스> (app 모듈)
- 패키지 : < 클래스>

### 2) 종류

```
- public : 명시하지 않으면 기본적으로 public 입니다 (어디 서나 접근할 수 있어요)

- private : 동일한 클래스 내부에서만 접근할 수 있습니다

- internal : 같은 모듈 내부에서만 접근할 수 있습니다

- protected : 기본적으로 private이지만 상속을 받은 경우에 타 모듈에서 접근할 수 있습니다
```

### 3) 예시

- AccessTestClass

```kotlin
open class AccessTestClass {
		//외부에서 접근 가능
    public var a:Int = 1
    var b = 2
    //클래스 안에서만 사용 가능
    private var c = 3
    //같은 모듈 내부에서 접근 가능
    internal var d = 4
    //상속 받은 애만 접근 가능
    protected var e = 5

    public fun publicTest() {
        println("public ${c}입니다")
    }

    fun publicTest2() {
        println("public 입니다")
    }

    private fun privateTest() {
        println("private 입니다")
    }

    internal fun internalTest() {
        println("internal 입니다")
    }

    protected fun protectedTest() {
        println("protected 입니다")
    }
}

```

- AccessTestChildClass

```kotlin
class AccessTestChildClass: AccessTestClass() {

    fun protectedTest1() {
        println("e의 값은 ${e}")
    }
}
```

- test.kt

```kotlin
//fun main() {
//    var access = AccessTestClass()
//    access.a
//    access.b
//    access.d
//}

fun main() {
    var accessTestClass = AccessTestClass()
    var accessTestChildClass = AccessTestChildClass()

// . 하고 접근가능한 요소를 확인
//    accessTestClass.
    accessTestChildClass.protectedTest1() //e의 값은 5
}
```

</br>

## 2. 지연 초기화

### 1) 정의

- 클래스를 설계할 때 안정성을 위해 반드시 변수의 값을 초기화 할 것을 권장
- 초기의 값을 정의하기 난처해서 나중에 대입하기 위한 문법

### 2) 방법

- 변수 : lateinit 지연 초기화
- 상수 : lazy 지연 초기화

### 3) 변수 지연초기화 (lateinit)

```kotlin
fun main(){
    var s1 = Student()
    s1.name = "참새"
    s1.displayInfo()

    s1.age = 10
    s1.displayInfo()
}

class Student {
    //var name:String = ""
    lateinit var name:String
    var age:Int = 0

    fun displayInfo() {
        println("이름은: ${name} 입니다.")
        println("나이는: ${age} 입니다.")
    }
}
```

- isInitialized : 초기화 확인 (참조 형태로 사용 this:: or ::)

```kotlin
fun main(){
    var s1 = Student()
    s1.name = "참새"
    s1.displayInfo()

    s1.age = 10
    s1.displayInfo()
}

class Student {
    lateinit var name:String
    var age:Int = 0

    fun displayInfo() {
        if(this::name.isInitialized) {
            println("이름은: ${name} 입니다.")
            println("나이는: ${age} 입니다.")
        } else {
            println("name변수를 초기화해주세요.")
        }
    }
}
```

### 4) 상수 지연 초기화 (by lazy)

```kotlin
fun main(){
    var s1 = Student()
    s1.name = "참새"
    s1.displayInfo()
//    이름은: 참새 입니다.
//    나이는: 0 입니다.
//    address 초기화
//    주소는: seoul 입니다.

    s1.age = 10
    s1.displayInfo()

}

class Student {
    lateinit var name:String
    var age:Int = 0
    //사용할 때 초기화 됨
    val address: String by lazy {
        println("address 초기화")
        "seoul"
    }

    fun displayInfo() {
        println("이름은: ${name} 입니다.")
        println("나이는: ${age} 입니다.")
        println("주소는: ${address} 입니다.")
    }
}
```

</br>

## 3. NULL 세이프티

### 1) 정의

- Null 예외는 프로그램의 가용성을 저하시키는 치명적 오류
- 안전한 설계를 위해 자료형에 Null 여부 명시
- ?, !!, ?., ?: 사용

### 2) 예시

- 주소를 저장하는 address 변수는 null 저장 가능 : String? 선언

```kotlin
fun main(){
    var s = Student()
    s.name = "참새"
    s.address = "서울"
    s.displayInfo()
}

class Student {
    lateinit var name:String
    var address:String? = null
    
    fun displayInfo() {
        println("이름은: ${name} 입니다")
        println("주소는: ${address} 입니다")
    }
}
```

- 메소드를 호출하고 전달 받은 리턴 값이 null이 아님을 보증 : !! 사용

```kotlin
fun main(){
//  var data = readLine()!!.toInt()

    //변수 값이 반드시 null이 아님
    var inputData = readLine()!!
    var data = inputData.toInt()
    println("Null아닌 값: ${data}")
}
```

- Null인지 확인하고 Null이 아닐 때만 참조 : ?. (안전 호출 연산자) 사용

```kotlin
fun main(){
    var s = Student()
    s.name = "참새"
    s.displayAddressLength() //주소의 길이는: null 입니다

    s.address = "서울"
    s.displayInfo()
}

class Student {
    lateinit var name:String
    var address:String? = null

    fun displayInfo() {
        println("이름은: ${name} 입니다")
        println("주소는: ${address} 입니다")
    }

    fun displayAddressLength() {
        //address가 null인지 확인하고 null이면 null 호출, null 아닐 때 길이 호출
        println("주소의 길이는: ${address?.length} 입니다")
    }
}
```

- null이 출력 되지 않게 null 대신 다른 문자열 출력 :  ?: (엘비스 연산자) 사용

```kotlin
fun main(){
    var s = Student()
    s.name = "참새"
    s.displayAddressLength()

    s.address = "서울"
    s.displayInfo()
}

class Student {
    lateinit var name:String
    var address:String? = null

    fun displayInfo() {
        println("이름은: ${name} 입니다")
        println("주소는: ${address} 입니다")
    }

    fun displayAddressLength() {
        println("주소의 길이는: ${address?.length ?: "초기화하세요"} 입니다")
    }
}
```

</br>

## 4. 배열

### 1) 정의

- 변수에 순서를 매겨 연속적으로 활용
- arryOf 메소드(키워드) 제공

### 2) 예시

- 국어 점수를 배열로 묶어 모든 점수 출력

```kotlin
fun main() {
    var kors = arrayOf(90, 94, 96)
    // value와 index 두 개의 값을 묶어서 리턴
    for((idx, kor) in kors.withIndex()) {
        println("${idx}번째 국어 점수는 ${kor}입니다")
    }
}
```

</br>

## 5. 컬렉션

### 1) 정의

- 리스트, 맵, 집합 자료구조

### 2) LIst

- 리스트 : 읽기 전용 + 수정 가능한 리스트
- 배열과 달리 크기가 정해져 있지 않아 동적으로 값 추가 가능

```kotlin
// 읽기전용 리스트입니다
// 0번, 1번, 2번 인덱스에 접근해서 값을 변경할 수 없습니다
var scores1 = listOf(값1, 값2, 값3)

// 수정가능 리스트입니다
// 0번, 1번, 2번 인덱스에 접근해서 값을 변경할 수 있습니다
var scores2 = mutableListOf(값1, 값2, 값3)
scores2.set(인덱스, 값) //값 변경

// 수정가능 리스트입니다 (주로 사용)
// 0번, 1번, 2번 인덱스에 접근해서 값을 변경할 수 있습니다
// array로 데이터들을 저장하는 ArrayList도 mutableListOf와 동일하게 사용할 수 있어요
// 저장할 데이터의 자료형을 < > 안에 지정해야 사용할 수 있어요
var scores3 = ArrayList<자료형>(값1, 값2, 값3)
scores3.set(인덱스, 값)
```

### 3) Map

- 맵 : 키와 값이 쌍으로 이루어진 자료형
- 읽기 전용 + 수정 가능한 맵

```kotlin
// 읽기전용 맵입니다
    // 변수명[키]로 데이터에 접근할 수 있습니다
    var scoreInfo1 = mapOf("kor" to 94, "math" to 90, "eng" to 92)
    println(scoreInfo1["kor"])

    // 수정가능 맵입니다
    // 변수명[키]로 데이터에 접근할 수 있습니다
    var scoreInfo2 = mutableMapOf("kor" to 94, "math" to 90)
    scoreInfo2["eng"] = 92
    println(scoreInfo2["eng"])

    // 맵의 키와 값을 동시에 추출해서 사용할 수 있습니다
    for((k,v) in scoreInfo2) {
        println("${k}의 값은 ${v}입니다")
    }
```

### 4) Set

- 셋 : 순서 존재 X, 중복 없이 데이터를 관리하는 집합 자료형
- 읽기 전용 + 수정 가능한 셋
- 요소가 존재하는 지에 집중 (list, map은 요소를 찾는 데 집중)

```kotlin
//  읽기전용 Set입니다.
    var birdSet = setOf("닭", "참새", "비둘기")

//  수정가능 Set입니다.
//  var mutableBirdSet = mutableSetOf("닭", "참새", "비둘기")
//  mutableBirdSet.add("꿩")
//  mutableBirdSet.remove("꿩")
    println("집합의 크기는 ${birdSet.size} 입니다")

    var findBird = readLine()!!

    if(birdSet.contains(findBird)) {
        println("${findBird} 종류는 존재합니다.")
    } else {
        println("${findBird}는 존재하지 않습니다.")
    }
```

```kotlin
fun main() {
// 귀여운 새의 집합
    var birdSet = setOf("닭", "참새", "비둘기", "물오리")

    // 날수있는 새의 집합
    var flyBirdSet = setOf("참새", "비둘기", "까치")

    // 모든 새의 집합 (합집합) 닭, 참새, 비둘기, 물오리, 까치
    var unionBirdSet = birdSet.union(flyBirdSet)

    // 귀엽고 날수있는 새의 집합 (교집합) 참새, 비둘기
    var intersectBirdSet = birdSet.intersect(flyBirdSet)

    // 귀여운 새들중에서 날수없는 새의 조합 (차집합) 닭, 물오리
    var subtractBirdSet = birdSet.subtract(flyBirdSet)

    println("=====합집합=====")
    println("모든 새의 집합 : ${unionBirdSet}")

    println("=====교집합=====")
    println("귀엽고 날수있는 새의 집합 : ${intersectBirdSet}")

    println("=====차집합=====")
    println("귀엽고 날수없는 새의 집합 : ${subtractBirdSet}")
}
```

### 5) 최종 예시

- 학생 3명의 점수를 입력 받아 평균 점수를 출력

```kotlin
fun main() {
    var students = mutableListOf<Student>()
    var averages = mutableMapOf<String, Int>()

		//3번 반복
    for(idx in 0..2) {
        println("학생의 이름을 입력하세요")
        var name = readLine()!!

        println("국어 점수를 입력하세요")
        var kor = readLine()!!.toInt()

        println("수학 점수를 입력하세요")
        var math = readLine()!!.toInt()

        println("영어 점수를 입력하세요")
        var eng = readLine()!!.toInt()

        var average = (kor + math + eng) / 3
        var tempStudent = Student(name, kor, math, eng)

        students.add(tempStudent)
        averages[name] = average
    }

    for(student in students) {
        var average = averages[student.name]
        student.displayInfo()
        println("평균점수는 ${average} 입니다")
    }
}

class Student(name:String, kor:Int, math:Int, eng:Int) {
    var name:String
    var kor:Int
    var math:Int
    var eng:Int
    
    init {
        this.name = name
        this.kor = kor
        this.math = math
        this.eng = eng
    }

    fun displayInfo() {
        println("이름: $name")
        println("국어: $kor")
        println("수학: $math")
        println("영어: $eng")
    }
}
```

</br>

## 6. Single-expression function

### 1) 정의

- 하나의 메소드를 간결하게 표현
- 람다식

```kotlin
{매개변수1, 매개변수2... -> 
		코드
}
```

### 2) 예시

- 세 개의 숫자의 평균을 리턴해주는 함수

```kotlin
fun add(num1:Int, num2:Int, num3:Int) = (num1+num2+num3)/3

var add = {num1: Int, num2: Int, num3: Int -> (num1+num2+num3) / 3}
println("평균값은 ${add(10,20,30)}입니다")
```

</br>

## 7. 싱글턴

### 1) 정의

- 각각의 객체는 상이한 위치 정보를 가지고 있어서 저장하는 값도 객체마다 고유
- 싱글턴 활용하면 해당 객체는 메모리 전역에서 유일함 보장 + 위치 정보 고정

- companion, object 키워드로 구현

### 2) 사용 이유

- 전역적으로 활용 가능해 다른 클래스들에서 쉽게 접근 가능
- 메모리 더욱 효율적으로 활용
- 객체 자원 간의 충돌 방지

### 3) 예시

- 객체 생성하지 않고 클래스 정보에 접근 (생성자 호출 X)

```kotlin
fun main() {
    Bird.fly("참새")
}

object Bird {
    fun fly(name:String) {
        println("${name}가 날아요~")
    }
}
```

- 객체 생성하지 않고 클래스 정보에 접근 (생성자 호출 O)

```kotlin
fun main() {
    // trash와 같이 생성자에 매개변수 전달 가능
    var singletonObject1 = MySingletonClass.getInstance(trash = 1)
    singletonObject1.setNum(5)
    println("num값은: ${singletonObject1.getNum()}")

    // singletonObject2에서 num을 10으로 대입
    var singletonObject2 = MySingletonClass.getInstance(trash = 1)
    singletonObject2.setNum(10)

    // singletonObject1의 num이 10으로 출력됨
    // singletonObject1과 singletonObject2는 같은 객체를 공유하기 때문
    println("num값은: ${singletonObject1.getNum()}")

}

//생성자 외부에서 만들기 막아둠
class MySingletonClass private constructor() {
    private var num:Int = 0

		//싱글턴
		//object : 외부에서 객체화, 인스턴스화 하지 않고 실행
    **companion object** {
				//자체 객체 = null
        @Volatile private var instance: MySingletonClass? = null
        private var trash = 0

				//메소드를 통해 이미 생성된 클래스의 객체를 외부에서 가져가기 위한 코드
        fun getInstance(trash: Int): MySingletonClass {
            this.trash = trash
            // 외부에서 요청왔을때 instance가 null인지 검증
            if(instance == null) {
		            // synchronized로 외부 쓰레드의 접근을 막음
								// 쓰레드는 다음챕터에서 소개합니다!
		            // 쓰레드간의 객체상태 혼돈을 막기위해 사용한다고 이해해주세요
                synchronized(this) {
                    instance = MySingletonClass()
                }
            }
            return instance!!
            
//            엘비스연산자와 뒷장에서배울 scope function을 이용하면
//            아래와같이 더욱 직관적인 코드 작성이 가능합니다
//            return instance ?: synchronized(this) {
//                // also는 호출한 객체를 it으로 넘김
//                // instance가 null이라면 새로 생성하고 아니면 무시함
//                instance ?: MySigletonClass().also {
//                    instance = it
//                }
//            }
        }
    }
    fun setNum(num: Int) {
        this.num = num
    }

    fun getNum(): Int{
        return this.num
    }
}
```
