# Haskell 학습

Bash에서 `cd haskell` 후 실행한다.

## 빌드와 실행

```bash
cabal update
cabal build all
cabal run hello
```

예상 출력: `Hello, Haskell!`

## 두 번째 예제 추가

`app/wordcount/Main.hs`를 만든다. learning.cabal의 executable hello 블록을 복사하여 이름을 wordcount, hs-source-dirs를 app/wordcount로 바꾼다. 별도의 module Main과 main을 작성한다.

```bash
cabal run wordcount
```

## 학습 지도

읽기 → 직접 구현 → 오류 입력 확인 → 자신의 말로 설명 순서로 진행한다.

1. 시작: GHCi, 식·타입 추론·함수 적용, 리스트·튜플·패턴 매칭·guard. 통과: 재귀로 목록 통계 계산.
2. 함수형 사고: 순수 함수, 불변성, 고차 함수, 부분 적용·합성, map/filter/fold, 지연 평가. 통과: 여러 순수 함수를 합친 텍스트 처리.
3. 모델링: algebraic data type, record, Maybe·Either, typeclass·instance, module. 통과: 실패를 타입으로 표현하는 파서.
4. 효과 연결: Functor → Applicative → Monad, fmap·pure·<*>·>>=·do 표기. Maybe/Either에서 실패 전달을 익힌 뒤 IO로 확장한다. 통과: 같은 처리를 >>=와 do 두 방식으로 작성하고 설명.
5. 실용 프로그램: 순수 핵심과 IO 경계, 파일·인자·예외·자원 정리, Text·Map, Cabal 의존성. 통과: 입력 오류를 처리하는 CLI.
6. 검증과 평가: QuickCheck 속성 테스트, 단위 테스트 기초, strictness·foldl'·공간 누수 기초. 통과: 속성 하나를 세우고 반례를 해석.
7. 중급 종합: 파서 기반 파일 분석기. State·Reader·transformer는 필요할 때 선택 심화하며 Monad 이해의 선행 조건으로 삼지 않는다.
