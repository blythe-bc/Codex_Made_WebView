# Codex Made WebView

안드로이드용 사내 포털(WebView) 클라이언트 예제 프로젝트입니다. Kotlin과 Jetpack Compose를 기반으로 하며, 로그인 화면, 웹뷰, 바코드 스캔, 사진 촬영 및 전송 워크플로를 포함합니다. 백엔드 연동은 실제 서버 API에 맞춰 별도 구현이 필요합니다.

## 주요 기능

- **로그인 화면**: 간단한 폼과 유효성 검사를 제공하며, 뷰모델에서 추후 실제 인증 API로 교체할 수 있는 구조입니다.
- **웹뷰**: 사내 인트라넷 URL을 Android WebView로 로드합니다. `INTRANET_URL` 상수를 원하는 주소로 수정하세요.
- **바코드 스캔**: ZXing Embedded 라이브러리를 사용하여 다양한 포맷의 바코드를 읽어옵니다.
- **사진 촬영 및 전송 준비**: 카메라 권한을 요청하고 FileProvider를 통해 이미지를 촬영·저장합니다. 촬영된 이미지는 미리보기와 함께 업로드 버튼이 제공되며, 현재는 모의 업로드(Progress UI만)로 구성되어 있습니다.

## 프로젝트 구조

- `MainActivity` 및 `MainViewModel`: 전역 UI 상태와 내비게이션 담당
- `ui/login`: 로그인 화면 Compose UI
- `ui/webview`: 웹뷰 화면 및 바코드/카메라 기능 UI
- `util/ImageCaptureUtils`: FileProvider를 통한 임시 이미지 URI 생성 헬퍼
- `ui/theme`: Material3 테마 설정

## 빌드 및 실행

1. Android Studio (Giraffe 이상) 혹은 최신 버전의 Android Gradle Plugin이 설치된 환경을 사용하세요.
2. 프로젝트를 열면 Gradle Wrapper가 자동으로 필요한 도구를 다운로드합니다. (Wrapper JAR이 누락되어 있다면, 로컬 Gradle에서 `gradle wrapper` 명령으로 재생성할 수 있습니다.)
3. 최소 SDK 24, Target SDK 34에 맞춰 프로젝트가 설정되어 있습니다.
4. 앱을 실행하면 로그인 화면이 나타나며, 임의의 ID/비밀번호 입력 후 로그인하면 웹뷰 화면으로 이동합니다.

## 권한 및 보안

- 카메라 권한(`android.permission.CAMERA`)이 필요합니다. 최초 촬영 시 권한을 요청합니다.
- FileProvider를 통해 캐시 디렉터리에 이미지를 저장합니다. 실제 업로드 시에는 HTTPS 통신과 적절한 인증을 적용하세요.

## 커스터마이징 팁

- **백엔드 연동**: `MainViewModel.authenticate`와 `onUploadRequested`에 있는 모의 지연/상태 코드를 실제 네트워크 호출로 교체하세요.
- **인트라넷 주소**: `ui/webview/IntranetWebViewScreen.kt`의 `INTRANET_URL` 상수를 수정하세요.
- **스캔 옵션**: `ScanOptions` 설정을 통해 특정 바코드 포맷만 허용하거나 UX를 조정할 수 있습니다.

## 라이선스 고지

이 프로젝트는 예제로 제공되며, 회사 정책에 맞게 수정하여 사용하세요.
