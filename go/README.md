# Go 학습

Bash에서 `cd go` 후 실행한다.

## 빌드와 실행

```bash
go build ./...
go vet ./...
test -z "$(gofmt -l .)"
go run ./cmd/hello
```

예상 출력: `Hello, Go!`

## 두 번째 예제 추가

`cmd/wordcount/main.go`를 만든다. package main과 main 함수를 작성한다. 예제마다 폴더를 나눈다. 같은 폴더의 여러 소스는 함께 컴파일된다. test.go는 일반 소스이고 자동 테스트는 *_test.go다.

```bash
go run ./cmd/wordcount
```

## 학습 지도

읽기 → 직접 구현 → 오류 입력 확인 → 자신의 말로 설명 순서로 진행한다.

1. 시작: go run/build, package와 module, 변수·상수·기본 타입·조건·반복·함수. 통과: 숫자와 문자열을 입력받는 계산기.
2. 자료 표현: 배열·slice·map, struct, 포인터, 메서드, 문자열과 rune. 통과: 유니코드 텍스트 단어 빈도 집계.
3. 프로그램 구성: interface, error와 wrapping, defer, 파일 I/O, JSON, 패키지 분리, 제네릭 기초. 통과: 오류를 설명하는 파일 기반 명령줄 도구.
4. 품질: 표 기반 테스트, go test, benchmark 기초, go fmt/vet, 의존성 관리. 통과: 정상·빈 입력·잘못된 입력 검사.
5. 동시성: goroutine, channel, select, mutex, context 취소, race 탐지. 통과: 동시 작업 수가 제한되고 취소 가능한 작업 처리기.
6. 네트워크: TCP 스트림과 메시지 경계, UDP 데이터그램, DNS, HTTP 클라이언트·서버, JSON API, TLS 개념, timeout과 종료 처리. 통과: TCP echo와 HTTP API를 각각 작성하고 연결 실패·시간 초과 확인. WebSocket은 선택 심화.
7. 중급 종합: 제한된 동시 요청으로 URL 상태를 수집하는 도구. 본문 닫기, 취소, 종료, 테스트까지 설명한다.
