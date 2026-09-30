# 2주차 - React 컴포넌트 및 상태 기반 UI 구성

# ❗ 학습 목표

---

<aside>
🎯

이번 주차를 마치면 다음을 할 수 있어요.

- React 프로젝트를 만들고 개발 서버를 실행할 수 있어요.
- JSX와 TSX의 역할과 차이를 설명하고 TSX로 컴포넌트를 작성할 수 있어요.
- props에 타입을 붙여 부모 컴포넌트의 값을 자식 컴포넌트에 전달할 수 있어요.
- 조건부 렌더링과 목록 렌더링으로 데이터에 따라 달라지는 UI를 작성할 수 있어요.
- 이벤트와 `useState`를 연결하고 배열 상태를 직접 바꾸지 않으면서 업데이트할 수 있어요.
- 상태 끌어올리기와 Context API의 역할, props와 Context의 선택 기준을 설명할 수 있어요.
</aside>

# 📸 잠깐! 스터디 인증샷은 찍으셨나요? 📸

---

- 스터디 리더께서 대표로 매주 한 장씩 남겨주시면 좋겠어요! 🙆💗
- 사진을 저장해 이미지로 첨부하거나 복사하여 붙여 넣어 주세요.

![1000045979.jpg](1000045979.jpg)

# ✨ 학습 내용

---

<aside>
🤖

**AI를 학습에 적극 활용해요.**

AI는 **개념 이해, 코드 읽기, 오류 해결, 복습**에 활용할 수 있어요. 답을 대신 작성하게 하기보다, 이해하기 어려운 부분을 더 쉽게 설명해 달라고 요청하고 꼬리 질문을 이어가며 학습해 보세요.

- "이 개념을 초등학생도 이해할 수 있는 말로 설명해 줘. 단, 설명이 너무 길어지지 않도록 핵심만 알려 줘."
- "내 생각에는 이 부분 때문에 오류가 발생한 것 같아. 내 생각이 맞는지 확인하고, 다른 원인도 함께 알려 줘."
- "이 개념은 어느 정도 이해했어. 다음으로 알아 두면 좋은 내용도 알려 줘."
- "내가 이해한 내용을 설명할게. 틀리거나 빠진 부분을 짚어 주고, 이해했는지 확인할 질문도 해 줘."

AI의 답변이 항상 정확한 것은 아니에요. 제안받은 코드는 직접 실행하여 결과를 확인하고, 중요한 내용은 공식 문서와 함께 확인해 주세요.

</aside>

## 0. 시작하기 전

1. 이번 주차에서 배우는 내용
    
    0주차에서는 HTML, CSS, JavaScript의 역할과 개발 도구를 준비했고, 1주차에서는 TypeScript의 타입을 배웠어요. 이번 주차에는 그 지식을 사용해 **데이터가 바뀌면 화면도 함께 바뀌는 React UI**를 만들어요.
    
    JSX와 TSX로 화면 구조를 작성하는 방법부터 익혀요. 그다음 컴포넌트의 역할과 부모, 자식 관계, props, 조건부 렌더링, 목록 렌더링, 이벤트와 `useState`를 순서대로 배우고 렌더링과 리렌더링의 흐름을 확인한 뒤 Context API까지 연결해요.
    
2. 학습하는 방법
    
    각 단원의 번호를 따라 위에서 아래로 진행해요.
    
    1. 새로운 개념을 쉬운 설명부터 읽어요.
    2. 번호가 붙은 설명과 실습을 위에서 아래로 따라가요.
    3. 안내된 방법으로 결과를 확인해요.
    4. 텍스트, 색상이나 숫자 중 하나만 바꾸어 다시 확인해요.
    5. 예상과 다르면 직전에 작성한 코드부터 한 줄씩 살펴봐요.
    
    <aside>
    📌
    
    코드를 한 번에 완벽하게 작성하기보다 **작게 작성하고, 바로 확인하고, 한 가지씩 바꾸는 과정**이 중요해요.
    
    같은 `src/App.tsx` 파일에서 새 예제를 실행할 때는 **"이어서 작성해요"라는 안내가 없다면 기존 코드를 지우고 새 예제로 바꿔요.** 이전 예제를 계속 붙이면 같은 변수, 타입이나 함수 이름이 겹쳐 오류가 생길 수 있어요.
    
    </aside>
    
3. 개념 사전 활용하기
    
    본문을 읽다가 낯선 용어가 나오면 아래 개념 사전에서 필요한 항목만 찾아보세요. 사전을 먼저 외우거나 처음부터 끝까지 읽을 필요는 없어요. 문법과 실습 방법은 이 본문에서 순서대로 설명해요.
    
    [2주차 개념 사전](https://app.notion.com/p/2-da0d62e145e382bfae27010e158b8458?pvs=21)
    

## 1. React 실습 환경 준비하기

React는 화면을 컴포넌트라는 작은 단위로 나누어 만드는 사용자 인터페이스 라이브러리예요. React가 라이브러리인 이유와 Vue, Angular와의 차이는 2주차 개념 사전에 정리했어요. 이번 본문에서는 Vite가 React와 TypeScript 프로젝트의 기본 파일을 준비하고 개발 서버를 실행하도록 맡겨요.

먼저 Node.js와 pnpm을 확인한 뒤 프로젝트를 만들어요. 명령은 VS Code의 통합 터미널에 입력해요.

- 1.1. Node.js와 pnpm 버전 확인하기
    
    터미널에서 아래 명령을 실행해요.
    
    ```bash
    node -v
    pnpm -v
    ```
    
    Vite 공식 문서는 현재 Node.js `20.19` 이상 또는 `22.12` 이상을 요구해요. 0주차에서 설치한 Node.js 22 LTS 이상이 보이면 다음 단계로 이동해요.
    
- 1.2. Vite로 React + TypeScript 프로젝트 만들기
    
    아래 명령어를 실행해서 프로젝트를 만들어요.
    
    ```bash
    pnpm create vite umcine --template react-ts
    ```
    
    - `umcine`: 새로 만들 프로젝트 폴더 이름이에요.
    - `react-ts`: React와 TypeScript를 함께 쓰는 템플릿이에요.
    
    아래 사진과 같이 옵션을 선택해서 프로젝트를 설치해요.
    
    ![clipboard.png](clipboard.png)
    
    ![clipboard.jpeg](clipboard.jpeg)
    
- 1.3. 개발 서버 실행하고 종료하기
    
    이제 만들어진 `umcine` 폴더로 이동해서 의존성을 설치하고 개발 서버를 실행해요.
    
    ```bash
    cd umcine
    pnpm install
    pnpm dev
    ```
    
    터미널에 표시된 `http://localhost:5173`과 같은 주소를 브라우저에서 열어요. Vite 시작 화면이 보이면 준비가 끝났어요. 포트 번호는 다른 프로젝트의 실행 상태에 따라 달라질 수 있어요.
    
    개발 서버를 종료할 때는 서버가 실행 중인 터미널을 선택한 뒤 운영체제에 맞는 키를 눌러요.
    
    - macOS: `Control + C`를 눌러요. 키보드 기호로는 `⌃C`예요. `Command + C`는 복사 단축키이므로 사용하지 않아요.
    - Windows와 Linux: `Ctrl + C`를 눌러요.
    - Windows 명령 프롬프트에서 `Terminate batch job (Y/N)?`이 보이면 `Y`를 입력하고 `Enter`를 눌러요.
    
    터미널에 새로운 명령을 입력할 수 있는 줄이 다시 보이면 개발 서버가 종료된 거예요.
    
- 1.4. 자주 수정할 파일 알아보기
    - `src/main.tsx`: React 앱을 HTML의 `root` 요소에 연결하는 시작 파일이에요.
    - `src/App.tsx`: 이번 주차에 주로 수정할 최상위 컴포넌트예요.
    - `src/App.css`, `src/index.css`: 화면의 스타일을 작성하는 파일이에요.
    - `package.json`: 설치된 패키지와 `dev`, `build` 같은 실행 명령을 기록해요.
    
    이번 주차에는 기본으로 생성된 `App.tsx`의 내용을 지우고 예제로 교체해요. `main.tsx`는 수정하지 않아도 돼요.
    
- 미니 실습: 첫 화면 바꾸고 빌드하기
    1. `src/App.tsx`에서 `App` 컴포넌트의 기존 `return (...)` 부분을 찾고, 그 안의 내용을 `<h1>(본인 닉네임)의 React 학습</h1>`로 바꿔요. 지금은 코드를 외우지 말고 화면이 바뀌는지만 확인해요. JSX와 `return`은 2단원부터 차례로 배워요.
    2. 파일을 저장하고 브라우저 화면이 바뀌는지 확인해요.
    3. 개발 서버를 종료한 뒤 아래 명령을 실행해요.
    
    ```bash
    pnpm build
    ```
    
    1. 타입 오류 없이 `dist` 폴더가 만들어지면 정상이에요.
- 📚 같이 보면 좋은 자료
    - [Vite - Getting Started](https://vite.dev/guide/) - 프로젝트 생성 명령, Node.js 요구 버전과 개발 서버 사용법을 확인할 수 있어요.

## 2. JSX와 TSX로 화면 구조 작성하기

0주차에서는 HTML로 화면 구조를 작성했어요. React에서는 컴포넌트가 화면에 보여 줄 구조를 JSX로 작성해요. **반환**은 함수가 실행 결과를 함수 바깥으로 내보내는 것을 뜻해요.

JSX는 UI 구조를 JavaScript 코드 가까이에 작성하게 해 주고, TSX는 JSX에 TypeScript의 타입 검사를 함께 적용해요.

- 2.1. React는 데이터로 화면을 설명해요
    
    영화 카드의 북마크 여부가 `false`라면 비활성 모습을, `true`라면 활성 모습을 보여 준다고 생각해 볼 수 있어요. 개발자는 화면 요소를 하나씩 찾아 바꾸는 순서보다 **현재 데이터에 맞는 화면의 모습**을 JSX로 작성해요.
    
    React는 컴포넌트가 반환한 JSX를 읽고 브라우저 화면에 반영해요. 사용자 동작으로 데이터와 화면이 바뀌는 자세한 과정은 6단원에서 직접 상태를 만든 뒤 살펴봐요.
    
- 2.2. JSX는 무엇인가요?
    
    JSX는 JavaScript 파일 안에서 HTML과 비슷한 마크업을 작성할 수 있게 해 주는 **JavaScript 문법 확장**이에요. JSX는 HTML 문자열이 아니며, 브라우저가 그대로 읽는 문법도 아니에요. Vite 같은 빌드 도구가 JSX를 JavaScript로 바꾼 뒤 React가 화면을 만들 때 사용해요.
    
    React와 JSX는 같은 것이 아니에요. React는 UI를 만들고 갱신하는 라이브러리이고, JSX는 그 UI의 모양을 읽기 쉽게 작성하는 문법이에요.
    
    - JavaScript와 JSX를 함께 작성하는 파일은 보통 `.jsx` 확장자를 사용해요.
    - TypeScript와 JSX를 함께 작성하는 파일은 `.tsx` 확장자를 사용해요.
    
    이번 프로젝트는 TypeScript 템플릿으로 만들었기 때문에 `App.tsx`를 사용해요. 따라서 **TSX는 JSX의 규칙을 그대로 사용하면서 TypeScript의 타입 검사도 받는 코드**라고 이해하면 돼요.
    
- 2.3. HTML과 다른 JSX의 기본 규칙
    
    `src/App.tsx`의 기존 코드를 지우고 아래 코드로 바꿔요.
    
    ```tsx
    export default function App() {
      const movieTitle = "오디세이";
      const releaseDate = "2026.08.05";
    
      return (
        <main className="movie-page">
          <h1>{movieTitle}</h1>
          <p>개봉일: {releaseDate}</p>
        </main>
      );
    }
    ```
    
    1. 여러 요소는 `<main>`처럼 하나의 부모 요소로 감싸요. 불필요한 HTML 요소를 만들고 싶지 않다면 `<>...</>` 형태의 Fragment로 감쌀 수 있어요.
    2. 모든 태그를 닫아요. 내용이 없는 이미지는 `<img />`처럼 스스로 닫는 형태로 작성해요.
    3. HTML의 `class` 대신 `className`을 사용해요. JavaScript에서 `class`가 이미 다른 의미로 사용되기 때문이에요.
    4. JavaScript 값과 계산식은 중괄호 `{}` 안에 작성해요.
    
    파일을 저장한 뒤 브라우저에 영화 제목과 개봉일이 보이는지 확인해요. `movieTitle`을 다른 영화 제목으로 바꾸고 화면도 함께 바뀌는지 확인해 보세요.
    
- 2.4. 중괄호로 JavaScript 값 사용하기
    
    JSX의 중괄호 안에는 변수, 계산식과 함수 호출 결과처럼 하나의 값을 만드는 JavaScript 표현식을 넣을 수 있어요.
    
    - `{movieTitle}`: 변수에 저장된 문자열을 보여 줘요.
    - `{releaseYear + 1}`: 계산 결과를 보여 줘요.
    - `{movieTitle.toUpperCase()}`: 함수 실행 결과를 보여 줘요.
    
    중괄호 안에 `if`문이나 `for`문을 그대로 작성할 수는 없어요. 조건에 따른 UI와 배열을 반복하여 UI로 바꾸는 방법은 5단원에서 배워요.
    
- 미니 실습: 영화 정보 카드 작성하기
    
    `src/App.tsx`의 기존 코드를 아래 코드로 바꿔요.
    
    ```tsx
    export default function App() {
      const movieTitle = "오디세이";
      const genre = "모험";
    
      return (
        <article className="movie-card">
          <h1>{movieTitle}</h1>
          <p>장르: {genre}</p>
        </article>
      );
    }
    ```
    
    1. 파일을 저장하고 브라우저에 영화 제목과 장르가 보이는지 확인해요.
    2. `movieTitle`과 `genre`의 값을 원하는 내용으로 바꿔요.
    3. `releaseDate` 변수를 추가하고 `<p>개봉일: {releaseDate}</p>`로 화면에 표시해요.
    4. 저장 후 브라우저 화면과 개발자 도구의 Console에 JSX 오류가 없는지 확인해요.
- 📚 같이 보면 좋은 자료
    - [React - Writing Markup with JSX](https://ko.react.dev/learn/writing-markup-with-jsx) - JSX가 필요한 이유와 HTML, JSX의 차이를 확인할 수 있어요.
    - [React - JavaScript in JSX with Curly Braces](https://ko.react.dev/learn/javascript-in-jsx-with-curly-braces) - 중괄호 안에서 JavaScript 값을 사용하는 방법을 살펴볼 수 있어요.

## 3. 컴포넌트의 역할과 관계 이해하기

컴포넌트는 React UI를 이루는 기본 단위예요. 버튼처럼 작은 부분도 컴포넌트가 될 수 있고, 영화 카드, 영화 목록과 페이지 전체도 컴포넌트가 될 수 있어요.

컴포넌트는 **화면에 보여 줄 JSX를 반환하는 JavaScript 함수**예요. 정의한 컴포넌트는 다른 컴포넌트의 JSX에서 태그처럼 사용하고 여러 번 조합할 수 있어요.

- 3.1. 컴포넌트를 정의하고 사용하기
    
    `src/App.tsx`의 기존 코드를 아래 코드로 바꿔요.
    
    ```tsx
    function MovieTitle() {
      return <h2>오디세이</h2>;
    }
    
    function MovieCard() {
      return (
        <article>
          <MovieTitle />
          <p>2026.08.05</p>
        </article>
      );
    }
    
    export default function App() {
      return (
        <main>
          <h1>영화 목록</h1>
          <MovieCard />
        </main>
      );
    }
    ```
    
    - `function MovieCard() { ... }`: 컴포넌트를 정의하는 부분이에요.
    - `<MovieCard />`: 정의한 컴포넌트를 화면에 사용하겠다고 나타내는 부분이에요.
    - `return`: 이 컴포넌트가 화면에 보여 줄 JSX를 반환해요.
    
    React가 직접 만든 컴포넌트와 HTML 태그를 구분할 수 있도록 컴포넌트 이름은 `MovieCard`처럼 반드시 대문자로 시작해요. 소문자로 시작하는 `<movieCard />`는 브라우저의 HTML 태그로 해석돼요.
    
- 3.2. 부모 컴포넌트와 자식 컴포넌트
    
    한 컴포넌트가 반환하는 JSX 안에서 다른 컴포넌트를 사용하면 두 컴포넌트 사이에 포함 관계가 생겨요.
    
    - **부모 컴포넌트**: 자신의 JSX 안에서 다른 컴포넌트를 사용하는 쪽이에요.
    - **자식 컴포넌트**: 다른 컴포넌트의 JSX 안에서 사용되는 쪽이에요.
    
    앞 예제에서 `App`은 `<MovieCard />`를 사용하므로 `MovieCard`의 부모예요. `MovieCard`는 `App`의 자식인 동시에 `<MovieTitle />`을 사용하므로 `MovieTitle`의 부모이기도 해요.
    
    부모와 자식은 파일이 저장된 폴더의 상하 관계나 컴포넌트의 중요도를 뜻하지 않아요. **현재 화면 구조에서 누가 누구를 포함하여 렌더링하는지**를 설명하는 용어예요.
    
- 3.3. 컴포넌트 트리로 화면 구조 읽기
    
    컴포넌트가 다른 컴포넌트를 포함하면 나무처럼 위에서 아래로 이어지는 구조가 생겨요. 이를 컴포넌트 트리라고 해요.
    
    ![출처: [트리로서 UI 이해하기](https://ko.react.dev/learn/understanding-your-ui-as-a-tree#your-ui-as-a-tree)](image.png)
    
    출처: [트리로서 UI 이해하기](https://ko.react.dev/learn/understanding-your-ui-as-a-tree#your-ui-as-a-tree)
    
    ```
    App
    ├── Header
    └── MovieList
        ├── MovieCard
        ├── MovieCard
        └── MovieCard
    ```
    
    이 구조에서 `App`은 가장 위의 컴포넌트예요. `MovieList`는 `App`의 자식이고 여러 `MovieCard`의 부모예요. 화면이 복잡해질수록 컴포넌트 트리를 그려 보면 값과 상태를 어디에서 관리해야 할지 판단하기 쉬워요.
    
- 추가로 알아보기: 컴포넌트를 나누는 기준
    
    반복해서 사용하는 UI, 한 가지 역할이 분명한 UI, 코드가 길어져 따로 읽고 싶은 부분을 컴포넌트로 나눌 수 있어요. Figma의 영화 목록 화면이라면 `Header`, `MovieGrid`, `MovieCard`, `Pagination`처럼 역할이 드러나는 이름을 붙일 수 있어요.
    
    컴포넌트 함수 안에 다른 컴포넌트 함수를 정의하지 않도록 주의해 주세요. 각 컴포넌트는 파일의 최상위에 작성해요.
    
- 미니 실습: 영화 목록 화면을 컴포넌트로 나누기
    1. `Header`, `MovieList`, `MovieCard` 컴포넌트를 `App.tsx`의 최상위에 작성해요.
    2. `App`에서 `<Header />`와 `<MovieList />`를 사용해요.
    3. `MovieList`에서 `<MovieCard />`를 두 번 사용해요.
    4. 각 컴포넌트의 부모와 자식 관계를 글이나 트리로 정리해요.
    5. 브라우저에서 헤더 하나와 영화 카드 두 개가 보이는지 확인해요.
- 📚 같이 보면 좋은 자료
    - [React - Your First Component](https://ko.react.dev/learn/your-first-component) - 컴포넌트를 정의하고 다른 컴포넌트 안에서 사용하는 과정을 확인할 수 있어요.

## 4. props로 컴포넌트에 값 전달하기

같은 `MovieCard`를 여러 번 사용하더라도 영화 제목과 개봉일은 달라야 해요. props는 부모 컴포넌트가 자식 컴포넌트를 사용할 때 전달하는 입력값이에요.

컴포넌트 함수는 전달받은 props 객체를 읽어 서로 다른 화면을 만들어요. 데이터는 부모에서 자식 방향으로 내려가며, 자식은 전달받은 props를 직접 바꾸지 않아요.

- 4.1. props를 함수의 입력값으로 이해하기
    
    일반 함수가 매개변수로 값을 받듯이 React 컴포넌트는 하나의 props 객체를 받아요.
    
    ```tsx
    interface MovieCardProps {
      title: string;
      releaseDate: string;
      isBookmarked: boolean;
    }
    
    function MovieCard({
      title,
      releaseDate,
      isBookmarked,
    }: MovieCardProps) {
      return (
        <article>
          <h2>{title}</h2>
          <p>{releaseDate}</p>
          <p>{isBookmarked ? "북마크됨" : "북마크 안 됨"}</p>
        </article>
      );
    }
    
    export default function App() {
      return (
        <main>
          <MovieCard
            title="오디세이"
            releaseDate="2026.08.05"
            isBookmarked={true}
          />
          <MovieCard
            title="토이 스토리 5"
            releaseDate="2026.06.17"
            isBookmarked={false}
          />
        </main>
      );
    }
    ```
    
    `App`은 부모 컴포넌트로서 제목, 개봉일과 북마크 여부를 전달해요. `MovieCard`는 자식 컴포넌트로서 값을 받아 화면에 사용해요.
    
    문자열은 `title="오디세이"`처럼 전달할 수 있어요. 불리언, 숫자와 변수 같은 JavaScript 값은 `isBookmarked={true}`처럼 중괄호 안에 넣어요.
    
- 4.2. props 타입과 구조 분해 할당
    
    `MovieCardProps`는 컴포넌트가 받을 값의 이름과 타입을 약속해요. `releaseDate`를 빼거나 `isBookmarked="true"`처럼 문자열을 전달하면 TypeScript가 오류를 알려 줘요.
    
    `function MovieCard(props: MovieCardProps)`처럼 props 객체 전체를 받을 수도 있어요. 예제의 `{ title, releaseDate, isBookmarked }`는 객체에서 필요한 속성을 바로 꺼내는 구조 분해 할당 문법이에요.
    
    props 타입은 코드를 검사하는 역할뿐 아니라 이 컴포넌트를 사용할 때 어떤 값이 필요한지 알려 주는 설명서 역할도 해요.
    
- 4.3. 단방향 데이터 흐름과 읽기 전용 props
    
    React의 데이터는 기본적으로 부모에서 자식으로 내려가요. 이를 단방향 데이터 흐름이라고 해요. 값이 어디에서 왔는지 위쪽으로 따라갈 수 있어 화면의 동작을 찾기 쉬워요.
    
    자식 컴포넌트 안에서 `title = "다른 영화"`처럼 props를 직접 바꾸지 않아요. 자식이 다른 값을 보여 줘야 한다면 부모가 새로운 props를 전달해야 해요.
    
- 4.4. 컴포넌트를 별도 파일로 분리하기
    
    컴포넌트가 길어지면 `src/components/movie-card.tsx`처럼 별도 파일로 옮길 수 있어요. 새로 만드는 파일과 폴더의 이름은 영문 소문자와 하이픈을 사용하는 케밥 케이스로 작성해요. Vite가 만든 `App.tsx`와 `main.tsx`는 이름을 그대로 유지해도 돼요.
    
    파일 이름은 `movie-card.tsx`로 작성하더라도 컴포넌트 함수 이름은 `MovieCard`처럼 대문자로 시작하는 파스칼 케이스를 사용해요. 컴포넌트 파일에서는 `export default`로 내보내고, 사용하는 파일에서는 `import MovieCard from "./components/movie-card"`로 가져와요.
    
    파일을 나누어도 부모와 자식 관계는 파일 위치가 아니라 JSX의 포함 관계로 결정돼요. `App.tsx`가 `<MovieCard />`를 사용하면 `App`이 부모예요.
    
- 미니 실습: 영화 카드 재사용하기
    1. `MovieCardProps`에 `title`, `releaseDate`, `isBookmarked` 타입을 작성해요.
    2. `MovieCard`를 세 번 사용하고 서로 다른 영화 정보를 전달해요.
    3. 불리언 값에 따라 `"북마크됨"` 또는 `"북마크 안 됨"`을 표시해요.
    4. props 하나를 일부러 빠뜨려 타입 오류를 확인한 뒤 다시 추가해요.
    5. 브라우저에 서로 다른 영화 카드 세 개가 보이는지 확인해요.
- 📚 같이 보면 좋은 자료
    - [React - Passing Props to a Component](https://ko.react.dev/learn/passing-props-to-a-component) - 부모가 자식에게 props를 전달하고 자식이 값을 읽는 기본 흐름을 확인할 수 있어요.
    - [React - Using TypeScript](https://ko.react.dev/learn/typescript) - 컴포넌트 props와 Hook에 TypeScript 타입을 적용하는 예제를 살펴볼 수 있어요.

## 5. 조건에 따라 UI와 목록 보여 주기

React 컴포넌트는 현재 데이터에 맞는 JSX를 반환해요. 따라서 영화가 있는지, 북마크되었는지와 같은 조건에 따라 다른 UI를 보여 줄 수 있어요.

0주차에서 배열은 배웠지만 `map()`은 아직 자세히 다루지 않았어요. `map()`은 배열의 각 값을 하나씩 받아 원하는 값으로 바꾸고, 그 결과를 **새 배열**로 반환하는 JavaScript 배열 메서드예요. React에서는 영화 객체 배열을 같은 모양의 JSX 요소 배열로 바꿀 때 사용해요. 목록의 각 항목에는 React가 항목을 구분할 수 있도록 고유한 `key`도 지정해야 해요.

- 5.1. map()과 조건부 렌더링으로 목록 만들기
    
    `movies.map((movie) => ...)`를 왼쪽부터 읽어 봐요.
    
    1. `movies`: 변환할 원본 영화 배열이에요.
    2. `movie`: 배열에서 현재 차례에 꺼낸 영화 객체예요.
    3. `=>` 뒤의 JSX: 현재 영화 객체를 어떤 화면 요소로 바꿀지 나타내요.
    4. 모든 영화의 변환이 끝나면 `map()`이 새 JSX 요소 배열을 반환해요.
    
    이제 `src/App.tsx`의 기존 코드를 아래 예제로 바꿔요.
    
    ```tsx
    interface Movie {
      id: number;
      title: string;
      releaseDate: string;
    }
    
    const movies: Movie[] = [
      { id: 1, title: "오디세이", releaseDate: "2026.08.05" },
      { id: 2, title: "토이 스토리 5", releaseDate: "2026.06.17" },
    ];
    
    export default function App() {
      return (
        <main>
          <h1>영화 목록</h1>
          {movies.length === 0 ? (
            <p>표시할 영화가 없어요.</p>
          ) : (
            <ul>
              {movies.map((movie) => (
                <li key={movie.id}>
                  {movie.title} - {movie.releaseDate}
                </li>
              ))}
            </ul>
          )}
        </main>
      );
    }
    ```
    
    `movies.length === 0`이 참이면 빈 목록 안내를 보여 주고, 거짓이면 영화 목록을 보여 줘요. `map()`은 영화 객체 하나를 `<li>` 하나로 바꾸어 새로운 JSX 목록을 만들어요.
    
    `movies`를 빈 배열로 바꾸어 안내 문구를 확인한 뒤 예시 데이터를 다시 넣어요.
    
- 5.2. 조건을 표현하는 방법
    
    두 UI 중 하나를 선택할 때는 `조건 ? 참일 때 UI : 거짓일 때 UI` 형태의 삼항 연산자를 사용할 수 있어요. 특정 조건에서만 UI를 보여 줄 때는 `조건 && UI` 형태도 사용할 수 있어요.
    
    조건식이 길어지면 JSX 안에서 한 번에 해결하지 말고 컴포넌트 위에서 변수로 계산하거나 별도 컴포넌트로 나누어요. 화면 구조를 읽기 쉽게 유지하는 것이 중요해요.
    
- 5.3. key의 역할
    
    `key`는 배열 안에서 각 항목을 구분하는 이름표예요. 항목이 추가, 삭제되거나 순서가 바뀔 때 React가 어떤 항목이 달라졌는지 판단하는 데 사용해요.
    
    데이터에 고유한 `id`가 있다면 `key={movie.id}`처럼 사용해요. 순서가 바뀔 수 있는 목록에서는 배열 인덱스를 `key`로 사용하지 않도록 주의해 주세요.
    
    `key`는 자식 컴포넌트가 읽는 일반 props가 아니에요. 자식에게 ID가 필요하다면 `movieId={movie.id}`처럼 별도의 props로 전달해요.
    
- 미니 실습: 영화 목록 렌더링하기
    1. `movies` 배열에 영화 한 편을 더 추가하고 고유한 `id`를 지정해요.
    2. `map`으로 제목과 개봉일을 모두 표시해요.
    3. `movies`가 비어 있을 때는 `"표시할 영화가 없어요."`만 보이게 해요.
    4. 목록의 `key`에서 `id`를 지워 경고를 확인한 뒤 다시 추가해요.
    5. 브라우저 화면과 Console에 목록 관련 경고가 없는지 확인해요.
- 📚 같이 보면 좋은 자료
    - [React - Rendering Lists](https://ko.react.dev/learn/rendering-lists) - `map()`으로 목록을 만들고 각 항목에 `key`를 지정하는 방법을 확인할 수 있어요.

## 6. 이벤트와 useState로 화면 바꾸기

이벤트는 클릭이나 입력처럼 사용자가 화면에서 일으킨 일이에요. 이벤트가 발생했을 때 실행할 함수를 이벤트 핸들러라고 해요.

일반 변수의 값을 바꾸는 것만으로는 React에 리렌더링을 요청할 수 없어요. 컴포넌트가 렌더링 사이에 값을 기억하고, 값이 바뀔 때 새로운 UI를 계산하려면 **state(상태)**를 사용해요. 본문에서는 문장을 자연스럽게 읽을 수 있도록 주로 ‘상태’라고 쓰고, 코드와 API 이름에서는 `state`를 그대로 사용해요.

- 6.1. 클릭 이벤트와 이벤트 핸들러
    
    React의 이벤트 이름은 `onClick`처럼 소문자와 대문자를 섞어 작성해요. 함수는 실행 결과가 아니라 함수 자체를 전달해야 해요.
    
    ```tsx
    export default function App() {
      function handleClick() {
        console.log("버튼을 클릭했어요.");
      }
    
      return (
        <button onClick={handleClick}>
          클릭하기
        </button>
      );
    }
    ```
    
    `src/App.tsx`에 작성하고 버튼을 누른 뒤 브라우저 개발자 도구의 Console에서 문구를 확인해요. `onClick={handleClick()}`라고 쓰면 렌더링 중에 함수가 바로 실행돼요. 클릭할 때 실행하려면 괄호 없이 `onClick={handleClick}`로 전달해요.
    
- 6.2. useState로 카운터 만들기
    
    `src/App.tsx`의 기존 코드를 아래 예제로 바꿔요.
    
    ```tsx
    import { useState } from "react";
    
    export default function App() {
      const [count, setCount] = useState(0);
    
      return (
        <main>
          <h1>카운터</h1>
          <p>현재 값: {count}</p>
          <button onClick={() => setCount((current) => current + 1)}>
            +1
          </button>
          <button onClick={() => setCount((current) => current - 1)}>
            -1
          </button>
          <button onClick={() => setCount(0)}>
            초기화
          </button>
        </main>
      );
    }
    ```
    
    - `count`: 현재 렌더링에서 사용할 상태 값이에요.
    - `setCount`: state를 업데이트하고 리렌더링을 요청하는 set 함수예요.
    - `useState(0)`: 처음 상태를 `0`으로 정해요. TypeScript는 상태를 `number`로 추론해요.
    
    세 버튼을 번갈아 눌러 값이 증가, 감소, 초기화되는지 확인해요.
    
- 6.3. 렌더링과 리렌더링 과정
    
    처음 화면이 열리면 React가 `App`과 그 아래 컴포넌트를 호출해 JSX를 계산하고, 필요한 DOM을 브라우저에 반영해요. 이 과정을 첫 렌더링이라고 해요.
    
    이제 `+1` 버튼을 눌렀을 때의 흐름을 살펴봐요.
    
    1. 클릭 이벤트가 발생하고 이벤트 핸들러가 실행돼요.
    2. 이벤트 핸들러가 `setCount`로 다음 상태를 요청해요.
    3. React가 `App` 컴포넌트를 다시 호출해 새 JSX를 계산해요. 이 과정이 리렌더링이에요.
    4. React가 이전 결과와 새 결과를 비교하고 달라진 숫자만 DOM에 반영해요.
    
    리렌더링은 브라우저 페이지 전체를 새로고침하거나 모든 DOM을 다시 만드는 것과 달라요. props나 상태가 바뀌면 관련 컴포넌트가 다시 계산될 수 있어요.
    
- 6.4. 이전 상태로 다음 상태 계산하기
    
    set 함수에 `setCount((current) => current + 1)`처럼 함수를 전달할 수 있어요. 이 함수를 **업데이터 함수**라고 해요. 업데이터 함수는 React가 전달한 가장 최신 상태를 기준으로 다음 값을 계산해요.
    
    `setCount(count + 1)`도 한 번의 단순한 클릭에는 동작하지만, 짧은 시간에 여러 업데이트를 모아 처리할 때는 같은 렌더링의 `count`를 반복해서 사용할 수 있어요. 증가와 감소처럼 이전 값이 필요한 업데이트에는 함수 형태를 습관으로 익혀요.
    
- 6.5. Hook(훅)의 뜻과 기본 규칙
    
    Hook은 함수 컴포넌트에서 상태와 Context 같은 React 기능을 사용할 수 있게 해 주는 특별한 함수예요. React가 제공하는 Hook과 직접 만드는 사용자 정의 Hook의 이름은 `use`로 시작해요.
    
    - Hook은 컴포넌트 함수의 최상위에서 호출해요.
    - 조건문, 반복문과 중첩 함수 안에서 호출하지 않아요.
    - 일반 JavaScript 함수가 아니라 React 컴포넌트나 다른 Hook 안에서 호출해요.
    
    호출 순서가 항상 같아야 React가 각 상태를 올바르게 연결할 수 있어요. 이번 본문에서는 `useState`와 `useContext`를 실제 코드로 사용해요.
    
    React 19의 `use`는 이름이 `use`로 시작하지만 Hook 규칙의 예외인 React API예요. Context를 읽을 수 있고 조건문 안에서도 호출할 수 있어요. 8단원에서 `useContext`와 함께 살펴봐요.
    
- 미니 실습: 카운터에 제한 추가하기
    1. 카운터 예제의 최솟값을 `0`, 최댓값을 `5`로 정해요.
    2. 현재 값이 `5`라면 `+1` 버튼을 비활성화해요.
    3. 현재 값이 `0`이라면 `-1` 버튼을 비활성화해요.
    4. 값이 범위를 벗어나지 않는지 버튼을 여러 번 눌러 확인해요.
    5. `pnpm build`로 타입 오류가 없는지 확인해요.
- 📚 같이 보면 좋은 자료
    - [React - Responding to Events](https://ko.react.dev/learn/responding-to-events) - 이벤트 핸들러를 전달하고 이벤트가 퍼지는 방식을 확인할 수 있어요.
    - [React - State: A Component's Memory](https://ko.react.dev/learn/state-a-components-memory) - 컴포넌트에 상태가 필요한 이유와 `useState`의 기본 동작을 살펴볼 수 있어요.
    - [React - Render and Commit](https://ko.react.dev/learn/render-and-commit) - 첫 렌더링, 리렌더링과 DOM 반영의 흐름을 확인할 수 있어요.

## 7. 배열 상태를 안전하게 업데이트하고 공유하기

영화 목록처럼 여러 객체를 상태로 관리할 때도 기존 배열과 객체를 직접 바꾸지 않아요. `map`, `filter`와 전개 문법으로 새로운 배열과 객체를 만든 뒤 상태를 교체해요.

여러 자식 컴포넌트가 같은 데이터를 보여 주고 바꿔야 한다면 가장 가까운 공통 부모가 상태를 관리해요. 자식은 props로 값과 함수를 받아 화면을 표시하고 변경을 요청해요.

- 7.1. 영화 북마크 배열 상태 만들기
    
    `src/App.tsx`의 기존 코드를 아래 예제로 바꿔요.
    
    ```tsx
    import { useState } from "react";
    
    interface Movie {
      id: number;
      title: string;
      releaseDate: string;
      isBookmarked: boolean;
    }
    
    const initialMovies: Movie[] = [
      {
        id: 1,
        title: "오디세이",
        releaseDate: "2026.08.05",
        isBookmarked: true,
      },
      {
        id: 2,
        title: "토이 스토리 5",
        releaseDate: "2026.06.17",
        isBookmarked: false,
      },
    ];
    
    export default function App() {
      const [movies, setMovies] = useState(initialMovies);
    
      function handleToggleBookmark(movieId: number) {
        setMovies((currentMovies) =>
          currentMovies.map((movie) =>
            movie.id === movieId
              ? { ...movie, isBookmarked: !movie.isBookmarked }
              : movie,
          ),
        );
      }
    
      return (
        <main>
          <h1>영화 목록</h1>
          <ul>
            {movies.map((movie) => (
              <li key={movie.id}>
                <span>{movie.title}</span>
                <button
                 
                  aria-pressed={movie.isBookmarked}
                  onClick={() => handleToggleBookmark(movie.id)}
                >
                  {movie.isBookmarked ? "북마크 해제" : "북마크 추가"}
                </button>
              </li>
            ))}
          </ul>
        </main>
      );
    }
    ```
    
    버튼을 누르면 클릭한 영화의 북마크 상태만 반대로 바뀌어요. 다른 영화 객체는 그대로 유지돼요.
    
- 7.2. 상태를 직접 바꾸지 않는 이유
    
    `movies[0].isBookmarked = true`나 `movies.push(newMovie)`는 기존 상태를 직접 수정하는 코드예요. 이렇게 원본을 수정하면 이전 값과 다음 값을 구분하기 어려워지고 React가 변경을 올바르게 추적하기 어려워요.
    
    예제의 `map`은 새로운 배열을 만들어요. 선택한 영화에서는 `{ ...movie, isBookmarked: ... }`로 새로운 객체도 만들어요. 변경하지 않을 영화는 기존 객체를 그대로 반환해요.
    
    - 추가: `[...currentMovies, newMovie]`
    - 삭제: `currentMovies.filter((movie) => movie.id !== movieId)`
    - 변경: `currentMovies.map((movie) => 조건 ? 새 객체 : movie)`
    
    `push`, `pop`, `splice`는 기존 배열을 바꾸므로 상태 업데이트에 바로 사용하지 않아요.
    
- 7.3. 상태 끌어올리기
    
    `MovieCard`마다 서로 다른 상태를 만들면 전체 영화 목록의 북마크 정보를 한 번에 확인하기 어려워요. 영화 목록을 가진 `App`이나 `MovieGrid`가 상태를 관리하고 각 `MovieCard`에 필요한 값을 전달하는 편이 자연스러워요.
    
    공통 부모로 상태를 옮기는 일을 **상태 끌어올리기**라고 해요. 상태를 가진 부모는 `movie`와 `handleToggleBookmark`를 자식에게 props로 전달해요. 자식은 상태를 직접 수정하지 않고 전달받은 함수를 호출해 변경을 요청해요.
    
    이처럼 같은 데이터를 여러 곳에 복사하지 않고 한 컴포넌트만 기준 값을 관리하는 원칙을 **Single Source of Truth(SSoT)**라고 해요. 쉽게 말해 기준이 되는 값은 한 곳에만 둔다는 뜻이에요.
    
- 7.4. 함수도 props로 전달할 수 있어요
    
    자식 컴포넌트가 받을 함수의 타입은 `(movieId: number) => void`처럼 작성할 수 있어요. `void`는 호출한 쪽에서 사용할 반환값이 없다는 뜻이에요.
    
    자식의 북마크 버튼은 `onClick={() => onToggleBookmark(movie.id)}`처럼 자신의 영화 ID를 부모 함수에 전달해요. 부모는 전달받은 ID로 배열 상태를 업데이트해요.
    
- 미니 실습: 영화 카드로 상태 분리하기
    1. `MovieCardProps`에 `movie: Movie`와 `onToggleBookmark: (movieId: number) => void`를 작성해요.
    2. `MovieCard`에서 제목, 개봉일과 북마크 버튼을 표시해요.
    3. 부모 컴포넌트에서 `map`으로 `MovieCard`를 렌더링해요.
    4. 서로 다른 카드의 버튼을 눌러 선택한 카드만 바뀌는지 확인해요.
    5. 배열이나 영화 객체를 직접 수정한 코드가 없는지 확인해요.
- 추가로 알아보기: useReducer를 고려할 때
    
    상태 값과 업데이트 방법이 단순하면 `useState`가 더 짧고 읽기 쉬워요. 하나의 상태를 바꾸는 이벤트와 규칙이 여러 곳에 흩어져 복잡해질 때는 `useReducer`로 변경 규칙을 reducer 함수 한 곳에 모을 수 있어요.
    
    - [React - Extracting State Logic into a Reducer](https://ko.react.dev/learn/extracting-state-logic-into-a-reducer) - `useState`에서 reducer로 옮기는 기준과 과정을 확인할 수 있어요.
- 📚 같이 보면 좋은 자료
    - [React - Updating Arrays in State](https://ko.react.dev/learn/updating-arrays-in-state) - 배열 상태의 추가, 삭제와 변경 방법을 확인할 수 있어요.
    - [React - Sharing State Between Components](https://ko.react.dev/learn/sharing-state-between-components) - 공통 부모로 상태를 끌어올리고 자식에 전달하는 과정을 살펴볼 수 있어요.

## 8. Context API로 컴포넌트 트리 깊숙한 곳에 값 전달하기

가까운 부모와 자식 사이에서는 props가 가장 분명한 전달 방법이에요. 하지만 같은 값을 여러 단계 아래의 컴포넌트가 모두 필요로 하면 중간 컴포넌트가 사용하지 않는 props까지 계속 전달해야 할 수 있어요. 이를 **props drilling(프롭 드릴링)**이라고 불러요.

Context API는 컴포넌트 트리의 위쪽에서 값을 제공하고 아래쪽의 필요한 컴포넌트가 직접 읽도록 도와줘요. Context는 상태를 자동으로 만들어 주는 도구가 아니라 **값을 전달하는 범위를 넓히는 방법**이에요.

- 8.1. Context의 세 단계
    1. `createContext`로 Context를 만들어요.
    2. 부모 컴포넌트가 `value`로 값을 제공해요.
    3. 아래쪽 컴포넌트가 `useContext`나 `use`로 가장 가까운 값을 읽어요.
    
    Context 값을 제공하는 컴포넌트 바깥에서 값을 읽으면 `createContext`에 넣은 기본값을 사용해요. 기본값이 실제로 어떤 의미인지 분명하게 정해요.
    
- 8.2. 테마 Context 만들고 useContext로 읽기
    
    `src/App.tsx`의 기존 코드를 아래 예제로 바꿔요. 이 예제는 React 19의 Context 제공 문법을 사용해요.
    
    ```tsx
    import { createContext, useContext, useState } from "react";
    
    type Theme = "light" | "dark";
    
    const ThemeContext = createContext<Theme>("light");
    
    function ThemeStatus() {
      const theme = useContext(ThemeContext);
    
      return <p>현재 테마: {theme}</p>;
    }
    
    export default function App() {
      const [theme, setTheme] = useState<Theme>("light");
    
      function handleToggleTheme() {
        setTheme((currentTheme) =>
          currentTheme === "light" ? "dark" : "light",
        );
      }
    
      return (
        <ThemeContext value={theme}>
          <ThemeStatus />
          <button onClick={handleToggleTheme}>
            테마 바꾸기
          </button>
        </ThemeContext>
      );
    }
    ```
    
    `App`이 현재 테마를 상태로 관리하고 `<ThemeContext value={theme}>`로 아래쪽에 제공해요. `ThemeStatus`는 중간 컴포넌트의 props를 거치지 않고 `useContext(ThemeContext)`로 값을 읽어요.
    
    버튼을 눌러 `light`와 `dark`가 바뀌는지 확인해요.
    
- 추가로 알아보기: use로 Context 읽기
    
    React 19에서는 `use` API에 Context를 전달해도 같은 값을 읽을 수 있어요. 위 예제의 `ThemeStatus`만 다음처럼 바꿀 수 있어요.
    
    ```tsx
    import { use } from "react";
    
    function ThemeStatus() {
      const theme = use(ThemeContext);
    
      return <p>현재 테마: {theme}</p>;
    }
    ```
    
    `useContext`는 다른 Hook처럼 컴포넌트 최상위에서 호출해야 해요. `use`는 조건문과 반복문 안에서도 호출할 수 있지만, 둘 다 React 컴포넌트나 Hook 안에서만 사용해요. 이번 예제처럼 조건이 없다면 최상위에서 읽는 형태로 시작해도 충분해요.
    
- 8.3. props와 Context 중 선택하기
    
    가까운 컴포넌트 한두 개에 값을 전달한다면 props를 먼저 사용해요. 어떤 값이 어디에서 왔는지 코드만 보고 쉽게 알 수 있어요.
    
    테마, 로그인 사용자, 언어처럼 같은 값을 멀리 떨어진 여러 컴포넌트가 필요로 할 때 Context를 고려해요. Context를 사용하기 전에 컴포넌트 구성이나 상태 위치를 더 단순하게 바꿀 수 있는지도 확인해요.
    
- 미니 실습: 학습 모드 Context 만들기
    1. `StudyMode` 타입을 `"focus" | "break"`로 만들어요.
    2. 기본값이 `"focus"`인 `StudyModeContext`를 만들어요.
    3. 자식 컴포넌트에서 `useContext`나 `use` 중 하나로 현재 모드를 읽어 화면에 표시해요.
    4. 부모의 버튼으로 모드를 바꾸고 자식 화면도 함께 바뀌는지 확인해요.
- 📚 같이 보면 좋은 자료
    - [React - Passing Data Deeply with Context](https://ko.react.dev/learn/passing-data-deeply-with-context) - props와 Context를 선택하는 기준과 Context로 값을 전달하는 방법을 확인할 수 있어요.
    - [React - use](https://ko.react.dev/reference/react/use) - React 19에서 Context를 `use`로 읽는 방법과 Hook 규칙과의 차이를 확인할 수 있어요.

# 🎯 핵심 키워드

---

<aside>
💡

아래 키워드를 직접 조사하고 자신의 말로 정리해 보세요. 정의만 옮기지 말고, 워크북에서 작성한 예시나 실제 사용 상황을 함께 기록하면 좋아요.

</aside>

- React 컴포넌트와 JSX
    - JSX는 HTML과 어떤 점이 다르며 React 컴포넌트 안에서 어떤 역할을 하나요?
    - 하나의 화면을 여러 컴포넌트로 나누면 어떤 장점이 있으며, 분리 기준은 어떻게 정할 수 있을까요?
    - 조건부 렌더링과 목록 렌더링은 데이터에 따라 보여 줄 컴포넌트를 어떻게 결정하나요?
- props와 단방향 데이터 흐름
    - 부모와 자식 컴포넌트 사이에서 props는 어떤 역할을 하나요?
    - 데이터가 부모에서 자식으로만 흐르면 화면의 변화를 추적하는 데 어떤 도움이 되나요?
    - props에 TypeScript 타입을 붙이면 컴포넌트를 잘못 사용하는 실수를 어떻게 찾을 수 있나요?
- 상태와 리렌더링
    - 일반 변수와 state(상태)는 값이 바뀐 뒤 화면을 다시 보여 주는 방식이 어떻게 다른가요?
    - React에서 원본 상태를 직접 수정하지 않고 새로운 값으로 업데이트해야 하는 이유는 무엇일까요?
    - 이전 상태로 다음 상태를 계산할 때 업데이터 함수를 사용하는 이유는 무엇일까요?
- 상태 공유와 Context
    - 여러 컴포넌트가 같은 상태를 사용해야 할 때 상태를 어느 컴포넌트에 두는 것이 좋을까요?
    - props 전달, 상태 끌어올리기와 Context는 각각 어떤 상황에 알맞을까요?
    - 모든 값을 Context로 전달하면 어떤 문제가 생길 수 있을까요?

# 📢 학습 후기

---

<aside>
💡

이곳에 학습 후기를 작성해 주세요.

</aside>

# 🔥 미션

---

<aside>
📝

필수 미션을 진행하며 작성한 **핵심 코드와 최종 확인 결과만** 아래 **미션 기록**의 **필수 미션** 토글에 기록해 주세요. 모든 명령과 중간 과정을 빠짐없이 적을 필요는 없어요.

선택 미션을 진행했다면 결과를 **선택 미션** 토글에 기록해 주세요.

</aside>

Figma의 UMCine 영화 목록 화면을 React와 CSS로 완성해요. 컴포넌트, props, 목록 렌더링과 북마크 상태를 하나의 결과물로 연결해요.

- 미션 준비: 영화 에셋과 더미 데이터 준비하기
    
    이미지 에셋과 더미 데이터는 2주차에서 한 번만 준비하고, 3주차에도 같은 파일을 그대로 사용해요.
    
    1. 아래 두 ZIP 파일을 내려받아 압축을 풀어요.
        
        [umcine-images.zip](umcine-images.zip)
        
        [movie-icons.zip](movie-icons.zip)
        
    2. `umcine-images.zip`의 `images` 폴더는 `public`에 넣고, `movie-icons.zip`의 아이콘은 `public/icons`에 넣어요. 파일 이름은 바꾸지 않아요.
    3. `src/types/movie.ts`를 만들고 아래 타입을 작성해요.
        
        ```tsx
        export interface Movie {
          id: number;
          title: string;
          originalTitle: string;
          releaseDate: string;
          posterPath: string;
          backdropPath: string;
          genres: string[];
          runtime: string;
          tagline: string;
          overview: string;
          isBookmarked: boolean;
        }
        ```
        
    4. `src/data/movies.ts`를 만들고 아래 더미 데이터를 작성해요.
        
        ```tsx
        import type { Movie } from "../types/movie";
        
        export const movies: Movie[] = [
          {
            id: 1,
            title: "스파이더맨: 브랜드 뉴 데이",
            originalTitle: "Spider-Man: Brand New Day",
            releaseDate: "2026.07.29",
            posterPath: "/images/movies/spider-man-brand-new-day.jpg",
            backdropPath: "/images/movies/spider-man-brand-new-day-backdrop.jpg",
            genres: ["SF", "액션", "모험"],
            runtime: "2시간 25분",
            tagline: "스파이더맨의 새로운 날을 확인하라!",
            overview: "모두의 기억에서 사라진 피터 파커가 새로운 힘과 자신의 정체를 아는 적을 마주해요.",
            isBookmarked: false,
          },
          {
            id: 2,
            title: "오디세이",
            originalTitle: "The Odyssey",
            releaseDate: "2026.08.05",
            posterPath: "/images/movies/odyssey.jpg",
            backdropPath: "/images/movies/odyssey-backdrop.jpg",
            genres: ["모험", "드라마"],
            runtime: "2시간 30분",
            tagline: "집으로 돌아가기 위한 가장 긴 여정",
            overview: "긴 전쟁을 마친 영웅이 수많은 시련을 지나 고향으로 돌아가는 여정을 그려요.",
            isBookmarked: true,
          },
          {
            id: 3,
            title: "스파이더맨: 노 웨이 홈",
            originalTitle: "Spider-Man: No Way Home",
            releaseDate: "2021.12.15",
            posterPath: "/images/movies/spider-man-no-way-home.jpg",
            backdropPath: "/images/movies/spider-man-no-way-home-backdrop.jpg",
            genres: ["액션", "모험", "SF"],
            runtime: "2시간 28분",
            tagline: "모든 세계의 운명이 하나로 이어진다",
            overview: "정체가 드러난 피터 파커가 도움을 청하는 과정에서 여러 세계의 문이 열려요.",
            isBookmarked: false,
          },
          {
            id: 4,
            title: "라스트 하우스",
            originalTitle: "The Last House",
            releaseDate: "2026.08.07",
            posterPath: "/images/movies/last-house.jpg",
            backdropPath: "/images/movies/last-house-backdrop.jpg",
            genres: ["스릴러", "미스터리"],
            runtime: "1시간 42분",
            tagline: "마지막 문을 열면 진실이 드러난다",
            overview: "외딴 저택에 모인 사람들이 감춰진 사건의 흔적을 발견해요.",
            isBookmarked: false,
          },
          {
            id: 5,
            title: "미니언즈 & 몬스터즈",
            originalTitle: "Minions & Monsters",
            releaseDate: "2026.07.15",
            posterPath: "/images/movies/minions-monsters.jpg",
            backdropPath: "/images/movies/minions-monsters-backdrop.jpg",
            genres: ["애니메이션", "코미디", "모험"],
            runtime: "1시간 35분",
            tagline: "작은 영웅들의 거대한 소동",
            overview: "미니언들이 도시를 찾아온 몬스터와 친구가 되며 새로운 모험을 시작해요.",
            isBookmarked: false,
          },
          {
            id: 6,
            title: "군체",
            originalTitle: "Colony",
            releaseDate: "2026.05.21",
            posterPath: "/images/movies/colony.jpg",
            backdropPath: "/images/movies/colony-backdrop.jpg",
            genres: ["SF", "스릴러"],
            runtime: "1시간 48분",
            tagline: "하나의 신호가 모두를 바꾼다",
            overview: "고립된 연구 기지의 구성원들이 정체를 알 수 없는 신호와 마주해요.",
            isBookmarked: false,
          },
          {
            id: 7,
            title: "토이 스토리 5",
            originalTitle: "Toy Story 5",
            releaseDate: "2026.06.17",
            posterPath: "/images/movies/toy-story-5.jpg",
            backdropPath: "/images/movies/toy-story-5-backdrop.jpg",
            genres: ["애니메이션", "모험", "가족"],
            runtime: "1시간 45분",
            tagline: "장난감들의 새로운 모험이 시작된다",
            overview: "우디와 친구들이 새로운 주인을 만나며 장난감의 의미를 다시 찾아가요.",
            isBookmarked: true,
          },
          {
            id: 8,
            title: "로빈 후드의 죽음",
            originalTitle: "The Death of Robin Hood",
            releaseDate: "2026.06.18",
            posterPath: "/images/movies/death-of-robin-hood.jpg",
            backdropPath: "/images/movies/death-of-robin-hood-backdrop.jpg",
            genres: ["액션", "모험", "드라마"],
            runtime: "2시간 10분",
            tagline: "전설의 마지막 화살",
            overview: "오랜 싸움을 마친 로빈 후드가 자신의 마지막 선택과 마주해요.",
            isBookmarked: false,
          },
          {
            id: 9,
            title: "옵세션",
            originalTitle: "Obsession",
            releaseDate: "2026.09.02",
            posterPath: "/images/movies/obsession.jpg",
            backdropPath: "/images/movies/obsession-backdrop.jpg",
            genres: ["스릴러", "드라마"],
            runtime: "1시간 50분",
            tagline: "완벽한 믿음이 집착으로 변한다",
            overview: "한 사람을 향한 믿음이 점차 위험한 집착으로 바뀌기 시작해요.",
            isBookmarked: false,
          },
          {
            id: 10,
            title: "이블 데드 번",
            originalTitle: "Evil Dead Burn",
            releaseDate: "2026.07.07",
            posterPath: "/images/movies/evil-dead-burn.jpg",
            backdropPath: "/images/movies/evil-dead-burn-backdrop.jpg",
            genres: ["공포", "스릴러"],
            runtime: "1시간 40분",
            tagline: "꺼진 불길 속에서 악이 깨어난다",
            overview: "버려진 오두막을 찾은 사람들이 오래 잠들어 있던 악을 깨워요.",
            isBookmarked: false,
          },
        ];
        ```
        

## 필수 미션

- UMCine 영화 목록 화면 완성하기
    - [Figma의 UMCine 영화 목록 페이지](https://www.figma.com/design/erFuXxEy5svB8Be5gjIqdu/%EC%98%81%ED%99%94-%ED%8E%98%EC%9D%B4%EC%A7%80?node-id=129-2&t=cjpCEJdEpuI8kGy1-4)의 `영화 목록` 프레임과 제공된 포스터 및 아이콘을 사용해 데스크톱 화면을 React와 CSS로 퍼블리싱해요.
    - 위에서 준비한 이미지 에셋과 더미 데이터를 사용해요.
    - 새 파일과 폴더 이름은 케밥 케이스로 작성하고, `header.tsx`, `movie-card.tsx`, `movie-grid.tsx`, `pagination.tsx`, 영화 데이터와 타입을 역할에 맞게 분리해요.
    - 영화 10편을 목록으로 표시하고 `useState`와 props를 사용해 선택한 영화의 북마크 상태와 아이콘만 변경되게 작성해요.
    - Figma의 데스크톱 화면과 비교하고 북마크 동작, Console 오류와 `pnpm build` 성공 여부를 확인해요.

## 선택 미션

- 화면 너비에 따라 영화 그리드가 3열, 2열, 1열로 바뀌도록 미디어 쿼리를 작성해 보세요.
- 현재 페이지를 `useState`로 관리하고 1부터 5까지의 페이지 버튼 중 선택한 번호만 활성 스타일로 표시해 보세요.

# 💪 미션 기록

---

<aside>
🍀

미션 기록은 아래 토글 안에 작성하거나, 별도 페이지를 만들어 작성해도 좋아요.

</aside>

- 필수 미션
- 선택 미션

# 📢 미션 제출 안내 & CodeRabbit 사용법 안내

---

<aside>
👊

미션을 마친 뒤 미션 기록이 포함된 Notion 페이지 URL을 https://umc.ai.kr/ 에 제출해 주세요.

Github에 올리신 코드는 하단의 CodeRabbit을 통해 직접 AI에게 피드백 받으실 수 있습니다!

</aside>

1. 개인 미션 페이지 오른쪽 위의 **공유** 버튼을 눌러 주세요.
2. **링크 복사**를 클릭해 주세요.
3. https://umc.ai.kr/ 에 제출해주세요.
    
    방법은 [‣](https://app.notion.com/p/3d4b57f4596b804cb1bbf4eb8eb20889?pvs=21) 에 적혀져 있습니다.
    
- 미션 제출 링크: 링크를 입력해 주시고, 하단의 CodeRabbit 설정으로 직접 AI를 통해 코드 피드백을 받아보세요!

[‣](https://app.notion.com/p/3c7b57f4596b80d9b804de47e3de2176?pvs=21) 

# 🍥 블로그 챌린지 안내

---

<aside>

☘️ 다음 활동들은 **권장 사항**이며 수행 시 챌린저 개인에게 상점이 부여됩니다.

[‣](https://app.notion.com/p/3d4b57f4596b800fab5bc9743ce8c255?pvs=21) 

</aside>

> 가이드라인에 제시된 **카테고리 중 1개를 선택해** 블로그를 작성합니다.
본인이 작성한 블로그 URL를 노션 폼에 제출하면, 상점 `+3점` 이 부여됩니다. (주 1회 제출 제한)
> 

<aside>

[‣](https://app.notion.com/p/3d5b57f4596b8023b08de1d77757de87?pvs=21) 

</aside>

> 
> 
> 
> 매주차별 챌린저분들이 작성해주신 블로그는 아래 아카이빙 페이지에서 확인 가능합니다!
> 
> [‣](https://app.notion.com/p/3d5b57f4596b80ebb468de68a6da651e?pvs=21) 
> 

## 📝 기술 블로그 주제 추천

---

<aside>
🌟

이번 주차에서 배운 내용을 자신의 말로 정리하며 복습해 보세요. 워크북에 나온 내용에 그치지 않고, 궁금한 부분을 직접 조사하거나 AI와 꼬리 질문을 이어가면 이해를 넓히는 데 도움이 돼요.

</aside>

아래 주제 중 하나를 선택하여 작성해도 좋아요.

- React 컴포넌트를 분리하고 재사용하는 기준
- props와 state가 UI를 변경하는 방식의 차이
- React 목록 렌더링에서 key가 컴포넌트를 구분하는 방식
- props 전달, 상태 끌어올리기와 Context를 선택하는 기준
- 기술 블로그 제출 링크: 링크를 입력해 주세요

# ⚡ 트러블 슈팅

---

<aside>
💡

실습 중 문제가 발생하면 **이슈 → 원인 → 해결 → 배운 점** 순서로 기록해 주세요. 오류 메시지를 지우거나 요약하지 말고 원문을 함께 남기면 원인을 찾는 데 도움이 돼요.

</aside>

- ⚡ 이슈 작성 예시
    
    **`이슈`**
    
    👉 `MovieCard`에서 북마크 함수를 사용한 뒤 `Property 'onToggleBookmark' is missing in type ...` 오류가 보였어요.
    
    **`원인`**
    
    👉 `MovieCardProps`에는 `onToggleBookmark`를 필수 함수로 작성했지만 부모가 `<MovieCard />`를 사용할 때 해당 props를 전달하지 않았어요.
    
    **`해결`**
    
    👉 부모의 영화 목록에서 `onToggleBookmark={handleToggleBookmark}`를 전달하고 자식 함수의 타입을 `(movieId: number) => void`로 맞추었어요. 아래 명령으로 타입 오류가 사라졌는지 확인했어요.
    
    ```bash
    pnpm build
    ```
    
    **`배운 점`**
    
    👉 자식 컴포넌트가 부모의 상태 변경을 요청하려면 부모가 함수 props를 전달해야 해요. props 이름과 함수의 매개변수 타입도 양쪽에서 같아야 해요.
    
    **`참고 레퍼런스`**
    
    - [React - Passing Props to a Component](https://ko.react.dev/learn/passing-props-to-a-component)
- ⚡ 이슈 No.1
    
    **`이슈`**
    
    👉 [트러블이 발생한 상태와 오류 메시지]
    
    **`원인`**
    
    👉 [오류가 발생한 이유]
    
    **`해결`**
    
    👉 [시도한 방법과 최종 해결 방법]
    
    **`배운 점`**
    
    👉 [다음에 같은 문제를 만났을 때 확인할 내용]
    
    **`참고 레퍼런스`**
    
    - [참고한 공식 문서 링크]

# 🤔 참고 자료

---

학습하다가 모르는 개념이 나오거나 예제가 예상대로 동작하지 않을 때 아래 자료를 참고해 보세요. 처음부터 끝까지 읽을 필요는 없어요. **궁금한 내용을 검색해 사전처럼 찾아보는 것**으로 충분해요.

각 학습 단원에는 지금 배우는 개념과 직접 연결된 공식 문서를 함께 소개했어요. React 학습 범위를 넓히고 싶을 때는 아래 사이트와 글도 찾아보세요.

- [React - Learn React](https://ko.react.dev/learn) - 컴포넌트, props, 상태와 Hook 등 React 개념과 API를 공식 설명과 예제로 찾아볼 수 있어요.
- [MDN Web Docs](https://developer.mozilla.org/ko/) - `map()` 같은 JavaScript 문법, 이벤트, DOM, HTML과 CSS를 함께 찾아볼 수 있어요.
- [TypeScript Handbook](https://www.typescriptlang.org/docs/handbook/intro.html) - TypeScript 문법과 타입 시스템을 더 자세히 확인하고 싶을 때 참고할 수 있어요.

---

Copyright © 2026 GwangSoo Lim(임광수) All rights reserved.