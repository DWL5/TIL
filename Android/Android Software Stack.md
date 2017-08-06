### PackageName
Android Studio 에서 프로젝트를 만들 때, 
Package name은 플레이스토어에 올라온 모든 앱들과 일름이 달라야 한다.

### Min and Target Vesions
Project Structure > App > Flavors
Virsion Code : 이 앱의 버젼을 나타내는 숫자, 구글 플레이스토어와 기기에서 인식되는 숫자
여기서 최소 SDK 버전과 대상의 SDK 버전을 정할 수 있다.

### Android Software Stack
![Alt text](https://source.android.com/images/android_framework_details.png)

> 1. Linux Kernel
안드로이드는 리눅스 커널을 기반으로 저수준의 하드웨어 작동, 드라이버 그리고 전력관리등을 수행하는 풀스택 소프트웨어.
> 2. C++ 라이브러리(LibsC) SQLite 그리고 핵심 안드로이드 라이브러리

> 3. Application FrameWork

> 4. Application Layer

### Gradle
App : Gradle로 빌드된 바이트 코드와 외부 이미지, UI, XML등이 압축되어있는 APK를 통해 실행
> Android Proejct > Gradle을 통해 Build > Bytecode,Resource,Manifest > Sign (Jar Signer) > ADB를 통해 기기에 APK를 넣어줌
