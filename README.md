# OSS_HomeWork-README- <과제2 - 조사내용 REAME파일로 정리하기>

> 목차
1) top 명령어
2) ps 명령어
3) jobs 명령어
4) kill 명령어
5) vim 매크로


  
  
  

## top
**리눅스 시스템의 운용상황을 실시간으로 전반적인 상황을 모니터링 하거나 프로세스 관리를 할 수 있는 유틸리티 이다.**
 <img src="https://user-images.githubusercontent.com/105004850/170911224-9a389932-6971-43e4-8a1d-615b7880d97d.PNG" width="1100" height="300">
 `$ top`
 
 **세부 정보 필드별 항목**
 * PID : 프로세스 ID (PID)
 * USER : 프로세스를 실행시킨 사용자 ID
 * PRI : 프로세스의 우선순위 (Priority)
 * NI : NICE 값. 일의 nice value 값. 마이너스를 가지는 nice value는 우선순위가 높다.
 * VIRT : 가상 메모리의 사용량(SWAP+RES)
 * RES : 현재 페이지가 상주하고 있는 크기(Resident Size)
 * SHR : 분할된 페이지, 프로세스에 의해 사용된 메모리를 나눈 메모리의 총합.
 * S : 프로세스의 상태 - S(sleeping), R(running), W(swapped out process), Z(zombies)
 * %CPU : 프로세스가 사용하는 CPU의 사용률
 * %MEM : 프로세스가 사용하는 메모리의 사용률
 * TIME+ : 프로세스가 시작된 이후 경과된 총 시간
 * COMMAND : 실행된 명령어
 * Load average : 세개의 숫자는 각각 1분, 5분, 15분 간의 평균 실행/대기 중인 프로세스의 수를 나타낸다. uptime 명령어로도 확인할 수 있으며, 시스템 부하를 모니터링 할 수 있다. 숫자가 높을수록 시스템에 부하가 있다는 것이다. Load average 값은 CPU의 코어 수를 같이 확인해야 하며, 코어 수 보다 적으면 문제가 없다.

**top 실행 전 옵션**
* -b : 배치모드 옵션
* -n : top 실행 주기를 설정
* -p : process ID

**top 실행 후 사용할 수 있는 옵션**
|옵션|기능|
|-----|---|
|shift + t|실행된 시간이 큰 순서로 정렬|
|shift + m|메모리 사용량이 큰 순서로 정렬|
|shift + p|cpu 사용량이 큰 순서로 정렬|
|k|Process 종료|
|k + 종료할 PID|해당 Process 종료|
|c|명령 인자 표시 / 비표시|
|l|uptime line(첫번째 행)을 표시 / 비표시|
|space bar|Refresh|
|u|입력한 유저 소유의 Process만 표시|
|shift + b|상단의 uptime 및 기타 정보값을 블럭선택해 표시|
|f|화면에 표시될 프로세스 관련 항목 설정|
|i|idle 또는 좀비 상태의 프로세스는 표시 되지 않음|
|z|출력 색상 변경|
|d &#91;sec&#93;|설정된 초단위로 Refresh|
|q|명령어 종료|

**top과 ps의 차이점**
* top은 proc에서 일정 주기로 합산해서 cpu 사용률을 출력한다.
* ps는 ps한 시점에 proc에서 검색한 cpu 사용량이다.





  
  
  
## ps
**현재 실행중인 프로세스 목록을 보여준다. 주로 파이프라인, grep명령어와 함께 사용하여 특정 프로세스를 확인하는데 사용된다.**
<img src="https://user-images.githubusercontent.com/105004850/170917879-2becd5d4-20f6-4d0a-a1ae-6b895e0be475.PNG" width="1100" height="300">
`$ ps -ef : 모든 프로세스를 풀 포맷으로 출력`

**세부정보 필드별 항목**
* UID : 실행 유저
* PID : 프로세스 ID
* PPID : 부모 프로세스 PID
* C : CPU 사용량
* STIME : Start Time
* TTY : 프로세스 제어 위치 ( -콘솔 : tty1, -원격 : pts/1 )
* TIME : 구동시간
* CMD : 실행 명령어

**주요 옵션**
|옵션|기능|
|---|---|
|-e|모든 프로세스를 출력해 준다.|
|-f|풀 포맷으로 보여준다.(UID,PID등)|
|-l|긴 포맷으로 보여준다.|
|p, -p|특정 PID의 프로세스를 보여준다.|
|-u|특정 사용자의 프로세스를 보여준다.|

**대표적인 사용예시**
* `ps -f : 풀 포맷으로 출력`
* `ps -l : 긴 포맷으로 출력`
* `ps -p 1 : 프로세스 번호가 1인 프로세스 출력`
* `ps -u ssh : 계정이 ssh인 프로세스들을 출력`
* `ps -e : 모든 프로세스 출력`
* `ps -ef | more : 모든 프로세스를 풀 포맷으로 출력. more명령어를 줘서 페이지 단위로 출력`
* `ps -ef | grep ssh : 모든 프로세스의 출력값을 grep을 이용하여 ssh가 포함된 라인들을 출력`



  
  
  


## jobs
**작업의 상태를 표시하는 명령어 이다. 현재 쉘 세션에서 실행시킨 백그라운드 작업의 목록이 출력되며, 각 작업에는 번호가 붙어 있어 kill 명령어 뒤에 '%번호' 등으로 사용할 수 있다. 쉽게 말하면, 현재 쉘 프로세스의 자식 백그라운드 프로세스들을 보여준다고 생각하면 된다.**

**jobs로 출력되는 백그라운드 작업의 상태값**
* Running : 작업이 계속 진행중임
* Done : 작업이 완료되어 0을 반환
* Done(code) : 작업이 종료되었으며 0이 아닌 코드를 반환
* Stopped : 작업이 일시 중단
* Stopped(SIGSTP) : SIGSTP 시그널이 작업을 일시 중단
* Stopped(SIGSTOP) : SIGSTOP 시그널이 작업을 일시 중단
* Stopped(SIGTTIN) : SIGTTIN 시그널이 작업을 일시 중단
* Stopped(SIGTTOU) : SIGTTOU 시그널이 작업을 일시 중단

|옵션|기능|
|---|---|
|-l|프로세스 그룹 ID를 state 필드 앞에 출력|
|-n|프로세스 그룹 중에 대표 프로세스 ID를 출력|
|-p|각 프로세스 ID에 대해 한 행씩 출력|
|command|지정한 명령어를 실행|





  
  
  

## kill
**프로세스에 특정한 signal을 보내는 명령어 이다. 일반적으로 종료되지 않는 프로세스를 종료 시킬 때 많이 사용한다.**

**kill 시그널 리스트는 아래의 명령어를 입력하면 확인할 수 있다. 모든 시그널 리스트는 아래 사진에 해당된다.**
`$ kill -l`
<img src="https://user-images.githubusercontent.com/105004850/170922569-964e9fe0-46b3-4cc2-b04d-f97f4355bbaf.PNG" width="1100" height="300">

**주요 시그널**
|시그널|영어|기능|
|----|---|---|
|1) SIGHPUP|Hang Up|세션이 종료될 때 시스템이 내리는 시그널|
|2) SIGINT|Interrupt|Ctrl + C, 종료 요청 시그널|
|9) SIGKILL|Kill|강제 종료 시그널|
|11) SiGSEGV|Segment Violation|메모리 침범이 일어날 때 시스템이 보내는 시그널|
|15) SIGTERM|Terminate|기본 값, 강제 종료 시그널|
|20) SIGTSTP|Temporary Stop|Ctrl + Z, 일시 중지 요청 시그널|

**프로세스에 시그널 보내기 예시**
```
$ kill [option] PID

# 1111(PID) 프로세스 종료
$ kill -9 1111
$ kill -SIGKILL 1111
```
  
  
  

## Vim 에디터에서 매크로 활용법
**네임 레지스터에 자주 사용하는 액션을 등록하여 사용한다.**

|기능|일반모드|예제|
|---|-------|---|
|녹화|q+(매크로KEY)|qa|
|녹화종료|q|q|
|재생|@+(매크로KEY)|@a|
|마지막 매크로 실행|@@|@@|
|횟수 실행|(횟수)@(매크로KEY)|10@a|

1) 일반모드에서 q+KEY 입력을 누르면, vim의 상태바에 'Recording'이라는 표시가 나온다.
2) 이후, 반복적으로 수행할 키로그를 녹화하고 동작이 다 끝나면 q를 입력하여 종료한다.
3) @+KEY를 입력하여 매크로 동작을 실행한다.
4) 매크로를 여러번 실행할 때는 @@ 를 입력하여 빠르게 반복 실행한다.
5) 저장한 매크로 작업을 n번 반복하고 싶은 경우, n@KEY 를 입력한다. ex) 10번 반복 --> 10@KEY
