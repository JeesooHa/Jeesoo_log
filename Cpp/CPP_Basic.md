**목차**
- [C++ 기초](#c-기초)
  - [C++ 역사](#c-역사)
  - [C++ 시작하기](#c-시작하기)
    - [이름공간 (namespace)](#이름공간-namespace)
      - [namespace 요소 접근방법 3가지](#namespace-요소-접근방법-3가지)
    - [std namespace](#std-namespace)
    - [C++ 표준 헤더 파일](#c-표준-헤더-파일)
    - [참고자료](#참고자료)


----


# C++ 기초

- C++은 게인엔진, 컴파일러, 동영상 및 오디오 처리, 운영체제, 상용 프로그램, 딥러닝 프레임워크, 서버 프로그램 등 성능이 중요한 다양한 프로그램에서 사용되고 있으나 쓰기 어렵다는 단점이 있다. (수많은 컴파일 오류, 복잡한 템플릿 문법 등). C++을 제대로 공부해야 한다 [2]


## C++ 역사
- C++은 역사가 매우 긴 언어. 
- 1979년 컴퓨터 과학자인 비아르네 스트로우스트루프 (Bjarne Stroustrup)이 C언어에 클래스라는 개념을 적립한 *C with Classes* 라는 언어를 만듬. C++의 전신
- 1982년 해당 언어를 발전시켜 C++ 이라 명명함
- **C++98** 1998년 C++의 첫 번째 표준이 공개됨. STL 라이블러리 발표 
- **C++03** 2003년 표준화 버그 수정,개선 
- **Modern C++** : 3년마다 한번씩 새로운 표준(새로운 문법, 라이브러리등 추가)을 만들어서 발표
  - **C++11** 2011년 boost 라이브러리, 중요한 신 개념과 편의기능들이 많이 추가됨 
  - **C++14** 2014년 비교적 작은 변화 
  - **C++17** 2017년 표준라이브러리의 새로운 기능, 파일시스템, STL 병렬 알고리즘 처리 등 추가 
  - **C++20** 2020년 대규모의 업그레이드 예정 
  
![cpp_history](https://isocpp.org/files/img/wg21-timeline-2019-07.png)


## C++ 시작하기

### 이름공간 (namespace)
- 어떤 정의된 객채에 어디 소속인지 지정해주는 것
- 프로그램의 기능별로 연관된 코드를 묶어서 관리함.
- 변수 or 함수 등의 이름 충돌을 방지할 수 있음
#### namespace 요소 접근방법 3가지
   ```cpp
    #include <stdio.h>
    namespace Audio {
      void init() { printf("Audio init\n"); }
      void reset() { printf("Audio reset\n"); }
    }
    void init() {
      printf("Program init\n");
    }
  ```

1. **qualified name (완전한 이름)** 을 사용한 접근 -> 가장 안전한 방법
    ```cpp
    int main()
    {
        Audio::init();   // 완전한 이름을 사용한 접근
    }
    ```

2. **using declaration (선언)** 을 사용한 접근
   - 사용 시 전역 공간에 동일 이름의 함수가 있으면 충돌 발생
   ```cpp
    int main()
    {
      using Audio::init;          // using 선언을 사용한 접근
      init();     // ok
      reset();    // error
    }
   ```
  
3. **using directive (지시어)** 을 사용한 접근 -> 이름 충돌이 나올 수 있음
     - 사용 시 전역 공간에 동일 이름의 함수가 있으면 충돌 발생
     - global namespace에 접근하려면 :: 연산자를 함수 앞에 사용
   ```cpp
    int main()
    {
      using namespace Audio;      // using 지시어를 사용한 접근
      init();     // ok
      reset();    // ok

      ::init();       // global namespace에 접근
    }
   ```
  

### std namespace
- std : C++ 표준 라이브러리의 모든 함수, 객체 등이 정의된 이름공간(namespace)
- C++의 모든 표준 라이브러리는 **std** 이름 공간 안에 있다.


### C++ 표준 헤더 파일
- 표준 라이브러리 헤더는 .h를 안붙이는게 관례다.

|언어|내용|예시|
|----|----|----|
|C언어      |파일 이름 뒤에 .h를 붙인다         | <stdio.h> |
|C++언어    |파일 이름 뒤에 .h가 붙어 있지 않다  | <iostream\>, <algorithm\> |
|사용자헤더|사용자 헤더를 만들 때는 .h를 붙이는 것이 관례이다|"user_header.h"|

- C++은 모든 표준라이브러리가 std 이름 공간에 있다.
- C표준함수도 결국 C++ 표준의 일부 임으로 std 이름공간 안에 넣어졌다
  - <stdio.h\> 대신 **<cstdio\>** 사용
  - <stdio.h\> : printf 함수가 전역공간에만 있다
  - <cstdio\> : printf 함수, std::printf 함수 모드 사용 가능하다.
- C++에서 C언어 헤더 사용하는 방법
  - 기존의 C언어 헤더 파일을 모두 계속 사용 가능
  - C언어 헤더에서 '.h'를 제거하고 앞에 'c'를 붙여서 사용한다
    - <string.h\> &rarr; **<cstring\>**
    - <stdlib.h\> &rarr; **<cstdlib\>**
    - <math.h\> &rarr; **<cmath\>**





------
### 참고자료
[1] [C++ Basic](https://www.ecourse.co.kr/course/cppbasic/)
- 유료 강좌
- C++ 언어의 기본 문법과 객체지향 프로그래밍 개념 기초 학습. C++98/03과 Modern C++(11/14/17) 의 내용에 대해 배우게 됨
- C에 대한 기본적인 사전지식 필요

[2] [씹어먹는 C++강좌](https://modoocode.com/135)
- 무료 Wiki 자료


[3] [CPP 공식 사이트](https://isocpp.org/)

[4] [CPP 레퍼런스 위키](https://en.cppreference.com/w/)