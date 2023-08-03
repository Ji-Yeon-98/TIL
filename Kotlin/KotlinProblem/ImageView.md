## 이미지 넣기 (코드)

### setImageResource


- drawable 폴더 내 이미지
```

val iv1 = findViewById<ImageView>(R.id.iv1)
iv1.setImageResource(R.id.dog)

```

</br>

- Uri 이미지
```

val iv2 = findViewById<ImageView>(R.id.iv2)
iv2.setImageResource(Uri uri)

```

</br>
</br>

## 이미지 랜덤 넣기

- drawable 폴더 내 이미지

```

// 사진 경로 배열로 넣기
val img = arrayListOf<Int>(R.drawable.dog1_circle, R.drawable.dog2_circle, R.drawable.dog3_circle, R.drawable.dog4_circle, R.drawable.dog5_circle)

//imgsize 크기의 0부터 4사이의 랜덤값 불러오기 (Math.random : 0~1사이의 랜덤 소수점 값 불러옴)
var imageIndex = (Math.random() * img.size).toInt()

//이미지 띄우기
iv3.setImageResource(img[imageIndex])

```