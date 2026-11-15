# Java 학습

Bash에서 `cd java` 후 실행한다.

## 빌드와 실행

```bash
mvn -B package
java -cp target/classes learning.hello.Main
```

예상 출력: `Hello, Java!`

## 두 번째 예제 추가

`src/main/java/learning/wordcount/Main.java`를 만든다. package learning.wordcount;와 public class Main을 작성한다. 서로 다른 package의 Main은 함께 컴파일된다.

```bash
mvn -B package
java -cp target/classes learning.wordcount.Main
```

## 학습 지도

읽기 → 직접 구현 → 오류 입력 확인 → 자신의 말로 설명 순서로 진행한다.

1. 시작: JDK, javac/java, 클래스·main, 타입·제어문·메서드·배열·String. 통과: 입력을 받는 계산기.
2. 객체 모델: 생성자·접근 제어·interface·상속과 합성·package·enum·record. 통과: 데이터와 처리 책임을 나눈 연락처 관리기.
3. 자료 처리: collections·generics, equals/hashCode, exception, try-with-resources. 통과: 중복을 처리하는 파일 기반 목록.
4. 함수형 표현과 I/O: lambda·Stream·Optional, NIO Path/Files, 날짜·시간. 통과: 파일 집계 도구.
5. 개발 도구: Maven의 의존성과 빌드 생명주기, JUnit 기초, debugger. 통과: 입력 오류와 컬렉션 경계 테스트.
6. 동시성과 네트워크: executor·future, 동기화·가시성, virtual thread 개념, HttpClient, TCP socket, timeout. 통과: 동시 URL 검사기.
7. 중급 종합: 저장 기능이 있는 CLI 또는 작은 HTTP 서비스. JVM의 메모리·GC 기초를 설명한다. Spring과 대형 웹 프레임워크는 필수 범위 밖이다.
