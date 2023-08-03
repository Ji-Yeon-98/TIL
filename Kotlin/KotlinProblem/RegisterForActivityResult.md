## 1. RegisterForActivityResult

### 사용 이유

- 액티비티끼리 데이터를 주고받을 때 사용
- Activity or Fragment에 있을 때, 결과 콜백을 처리

</br>


### 사용 예제

- A 액티비티에서 -> B 액티비티로 이동
- B 액티비티에서 데이터 입력 받음
- B 액티비티에서 데이터를 A 액티비티로 콜백
- A 액티비티에서 B 액티비티가 넘겨준 값 확인

</br>


### 구조

```

public final <I, O> ActivityResultLauncher<I> registerForActivityResult(
    @NonNull ActivityResultContract<I, O> contract,
    @NonNull ActivityResultCallback<O> callback
) 

```

- registerForActivityResult : ActivityResultContract와 ActivityResultCallback을 인자로 가짐

- ActivityResultContract :  registerForActivityResult에서 반환된 ActivityResultLauncher가 어떤 행동을 할지를 결정하는 역할

- ActivityResultContracts.StartActivityForResult() : 다른 액티비티를 실행하고 해당 액티비티에서 결과를 받아오는 행동


- ActivityResultCallback : ActivityResultContract 실행 후 결과를 처리, 람다식 사용해서 더 간단하게 구현


</br>

### 사용 방법

</br>

- A Activity

```

val et_data = findViewById<EditText>(R.id.et_data)

// 두번재 인자 ActivityResultCallback 람다식으로 구현
val resultLauncher = registerForActivityResult(ActivityResultContracts.StartActivityForResult()) { result ->

    // resultCode : 액티비티 실행 결과 코드
    if (result.resultCode == Activity.RESULT_OK) {

        //B 액티비티에서 전달한 데이터 받아옴
        val data = result.data?.getStringExtra("CallBackData")

        et_data.setText(data)
    }
}


val btn = findViewById<Button>(R.id.btn)

btn.setOnClickListener {

    val intent = Intent(this, BActivity::class.java)

    //resultLauncher.launch() : 데이터를 받아올 Activity 실행
    resultLauncher.launch(intent)
}

```

</br>

- B Activity

```

intent.putExtra("CallBackData", "콜백하고 싶은 데이터")
setResult(RESULT_OK, intent)
finish()

```