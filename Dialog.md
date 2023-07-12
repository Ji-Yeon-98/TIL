# 1. Dialog 값 입력받고 수정

### 1) Dialog 값 입력 받기

- TextField 사용
- _textEditingController : 편집이 가능한 TextField에 입력된 값을 가지고 오거나 입력된 값이 변경될 때 사용
- TextEditingController(text: ''); : 초기값 설정

```
TextEditingController _textEditingNameController =
        TextEditingController(text: plists['name']);

...
    child: TextField(
        controller: _textEditingNameController,
        textAlign: TextAlign.center,
        decoration:InputDecoration(hintText: "이름"),
        ),
```

</br>

### 2) 입력받은 값 수정

- 확인 버튼
- _textEditingController.text : 값을 text로 변경시켜 String 값으로 만듦
- updateProfile(content, value) : List를 수정하는 함수에 보내줌
- Navigator.pop(context) : 이전 페이지로 넘어감

```
    actions: <Widget>[
        MaterialButton(
            color: Colors.blue,
            textColor: Colors.white,
            child: Text("확인"),
            onPressed: () {
                nametext = _textEditingNameController.text;
                profileService.updateProfile(
                    content: "name", value: nametext);
                Navigator.pop(context);
            },
        )
    ],
```