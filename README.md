# 개발 워크스테이션 구축

Windows의 WSL 2 Ubuntu에서 리눅스 CLI와 파일 권한을 실습했다. Docker Desktop으로 NGINX 웹 서버를 빌드하고, 포트 매핑과 두 가지 스토리지 연결 방식의 동작을 확인했다.

## 실행 환경

| 항목 | 환경 |
| --- | --- |
| 호스트 및 터미널 | Windows, Windows PowerShell 5.1 |
| 실습 환경 | WSL 2, Ubuntu 26.04.1 LTS, GNU Bash 5.3.9(1) |
| Docker | Docker Desktop WSL 2 백엔드, Docker CLI 및 Linux 엔진 29.9.3 |
| Git | Ubuntu Git 2.53.0 |

## 웹 서버 재현

Docker 엔진이 실행 중인지 `docker info`로 확인한 뒤, 저장소의 최상위 폴더에서 아래 명령을 실행한다. `8080`을 다른 프로세스가 사용 중이면 호스트 포트 `8080`과 접속 주소의 포트를 비어 있는 번호로 함께 바꾼다.

```bash
docker build -t workstation-web:1.0 .
docker run -d --name workstation-demo -p 127.0.0.1:8080:80 workstation-web:1.0
curl -fsS http://127.0.0.1:8080
```

```html
<h1>My Docker Workstation</h1>
```

[Dockerfile](Dockerfile)은 `nginx:alpine`을 기반으로 [직접 작성한 HTML](site/index.html)을 NGINX 문서 경로에 복사한다. 이미지에 파일을 포함하면 같은 이미지에서 실행한 컨테이너가 같은 페이지를 제공한다. 포트 매핑은 호스트에서 컨테이너의 웹 서버에 접속할 경로를 만든다.

## 수행 체크리스트와 검증 결과

- [x] [터미널 기본 조작](evidence/README.md#터미널-파일-및-디렉터리-조작)과 [권한 변경](evidence/README.md#파일과-디렉터리-권한-변경)
- [x] [Docker 설치와 엔진 점검, hello-world 실행](evidence/README.md#docker-설치와-동작-확인)
- [x] [Ubuntu 컨테이너 내부 접속](evidence/README.md#ubuntu-컨테이너-실행과-내부-접속)과 [운영 명령](evidence/README.md#docker-로그와-자원-사용량-중지-상태-확인)
- [x] [Dockerfile 빌드](evidence/README.md#nginx-커스텀-이미지-빌드)와 [포트 매핑·브라우저 접속](evidence/README.md#웹-컨테이너-실행과-포트-매핑)
- [x] [바인드 마운트 변경 반영](evidence/README.md#바인드-마운트-변경-반영)
- [x] [볼륨 영속성](evidence/README.md#docker-볼륨-영속성-확인)
- [x] [Git 초기화](evidence/README.md#git-저장소-초기화)와 [작성자 설정](evidence/README.md#git-커밋-작성자-설정)
- [x] [VS Code에서 WSL 과제 폴더 열기](evidence/README.md#vs-code에서-wsl-과제-폴더-열기)
- [ ] VS Code에서 GitHub 로그인 및 원격 저장소 연동

[실습 기록](evidence/README.md)에 명령별 목적, 실제 출력과 캡처, [트러블슈팅](evidence/README.md#트러블슈팅)을 정리했다.
