# Born2beroot


## 1. visudo
---
-	authfail_message : sudo 권한 실패 시 메세지 커스텀
-	badpass_message : 잘못된 패스워드 입력시 메세지 커스텀
-	log_input : 입력된 명령어를 log로 남긴다.
-	log_output : 출력된 결과를 log로 남긴다.
-	requiretty : tty 옵션을 강제한다.
-	iolog_dir : log를 해당 위치에 저장한다.
-	passwd_tries : 패스워드 입력 가능 횟수

## 2. ufw
---
 -	`uncomplicated fireWall`
		: `UFW`는 사용하기 쉽게 설계된 넷필터 방화벽을 관리하는 프로그램이다. 간단한 명령 및 명령수가 적은 명령줄 인터페이스를 사용하는것이 특징이며 프로그램 구성에는 `iptables` 를 사용한다
 -	`iptables` 
		: iptables는 커널상에서의 netfilter 패킷필터링 기능을 사용자 공간에서 제어하는 수준으로 사용할 수 있다
 -	설치  
 	- 설치 : `apt install ufw` 
	- 상태확인 : `ufw status verbose`
	- 활성화 : `ufw inactive`
	- 포트 룰 추가 : `ufw allow 4242`

## 3. Systemctl && SSH
---
 /usr/lib/systemd/system 디렉토리의 .service파일을 systemctl 명령어로 서비스를 제어할 수 있다.

-	`vim /etc/ssh/sshd_config` 에서 열어둘 포트 번호를 입력 후 주석 해제
-	`PermitRootLogin` 옵션은 해제해서 ssh를 통해 루트 접근 불가 설정
-	`ssh ${userName}@${localIp} -p ${Port}` 
-	`ps -ef | grep ssh` 입력 후 ssh 접속 ps 종료 `kill -9 ${PID}`


## 4. 유저 정보
	root 계정에서 실행.
- `grep ${userName} /etc/group`그룹 확인
- `groupadd ${groupName}` 그룹 생성
- `gpasswd`
	: /etc/group 과 /etc/gshadow 파일을 관리한다.
	- -a 사용자 계정을 그룹에 추가한다.
	- -d 사용자 계정을 그룹에서 삭제한다.
	- -r 그룹 암호를 삭제한다.

	- `gpasswd -a ${userName} {groupName}` 그룹에 유저 추가
	- `gpasswd -a ${userName} sudo` sudo그룹에 유저 추가++ 

- `passwd`
	- -a : 정보를 보여준다.
	- -S : 정보를 보여준다.
	- -x : 만료일을 설정한다.
	- -w : 만료 전에 경고메세지를 남긴다.
	- -n : 변경 후 사용하는 최소 날짜를 지정한다.

	/vim/etc/pam.d/common-password 
	lcredit ucredit dcredit ocredit > 0 각 문자를 사용할 때마다 부여되는 추가 점수
									< 0 최소로 사용해야하는 숫자.