## 1. Coroutine

#### Thread 차이점
- Coroutine은 Thread와 함께 사용
- Coroutine은 코드를 실행 중일 때 멈출 수 있고 다시 실행할 수 있는 제어 능력 가짐
- 스레드를 옮겨다니며 작업 가능


</br>

#### 작업 순서

- delay : 특정 스레드만 중단, 다른 스레드 정상 작동

```

//안드로이드 스튜디오 작동 X, JVM 환경에서는 스레드 기다리지 X 
fun main(){

    var job = GlobalScope.launch(){
        delay(3000)
        println("thread1")
    }

    println("thread2")
}

```

- thread2 출력되고 3초 뒤 thread1 출력
- thread2이 delay 상태에 들어갔을 때 thread2 뒤에서 실행



</br>
</br>

## 2. Run Blocking

#### 특징

- 호출한 위치를 Blocking 시킴

- 내부의 응답이 종료되기 전까지 응답 X

- 비동기가 아닌 동기화로 동작

</br>

#### 예시

```

fun main(){
    thread (true){
        println("thread1")
        runBlocking {
            launch {
                println("coroutine")
            }
        }
        println("thread out")
    }

    thread (true){
        println("thread2")
    }
}


//출력값
thread1
thread2
coroutine
thread out

```
</br>

```
1. thread 함수 사용하여 새로운 백그라운드 스레드 생성, thread1과 thread2 동시 실행

2. thread 함수 내부에서 runBlocking 함수 호출하여 thread1 블로킹

3. runBlocking 함수 내부의 코틀린 완료될 때까지 기다림

4. run Blocking 함수 내부에서 실행된 코루틴은 thread1만 블로킹, 다른 코루틴은 동시 실행
```

</br>

### runBlocking 쓰는 이유

- sleep과 똑같은 결과물
- runBlocking 안에 다른 스레드 실행 가능

```

//sleep
fun main(){
    println("Befor Sleep")
    sleep(2000)
    println("After Sleep")
}

//runBlocking - delay
fun main(){
    println("Befor Sleep")
    runBlocking {
        delay(2000)
    }
    println("After Sleep")
}

```

```

// runBlocking 안에 있는 코루틴 동시 실행 (동시 출력)
fun main(){
    println("Befor Sleep")
    runBlocking {
        launch {
            delay(2000)
            println("2초 1")
        }
        launch {
            delay(2000)
            println("2초 2")
        }
    }
    println("After Sleep")
}

```

</br>
</br>

## 3. Join & Cancel

### Join
- job.join이 끝날 때까지 현재 코루틴에게 기다리라고 명령하는 함수

```

fun main(){

    var job = GlobalScope.launch(){
        delay(3000)
        println("thread1")
    }

    runBlocking {
        job.join()
        println("thread2")
    }

    println("thread3")
}


//출력값
thread1
thread2
thread3

```
- GlobalScope 코루틴 실행 + runBlocking으로 Main 스레드 중지 (thread3 출력 X)
- runBlocking에서 job.join() 함수로인해 GlobalScope 코루틴 실행 끝날 때까지 기다림
- GlobalScope 코루틴 실행 (thread1 출력) 후 종료 -> runBlocking 실행 (thread2 출력) 후 종료 -> Main 스레드 실행

</br>

```

//JVM 환경 아니라고 가정
fun main(){

    var job = GlobalScope.launch(){
        delay(3000)
        println("thread1")
    }

    runBlocking {
        println("thread2")
    }

    println("thread3")
}

//출력값
thread2
thread3
thread1

```
- GlobalScope 코루틴 실행 + runBlocking으로 Main 스레드 중지
- delay로 인해 runBlocking 코루틴 먼저 실행(thread1)
- rurunBlocking 종료 후 MainThread 실행(thread3)
- delay 후 GlobalScope 코루틴 실행(thread1)

</br>

### Cancel

- 현재 진행 중인 코루틴 멈춤

```

fun main(){

    var job = GlobalScope.launch(){
        for (i in 0 until 5){
            println("thread1")
            delay(1000)
        }
    }

    runBlocking {
        delay(2000)
        job.cancel()
        println("thread2")
    }
}

//출력값
thread1
thread1
thread2

```

- job : 1초에 1번 반복
- runBlocking : delay 2초 후 job 끝냄


</br>

#### CoroutineScope 사용 시 정리 필요

```

fun main(args: Array<String>) {
    println("메인쓰레드 시작")
    var job = CoroutineScope(Dispatchers.Default).launch {
        delay(3000)
        println("여기는 코루틴...")
    }
    runBlocking {
        job.join()
    }
    println("메인쓰레드 종료")
		job.cancel() //CoroutineScope 사용 후 정리 필요
}

```

</br>

#### 문제점
- coroutine 안에 계산하는데 복잡하고 오래 걸리는 작업있으면 cancel 명령 전달 못받음

```

class MainActivity : AppCompatActivity() {

    val TAG = "MainActivity"

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)

        val job = GlobalScope.launch(Dispatchers.Default) {
            Log.d(TAG,"Starting long running calculation")
            for(i in 30..40){
                Log.d(TAG, "Result for i = $i : ${fib(i)}")

            }
            Log.d(TAG, "Ending Long running calculation")

        }

        runBlocking {

            delay(2000L)
            job.cancel()
            Log.d(TAG,"job canceled")
        }

    }

    fun fib(n:Int): Long{
        return if(n==0) 0
        else if(n ==1) 1
        else fib(n - 1)+ fib (n-2)
    }
}

```

</br>

#### 해결방법

- withTimeout : 안에 있는 함수가 정해진 시간보다 오래 걸릴 경우 cancel 시키는 함수

```

val job = GlobalScope.launch(Dispatchers.Default) {
            Log.d(TAG, "Starting long running calculation")
            withTimeout(3000L) {
                for (i in 30..40) {
                    if (isActive) {
                        Log.d(TAG, "Result for i = $i : ${fib(i)}")
                    }

                }
            }

            Log.d(TAG, "Ending Long running calculation")

        }

        runBlocking {

            delay(2000L)
            job.cancel()
            Log.d(TAG, "job canceled")
        }

```