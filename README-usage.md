# 독학 환경 사용 안내

Go, C, Rust, Java, Haskell을 한 언어씩 배우는 저장소다. 각 언어 폴더의 README에 단계와 통과 기준을 적었다. 예제는 직접 추가한다.

## Codespaces 시작과 재생성

GitHub 저장소에서 Code → Codespaces → Create codespace를 선택한다. 개발 컨테이너(dev container)는 `.devcontainer/Dockerfile`에 정의한 Linux 도구를 설치한다. 최초 설치는 다운로드와 GHC 설치 때문에 오래 걸릴 수 있다.
VS Code 명령 팔레트의 `Codespaces: Rebuild Container`로 설정 변경을 반영한다. 로컬 Dev Containers에서는 `Dev Containers: Rebuild Container`를 사용한다.
로컬 VS Code의 Codespaces 확장으로 접속하면 편집 화면은 로컬이고 컴파일은 원격이다. 로컬 clone을 열어 편집하는 방식과 구분한다.

## 도구 버전

Codespaces와 CI는 같은 Dockerfile을 빌드한다. Linux x86-64를 기본 대상으로 한다.

| 도구 | 선택 버전 |
|---|---|
| Go | 1.27.4 |
| Rust | stable 1.100.0, edition 2024 |
| GHC / Cabal | 9.12.4 / 3.16.0.0 |
| GCC / C 표준 | GCC 13.3.0 / C17 |
| Java | Temurin JDK 25.0.4+7, 장기 지원판(LTS) |
| Maven / Make | Ubuntu 24.04 제공 3.8.7 / 4.3 |
| GitHub Action | actions/checkout v7 |

GCC·Maven·Make의 배포판 패치 버전은 보안 업데이트에 따라 바뀐다. `gcc-13 --version`, `mvn -version`, `make --version`으로 확인한다. 도구 버전을 올릴 때 Dockerfile과 이 표를 함께 갱신한다. Rust는 `rust/rust-toolchain.toml`도 맞춘다.
설치 근거: [Go 배포 목록](https://go.dev/dl/), [Rust 안정 릴리스](https://blog.rust-lang.org/releases/latest/), [GHCup 설치](https://www.haskell.org/ghcup/install/), [GHC 배포](https://downloads.haskell.org/~ghc/9.12.4/), [Cabal 배포](https://downloads.haskell.org/~cabal/cabal-install-3.16.0.0/), [Temurin 지원](https://adoptium.net/support/), [checkout 사용법](https://github.com/actions/checkout). 개인 학습 자료는 별도로 관리한다.

## 빌드와 실행

아래 명령은 Codespaces의 Bash에서 저장소 루트를 기준으로 실행한다. 각 줄은 해당 언어 폴더로 이동한 뒤 수행해도 된다.

| 언어 | 빌드 | 실행 | 출력 |
|---|---|---|---|
| Go | `cd go && go build ./...` | `go run ./cmd/hello` | `Hello, Go!` |
| Rust | `cd rust && cargo build --bins --locked` | `cargo run --bin hello --locked` | `Hello, Rust!` |
| Haskell | `cd haskell && cabal update && cabal build all` | `cabal run hello` | `Hello, Haskell!` |
| C | `cd c && make` | `./build/hello` | `Hello, C!` |
| Java | `cd java && mvn -B package` | `java -cp target/classes learning.hello.Main` | `Hello, Java!` |

별도 언어를 실행하려면 저장소 루트로 돌아온다. Cabal과 Cargo의 실행 명령에는 도구 안내 출력이 함께 보일 수 있다. 두 번째 예제 추가법은 각 언어 README를 따른다.

## Git으로 작업 옮기기

remote 연결은 자동 동기화가 아니다. 로컬 작업을 먼저 저장하고 아래 순서로 옮긴다. `main` 대신 실제 작업 브랜치명을 사용한다.

```bash
git status
git add README.md README-usage.md .gitignore .devcontainer .github go rust haskell c java
# 저장소 규칙에 맞는 제목과 한국어 본문 세 문단으로 커밋한다.
git commit
git push origin main
```

Codespaces에서 `git status`로 미커밋 작업이 없는지 확인하고 `git pull --ff-only origin main`을 실행한다. 반대 방향은 Codespaces에서 commit/push한 뒤 로컬에서 pull한다. 충돌이나 분기가 생기면 덮어쓰지 말고 양쪽 변경을 먼저 확인한다.
Git에서 제외한 PLAN.md와 private-study/는 별도 복사와 백업이 필요하다. Git만으로 Codespaces에 전달되지 않는다.

## CI 확인과 로컬 개발

지속적 통합(Continuous Integration, CI)은 push와 pull request 때 별도 GitHub Actions 실행기에서 자동 빌드한다. Actions 탭에서 `learning-ci` → 실패한 언어 job → 실패한 step을 열어 첫 오류를 읽는다. `workflow_dispatch`로 수동 실행할 수도 있다.
언어별 독립 job은 같은 개발 이미지를 빌드한 뒤 hello의 종료 코드와 출력을 확인한다. 초기에는 이미지 캐시를 두지 않아 5개 job이 각자 설치한다. 실행 시간은 언어별 30분으로 제한한다.
빌드와 hello 확인은 모든 기능의 정확성을 보장하지 않는다. 입력 오류와 경계 조건을 검사하는 테스트는 학습 과정에서 직접 추가한다.

Windows 로컬에서는 Git과 편집기만 있어도 된다. 컴파일까지 하려면 Docker Desktop과 Dev Containers 확장으로 `Dev Containers: Reopen in Container`를 사용하거나 WSL2에 동일한 도구 버전을 설치한다. Windows 네이티브 설치 시 C Makefile의 Linux 명령은 별도 조정이 필요하다. 전역 도구를 자동 설치하는 스크립트는 없다.
네트워크 과제의 서버는 수동 실행하고 Codespaces 포트의 공개 범위를 private로 유지한다.

## 검증 기록

2026-11-15에 Windows Docker Desktop의 Linux 엔진에서 개발 이미지 빌드를 완료했다. CI에 기록된 명령으로 5개 언어의 빌드와 hello 출력·종료 코드 검사를 모두 통과했다. Java의 Maven 실행에서는 내부 Guava 라이브러리의 사용 중단 예정 API 경고가 나오지만 빌드는 성공했다.
컨테이너의 임시 복사본에서 각 언어에 두 번째 실행 예제를 추가하고 빌드·실행하는 절차도 모두 통과했다.
GitHub Actions 실행기와 실제 Codespaces 생성은 아직 확인하지 않았다. 첫 푸시 후 Actions 결과와 Codespaces 시작을 별도로 확인한다.
