## 1. 앱 구성 파일 분석

### 1) Gradle 빌드 설정 파일

- Gradle : 안드로이드 앱의 빌드 도구
- build.gradle : Gradle의 설정 파일
- build.gradle(Project:AndroidLab) : 프로젝트 수준
- build.gradle(Module:AndroidLab.app) : 모듈 수준

</br>

### 2) 매니페스트 파일

- 앱의 기본 특징 설명, 앱의 구성 요소인 컴포넌트(ex. activity, service)를 정의한 XML 파일

```kotlin
<?xml version="1.0" encoding="utf-8"?>
<manifest xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools">

    <application
        android:allowBackup="true"
        android:dataExtractionRules="@xml/data_extraction_rules"
        android:fullBackupContent="@xml/backup_rules"
        android:icon="@mipmap/ic_launcher" //앱 아이콘
        android:label="@string/app_name"   //앱 이름
        android:roundIcon="@mipmap/ic_launcher_round"
        android:supportsRtl="true"
        android:theme="@style/Theme.Lab6_doc"
        tools:targetApi="31">
        <activity                          //Application을 구성하는 컴포넌트 (Activity, Service, BroadcastReceiver)
            android:name=".MainActivity"   //액티비티 컴포넌트 이름
            android:exported="true">
            <intent-filter>                //앱을 시작할 때, 처음 수행되는 액티비티
                <action android:name="android.intent.action.MAIN" /> 

                <category android:name="android.intent.category.LAUNCHER" />
            </intent-filter>
        </activity>
    </application>

</manifest>
```

</br>

- **application 태그**
    - 컴포넌트 종류에 따른 태그
        - 액티비티의 경우<activity>요소
        - 서비스의 경우<service>요소
        - 브로드 캐스트 수신기의 경우<receiver>요소
        - 콘텐츠 제공자의 경우<provider>요소

</br>

- **activity 태그**
    - android : name 속성이 Activity 서브 클래스의 완전히 정규화된 클래스 이름 표현

</br>

- **intent-filter 태그**
    - 안드로이드 컴포넌트(ex. activity 태그) 하위에 포함되는 태그
    - 해당 컴포넌트가 수신할 수 있는 인텐트를 걸러내는 역할
    - MainActivity인 액티비티 컴포넌트가 앱을 시작 시키게 해주는 시작 점


</br>

### 3) 리소스 파일

- **리소스 파일**
    - 애플리케이션 리소스를 코틀린 코드에서 분리하여 독립적으로 유지
    - 다양한 환경 변화(ex. 화면 크기 변화, 사용 언어 변경)를 코드의 변경 없이 수용

</br>

- **리소스 폴더**
    - drawable : 이미지 리소스
    - layout : UI 구성에 필요한 XML 리소스
    - mipmap : 앱 아이콘 이미지
    - values : 문자열 등의 값으로 이용되는 리소스

</br>

- **주의**
    - res 하위 폴더 명은 지정된 폴더명 사용 (폴더 추가, 수정, 삭제 불가능)
    - 각 리소스 폴더에 다시 하위 폴더 정의 X
    - 리소스 파일 명에 알파벳 대문자 이용 X
    - File-based resource names must contain only lowercase a~z, 0~9, or underscore(_)

</br>

### 4) 코틀린 소스 파일

- **코틀린 소스 파일**
    - Android 앱은 코틀린 프로그래밍 언어로 작성

</br>

- **MainActivity.kt**
    
    ```kotlin
    package com.example.lab6_doc
    
    import androidx.appcompat.app.AppCompatActivity
    import android.os.Bundle
    import android.util.Log
    import android.widget.Button
    import android.widget.TextView
    import kotlin.random.Random
    
    class MainActivity : AppCompatActivity() {
        override fun onCreate(savedInstanceState: Bundle?) {
            super.onCreate(savedInstanceState)
            setContentView(R.layout.activity_main)
    
            val tv_num = findViewById<TextView>(R.id.tv_number)
            val btn_roll = findViewById<Button>(R.id.btn_roll)
    
            btn_roll.setOnClickListener {
    
                val random = Random
                //0~5 + 1 = 1~6 (0부터 시작)
                val num = random.nextInt(6) + 1
    
                tv_num.text = num.toString()
    
                Log.d("MainActivity", "num = ${num.toString()}")
            }
    
        }
    
    }
    ```
    

- **package** com.example.lab6_doc
    - MainActivity가 속한 패키지
    - 안드로이드 프로젝트 생성 시 설정된 이름

- **class MainActivity**
    - AppCompatActivity() : 안드로이드 액티비티는 Activity의 서브 클래스
    - AppCompatActivity : Activity의 서브 클래스로서 하위 플랫폼 버전을 지원

- **override fun** **onCreate** (savedInstanceState : Bundle?)
    - 안드로이드 플랫폼이 호출하는 메소드로서 액티비티가 생성되는 순간에 딱 한 번 호출됨
    - 주로 액티비티와 관련된 변수 초기화 및  사용자 인터페이스 설정 코드를 포함함

- **setContentView**(**R.layout**.activity_main)
    - R.layout.activity_main이 가리키는 리소스를 이 액티비티의 콘텐츠 뷰로 사용하겠다는 의미
    - R.layout.activity_main은 res/layout 폴더에 있는 activity_main.xml 가리키는 정적 상수

</br>
</br>

## 2. 프로젝트 빌드

### 1) 빌드 프로세스

- source code, resoure files  + 소스 코드 짤 때 사용했던 라이브러리 → 컴파일
- 컴파일 후 dex file, compiled resources 파일 됨

- apk packager 만들 때 키가 반드시 필요
    - release : 직접 생성, 마켓 올릴 때 만들어줌
    - debug : 안드로이드 스튜디오에서 자동 생성

- apk packager → zip 묶어서 확장자 .apk로 바꿈

</br>

### 2) build.gradle(Project level)

```kotlin
// Top-level build file where you can add configuration options common to all sub-projects/modules.
plugins {
    id 'com.android.application' version '8.0.2' apply false
    id 'com.android.library' version '8.0.2' apply false
    id 'org.jetbrains.kotlin.android' version '1.8.20' apply false
}
```

- 라이브러리 다운 받는 주소 지정

</br>

### 3) setting.gradle

```kotlin
include ':app'
```

- 어떤 모듈 포함할지

</br>

### 4) build.gradle(Module level)

```

plugins {
    id 'com.android.application'
    id 'org.jetbrains.kotlin.android'
}

android {
    namespace 'com.example.lab6_doc'
    compileSdk 33     //컴파일 시에 사용할 SDK 버전

    defaultConfig {
        applicationId "com.example.lab6_doc"
        minSdk 31     //앱이 지원하는 최소 API 버전
        targetSdk 33  //앱을 테스트하기 위해 사용할 API 버전  
        versionCode 1
        versionName "1.0"

        testInstrumentationRunner "androidx.test.runner.AndroidJUnitRunner"
    }

    buildTypes {
        release {
            minifyEnabled false
            proguardFiles getDefaultProguardFile('proguard-android-optimize.txt'), 'proguard-rules.pro'
        }
    }
    compileOptions {
        sourceCompatibility JavaVersion.VERSION_1_8
        targetCompatibility JavaVersion.VERSION_1_8
    }
    kotlinOptions {
        jvmTarget = '1.8'
    }
}

dependencies {

    //모듈 자체를 빌드하기 위해 요구되는 종속성 명세, 외부 저장소에서 해당 라이브러리 다운 받아와 빌드
    implementation 'androidx.core:core-ktx:1.8.0'
    implementation 'androidx.appcompat:appcompat:1.6.1'
    implementation 'com.google.android.material:material:1.5.0'
    implementation 'androidx.constraintlayout:constraintlayout:2.1.3'
    testImplementation 'junit:junit:4.13.2'
    androidTestImplementation 'androidx.test.ext:junit:1.1.5'
    androidTestImplementation 'androidx.test.espresso:espresso-core:3.5.1'
}

```