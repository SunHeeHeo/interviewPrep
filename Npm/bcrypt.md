# 📱 Bcrypt 


처음부터 <U>단방향 암호화</U>를 위해 만들어진 해시 함수.
salting 과 키 스트레칭을 구현한 해시 함수 중 대표적인 함수   

* 단방향 해시 함수  
단방향 해시 함수는 수학적인 연산을 통해, 원본 메세지를 변환하여 암호화된 메세지인 digest를 생성. 이 방식으로 암호화된 digest는 다시 평문으로 볼수 없다.    


## 문제점 
1. 동일한 메세지가 동일한 digest를 생성하는 경우. 즉, 똑같은 비밀번호가 똑같은 해시값을 생성하는 경우.    
    - 이와 같은 digest 목록을 담고 있는 테이블을 rainbow table 이라고 하고 이 공격 방식을 rainbow attack이라고 한다.

    * rainbow table attack : 미리 해시 값들을 계산해 놓은 테이블을 가지고 해시 함수 반환 값을 역추적해 원래 정보를 찾아내는 해킹 방법    

2) 해시 함수의 빠른 처리 속도   
해시 함수는 짧은 시간에 데이터를 검색하기 위해 설계 된 것. 따라서, 공격자가 마음만 먹으면, 임의의 digest를 대량으로 생성해서, 사용자의 암호가 해시도니 digest와 빠른 속도로 비교하여 원래 비밀번호를 알아 낼수 있다.


### 이런 취약점을 보완한 것이 바로 <U>bcrypt</U>의 솔팅(salting) 이라는 기법과 키 스트레칭(key stretching) 기법

<p align="center"><img width="692" alt="스크린샷 2021-12-16 오전 1 47 59" src="https://user-images.githubusercontent.com/88166362/146228739-7b50f978-6c8b-4b9b-b934-fbd5cf5b26b8.png">


* salting: 실제 정보 이외에 <U>추가적으로 무작위 데이터를 더해서</U> 해시 값을 계산 하는 방법. salt로 인해, 해시값이 달라지기 때문에, rainbow attack 와 같이 미리 해시 값을 계산해 공격하는 것을 무효화 시킨다.

* key stretching: 단방향 해시 값을 계산한 후 그 해시 값을 다시 해시하고, 이를 반복한다. 향후 컴퓨터 성능이 향상되어도, 해시 반복 횟수를 추가하여 계속 보완할 수 있다.   
기존 단방향 해시 알고리즘의 빠른 실행 속도가 취약 점이 됐던 것을 보완하는 방법   


## bcrypt의 값은 4 부분으로 나눠진다.  
* Algorithm : 알고리즘 식별자   
* Coast factor :  키 스트레칭 한 횟수 2^n으로 나타냄  
* Salt : 128 비트 솔트, 22자 base 64로 인코딩    
* Hash : salting과 키 스트레치이 후 해시 값   
* Bcrypt 에서 검증 : 비밀번호가 동일한지 검증하기 위해, 입력된 비밀번호에 salting, 키 스트레칭을 해서 저장된 bcrypt 문자열과 비교한다.  


[참고](https://velog.io/@sangmin7648/Bcrypt%EB%9E%80)  
[참고](https://velog.io/@sungjun-jin/bcrypt)


