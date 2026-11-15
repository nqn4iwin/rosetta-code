# C 학습

Bash에서 `cd c` 후 실행한다.

## 빌드와 실행

```bash
make
./build/hello
```

예상 출력: `Hello, C!`

## 두 번째 예제 추가

`exercises/wordcount/main.c`를 만든다. Makefile의 all에 build/wordcount를 추가한다. build/hello 규칙을 복사해 소스와 대상의 hello를 wordcount로 바꾼다. 명령 들여쓰기는 탭이다. clean에도 새 산출물을 추가한다.

```bash
make
./build/wordcount
```

## 학습 지도

읽기 → 직접 구현 → 오류 입력 확인 → 자신의 말로 설명 순서로 진행한다.

1. 시작: C17 기준 컴파일·링크 구분, main, 타입, printf, 조건·반복·함수. 통과: 경고 없이 계산기 빌드.
2. 메모리 기초: 배열·문자열·포인터·주소·수명·스택과 동적 할당. 통과: 버퍼 길이를 명시한 문자열 처리.
3. 데이터와 구성: struct·enum, 헤더와 소스, 선언과 정의, 전처리기, 여러 소스 링크. 통과: 동적 배열을 별도 모듈로 분리.
4. 안전과 디버깅: malloc/realloc/free, 소유권 규칙, 미정의 동작, 정수 범위, 파일과 오류 코드, debugger 및 sanitizer. 통과: 파일 통계 도구의 오류 경로와 메모리 해제 검증.
5. 중급: 함수 포인터·콜백, 연결 리스트·해시 테이블 기초, Makefile, assert 기반 검사. 통과: 한 자료구조를 직접 구현하고 경계 조건 확인.
6. 시스템 기초: POSIX 파일·프로세스·TCP socket 개념. 표준 C와 Linux 전용 API를 구분한다. 종합: 길이 제한과 오류 처리가 있는 TCP echo 또는 파일 검색 도구.
