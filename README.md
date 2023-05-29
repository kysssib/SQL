# SQL
- 주의사항
1. 대소문 구분 X 단, Value라면 구분해야함
2. 엔터 구분 X 명령어 구분은 오로지 ;
3. [] : 생략 가능
4. <sup>+</sup> : 1개 이상 존재
5. <sup>*</sup> : 0개 이상 존재
6. {} : 단위 문장으로 묶음

---

## 데이터베이스
- 생성

    ```sql
    Create Database 데이터베이스이름 Authorization 소유자이름;
    ```
    [예시](#데이터베이스-생성-예시)
- 제거
    ```sql
    DROP Database 데이터베이스이름 {삭제조건};
    ```
    - [삭제조건](#삭제조건)

    [예시](#데이터베이스-삭제-예시)

---

## 도메인

- 생성

    ```sql
    Create Domain 도메인이름 데이터타입
        [기본값정의]
        [Constraint 제약조건이름(제약조건)];
    ```

    - [데이터타입](#데이터타입)
    - [기본값정의](#기본값정의)
    - [제약조건](#제약조건)

- 변경

    ```sql
    Alter Domain 도메인이름 <변경내용>;
    ```

- 삭제

    ```sql
    Drop Domain 도메인이름 [삭제조건];
    ```
    - [삭제조건](#삭제조건)
    
---

## 테이블

- 생성

    ```sql
    Create Table 테이블이름
        ({애트리뷰트이름 데이터타입 [Not NULL][기본값정의]}+
        [Primary Key (애트리뷰트이름들),]
        {[Union (애트리뷰트이름들),]}*
        {[Foreign Key (애트리뷰트이름들)
            References 테이블이름[(애트리뷰트이름들)]
            [On Delete 옵션]
            [On Update 옵션],]}*
        [Constraint 제약이름][제약조건]);
    ```
    - [기본값정의](#기본값정의)
    - [데이터타입](#데이터타입)
    - [제약조건](#제약조건)

    [예시](#테이블-생성-예시)

- 변경
    ```sql
    Alter Table 테이블이름
        ([Add 추가할애트리뷰트이름 데이터타입][기본값정의]|
        [Drop 삭제할애트리뷰트이름][삭제조건]|
        [Alter 변경할애트리뷰트이름 (Drop Default | Set Default 기본값정의)]);
    ```
    - [데이터타입](#데이터타입)
    - [삭제조건](#삭제조건)
    - [기본값정의](#기본값정의)
    [예시](#테이블-변경-예시)

- 제거
    ```sql
    DROP Table 테이블이름
        {삭제조건};
    ```
    - [삭제조건](#삭제조건)

[관계데이터베이스 예시](#관계데이터베이스-예시)

---
 
## 검색

- 페쇄 시스템
    - 리턴값이 테이블
    - 중첩 질의가 가능

- SQL과 이론적 관계 모델의 차이
    - 한 테이블 내 같은 행 중복이 가능
    - 기본키 필수 X
    - 이론 상 SQL테이블 ≠ 튜플 집합
    - 같은 원소 중복 허용 => 다중집합/백
        - DISTINCT를 명세해 중복 제거

- <p id='검색기본구조'>기본 구조</p>

    ```sql
    Select 열리스트
    From 테이블리스트
    Where 조건문;
    ```

- <p id='검색일반형식'>일반적 형식</p>

    ```sql
    Select [All|Distinct] 열리스트
    From 테이블리스트
    [Where 조건문]
    [Group By 열리스트
    [Having 조건문]]
    [Order By 열리스트 [ASC|DESC]];
    ```
    - [Select 열리스트 문](#select-열리스트)은 출력결과 행의 이름을 명세
        - All:열 전체 선택,Distinct:출력 열의 중복 제거
    - [From 테이블리스트 문](#from-테이블리스트)은 참조할 테이블들을 명세
    - [Where 조건문](#조건문)은 참조할 테이블의 조건을 명세
        - 부속 질의문이 들어가기도 함
    - [Group By 문](#group-by-열리스트)은 그룹으로 묶을 열을 명세
    - Having문은 그룹의 조건을 명세
    - Order By문은 출력 순서를 명세
        - ASC:오름차순,DESC:내림차순
        - 여러개 지정 가능 순서대로 순차 정렬

- 검색문 합병
    - Union으로 합병
    - 합병 가능성 확인
        - 열의 차수 동일
        - 열의 도메인이 동일
    - 중복 제거됨

[검색 예시](#검색-예시)
       
---

## 갱신
- 일반적 형식
    ```sql
    Update 테이블이름
    Set {열이름=산술식}+
    [Where 조건];
    ```
    - [Where 조건문](#조건문)이 공란이면 모든 열이 변경됨

---

## 삽입
- 일반적 형식
    ```sql
    Insert
    Into 테이블[(열이름들)]
    Values (열값들);
    ```
    - 순서 중요
    - 열이름을 쓰지 않으면 정의한 순서대로 자동 매칭

    ```sql
    Insert
    Into 테이블[(열이름들)]
    Select 문장;
    ```
    - Select로 생성한 모든 튜플을 삽입함

---

## 삭제
- 일반적 형식
    ```sql
    Delete
    From 테이블이름
    [Where 조건];
    ```
    - [Where 조건문](#조건문)이 공란이면 모든 열이 삭제됨
---

##











---
---
참조
---
#### 데이터베이스 생성 예시
```sql
Create Database University Authorization SHLEE;
``` 
또는
```sql
Create Schema University Authorization SHLEE;
``` 
[데이터베이스](#데이터베이스)

---
#### 데이터베이스 삭제 예시
```sql
Drop Database University Restrict;
``` 
또는
```sql
Drop Database University Cascade;
``` 
[데이터베이스](#데이터베이스)

---

#### 기본값정의
```sql
Default '???'
```

- 값을 입력하지 않으면 '???'가 들어감

[도메인](#도메인)

[테이블](#테이블)

---

#### 제약조건

```sql
Check(Value In ('값1','값2'...))
```
-  ('값1','값2'...) 안에 Value가 안에 있는가 확인

[도메인](#도메인)

[테이블](#테이블)

---

#### 삭제조건

    Restrict
    
    - 다른 곳에서 이 도메인 참조 안할 때 삭제

    Cascade

    - 강제 삭제

[데이터베이스](#데이터베이스)

---

#### 데이터타입

    - 숫자
        - Int, Integer, Samllint : 정수
        - Float(n), Real, Double Precision : 실수(n은 소수점 n자리까지)
        - Decimal(i,j), Numeric(i,j) : 정형 숫자(전체 i자리 숫자, 그 중 소수점 j자리)
    - 문자 스트링
        - Char(n) : n자리 고정 문자
        - Varchar(n) : 초기 n자리 가변 문자열(기본적으로 n = 2)
    - 비트 스트링
        - Bit(n), Bit Varying(n)
    - 날짜
        - Date : YY-MM-DD
    - 시간
        - Time : hh:mm:ss
        - Timestamp : Date, Time포함
        - Interval : Date, Time, Timestamp 포함
[도메인](#도메인)

[테이블](#테이블)

---

#### 테이블 생성 예시
```sql
Create Table ENROL
    (Sno Integer Not Null,
    Cno Char(6) Not Null,
    Grade Int,
    Primary Key(Sno, Cno),
    Foreign key(Sno) References STUDENT(sno)
        on Delete Cascade
        on Update Cascade,
    Foreign Key(Cno) References COURSE
            on Delete Cascade
            on Update Cascade,
    Check(Grade >= 0 And Grade <= 100));
```
<details><summary>설명</summary>

> Sno는 Int형이며 Null이 불가

> Cno는 Int형이며 Null이 불가

> Grade는 Int형

> Primary Key는 Sno와 Cno의 조합

> Foreign Key인 Sno는 Student 테이블의 sno에서 왔으며 참조 테이블이 삭제/변형되면 같이 삭제/변형

> Foreign Key인 Cno는 Course 테이블에서 왔으며 참조 테이블이 삭제/변형되면 같이 삭제/변형 (애트리뷰트 이름이 대소문 구분 없이 동일하므로 생략)

> 이 테이블의 조건은 Grade값은 0보다 크고 100보다 작아야 한다
</details>

[테이블](#테이블)

---
#### 테이블 변경 예시
```sql
Alter Table Enrol
    Add Final Char Default 'F';

Alter Table Enrol
    Drop Grade Cascade;
```

[테이블](#테이블)

---
#### 관계데이터베이스 예시
- 학생 (STUDENT)
    |**학번<br>(Sno)**|이름<br>(Sname)|학년<br>(Year)|학과<br>(Dept)|
    |:---:|:---:|:---:|:---:|
    |100|나 수 영|4|컴퓨터|
    |200|이 찬 수|3|전기|
    |300|정 기 태|1|컴퓨터|
    |400|송 병 길|4|컴퓨터|
    |500|박 종 화|2|산공|

- 과목 (COURSE)
    |**과목번호<br>(Cno)**|과목이름<br>(Cname)|학점<br>(Credit)|학과<br>(Dept)|담당교수<br>(PRname)|
    |:---:|:---:|:---:|:---:|:---:|
    |C123|프로그래밍|3|컴퓨터|김성국|
    |C312|자료구조|3|컴퓨터|황수관|
    |C324|파일구조|3|컴퓨터|이규찬|
    |C413|데이터베이스|3|컴퓨터|이일로|
    |E412|반 도 체|3|전자|홍봉진|
    
- 등록 (ENROL)
    |**학번<br>(Sno)**|**과목번호<br>(Cno)**|성적<br>(Grade)|중간성적<br>(Midtrerm)|기말성적<br>(Final)|
    |:---:|:---:|:---:|:---:|:---:|
    |100|C413|A|90|95|
    |100|E412|A|95|95|
    |200|C123|B|85|80|
    |300|C312|A|90|95|
    |300|C324|C|75|75|
    |300|C413|A|95|90|
    |400|C312|A|90|95|
    |400|C324|A|95|90|
    |400|C413|B|80|85|
    |400|E412|C|65|75|
    |500|C312|B|85|80|

[테이블](#테이블)

---

#### 조건문
- 기본적으로 True or False로 반환됨
    - 열이름 = value, 열이름 >= value #값 비교 가능
    - 테이블이름.열이름 = value #테이블을 명시함
    - 조건 AND 조건 또는 조건 OR 조건 가능
    - [집계 함수](#집계함수) 사용가능
    - 열이름 [Not] In (부속 Select문) 으로 부속 질의문 생성이 가능
        - 위는 부속 질의문으로 생성된 열 값이 해당 열이름에 존재하는가[존재하지 않는가] 확인
        - In 대신 등호류 사용 가능
        - [Division 예시 확인](#디비젼-예시)
    - [Like문](#like) 사용 가능
        - 열이름에서 Sub String 패턴을 갖는 튜플을 확인
    - Null 파악
        - = 사용 안함
        - is [Not]을 사용
        - 열이름 is[Not] Null
    - Exists 사용
        - [Not] Exists (부속 select문)
        - 부속 질의문 Select가 공집합이 아니면 본 Select문 실행

[검색](#검색기본구조)

[갱신](#갱신)

[삭제](#삭제)

---


#### 검색 예시

```sql
select sname, sno
from student
where dept='컴퓨터';
```
[검색기본구조](#검색기본구조)

```sql
select S1.sno, S2.sno
from student s1, student s2
where s1.dept=s2.dept and s1.sno<s2.sno;
```

```sql
select cno, Avg(final) as 평균
from enrol
group by cno
having count(*) >= 3;
```

```sql
select sname
from student
where sno in (
                select sno
                from enrol
                where cno='C413');
```

[검색일반형식](#검색일반형식)

[검색](#검색)

---

#### Select 열리스트
- 기본적으로 열 이름들이 나옴
- 테이블명.열이름 형식의 직접 명시 가능
- 재정의이름.열이름 식도 가능
    - 단, from절에서 명시 필수
    - [하단 참조 참고](#from-테이블리스트)
- 열이름 As 재정의열이름 도 가능
- 열이름 사용 산술식 사용 가능

[검색](#검색일반형식)

---

#### From 테이블리스트
- 기본적으로 테이블 이름들이 나옴
- 열이름 재정의 가능
    - 형식 : 테이블명 재정의이름, ...
- 조인을 명시 가능
    - 테이블명 Join 테이블명 On(조건문)
        - 조건문 기준 join함
    - 테이블명 Join 테이블명 Using(열이름)
        - 열이름을 사용해 Join
    - 테이블명 Natural Join 테이블명
        - 자연조인 가능한 경우 가능

[검색](#검색일반형식)

---

#### Group By 열리스트
- 그룹으로 묶을 열을 명세
- 보통 [Select문](#select-열리스트)에 스칼라 값이 나오면 꼭 같이 나옴
    - [집계 함수](#집계함수)와 같이 나옴

[검색](#검색일반형식)

---

#### 집계함수

- count([All|Distinct]열이름) : 튜플에 개수를 셈
- Sum(열이름) : 열 Value의 합
- Avg(열이름) : 열 Value의 평균
- Max(열이름) : 열 Value의 최댓값
- Min(열이름) : 열 Value의 최솟값

[조건문](#조건문)

[상위 참조](#group-by-열리스트)

---

#### 디비젼 예시

```sql
select sno, cno
from enrol
where final> All
    (select final
    from enrol
    where sno =500);
```
- 해석
    - 학번 과번 추출
    - 등록 테이블에서
    - 기말점수가 좋은
        - 학번이 500인 모든 기말 점수보다

- Enrol ÷ (select 부속 질의문)
- 디비젼은 디비젼 하는 튜플의 값을 **모두 가지고** 있는 튜플 중 디비젼 하는 값 제외 출력

[조건문](#조건문)

---

#### Like
- % 어떤 길의의 문자 상관 X (0~)
- \- 어떤 문자 단 하나를 의미 (1)
- 열이름 Like '서브스트링'

ex : 'C%'
- 시작이 C인 모든 문자열

[조건문](#조건문)

---

####
