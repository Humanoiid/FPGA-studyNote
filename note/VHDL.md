# VHDL

## VHDL 문법 정리

link: [https://m.blog.naver.com/PostView.nhn?blogId=r2adne&logNo=120155040778&proxyReferer=https:%2F%2Fwww.google.com%2F](https://m.blog.naver.com/PostView.nhn?blogId=r2adne&logNo=120155040778&proxyReferer=https:%2F%2Fwww.google.com%2F)

내용이 많아서 정리 생략

- 기본문법:
    - 대소문자 구분 X
    - 파일명 공백 X
    - 문장구별: ;
    - 주석처리: —
    - 문장 첫글자에 숫자, 특수문자 불가
- VHDL 구성
    - (시스템 외적 입출력선 정의) Entity Declaration: 입출력 선언 (in, out 선언/ 선언부 마지막문장은 ; 없음)
    - (begin, end 사이) Architecture Body: 시스템 동작 세부적으로 정의 (in 값으로 연산을 하여 out을 출력함)
    - (begin 이전) 객체(Object): signal, variable, constant 등의 자료형. 값을 자질 수 있는 객체.
        - signal: VHDL에서 wire로 구현됨. 컴퍼넌트 연결에 사용되는 외적 변수. port는 입출력 구분 있으며, signal은 입출력 구분이 없음. 초기화 := / 대입<= .
        - variable: process 내에서만 유효한 내적변수(지역변수). 중간연산용 변수. 대입 := .
        - constant: 선언된 초기값 변경 불가. 대입시 := . Loop, generate 문, 부프로그램, generic에서 선언됨.
    - 자료형(Data Type):
        - 표현적 분류:
            - predefined data type/ user-defined type
        - 기능적 분류:
            - Scalar type (숫자형):
                - enumeration type - BIT, BOOLEAN, CHARACTER, STD_LOGIC
                - integer type - INTEGER
                - floating type - REAL
                - physical type - UNIT: TIME, DISTANCE
            - composite type (복합형)
    - 연산자(Operator)
    - 동작적 표현(Behavioral Description)
    - 구조적 표현 (Structural Description)
    - 순차 처리문
    - 병행 처리문
