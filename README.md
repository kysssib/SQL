# SQL
1. 대소문 구분 X

## 데이터베이스 생성

```sql
Create Database 데이터베이스이름 Authorization 소유자이름;
```

## 도메인

- 생성

    ```sql
    Create Domain 도메인이름 데이터타입
        [기본값정의]
        [도메인제약조건리스트];
    ```

    <details><summary>데이터 타입</summary>

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
    </details>

    <details><summary>기본값정의</summary>
    Default '???'
    
    - 값을 입력하지 않으면 '???'가 들어감
    </details>
    
    <details><summary>도메인제약조건</summary>
    Check(Value In ('값1','값2'...))

    -  ('값1','값2'...) 안에 Value가 안에 있는가 확인
    </details>

- 변경

    ```sql
    Alter Domain 도메인이름 <변경내용>;
    ```

- 삭제

    ```sql
    Drop Domain 도메인이름 삭제조건;
    ```
    
    <details><summary>삭제조건</summary>
    Restrict
    
    - 다른 곳에서 이 도메인 참조 안할 때 삭제

    Cascade

    - 강제 삭제


## 테이블

- 생성

    ```sql
    Create Table 테이블이름
        {애트리뷰트이름 데이터타입}
    ```
