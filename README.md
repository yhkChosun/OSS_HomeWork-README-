# OSS_HomeWork-README-


## top
**리눅스 시스템의 운용상황을 실시간으로 전반적인 상황을 모니터링 하거나 프로세스 관리를 할 수 있는 유틸리티 이다.**
 <img src="https://user-images.githubusercontent.com/105004850/170911224-9a389932-6971-43e4-8a1d-615b7880d97d.PNG" width="1100" height="300">
 '~$ top'
 
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
<img src=https://user-images.githubusercontent.com/105004850/170917879-2becd5d4-20f6-4d0a-a1ae-6b895e0be475.PNG width="1100" height="300">
'-$ ps -ef : 모든 프로세스를 풀 포맷으로 출력'

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
* 'ps -f : 풀 포맷으로 출력'
* '''ps -l : 긴 포맷으로 출력'''
* '''ps -p 1 : 프로세스 번호가 1인 프로세스 출력'''
* '''ps -u ssh : 계정이 ssh인 프로세스들을 출력'''
* '''ps -e : 모든 프로세스 출력'''
* '''ps -ef | more : 모든 프로세스를 풀 포맷으로 출력. more명령어를 줘서 페이지 단위로 출력'''
* '''ps -ef | grep ssh : 모든 프로세스의 출력값을 grep을 이용하여 ssh가 포함된 라인들을 출력'''

## jobs
