# 외부에서 PostgreSQL 접속하기

<br /><br />

```
PostgreSQL은 기본적으로 127.0.0.1, localhost 외에는
접속 제한이 되어있다.

해결 방법을 알아보자. 
```

<br /><br /><br />

1. 경로 이동

```
* 예시

1) C:\Program Files\PostgreSQL\15\data 폴더 경로 이동
```

<br /><br />

2. pg_hba.conf 파일 수정

```txt
# TYPE  DATABASE        USER            ADDRESS                 METHOD

# IPv4 local connections:
host    all             all             127.0.0.1/32            scram-sha-256
에서

host    all             all             0.0.0.0/0               scram-sha-256
으로 수정 한다.
(전체 아이피 허용 혹은 아이피 지정)
```

<br /><br />

3. postgresql.conf 파일 체크

```txt
# 어떤 IP 주소에서 수신할 것인지
listen_addresses = '*'

(필요 시 수신할 아이피를 설정)
```

<br /><br />

4. TIP

```
Windows 환경 혹은 리눅스 환경에서 인바운드 설정으로 포트번호를 열어줘야 한다.
```
