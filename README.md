# 우편번호 검색 서비스 연동 모듈

iOS, Android 네이티브 앱에서 웹뷰로 다음 우편번호 서비스 연동을 하기 위한 wrapper입니다.

## Installation

### Hosted module 이용

네이티브 앱의 웹뷰에 아래 URL을 로딩합니다.

https://binaryrocket.github.io/postcode-search-integration/v1.0.0/

### docker를 이용한 운영 환경 실행

CDN을 이용하지 않고 직접 배포하고자 하는 경우 아래와 같이 `docker` 이미지를 빌드하고 컨테이너를 실행시킬 수 있습니다.

```bash
docker build -t postcode-integration .
docker run --name postcode-integration -p 8080:80 -d postcode-integration
```

### docker를 이용한 개발 환경 실행

`docker-compose.yaml` 파일이 위치한 디렉토리에 `.env.example` 파일을 참고하여 `.env` 파일을 작성하고, 아래와 같이 `docker compose`를 이용하여 이미지를 빌드하고 컨테이너를 실행합니다.

```bash
docker compose build
docker compose up
```

`.env` 파일에는 아래와 같이 바인딩할 HOST 포트 번호를 입력합니다.

```bash
PORT=8080
```

## Usage

### Android

`onSelect`, `onResize` 메서드가 구현된 `JavascriptInterface`를 생성하고, 이를 `Android`라는 명칭으로 웹뷰에 추가합니다.

#### Kotlin

```kotlin
// 인터페이스 생성
class WebAppInterface(private val mContext: Context) {
  @JavascriptInterface
  fun onSelect(data: String) {
    // 선택된 주소 데이터 처리
  }

  @JavascriptInterface
  fun onResize(data: String) {
    // 리사이징 처리
 }
}

// 웹뷰 인터페이스 추가
val webView: WebView = findViewById(R.id.webview)
webView.addJavascriptInterface(WebAppInterface(this), "Android")
```

#### Java

```java
// 인터페이스 생성
public class WebAppInterface {
  Context mContext;

  WebAppInterface(Context c) {
    mContext = c;
  }

  @JavascriptInterface
  public void onSelect(String data) {
		// 선택된 주소 데이터 처리
  }

  @JavascriptInterface
  public void onResize(String data) {
		// 리사이징 처리
  }
}

// 웹뷰 인터페이스 추가
WebView webView = (WebView) findViewById(R.id.webview);
webView.addJavascriptInterface(new WebAppInterface(this), "Android");
```

#### Flutter

```dart
onWebViewCreated: (controller) {
  // Javascript 핸들러 생성
  controller.addJavaScriptHandler(handlerName: 'onSelect', callback: (data) {
    // 선택된 주소 데이터 처리
  });

  controller.addJavaScriptHandler(handlerName: 'onResize', callback: (data) {
    // 리사이징 처리
  });
},
```

참고: https://developer.android.com/develop/ui/views/layout/webapps/webview

### iOS
