# Rust 학습

Bash에서 `cd rust` 후 실행한다.

## 빌드와 실행

```bash
cargo fmt --check
cargo check --all-targets --locked
cargo build --bins --locked
./target/debug/hello
```

예상 출력: `Hello, Rust!`

## 두 번째 예제 추가

`src/bin/wordcount.rs`를 만든다. fn main()을 작성한다. Cargo가 자동으로 찾는다. 의존성을 추가하면 Cargo.lock도 추적한다.

```bash
cargo run --bin wordcount
```

## 학습 지도

읽기 → 직접 구현 → 오류 입력 확인 → 자신의 말로 설명 순서로 진행한다.

1. 시작: Cargo, 변수·타입·함수·분기·반복, match. 통과: 명령줄 계산기.
2. 핵심: ownership·move·borrow, 참조·가변성·slice, String과 &str. 통과: 복사나 clone을 남발하지 않는 텍스트 분석기.
3. 모델링: struct·enum, Option·Result와 ?, 패턴 매칭, module·crate. 통과: 실패 원인이 구분되는 파일 파서.
4. 추상화: trait·generic·lifetime 기초, iterator·closure, Box·Rc·RefCell 용도. 통과: 자료형에 독립적인 작은 처리 함수와 수명 설명.
5. 품질: unit/integration/doc test, rustfmt·Clippy, 의존성·Cargo.lock. 통과: 경계 입력 테스트와 경고 확인.
6. 동시성과 네트워크: thread·channel·Arc·Mutex, Send/Sync 개념, TCP, async/await와 runtime 구분. Tokio 등은 이 단계에서 필요할 때 추가한다.
7. 중급 종합: 동시 URL 검사기 또는 파일 검색 CLI. 오류 전달·취소·자원 수명을 설명한다. unsafe는 읽기 수준의 선택 심화.
