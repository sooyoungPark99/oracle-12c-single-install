# 4. Oracle 12c Database 생성

### 1. DB 생성(DBCA)

oracle 유저로 dbca를 실행한 뒤, 데이터베이스 생성을 선택한다.

![image.png](image.png)

생성 모드는 고급 구성을 선택하고, 컨테이너 데이터베이스 구성은 체크한다.

![image.png](image%201.png)

Oracle 일반 인스턴스 데이터베이스 선택
기본 제공 템플릿 중 "범용 또는 트랜잭션 처리"를 선택

![image.png](image%202.png)

DB 이름과 SID는 ora12로 설정한다.

![image.png](image%203.png)

저장 영역 유형은 파일 시스템으로 선택한다.

![image.png](image%204.png)

**빠른 복구 영역**을 활성화하고, 저장 영역 유형을 **파일 시스템**으로 선택한다.

![image.png](image%205.png)

기존 LISTENER(포트 1521)를 그대로 사용한다.

![image.png](image%206.png)

실습 환경이므로 별도의 보안 옵션 구성 없이 진행한다.

![image.png](image%207.png)

데이터베이스에 샘플 스키마 추가를 체크한다.

![image.png](image%208.png)

EM Database Express를 활성화하고 포트를 5560으로 설정한다.

![image.png](image%209.png)

편의상 모든 계정에 동일한 관리자 비밀번호를 설정한다(oracle).

![image.png](image%2010.png)

데이터베이스 생성, 템플릿 저장, 생성 스크립트 저장 옵션을 선택한다.

![image.png](image%2011.png)

최종 설치 구성 정보를 확인한 뒤 DB 생성을 시작한다.

![image.png](image%2012.png)

![image.png](image%2013.png)

아래 화면이 나오면 설치가 완료된다.

![image.png](image%2014.png)

---

### 2. 최종 점검

#### PMON 프로세스 확인

```bash
[oracle@oracle12c ~]$ ps -ef | grep pmon
```

#### .bash_profile 설정 및 접속 확인(예)

```bash
[oracle@oracle12c ~]$ vi .bash_profile
[oracle@oracle12c ~]$ cat .bash_profile

# (중략)
export ORACLE_BASE=/u01/app/oracle
export ORACLE_HOME=/u01/app/oracle/product/12.2.0/dbhome_1
export ORA_INVENTORY=/u01/app/oraInventory
export ORACLE_SID=ora12
export TNS_ADMIN=/u01/app/oracle/product/12.2.0/dbhome_1/network/admin
export PATH=$PATH:$HOME/bin:$ORACLE_HOME/bin
export LD_LIBRARY_PATH=$ORACLE_HOME/lib:/lib:/usr/lib
export CLASSPATH=$ORACLE_HOME/JRE:$ORACLE_HOME/jlib:$ORACLE_HOME/rdbms/jlib
export NLS_LANG=KOREAN_KOREA.AL32UTF8

alias sys='sqlplus / as sysdba'
alias scott='sqlplus scott/tiger'
alias net='cd /u01/app/oracle/product/12.2.0/dbhome_1/network/admin/'

[oracle@oracle12c ~]$ source .bash_profile
[oracle@oracle12c ~]$ sys
```

#### 인스턴스 OPEN 확인

```sql
select instance_name, status from v$instance;
-- ora12 / OPEN
```