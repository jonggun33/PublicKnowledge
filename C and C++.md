# C & C++
sub title
jonggun Gim <jonggun.gim@gmail.com>
:description: This document is for amassing knowledge of C++ programming and additionally for preparing for the competitive programming.
:author: Jonggun Gim
:sectnums:
:toc: left
:doctype: manpage
:source-highlighter: highlight.js

## About this document
{description}

## Compile and Link
### clang
#### compiler options
* /c:  compile without linking
* /O: Optimization
** s: favors small code
** t: favors fast code

### make Makefile
``` bash
----
CC=g++
CFLAGS=-Wall
LDFLAGS=
OBJS=
TARGET=a.out
```

all: $(TARGET)

clean:
  rm -f *.o
  rm -f $(TARGET)
  
$(TARGET): $(OBJS)
$(CC) -o $@ $(OBJS)
----
* $@: 현재 TARGET 이름
* $^: 현재 TARGET이 의존하는 대상들의 전체 목록
* $?: 현재 TARGET이 의존하는 대상중 변경된 것의 목록

### autoconf


## Basics
####
[엄마와 어린이를 위한 C++ 기초](https://docs.google.com/document/d/1-snJLOrtmSSvS4KDs5cHE8o48dxwHhEGY5qQSrhhDAE/edit?usp=drivesdk)
####
[Learn C++](https://www.learncpp.com/)
[An Overview of C++ STL Containers - Embedded Artistry](https://embeddedartistry.com/blog/2017/08/02/an-overview-of-c-stl-containers/?format=amp)
[Google C++ Style Guide](https://google.github.io/styleguide/cppguide.html)

## TIPS
[Migrating from C to C++: Take Advantage of RAII/SBRM - Embedded Artistry](https://embeddedartistry.com/blog/2017/07/17/migrating-from-c-to-c-take-advantage-of-raii-sbrm/)
[Function parameters and arguments](https://www.learncpp.com/cpp-tutorial/71-function-parameters-and-arguments/)

## Libraries
[A list of open source C++ libraries](https://en.cppreference.com/w/cpp/links/libs)
[Beginning Game Programming v2.0](http://lazyfoo.net/tutorials/SDL/index.php)

## C++ Optimization
Array, reference, pointer. New, malloc. Class, struct, union. Callback, functor. endian

## Algorithms
LinkedList. Queue. HashMap. Merge/Quick Sorting. Radix Sorting. Binary Search. Segmentation Tree. Parity Bit.
[Modulo 10^9+7 (1000000007) - GeeksforGeeks](https://www.geeksforgeeks.org/modulo-1097-1000000007/)
[Top 10 Algorithms and Data Structures for Competitive Programming - GeeksforGeeks](https://www.geeksforgeeks.org/top-algorithms-and-data-structures-for-competitive-programming/)
[Dynamic Programming - GeeksforGeeks](https://www.geeksforgeeks.org/dynamic-programming/)
[Bridges in a graph - GeeksforGeeks](https://www.geeksforgeeks.org/bridge-in-a-graph/)
[Find a path in a complete graph with cost limit and max reward](https://stackoverflow.com/questions/27564254/find-a-path-in-a-complete-graph-with-cost-limit-and-max-reward)
[최소 공통 조상(Lowest Common Ancestor) (수정: 2019-08-31)](http://blog.naver.com/PostView.nhn?blogId=kks227&logNo=220820773477)
[해시 테이블, 열린 주소 방식](https://juggernaut.tistory.com/entry/%ED%95%B4%EC%8B%9C-%ED%85%8C%EC%9D%B4%EB%B8%94-%EC%97%B4%EB%A6%B0-%EC%A3%BC%EC%86%8C-%EB%B0%A9%EC%8B%9D)
[Hamming weight](https://en.wikipedia.org/wiki/Hamming_weight)

## SWE 기출

함수최적화. 이미지복원. 방송신호. 대피소. 중고차 딜러. 루빅스 큐브. 36진법곱. 이미지복원2. 디스크. Photo. 쓰레기통. 퍼즐. 디스크2. Seditor. 정사각형 개수
2020/02/01:: <<, |, sort

## 문제 사이트

[Korea Olympiad in Informatics Training Program](https://koitp.org/category/SDS_PRO_201712_1/)
[JMBook 문제들 링크](https://algospot.com/wiki/read/JMBook_%EB%AC%B8%EC%A0%9C%EB%93%A4_%EB%A7%81%ED%81%AC)
[Sphere Online Judge (SPOJ) - Problems](https://www.spoj.com/problems/classical/)
[Past Contests | Google Code Jam](https://code.google.com/codejam/past-contests#other)
[Baekjoon Online Judge](https://www.acmicpc.net/)
[JUNGOL](http://www.jungol.co.kr/)
[2020 신입 개발자 블라인드 채용 1차 코딩 테스트 문제 해설](https://tech.kakao.com/2019/10/02/kakao-blind-recruitment-2020-round1/)
[Samsung SW Expert](https://swexpertacademy.com/main/main.do)
