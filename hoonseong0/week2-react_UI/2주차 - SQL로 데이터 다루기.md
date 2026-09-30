# 2주차 - SQL로 데이터 다루기

# ❗ 학습 목표

---

1. 1주차 온라인 도서 대여 관리 시스템 ERD에서 필요한 테이블과 관계를 찾아낼 수 있다.
2. 온라인 도서 대여 화면 요구사항을 조회할 데이터, 조건, 정렬, 목록 범위로 나누어 설명할 수 있다.
3. MySQL에서 제공된 스키마와 더미 데이터를 실행하고, SELECT, FROM, WHERE, JOIN, ORDER BY, LIMIT을 사용해 기본 조회 쿼리를 작성할 수 있다.
4. 동일한 실습 ERD를 바탕으로 쿼리 결과와 요구사항이 일치하는지 검증할 수 있다.

# 📸 잠깐 ! 스터디 인증샷은 찍으셨나요? 📸

---

* 스터디리더께서 대표로 매 주차마다 한 장 남겨주시면 좋겠습니다!🙆💗
 (사진을 저장해서 이미지 임베드를 하셔도 좋고, 복사+붙여넣기 해서 넣어주셔도 좋습니다!)

[](https://app.notion.com)

# ✨ 2주차 주제

---

1주차에는 온라인 도서 대여 관리 시스템의 요구사항을 ERD로 표현하며 “어떤 데이터를 저장할지”를 정했습니다.

2주차에는 그 ERD를 MySQL 테이블과 더미 데이터로 구현한 뒤, 화면에 필요한 데이터를 SQL로 조회합니다. 모든 챌린저가 같은 기준 ERD와 데이터에서 시작해 쿼리의 이유와 결과를 함께 검증합니다.

# 📑 2주차 본문 들어가기 전: 실습 환경과 기준 데이터 준비

---

이번 주차는 1주차의 온라인 도서 대여 관리 시스템 요구사항과 기준 ERD를 그대로 사용합니다. SQL 문법을 쓰기 전에, 모두 같은 MySQL 환경과 데이터에서 실습을 시작합니다.

<aside>
💡

- 0-1. MySQL Community Server와 MySQL Workbench를 설치합니다.
- 0-1. Workbench에서 로컬 서버 연결을 만들고 `SELECT VERSION();`으로 접속을 확인합니다.

---

- 0-2. 1주차 기준 ERD에서 user, category, book, rental, tag, book_tag, book_like, notification의 관계를 다시 확인합니다.
- 0-2. 제공된 `01_schema.sql`을 실행해 기준 ERD와 같은 테이블을 생성합니다.
- 0-2. 제공된 `02_seed.sql`을 실행해 책·카테고리·대여·태그·좋아요·알림 더미 데이터를 넣습니다.
- 0-2. 이후의 모든 SQL은 제공된 공통 데이터에서 실행하고, 마지막에 자신의 1주차 ERD로 확장합니다.

```jsx
01_schema.sql: CREATE TABLE users (user_id BIGINT PRIMARY KEY AUTO_INCREMENT, nickname VARCHAR(30) NOT NULL); CREATE TABLE category (category_id BIGINT PRIMARY KEY AUTO_INCREMENT, name VARCHAR(50) NOT NULL); CREATE TABLE book (book_id BIGINT PRIMARY KEY AUTO_INCREMENT, category_id BIGINT NOT NULL, title VARCHAR(100) NOT NULL, description TEXT, is_available BOOLEAN NOT NULL DEFAULT TRUE, FOREIGN KEY (category_id) REFERENCES category(category_id)); CREATE TABLE rental (rental_id BIGINT PRIMARY KEY AUTO_INCREMENT, user_id BIGINT NOT NULL, book_id BIGINT NOT NULL, rented_at DATETIME NOT NULL, due_at DATETIME NOT NULL, returned_at DATETIME NULL, FOREIGN KEY (user_id) REFERENCES users(user_id), FOREIGN KEY (book_id) REFERENCES book(book_id));
```

</aside>

설치 가이드, 기준 ERD, `01_schema.sql`, `02_seed.sql`은 실습 시작 전에 함께 제공합니다. 파일 실행 순서를 지키면 같은 데이터로 결과를 비교할 수 있습니다.

## 0. SQL 실습 준비

### 0-1. MySQL 설치 및 접속 확인

MySQL Community Server와 MySQL Workbench를 설치한 뒤 Workbench에서 로컬 연결을 만듭니다. 비밀번호는 안전한 곳에 보관하고, 아래 쿼리가 정상 실행되는지 먼저 확인해 주세요.

```jsx
SELECT VERSION();
```

버전 정보가 한 행으로 나오면 접속 준비가 완료된 것입니다. 설치 또는 연결이 막히면 운영체제, 오류 메시지, 화면 캡처를 함께 Q&A에 남깁니다.

- 서버: MySQL Community Server 설치
- 클라이언트: MySQL Workbench 설치
- 연결: Host `127.0.0.1`, Port `3306`, 설치 시 만든 계정으로 접속
- 확인: `SELECT VERSION();` 실행 결과 캡처

![스크린샷 2026-08-18 오후 10.03.08.png](%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA_2026-08-18_%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE_10.03.08.png)

### 0-2. 1주차 기준 ERD와 실습용 테이블·더미 데이터

기준 ERD 관계: users 1:N rental, category 1:N book, book N:M tag(book_tag), users N:M book(book_like), users 1:N notification. 이 관계를 1주차 요구사항과 함께 확인합니다.

```jsx
01_schema.sql: CREATE TABLE tag (tag_id BIGINT PRIMARY KEY AUTO_INCREMENT, name VARCHAR(30) NOT NULL); CREATE TABLE book_tag (book_id BIGINT, tag_id BIGINT, PRIMARY KEY (book_id, tag_id), FOREIGN KEY (book_id) REFERENCES book(book_id), FOREIGN KEY (tag_id) REFERENCES tag(tag_id)); CREATE TABLE book_like (user_id BIGINT, book_id BIGINT, PRIMARY KEY (user_id, book_id), FOREIGN KEY (user_id) REFERENCES users(user_id), FOREIGN KEY (book_id) REFERENCES book(book_id)); CREATE TABLE notification (notification_id BIGINT PRIMARY KEY AUTO_INCREMENT, user_id BIGINT NOT NULL, type VARCHAR(30) NOT NULL, FOREIGN KEY (user_id) REFERENCES users(user_id));
```

```jsx
02_seed.sql: INSERT INTO users (nickname) VALUES ('민서'), ('수현'); INSERT INTO category (name) VALUES ('문학'), ('과학'); INSERT INTO book (category_id, title, description, is_available) VALUES (1, '달빛 도서관', '소설', TRUE), (1, '겨울의 편지', '에세이', FALSE), (2, '우주를 읽는 법', '과학 교양', TRUE);
```

```jsx
02_seed.sql: INSERT INTO rental (user_id, book_id, rented_at, due_at, returned_at) VALUES (1, 2, '2026-08-10 10:00:00', '2026-08-17 10:00:00', NULL), (2, 1, '2026-08-01 10:00:00', '2026-08-08 10:00:00', '2026-08-07 15:00:00'); INSERT INTO tag (name) VALUES ('소설'), ('추천'), ('과학'); INSERT INTO book_tag (book_id, tag_id) VALUES (1, 1), (1, 2), (3, 3); INSERT INTO book_like (user_id, book_id) VALUES (1, 1), (1, 3);
```

- DDL은 테이블 구조를 만드는 SQL이고, INSERT는 테이블에 실제 데이터를 넣는 SQL입니다.
- 앞으로 작성하는 조회 쿼리는 이 기준 데이터를 바꾸지 않는 SELECT 쿼리입니다.
- 실습이 끝난 뒤에는 같은 사고 과정을 1주차에 자신이 설계한 ERD에도 적용해 봅니다.
- 실행 순서: 01_schema.sql → 02_seed.sql → 아래 SELECT 실습 쿼리
- 초기화가 필요하면 실습용 데이터베이스를 새로 만든 뒤 01_schema.sql부터 순서대로 다시 실행합니다.
- 요구사항: “대여 가능한 책의 제목과 설명을 최신순으로 보여 주세요.”

## 1. ERD에서 SQL로 화면에 필요한 데이터 꺼내기

단일 테이블에서는 화면에 필요한 컬럼, 조건, 정렬만 먼저 작성합니다.

### 1-1. 단일 테이블: 대여 가능한 책 찾기

요구사항: “대여 가능한 책의 제목과 설명을 최신순으로 보여 주세요.”

```jsx
SELECT book_id, title, description FROM book WHERE is_available = TRUE ORDER BY book_id DESC;
```

카테고리 이름이나 태그처럼 다른 테이블의 정보가 필요할 때만 ERD의 관계를 따라 JOIN합니다.

아래 예시는 1주차 ERD에서 book과 category의 관계를 따라 화면에 필요한 결과를 만드는 과정입니다.

### 1-2. JOIN: 카테고리별 도서 목록 만들기

요구사항: “문학 카테고리에서 대여 가능한 책을 10권 보여 주세요.”

```jsx
SELECT b.book_id, b.title, [c.name](http://c.name/) AS category_name FROM book b JOIN category c ON b.category_id = c.category_id WHERE [c.name](http://c.name/) = '문학' AND b.is_available = TRUE ORDER BY b.book_id DESC LIMIT 10;
```

category 이름은 book 테이블이 아니라 category 테이블에 있으므로 book → category JOIN이 필요합니다.

### 1-3. 책의 태그와 좋아요: 관계를 따라 JOIN하기

책 상세 화면에서는 book_tag·tag로 태그를, book_like로 현재 사용자의 좋아요 여부를 찾습니다.

- 필요한 관계만 JOIN하고, 이번 주차에는 복잡한 서브쿼리나 성능 최적화는 다루지 않습니다.
- 관계의 방향과 ON 조건을 1주차 기준 ERD의 PK/FK로 설명하는 데 집중합니다.
- 목록 조회는 일관된 정렬과 LIMIT을 함께 사용합니다.

첫 페이지: LIMIT 10 OFFSET 0

두 번째 페이지: LIMIT 10 OFFSET 10

OFFSET은 “몇 개를 건너뛸지”를 뜻합니다. API와 연결되는 페이지네이션은 이후 주차에서 확장합니다.

### 1-4. 도서 목록과 LIMIT/OFFSET

제공된 기준 ERD와 공통 데이터를 바탕으로, 요구사항을 결과 → 테이블 → 관계 → 조건 → 정렬·범위 순서로 SQL로 바꿉니다.

이제 1주차 온라인 도서 대여 관리 시스템의 요구사항을 직접 조회 쿼리로 바꿔 봅시다.

각 쿼리는 실행 결과와 요구사항 문장이 일치하는지까지 확인합니다.

실습 대상: 온라인 도서 대여 관리 시스템

공통 기준: 제공된 ERD와 01_schema.sql·02_seed.sql

확장 과제: 자신의 1주차 ERD에서 비슷한 조회 요구사항 한 가지 만들기

# 🔖 2주차 본문

---

관계와 조건은 ERD에 표시한 뒤 SQL로 옮깁니다.

## 2. 예시로 실습하는 온라인 도서 대여 SQL 작성법

## 2-1. 요구 사항

카테고리별 대여 가능 도서 목록

“문학 카테고리에서 대여 가능한 도서를 최신순으로 10권 보여 준다.”

- 결과: 책 제목, 설명, 카테고리 이름
- 테이블: book, category
- 관계: book → category
- 조건: 카테고리 이름이 문학, 대여 가능 상태
- 정렬·범위: book_id 내림차순, 10개

### 2-2. 내가 대여 중인 책

“로그인한 사용자가 아직 반납하지 않은 책을 반납 예정일 순으로 보여 준다.”

- 결과: 책 제목, 대여일, 반납 예정일
- 테이블: rental, book
- 관계: rental → book
- 조건: 현재 로그인한 사용자, returned_at이 NULL
- 정렬: due_at 오름차순

### 2-3. 도서 상세의 태그와 좋아요 여부

“책 상세 화면에서 태그 목록과 현재 사용자의 좋아요 여부를 함께 확인한다.”

- 결과: 책 제목, 태그 이름, 좋아요 여부
- 테이블: book, book_tag, tag, book_like
- 관계: book → book_tag → tag / book → book_like
- 조건: 선택한 book_id와 현재 로그인한 user_id

### 2-4. 실습 순서

1. 1주차 기준 ERD에서 필요한 테이블과 PK/FK 관계에 표시합니다.
2. 화면에 보여 줄 컬럼을 SELECT에 먼저 적습니다.
3. 기준 테이블을 FROM에 적고, ERD의 관계를 따라 필요한 JOIN만 연결합니다.
4. 현재 사용자, 카테고리, 대여 가능 상태처럼 결과를 좁히는 조건을 WHERE에 적습니다.
5. 목록이면 ORDER BY와 LIMIT을 마지막에 추가합니다.
6. 제공된 더미 데이터에서 실행한 결과가 요구사항 문장과 같은지 확인합니다.

## 3. 쿼리 작성 전 고려해야 할 사항

- 화면에 쓰지 않는 컬럼까지 SELECT *로 가져오지 않았나요?
- JOIN한 테이블마다 PK/FK 관계에 맞는 ON 조건을 적었나요?
- 현재 사용자, 카테고리, 대여 가능 상태처럼 빠지면 안 되는 조건을 WHERE에 넣었나요?
- 목록이라면 일관된 정렬 기준과 LIMIT이 있나요?
- 더미 데이터에서 결과가 0건일 때도 그 이유를 설명할 수 있나요?

FROM → JOIN → WHERE → SELECT → ORDER BY → LIMIT 순서로 생각하며 실행 결과를 확인합니다.

# 🎯 핵심 키워드

---

<aside>
💡 주요 내용들에 대해 조사해보고, 자신만의 생각을 통해 정리해보세요!
레퍼런스를 참고하여 정의, 속성, 장단점 등을 적어주셔도 됩니다.
조사는 공식 홈페이지 **Best**, 블로그(최신 날짜) **Not Bad**

</aside>

- 1. 요구사항 → SQL로 번역하기
    
    찾아보기: 화면 요구사항을 SELECT 컬럼, FROM 테이블, JOIN 관계, WHERE 조건, ORDER BY/LIMIT으로 나누는 방법을 정리해 보세요.
    
- 2. DDL과 DML
    
    찾아보기: CREATE TABLE이 테이블 구조를, INSERT가 행 데이터를 담당하는 이유와 ALTER TABLE과의 차이를 살펴보세요.
    
- 3. PK·FK와 JOIN 조건
    
    찾아보기: PK·FK가 무엇을 보장하는지, ON 절에서 관계가 잘못 연결되면 왜 중복 행이 생기는지 확인해 보세요.
    
- 4. WHERE와 NULL
    
    찾아보기: WHERE 조건에서 NULL을 = 과 비교할 수 없는 이유와 IS NULL을 사용하는 이유를 알아보세요.
    
- 5. ORDER BY와 일관된 정렬
    
    찾아보기: ORDER BY가 없을 때 목록 순서가 보장되지 않는 이유와 동일 값일 때의 보조 정렬 기준을 찾아보세요.
    
- 6. LIMIT / OFFSET과 페이지네이션
    
    찾아보기: LIMIT/OFFSET이 페이지 번호 방식과 어떻게 연결되는지, 데이터가 많아질 때 어떤 한계가 있는지 살펴보세요.
    

# 📢 학습 후기

---

- 이번 주차 워크북을 해결해보면서 어땠는지 회고해봅시다.
- 핵심 키워드에 대해 완벽하게 이해했는지? 혹시 이해가 안 되는 부분은 뭐였는지?

<aside>
💡

</aside>

# ✅ 실습 체크리스트

---

- [ ]  MySQL Server와 Workbench를 설치하고 SELECT VERSION(); 실행을 확인했다.
- [ ]  제공된 01_schema.sql과 02_seed.sql을 순서대로 실행했다.
- [ ]  1주차 기준 ERD에서 필요한 테이블과 PK/FK 관계를 다시 확인했다.
- [ ]  대여 가능한 책을 조회하는 단일 테이블 쿼리를 1개 이상 실행했다.
- [ ]  카테고리 또는 대여 정보가 필요한 JOIN 쿼리를 1개 이상 실행했다.
- [ ]  도서 목록 쿼리에 ORDER BY와 LIMIT/OFFSET을 적용하고 결과를 검증했다.

# 🔥 미션

---

<aside>
🔥

제공된 온라인 도서 대여 관리 시스템 기준 ERD와 더미 데이터를 바탕으로 3개 조회 쿼리를 작성합니다. 마지막에는 자신의 1주차 ERD로 조회 요구사항 1개를 확장합니다.

</aside>

1. 미션 1. 문학 카테고리의 대여 가능한 도서를 최신순으로 10개 조회합니다.
    - 미션 1 결과에는 책 제목, 설명, 카테고리 이름을 포함합니다.
    - 미션 2. 특정 사용자가 아직 반납하지 않은 책을 반납 예정일 순으로 조회합니다.
2. 미션 2 결과에는 책 제목, 대여일, 반납 예정일을 포함합니다.
    - 미션 3. 특정 책의 태그 목록과 특정 사용자의 좋아요 여부를 조회합니다.
    - 각 쿼리에서 기준 테이블, JOIN한 이유, WHERE 조건, 정렬·목록 기준을 설명합니다.
    - 확장. 자신의 1주차 ERD에서 같은 방식으로 화면 조회 요구사항 1개와 SQL을 작성합니다.
3. 공통 더미 데이터에서 실행한 결과를 캡처합니다.
    - 1주차 기준 ERD 또는 자신의 ERD에서 JOIN 경로를 표시합니다.
    - 실행 결과가 요구사항 문장과 일치하는지 한 문장으로 검증합니다.

## 제출물

- 01_schema.sql·02_seed.sql 실행 확인 화면, 요구사항별 SQL 파일 또는 실행 화면 캡처
- 각 쿼리 아래에 기준 테이블, JOIN한 이유, WHERE 조건, 정렬·목록 기준을 2~3문장으로 설명합니다.
- 공통 실습 3개 결과와 자신의 1주차 ERD 확장 쿼리 1개를 제출합니다.

# 💪 미션 기록

---

<aside>
🍀 미션 기록의 경우, 아래 미션 기록 토글 속에 작성하시거나, 페이지를 새로 생성하여 해당 페이지에 기록하여도 좋습니다!

하지만, 결과물만 올리는 것이 아닌, **중간 과정 모두 기록하셔야 한다는 점!** 잊지 말아주세요.

</aside>

미션을 수행하며 아래 질문에 답해 기록해 주세요.

- 어떤 요구사항에서 어떤 테이블을 기준으로 시작했나요?
- JOIN이 필요한 이유를 1주차 기준 ERD의 관계로 설명할 수 있나요?
- 더미 데이터에서 결과가 예상과 달랐을 때 어떤 조건 또는 관계를 먼저 확인했나요?
- **미션 기록**
    
    ERD 사진
    
    [](https://app.notion.com)
    
    설명
    
    <aside>
    
    </aside>
    

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

# ⚡ 트러블 슈팅

---

<aside>
💡 실습하면서 생긴 문제들에 대해서, **이슈 - 문제 - 해결** 순서로 작성해주세요.

</aside>

<aside>
💡 스스로 해결하기 어렵다면? 스터디원들에게 도움을 요청하거나 **너디너리의 지식IN 채널에 질문**해보세요!

</aside>

- ⚡이슈 작성 예시 (이슈가 생기면 아래를 복사해서 No.1, No.2, No3 … 으로 작성해서 트러블 슈팅을 꼭 해보세요!)
    
    **`이슈`**
    
    👉 런타임 단계에서 SQLException: Access denied for user 'root'@'localhost' (using password: YES) 이 발생했다
    
    **`문제`**
    
    👉 application.yml에 DB 부분에 username, password를 로컬 DB username, password와 일치하지 않았다
    
    **`해결`**
    
    👉  로컬 DB 접속할때 쓰는 username, password를 제대로 기입했다
    
    **`참고레퍼런스`**
    
    - 링크
- ⚡이슈 No.1
    
    **`이슈`**
    
    👉 [트러블이 생긴 상태 작성]
    
    **`문제`**
    
    👉 [어떤 이유로 해당 이슈가 일어났는지 작성]
    
    **`해결`**
    
    👉  [해결 방법 작성]
    
    **`참고레퍼런스`**
    
    - [문제 해결 시 참고한 링크]

---

Copyright © 2026 UMC 11th Workbook TF All rights reserved.