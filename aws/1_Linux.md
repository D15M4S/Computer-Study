# 1. Linux 톺아보기

+ 22번 포트로 진입하기 위해 사용하는 SSH는 Linux 명령어를 통해 조작한다.
+ 차근차근 Linux 명령어를 톺아보자!

### 1. 리눅스 명령어로 파일 조작 톺아보기😁

```shell
# 현재 위치 확인
~$ pwd

# 한칸 상위 폴더로 이동 (cd ../.. 는 두칸 상위 폴더로 이동한다.)
~$ cd.. 

# 절대 경로 사용
~$ cd home/linux

# 루트 폴더로 이동
~$ cd /

# 각 파일의 자세한 정보를 보여줍니다 (-l = long)
~$ ls -l

# 숨겨진 파일을 보여줍니다 (-a = all)
~$ ls -a

# 사용자가 이해하기 편하도록 크기의 단위를 변경합니다 ex) KB, MB (-h = human-readable)
~$ ls -h

# 다음과 같이 여러개의 속성 사용이 가능합니다.
~$ ls -al

```
+ pwd (Print Working Directory) : 현재 위치한 경로를 확인하기 위해 사용되는 명령어입니다
+ cd (Change Directory) : 다른 폴더로 이동하기 위해 사용되는 명령어 입니다.
+ ls (List) : 현재 폴더에 있는 모든 파일들을 확인하는 명령어 입니다.

```shell
# 폴더 생성하기
~$ mkdir [폴더 이름]

# 파일 생성하기
# 이미 존재하는 파일에 touch 사용 시, 최근 수정시간이 현재 시간으로 변경됩니다.
~$ touch [생성할 파일 이름]

#파일 삭제하기
~$ rm [삭제할 파일 이름]
```
+ mkdir (make directory) : 폴더를 생성합니다
+ touch : 파일을 생성하거나 최근 수정 시간을 변경합니다. 
+ rm (remove) : 파일을 삭제합니다.
  + rm -r : (recursive) 폴더 안에 들어있는 파일까지 모두 삭제합니다.
  + rm -f : (force) 삭제가 안될 경우 강제로 삭제합니다. (대용량 파일 삭제시 유용)

```shell
# 복사 시 사용합니다.
~$ cp [복사할 파일명] [생성할 파일명]

# 파일의 위치를 변경합니다
# ex) 새로운 이름 사용      : mv old_name_file home/linux/new_name_file
# ex2) 원래 이름 그대로 사용 : mv old_name_file home/linux
~$ mv [이동시킬 파일명] [이동시킬 위치/(변경할 파일명)]

# 바로가기를 생성합니다
# 하드 링크, 심볼링 링크에 대한 별도 학습 필요
~$ ln -s [원본 파일명] [링크 파일명]
```
+ cp (copy) : 복사 시 사용합니다
+ mv (move) : 파일 이동 시 사용합니다.

### 2. 리눅스로 다운로드 톺아보기 🎇

+ 프로그램을 다운받기 위해서 우리는 ubuntu repository를 사용합니다.

```shell
# 사용자 확인
~$ whoami

# 다운로드 가능한 SW의 리스트를 가져옵니다.
~$ sudo apt update

# 리스트를 조회합니다.
~$ sudo apt-cache

# 다운 받고자 하는 SW가 리스트에 있는 지 조회합니다.
~$ sudo apt-cache search [찾을 SW]
~$ sudo apt-cache search [찾을 SW] | grep [찾을 SW]

# 포트 확인
~$ sudo apt install net-tools
~$ sudo apt net-tools
~$ netstat -nlpt

```
+ sudo (Superuser Do) - 일반 사용자가 슈퍼 유저의 권한으로 명령을 실행할 수 있도록 합니다.
+ apt (Advanced Package Tool) - Ubuntu에서 소프트웨어 패키지를 관리하기 위한 고급 패키지 관리 도구입니다.

### 3. 리눅스로 프로세스 톺아보기 💘

#### A. 서비스 확인하기
```shell
# Service (systemctl의 wrapper script)
# 실행 중인 서비스 확인
~$ service --status-all

# 서비스 종료
~$ service [서비스명] stop

# 서비스 시작
~$ service [서비스명] start
```

```shell
# SystemCtl (System Control)

# 시스템에서 사용 가능한 모든 유닛의 목록과 그 상태 표시
~$ sudo systemctl list-unit-files

# 실행 중인 서비스 검색
# Ctrl + C 를 통해 나올 수 있다.
~$ sudo list-unit-files | grep [서비스명]

# 상태 확인
~$ sudo systemctl status [서비스명]

# 서비스 종료
~$ sudo systemctl stop [서비스명]

# 서비스 시작
~$ sudo systemctl start [서비스명]

# 서비스 재시작
# 정확하게 systemctl로 종료하지 않으면 restart로 시작해야 한다
~$ sudo systemctl restart [서비스명]
```


#### B. 프로세스 확인하기

+ 프로세스 = 실행 중인 프로그램의 인스턴스 입니다.
+ 서비스 = 데몬(daemon)이라고 불리는 해당 프로세스는 시스템이 부팅될 때 자동으로 시작되고, 백그라운드에서 지속적으로 실행되는 장기 프로세스입니다.

```shell
# 실행 중인 프로세스를 조회합니다.
~$ ps -ef

# SIGKILL 강제로 죽이기 
~$ sudo kill -9 [PID]

# SIGTERM 프로세스를 안전하게 종료시키기
~$ sudo kill -15 [PID]

# 프로그램 중지
~$ sudo kill -2 [PID]

```
+ UID : 프로세스의 주인
+ PID : 프로세스의 아이디

+ ps (Process Status) : 실행 중인 프로세스의 정보를 표시하는 데 사용됩니다.
  + -e : (everyone) 모든 사용자에 대한 프로세스를 표시합니다
  + -f : (full) 프로세스에 대한 상세 프로세스를 표시합니다

### 4. 리눅스로 권한 톺아보기 🎠

```shell
# root 계정으로 변경된다.
~$ su root
# 패스워드를 변경한다
~$ sudo passwd [사용자]
```
+ su (Switch User) : 현재 사용자의 권한을 다른 사용자로 전환하는 데 사용됩니다.