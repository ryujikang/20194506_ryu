# 명령어(top, ps, jobs, kill)

### top
> 시스템의 상태를 전반적으로 가장 빠르게 파악 가능(CPU, Memory, Process)  

* 옵션 없이($ top) 입력하면 interval 간격(기본 3초)으로 화면을 갱신하며 정보를 보여줌  
![top](https://user-images.githubusercontent.com/104420236/168477277-053b1fd5-9edf-458a-bd8c-7394d14e89cf.png)


* top *실행 전* 옵션  
  * -b : 순간의 정보를 확인(batch 모드)  
  * -n : top 실행 주기 설정(반복 횟수)  
  * ex) $ top -b -n 1  ![top -b -n 1](https://user-images.githubusercontent.com/104420236/168477552-fe33576d-d712-4fa3-a6c9-0aa0171d1d91.png)

  
* top *실행 후* 명령어
  * P : CPU 사용률 내림차순
  * M : 메모리 사용률 내림차순
  * T : 프로세스가 돌아가고 있는 시간 순
  * k : kill. k 입력 후 PID번호 작성. signal은 9
  * f : sort field 선택 화면 -> q 누르면 RES순으로 정렬
  * a : 메모리 사용량에 따라 정렬
  * b : Batch 모드로 작동
  * 1 : CPU Core별로 사용량 보여줌

  
* ps와 top의 차이점  
  * ps : ps한 시점에 proc에서 검색한 cpu 사용량
  * top : proc에서 일정 주기로 합산해 cpu 사용률 출력


### ps
> (Process Status)현재 돌아가고 있는 프로세스를 확인할 수 있는 명령어  
> * PID (프로세스 ID)  
> * TTY (터미널 번호)  
> * TIME (CPU 점유시간)  
> * CMD (프로세스가 수행된 명령어)  

![ps](https://user-images.githubusercontent.com/104420236/168513161-2077edc5-dcd7-41fb-9e84-da1daea3edde.png)



* ps 명령어의 세가지 종류
 1) Unix Option : 앞에 '-' (dash)가 붙임
 2) BSD Option : '-'를 붙이지 않음
 3) GNU Option : 명령어 앞에 '--' (double dash)를 붙임


* 옵션
  * -e : 실행중인 모든 프로세스의 정보를 출력
  * -f : 프로세스에 대한 자세한 정보를 출력(PPID확인 가능)
  * -u \[사용자이름\] : 특정 사용자에 대한 모든 프로세스의 정보를 출력
  * -p pid : pid로 지정한 프로세스의 정보를 출력
  * u : 프로세스 소유자의 이름, CPU 사용량, 메모리 사용량 등 상세 정보를 출력
  * a : 터미널에서 실행한 프로세스의 정보를 출력
  * x : 실행 중인 모든 프로세스의 정보를 출력


### jobs

### kill

---

# 매크로(Vim Editor)
