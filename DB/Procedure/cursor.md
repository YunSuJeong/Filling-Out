# CURSOR 너 내 동료가 되라.!

### CURSOR 좀 어색할지두..

### MISSION 회사에서 FOR LOOP로만 데이터를 변경했다면 이번엔 커서를 이용하여 직접했던 반복적인 작업을 줄여보자❤️‍🔥
#### 🔖history
> A, B, C 프로그램 각각에 해당하는 코드를 시스템상에서 사용자가 수동으로 등록하여 사용할 수 있었다.  
> 하지만 사용자쪽에선 각 코드명을 각각의 코드규칙에 따라 수동입력하는 것이 불편하게 느껴졌고<br>(실제로 코드명은 유일성을 만족해야 했기 때문에 더 귀찮았을 듯)  
> 코드가 등록될 때 자동적으로 코드명이 부여되어 저장될 수 있도록 수정요청이 들어왔다.  
> 시스템 로직은 변경하였지만 기존 부여된 코드들이 존재했기에 기존 데이터들도 변경해줘야하는 상황,,  
> 귀차니즘이 극에 달했기 때문에, 구글링하다가 알게된 FOR LOOP블록을 이용해 손쉽게 대략 250건 정도의 데이터 변경 성공!  
> 그러나 3번의 FOR LOOP블록을 각각 실행하여 데이터 변경하는 것조차 귀찮았다..  
> 그렇게 2주의 시간이 흐르고 맞이한 스터디에서 처음 알게된 '커서'의 존재,,  
> 이거로 실습하면 딱이겠다 싶어 스터디 과제로 선정하게 되었다. 땅땅

<br><br><br>

```
-- A,B는 같은 프로그램으로 구분컬럼 존재, C는 아예 테이블 자체가 다름

-- 프로그램 구분값을 입력변수로 받아 SDDPC_KND_CD, SDDPC_CD를 내부변수로 선언하여 정의하면 될 듯 (정리예정)
select TO_CHAR(input_dm, 'yyyy'), count(1) from SY_DICA_D_PGM_CODE where SDDPC_KND_CD = '0002' group by TO_CHAR(input_dm, 'yyyy') order by TO_CHAR(input_dm, 'yyyy');

-- where조건의 년도는 위 select문에서 cursor로 한개씩 받아오면 될 듯 (정리예정)
BEGIN
    FOR sddpc IN (SELECT SDDPC_SEQ, TO_CHAR(input_dm, 'yy') AS YY FROM SY_DICA_D_PGM_CODE WHERE SDDPC_KND_CD = '0001' and TO_CHAR(input_dm, 'yyyy') = '2020' ORDER BY INPUT_DM) LOOP
        UPDATE
            SY_DICA_D_PGM_CODE
        SET
            SDDPC_CD = 'P' || sddpc.YY || LPAD(UPDATE_SAMPLE_SEQ.NEXTVAL, 3, '0') -- 한 프로그램의 한 년도마다 초기화되서 1부터 들어가야하기 때문에 seq초기화하는 로직 필요 (정리예정)
        WHERE
           SDDPC_SEQ = sddpc.SDDPC_SEQ
           AND SDDPC_KND_CD = '0001';
    END LOOP;
END;

```

<br><br>
[참고출처]  
https://bacha.tistory.com/20  
https://coding-factory.tistory.com/455  
