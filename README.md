# 우편번호 검색 서비스 연동 모듈

iOS, Android 네이티브 앱에서 웹뷰로 다음 우편번호 서비스 연동을 하기 위한 wrapper입니다.

## Installation

### CDN 배포본 이용

TODO: CDN 배포 후 URL 및 설치 방법 작성

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

TODO: 사용법 작성
