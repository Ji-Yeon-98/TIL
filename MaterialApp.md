## 1. No MaterialLocalizations found 오류

```
class MyApp extends StatelessWidget {
  const MyApp({Key? key}) : super(key: key);

  @override
  Widget build(BuildContext context) {
    return JiYeonPage(),
  }
}


class JiYeonPage extends StatefulWidget {
  const JiYeonPage({Key? key}) : super(key: key);

  @override
  State<JiYeonPage> createState() => _JiYeonPageState();
}

class _JiYeonPageState extends State<JiYeonPage> {
  @override
  Widget build(BuildContext context) {
    ProfileService profileService = context.read<ProfileService>();
    var plists = profileService.plists;

    return Consumer<ProfileService>(
      builder: (context, profileService, child) {
        return MaterialApp(
            return Scaffold(
                appBar: AppBar()
            );
        );    
      }
    );
  }
}

```

- MaterialApp을 가장 최상단에 두기
- MaterialApp 배치 변경

```
class MyApp extends StatelessWidget {
  const MyApp({Key? key}) : super(key: key);

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      debugShowCheckedModeBanner: false,
      home: JiYeonPage(),
    );
  }
}

class JiYeonPage extends StatefulWidget {
  const JiYeonPage({Key? key}) : super(key: key);

  @override
  State<JiYeonPage> createState() => _JiYeonPageState();
}

class _JiYeonPageState extends State<JiYeonPage> {
  @override
  Widget build(BuildContext context) {
    ProfileService profileService = context.read<ProfileService>();
    var plists = profileService.plists;

    return Consumer<ProfileService>(
      builder: (context, profileService, child) {
        return Scaffold(
            appBar: AppBar()
        );
      }
    );
  }
}

```

</br>


## 2. Providers 사용법

1. flutter pub add provider 터미널 입력

</br>

2. ChangeNorifier 클래스 상속받아 notifylisteners() 호출하여 위젯 갱신

```
import 'package:flutter/material.dart';

import 'main.dart';

class Provider {
  Provider({
    required this.content, //변수 설정
  });

  String content;
}

// Memo 데이터는 모두 여기서 관리
class ProviderService extends ChangeNotifier {
  var List = [];
}
```
</br>

3. Provider 패키지 설정

- 모든 위젯 최상단에 provider 등록
```
runApp(
    MultiProvider(
      providers: [
        ChangeNotifierProvider(create: (context) => ProviderService()),
      ],
      child: const MyApp(),
    ),
  );
```

</br>

4. Provider 적용
- Cusomer<클래스 이름> : 클래스 정보 갱신시 함께 새로고침 할 때 사용
- builder: (context, providerService, child) { return 위젯; } : 화면에 보여줄 위젯을 반환하는 함수

```
Cusomer<ProviderService>(
	builder: (context, providerService, child) { 
		//providerService 라는 변수에 ProviderService 를 담아서 쓸 수 있습니다.
        var list = providerService.List;
		return 위젯;
	}
)
```

- 다른 class에서 Provider 접근
- 변수나 함수만 이용

```
ProviderSerivce providerService = context.read<ProviderService>();
```

