# 1. 화면 분리해서 동작

### 1) Directionaltiy 위젯

- 언어 방향을 지정하는 위젯
- 최상위 위젯

```
class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: Directionality(
        textDirection: TextDirection.ltr, // 왼쪽에서 오른쪽 방향
        child: MyPage(),
      ),
    );
  }
}
```

</br>

### 2) 위 아래 위젯 나누기

- 위 아래 위젯 만들기
```
// 위쪽 부분을 구성하는 위젯 반환
Widget _buildUpperSection() {
    return Container(
      width: double.infinity,
      height: 100,
      color: Colors.black,
      child: Row(
        children: [
          TextButton(
            onPressed: () {
              setState(() {
                // 아래쪽 부분을 변경하기 위해 상태 변경
                selectedIndex = 0;
              });
            },
            child: Text(
              "TEXTButton",
              style: TextStyle(color: Colors.white),
            ),
          ),
          TextButton(
            onPressed: () {
              setState(() {
                // 아래쪽 부분을 변경하기 위해 상태 변경
                selectedIndex = 1;
              });
            },
            child: Text(
              "TEXTButton",
              style: TextStyle(color: Colors.white),
            ),
          ),
        ],
      ),
    );
  }

// 아래쪽 부분을 구성하는 위젯 반환
  Widget _buildLowerSection() {
    Widget content;
    if (selectedIndex == 0) {
      content = Container(
        width: double.infinity,
        color: Colors.green,
        child: Center(
            child: Column(
          children: [
            Text(
              '첫 번째 화면',
              style: TextStyle(
                color: Colors.white,
              ),
            ),
            SizedBox(
              height: 50,
            ),
            Container(
              width: double.infinity,
              height: 50,
              color: Colors.yellow,
            ),
          ],
        )),
      );
    } else {
      content = Container(
        width: double.infinity,
        color: Colors.yellow,
        child: Center(
            child: Text('두 번째 화면', style: TextStyle(color: Colors.black))),
      );
    }

    return Expanded(
      child: Container(
        color: Colors.white,
        child: content,
      ),
    );
  }
```

- 위아래 연결

```
@override
  Widget build(BuildContext context) {
    return Scaffold(
      body: Column(
        children: [
          _buildUpperSection(),
          _buildLowerSection(),
        ],
      ),
    );
  }
```
</br>

### 3) 최종 코드

```
import 'package:flutter/material.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: Directionality(
        textDirection: TextDirection.ltr, // 왼쪽에서 오른쪽 방향
        child: MyPage(),
      ),
    );
  }
}

class MyPage extends StatefulWidget {
  @override
  _MyPageState createState() => _MyPageState();
}

class _MyPageState extends State<MyPage> {
  int selectedIndex = 0;

  Widget _buildUpperSection() {
    // 위쪽 부분을 구성하는 위젯 반환
    return Container(
      width: double.infinity,
      height: 100,
      color: Colors.black,
      child: Row(
        children: [
          TextButton(
            onPressed: () {
              setState(() {
                // 아래쪽 부분을 변경하기 위해 상태 변경
                selectedIndex = 0;
              });
            },
            child: Text(
              "TEXTButton",
              style: TextStyle(color: Colors.white),
            ),
          ),
          TextButton(
            onPressed: () {
              setState(() {
                // 아래쪽 부분을 변경하기 위해 상태 변경
                selectedIndex = 1;
              });
            },
            child: Text(
              "TEXTButton",
              style: TextStyle(color: Colors.white),
            ),
          ),
        ],
      ),
    );
  }

  Widget _buildLowerSection() {
    // 아래쪽 부분을 구성하는 위젯 반환
    Widget content;
    if (selectedIndex == 0) {
      content = Container(
        width: double.infinity,
        color: Colors.green,
        child: Center(
            child: Column(
          children: [
            Text(
              '첫 번째 화면',
              style: TextStyle(
                color: Colors.white,
              ),
            ),
            SizedBox(
              height: 50,
            ),
            Container(
              width: double.infinity,
              height: 50,
              color: Colors.yellow,
            ),
          ],
        )),
      );
    } else {
      content = Container(
        width: double.infinity,
        color: Colors.yellow,
        child: Center(
            child: Text('두 번째 화면', style: TextStyle(color: Colors.black))),
      );
    }

    return Expanded(
      child: Container(
        color: Colors.white,
        child: content,
      ),
    );
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      body: Column(
        children: [
          _buildUpperSection(),
          _buildLowerSection(),
        ],
      ),
    );
  }
}

```