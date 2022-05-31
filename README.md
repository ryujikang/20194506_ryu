# 명령어(top, ps, jobs, kill)
---
## `top`
> ***시스템의 상태를 전반적으로 가장 빠르게 파악*** 가능(CPU, Memory, Process)  

* 옵션 없이($ `top`) 입력하면 interval 간격(기본 3초)으로 화면을 갱신하며 정보를 보여줌  
<img src="https://user-images.githubusercontent.com/104420236/168477277-053b1fd5-9edf-458a-bd8c-7394d14e89cf.png" width="640" height="480">

* `top` ***실행 전*** 옵션  
  * `-b` : 순간의 정보를 확인(batch 모드)  
  * `-n` : top 실행 주기 설정(반복 횟수)  
  * ex) $ `top -b -n 1`  
   <img src="https://user-images.githubusercontent.com/104420236/168477552-fe33576d-d712-4fa3-a6c9-0aa0171d1d91.png" width="640" height="480">

  
* `top` ***실행 후*** 명령어
  * `P` : CPU 사용률 내림차순
  * `M` : 메모리 사용률 내림차순
  * `T` : 프로세스가 돌아가고 있는 시간 순
  * `k` : kill. k 입력 후 PID번호 작성. signal은 9
  * `f` : sort field 선택 화면 -> q 누르면 RES순으로 정렬
  * `a` : 메모리 사용량에 따라 정렬
  * `b` : Batch 모드로 작동
  * `1` : CPU Core별로 사용량 보여줌
  * `h` : 도움말
  
* ***`ps`와 `top`의 차이점***  
  * `ps` : ps한 시점에 proc에서 검색한 cpu 사용량 출력
  * `top` : proc에서 일정 주기로 합산해 cpu 사용률 출력
---

## `ps`
> (Process Status)***현재 돌아가고 있는 프로세스를 확인***할 수 있는 명령어  
> * PID (프로세스 ID)  
> * TTY (터미널 번호)  
> * TIME (CPU 점유시간)  
> * CMD (프로세스가 수행된 명령어)  

<img src="https://user-images.githubusercontent.com/104420236/168513161-2077edc5-dcd7-41fb-9e84-da1daea3edde.png" width="640" height="480">



* ps 명령어의 세가지 종류
 1) Unix Option : 앞에 '-' (dash)가 붙임
 2) BSD Option : '-'를 붙이지 않음
 3) GNU Option : 명령어 앞에 '--' (double dash)를 붙임


* 옵션
  * `-e`, `-A` : 실행중인 모든 프로세스의 정보를 출력
  * `-f` : 프로세스에 대한 자세한 정보를 출력(PPID확인 가능)
  * `-ef` : 모든 프로세스를 full format으로 보여줌(-e와 -f의 조합)
  * `-u` \[사용자이름\] : 특정 사용자에 대한 모든 프로세스의 정보를 출력
  * `-p pid` : pid로 지정한 프로세스의 정보를 출력
  * `u` : 프로세스 소유자의 이름, CPU 사용량, 메모리 사용량 등 상세 정보를 출력
  * `a` : 터미널에서 실행한 프로세스의 정보를 출력
  * `x` : 실행 중인 모든 프로세스의 정보를 출력

* format 정리표  

|CODE|NORAML|HEADER|
|:---:|:------|:-----|
|%C|pcpu|%CPU|
|%G|group|GROUP|
|%P|ppid|PPID|
|%U|user|USER|
|%a|args|COMMAND|
|%c|comm|COMMAND|
|%g|rgroup|RGROUP|
|%n|nice|NI|
|%p|pid|PID|
|%r|pgid|PGID|
|%t|etime|ELAPSED|
|%u|ruser|RUSER|
|%x|time|TIME|
|%y|tty|TTY|
|%z|vsz|VSZ|

* `ps | grep <option>`
  * 원하는 프로세스만 추출  
<img src="https://user-images.githubusercontent.com/104420236/170738534-e4741c22-f695-4427-b3ce-cdbf3405037c.png" width="640" height="480">


* `ps -ejH`  
  * 프로세스를 트리 형태로 조금 보기 좋게 표시. 자식 트리면 CMD가 한칸 띄어져서 출력  
<img src="https://user-images.githubusercontent.com/104420236/170737396-f30394fd-aaf9-4ab1-8574-6df6ff14d7cf.png" width="640" height="480">

* `pstree`  
  * `ps -ejH`보다 `pstree` 명령이 더 보기 좋음. 이 트리는 기본적으로 init 혹은 systemd 프로세스가 루트인데, 만약 pid를 명시한다면 그 pid가 루트가 됨  
<img src="https://user-images.githubusercontent.com/104420236/170737495-b48778cb-0f28-4fbe-9490-b301c055437f.png" width="640" height="480">


---
## `jobs`
> ***백그라운드로 실행되는 작업목록(작업번호, 상태, 명령어)을 보여***주는 명령어  
> $ `jobs [Option] [job ID]`


* 옵션  

|Option|Explanation|
|:---:|:---|
|`-l`|프로세스 그룹 ID를 state 필드 앞에 출력|
|`-n`|프로세스 그룹 중에 대표 프로세스 ID를 출력|
|`-p`|각 프로세스 ID에 대해 한 행씩 출력|
|command|지정한 명령어를 실행|  


* `jobs`로 알 수 있는 세션의 상태 값  

|Status|Explanation|
|:---:|:---|
|Running|작업이 일시 중단되지 않았고 종료하지 않고 계속 진행 중임|
|Done|작업이 완료되어 0을 반환하고 종료 했음을 의미|
|Done(code)|작업이 정삭적으로 완료되었으며, 0이 아닌 코드를 반환 했음을 의미|
|Stopped|작업이 일시 중단|
|Stopped(SIGTSTP)|SIGTSTP 신호가 작업을 일시 중단|
|Stopped(SIGSTOP)|SIGSTOP 신호가 작업을 일시 중단|
|Stopped(SIGTTIN)|SIGTTIN 신호가 작업을 일시 중단|
|Stopped(SIGTTOU)|SIGTTOU 신호가 작업을 일시 중단|


---
## `kill`
> 프로세스에 특정한 시그널(signal)을 보내는 명령어  
> 일반적으로 ***종료되지 않는 프로세스를 종료 시킬 때*** 많이 사용  

 
* `kill -l` : signal의 종류를 출력  
  * > `kill [Otion or signal(number or name)] PID`  
  ex) $ `kill -9 1234`  >> 보통 -1(-HUP, 프로세스 재활성화)와 -9(-kill, 프로세스 강제 종료)를 많이 씀  
  ex) $ `kill -SIGKILL 1234`  

<img src="https://user-images.githubusercontent.com/104420236/168520288-a3bc9c4d-7267-4107-99a6-a01ee77046e9.png" width="640" height="480">


---

# 매크로(Vim Editor - macro)
> 특정한 움직임 또는 ***입력을 키에 저장***함으로써 단순하면서 ***반복되는 동작을 쉽고 빠르게*** 해주는 것  
> vim 명령어모드 -> `q + key(알파벳)` : 특정 알파벳(key)에 매크로를 저장  


* 매크로(macro) 사용순서
 1) `q + a` : ***a키***에 ***recording 시작***
 2) 자신이 원하는 반복 동작
 3) `q` : ***recording 종료***
 4) 1) `@a` : ***1회*** 실행
    2) `@@` : ***방금 실행한 매크로*** 실행
    3) `10@a` : 매크로 ***10회*** 실행


* 매크로 응용(숫자 증가)
 1) 숫자 1 입력
 2) 매크로 시작
 3) 숫자 1을 복사해서 다음 줄에 붙여넣기
 4) 두번째줄 1에 커서를 올리고 Ctrl+a(숫자 증가) - (Ctrl+x = 숫자 감소)
 5) 매크로 종료

---
# 출처 사이트
* [top]<https://ironmask84.tistory.com/355> | <https://zzsza.github.io/development/2018/07/18/linux-top/>   
* [ps]<https://reakwon.tistory.com/183> | <https://jhnyang.tistory.com/268> | <https://blog.naver.com/PostView.nhn?isHttpsRedirect=true&blogId=jsky10503&logNo=220728880785&parentCategoryNo=&categoryNo=109&viewDate=&isShowPopularPosts=false&from=postView>   
* [jobs]<https://shaeod.tistory.com/968> | <https://zetawiki.com/wiki/%EB%A6%AC%EB%88%85%EC%8A%A4_jobs>   
* [kill]<https://m.blog.naver.com/koromoon/220804715310> | <https://bigsun84.tistory.com/355>   
* [매크로]<http://aboutmadlife.blogspot.com/2014/09/linux-vi-macro.html> | <https://booolean.tistory.com/849> | <https://tzara.tistory.com/150>   

