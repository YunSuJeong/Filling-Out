# CURSOR 너 내 동료가 되라.!

### CURSOR 좀 어색할지두..

### ❤️‍🔥MISSION : 회사에서 FOR LOOP로만 변경한 데이터 이번엔 커서를 이용하여 직접했던 반복작업을 줄여보자!
#### 🔖history
> A, B, C 프로그램 각각에 해당하는 코드를 시스템상에서 사용자가 수동으로 등록하여 사용할 수 있었다.  
> 하지만 사용자쪽에선 각 코드명을 각각의 코드규칙에 따라 수동입력하는 것이 불편하게 느껴졌고<br>(실제로 코드명은 유일성을 만족해야 했기 때문에 더 귀찮았을 듯)  
> 코드가 등록될 때 자동적으로 코드명이 부여되어 저장될 수 있도록 수정요청이 들어왔다.  
> 시스템 로직은 변경하였지만 기존 부여된 코드들이 존재했기에 기존 데이터들도 변경해줘야하는 상황,,  
> 귀차니즘이 극에 달했기 때문에, 구글링하다가 알게된 FOR LOOP블록을 이용해 손쉽게 대략 250건 정도의 데이터 변경 성공!  
> 그러나 각 프로그램마다 년도를 구분하여 update해줘야 했기때문에 FOR LOOP블록을 조건 변경해가며 10번이상 실행해줘야했다,,(실수할까봐 쫄고..귀찮았음..)
> 그렇게 2주의 시간이 흐르고 맞이한 스터디에서 처음 알게된 '커서'의 존재,,  
> 이거로 실습하면 딱이겠다 싶어 스터디 과제로 선정하게 되었다. 땅땅

<br><br><br>

#### 기존 코드값 update 쿼리
```
/* A프로그램 */
select TO_CHAR(input_dm, 'yyyy') from SY_DICA_D_PGM_CODE where SDDPC_KND_CD = '0001' group by TO_CHAR(input_dm, 'yyyy') order by TO_CHAR(input_dm, 'yyyy');

-- 년도마다 아래 블록 년도 조건 변경 + 시퀀스 DROP 후 재생성하여 실행줬어야함
BEGIN
    FOR sddpc IN (SELECT SDDPC_SEQ, TO_CHAR(input_dm, 'yy') AS YY FROM SY_DICA_D_PGM_CODE WHERE SDDPC_KND_CD = '0001' and TO_CHAR(input_dm, 'yyyy') = '2020' ORDER BY INPUT_DM) LOOP
        UPDATE
            SY_DICA_D_PGM_CODE
        SET
            SDDPC_CD = 'P' || sddpc.YY || LPAD(UPDATE_SAMPLE_SEQ.NEXTVAL, 3, '0') 
        WHERE
           SDDPC_SEQ = sddpc.SDDPC_SEQ
           AND SDDPC_KND_CD = '0001';
    END LOOP;
END;

/* B프로그램 */
select TO_CHAR(input_dm, 'yyyy') from SY_DICA_D_PGM_CODE where SDDPC_KND_CD = '0001' group by TO_CHAR(input_dm, 'yyyy') order by TO_CHAR(input_dm, 'yyyy');

BEGIN
    FOR sddpc IN (SELECT SDDPC_SEQ, TO_CHAR(input_dm, 'yy') AS YY FROM SY_DICA_D_PGM_CODE WHERE SDDPC_KND_CD = '0002' and TO_CHAR(input_dm, 'yyyy') = '2023' ORDER BY INPUT_DM) LOOP
        UPDATE
            SY_DICA_D_PGM_CODE
        SET
            SDDPC_CD = 'A' || sddpc.YY || LPAD(UPDATE_SAMPLE_SEQ.NEXTVAL, 3, '0')
        WHERE
           SDDPC_SEQ = sddpc.SDDPC_SEQ
           AND SDDPC_KND_CD = '0002';
    END LOOP;
END;

/* C프로그램 */
select TO_CHAR(input_dm, 'yyyy'), count(1) from SY_TS_CODE_MNGT group by TO_CHAR(input_dm, 'yyyy') order by TO_CHAR(input_dm, 'yyyy');

BEGIN
    FOR stcm IN (SELECT STCM_SEQ, TO_CHAR(input_dm, 'yy') AS YY FROM SY_TS_CODE_MNGT WHERE TO_CHAR(input_dm, 'yyyy') = '2023' ORDER BY INPUT_DM) LOOP
        UPDATE
            SY_TS_CODE_MNGT
        SET
            STCM_CD = 'G' || stcm.YY || LPAD(UPDATE_SAMPLE_SEQ.NEXTVAL, 3, '0')
        WHERE
           STCM_SEQ = stcm.STCM_SEQ;
    END LOOP;
END;



```

#### 로직 설계
A,B는 같은 프로그램으로 구분컬럼 존재, C는 아예 테이블 자체가 다름
프로그램 구분값을 입력변수로 받아 SDDPC_KND_CD, SDDPC_CD를 내부변수로 선언하여 정의하면 될 듯 (정리예정)
where조건의 년도는 위 select문에서 cursor로 한개씩 받아오면 될 듯 (정리예정)
한 프로그램의 한 년도마다 초기화되서 1부터 들어가야하기 때문에 seq초기화하는 로직 필요 (정리예정)

#### 구현
```
-- 0001 : A, 0002 : B, 0003 : C

CREATE OR REPLACE PROCEDURE AUTO_UPDATE_CD (
    -- in/out 변수 선언
    IN_PRGM_TYPE_CD varchar2
) IS
    -- 프로시저 멤버변수 선언
    AUC_SDDPC_CD varchar2;
    AUC_SDDPC_KND_CD varchar2;
    AUC_YY varchar2(4);
BEGIN
    /* 프로그램 유형따라 조건설정 */
    IF IN_PRGM_TYPE_CD = '0001' THEN
        AUC_SDDPC_CD := 'P'
        AUC_SDDPC_KND_CD := '0001'
    ELSEIF IN_PRGM_TYPE_CD = '0002' THEN
        AUC_SDDPC_CD := 'A'
        AUC_SDDPC_KND_CD := '0001'
    ELSE
        AUC_SDDPC_CD := 'G'
    END IF;

    /* 코드 자동 업데이트 로직 시작 */
    IF( IN_PRGM_TYPE_CD = '0001' OR IN_PRGM_TYPE_CD = '0002' ) THEN 
        FOR auto IN ( select TO_CHAR(input_dm, 'yyyy') input_dm from SY_DICA_D_PGM_CODE where SDDPC_KND_CD = AUC_SDDPC_KND_CD group by TO_CHAR(input_dm, 'yyyy') order by TO_CHAR(input_dm, 'yyyy') ) LOOP
    
            /* 자동으로 코드를 부여하기위한 시퀀스 생성 */
            CREATE SEQUENCE UPDATE_SAMPLE_SEQ 
            INCREMENT BY 1
            START WITH 1
            MINVALUE 1; 
    
            /* 년도마다 코드 update */
            FOR sddpc IN (SELECT SDDPC_SEQ, TO_CHAR(input_dm, 'yy') AS YY FROM SY_DICA_D_PGM_CODE WHERE SDDPC_KND_CD = AUC_SDDPC_KND_CD and TO_CHAR(input_dm, 'yyyy') = auto.INPUT_DM ORDER BY INPUT_DM) LOOP
                UPDATE
                    SY_DICA_D_PGM_CODE
                SET
                    SDDPC_CD = AUC_SDDPC_CD || sddpc.YY || LPAD(UPDATE_SAMPLE_SEQ.NEXTVAL, 3, '0') 
                WHERE
                   SDDPC_SEQ = sddpc.SDDPC_SEQ
                   AND SDDPC_KND_CD = AUC_SDDPC_KND_CD;
            END LOOP;
    
            /* 매년 코드 시작은 1부터 시작되어야하기 때문에 시퀀스 삭제 */
            DROP SEQUENCE UPDATE_SAMPLE_SEQ;
            
        END LOOP;
    ELSE
        FOR auto IN ( select TO_CHAR(input_dm, 'yyyy') AS INPUT_DM from SY_TS_CODE_MNGT GROUP BY TO_CHAR(INPUT_DM, 'yyyy') order by TO_CHAR(INPUT_DM, 'yyyy') ) LOOP

            /* 자동으로 코드를 부여하기위한 시퀀스 생성 */
            CREATE SEQUENCE UPDATE_SAMPLE_SEQ 
            INCREMENT BY 1
            START WITH 1
            MINVALUE 1; 

            BEGIN
                FOR stcm IN (SELECT STCM_SEQ, TO_CHAR(INPUT_DM, 'yy') AS YY FROM SY_TS_CODE_MNGT WHERE TO_CHAR(INPUT_DM, 'yyyy') = auto.INPUT_DM ORDER BY INPUT_DM) LOOP
                    UPDATE
                        SY_TS_CODE_MNGT
                    SET
                        STCM_CD = AUC_SDDPC_CD || stcm.YY || LPAD(UPDATE_SAMPLE_SEQ.NEXTVAL, 3, '0')
                    WHERE
                       STCM_SEQ = stcm.STCM_SEQ;
                END LOOP;
            END;

            /* 매년 코드 시작은 1부터 시작되어야하기 때문에 시퀀스 삭제 */
            DROP SEQUENCE UPDATE_SAMPLE_SEQ;

        END LOOP;

    END IF;
    
EXCEPTION WHEN OTHERS THEN 
END;
```

<br><br>
[참고출처]  
https://bacha.tistory.com/20  
https://coding-factory.tistory.com/455  

#### 의문점
Q1. 커서 선언은 선언부에서만 가능한건지,, BEGIN안에서 DECLARE하면 안되나.?
Q2. FOR LOOP도 커서였던거임...? 와아  
https://blog.kjslab.com/20  
