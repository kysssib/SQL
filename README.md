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
        ({애트리뷰트이름 데이터타입 [Not NULL][기본값정의]}⁺
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
        ([Add 추가할애트리뷰트이름 데이터타입][기본값정의]|[Drop 삭제할애트리뷰트이름][삭제조건]|[Alter 변경할애트리뷰트이름 (Drop Default | Set Default 기본값정의)]);
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
    |<u>학번<br>(Sno)</u>|이름<br>(Sname)|학년<br>(Year)|학과<br>(Dept)|
    |:---:|:---:|:---:|:---:|
    |100|나 수 영|4|컴퓨터|
    |200|이 찬 수|3|전기|
    |300|정 기 태|1|컴퓨터|
    |400|송 병 길|4|컴퓨터|
    |500|박 종 화|2|산공|

- 과목 (COURSE)
    |<u>과목번호<br>(Cno)</u>|과목이름<br>(Cname)|학점<br>(Credit)|학과<br>(Dept)|담당교수<br>(PRname)|
    |:---:|:---:|:---:|:---:|:---:|
    |C123|프로그래밍|3|컴퓨터|김성국|
    |C312|자료구조|3|컴퓨터|황수관|
    |C324|파일구조|3|컴퓨터|이규찬|
    |C413|데이터베이스|3|컴퓨터|이일로|
    |E412|반 도 체|3|전자|홍봉진|
    
- 등록 (ENROL)
    |<u>학번<br>(Sno)</u>|<u>과목번호<br>(Cno)</u>|성적<br>(Grade)|중간성적<br>(Midtrerm)|기말성적<br>(Final)|
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

