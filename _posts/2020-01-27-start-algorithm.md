---
title: 알고리즘 공부 시작하기
date: 2020-01-27
categories: algorithm
---

알고리즘 공부를 시작하면서 겪는 좌우충돌...



# 시작하기

아주 기초적인 알고리즘에 대해서는 예전에 이미 학습한 적이 있지만, 올해 목표로 알고리즘을 조금 더 체계적으로 학습하려는 계획을 세웠습니다.

단순히 "생각을 열심히 해서 논리적 사고력을 키우자" 같은 취미 영역이 아닌, 정해진 시간에 정해진 문제를 풀기 위한 구조적인 학습 반복 패턴을 연습하여, 경진대회 또는 자격증에 필요한 알고리즘 능력(?)을 키우려고 합니다.



# 프로그래밍 언어 바꾸기

이번에 알고리즘을 공부하면서, 주 프로그래밍 언어를 변경하려고 합니다. 이전에는 Java로 프로그래밍을 하였으나, 이번에는 C 또는 C++ 로 프로그래밍 언어를 변경하려고 합니다.

이에 대한 고려사항을 한번 이야기 해보려고 합니다.

> 이번에 연습을 할 때는 C 언어를 사용하였습니다.
>
> 그런 이유로,  아래 예시는 C 프로그래밍을 기준으로 설명합니다.



##  입출력 처리

보통 알고리즘은 최소한의 라이브러리를 사용해서 기본 문법으로 작성하기 때문에, 많은 라이브러리를 학습할 필요는 없습니다.

그러나, 기본 입출력을 통해서 문제를 입력하고, 이에 대한 해답을 출력해야 하기 때문에, 이에 대한 기본지식이 필요합니다.

`C` 의 경우에는 기본적으로 입력으로  `scanf(...)` 를 사용하고, 출력으로 `printf(...)` 를 사용합니다.

 다음은 간단히 입출력 예제입니다.

```c
#include <stdio.h>
#define INPUT_LEN 100
int main(int argc, const char * argv[]) {
  int input[INPUT_LEN+1];
  for(int i=1; i<=INPUT_LEN; i++) {
        scanf("%d", &input[i]);
  };
  
  for(int i=1; i<=INPUT_LEN; i++) {
        printf("%d ", &input[i]);
  };
  printf("\n");
}
```



그 외에, `gets(...)` 와 `fgets(...)` 를 이용해서 문자열을 처리할 수도 있습니다.

특히 `fgets(...)` 은 표준 입출력(`stdin`) 만이 아니라 파일  입출력을 위해 `fopen(...)` 과 `fclose(...)` 와 같이 사용할 수 있습니다.

> 이 부분에 대한 코딩 패턴은 조금 더 연습을 한 후, 다시 다루도록 하겠습니다.



## 전역 변수 다루기

기존에 Java 로 연습을 할 때는 객체단위로 설계를 하였으나, C 의 경우, 함수형 프로그래밍(functional programming) 에 적합하기 때문에, 필요한 값을 적절하게 전역변수로 설정할 필요가 있습니다.

특히, 알고리즘 코딩의 경우, 스택 메모리 제한이 있기 때문에, 로컬 변수에 너무 큰 값을 설정하면 메모리 오버플로가 발생할 수 있습니다.

또한 동적 메모리 할당이 아닐 경우에는 변수를 사이즈로 설정할 수 없기 때문에, 적절한 사이즈를 사전에 설정할 수 있어야 합니다.

제 경우에는 예전에 객체 내 메타데이터를 각각의 데이터 베열로 정의해 주는 방향으로 연습하고 있습니다.

예를 들면 다음과 같습니다.

```java
//Java
import java.util.Scanner;

public class Entity {
  int src;
  int dst;
}
Entity[] gEntities; 

public class Main {
  public static void main(string[] args) {
    Scanner scanner = new Scanner(System.in)
    int size = scanner.nextInt();
		gEntities = new Entity[sizse];
    //...
  }
}
```

```C
//C
int src[100];
int dst[100];

int main(int argc, const char * argv[]) {
	//...
  return 0;
}
```



## 문자열 처리

(나중에 업데이트)



## 정렬 처리

알고리즘의 경우, 제한된 라이브러리를 사용하기 때문에, 원하는 라이브러리를 시스템에서 지원하지 않을 수가 있습니다.

일반적으로 라이브러리로 처리하는 흔한 알고리즘으로 정렬과 큐가 있는데, 자주 사용하는 정렬로는 `Quick sort` 가 있으며, 큐로는 `Priority queue` 가 있습니다.

Java 의 경우, 기본적으로 다음과 같이 사용할 수 있습니다.

```java
import java.util.PriorityQueue;
import java.util.Arrays

public class Main {
    public static void main(String[] args) {
      //Quick sort
      int[] arr = new int[] {5, 3, 122, 1, 8};
      Arrays.sort(arr);
      
      //Priority queue
    	PriorityQueue<Integer> queue = new PriorityQueue<Integer>();
      //...
    }
}
```



C 의 경우에는 `Quick sort` 의 경우에는  `stdlib.h` 에 정의되어 있는 `qsort(...)` 를 사용할 수 있습니다.

```C
#include <stdio.h>
#include <stdlib.h>

// 오름차순
int compare (void *first, void *second)
{
    if (*(int*)first > *(int*)second)
        return 1;
    else if (*(int*)first < *(int*)second)
        return -1;
    else 
        return 0;
}

int main(int argc, char** argv)
{
    int arr[] = {4,3,1,7,5,9,8,2,6};
    int arr_size = sizeof(arr) / sizeof(int);
    int i;

    // apply quick sort
    qsort(arr, arr_size, sizeof(int), compare);
    //...
}
```

그러나 `Priority queue` 의 경우에는 적절한 기본 라이브러리가 없습니다. 

> C++ 의 경우, std::priority_queue 구현체를 제공합니다.
>
> - `#include <quueue>` 헤더가 필요합니다. 



그렇기 때문에, 이런 기본적으로 자주 사용하는 기본 알고리즘의 경우 라이브러리에 의존하지 않고 코드를 짤 수 있는 정도로 학습하는 것이 좋을 것 같습니다.



# 프로그래밍 고려사항

## 변수명 패턴화하기

Java 에서 C 로 프로그래밍 언어를 바꾸면서, 카멜 표기법(Camel case), 스네이크 표기법(Snake case) 또는 헝가리안 표기법(Hungarian notation) 와 같은 변수명을 정하는 방법에 대해 패턴화할 필요가 있습니다.

- backgroundColor : Camel case
- background_color : Snake case
- strName : Hungarian notaion - prefix 로 데이타 타입을 명시하는 방법



저의 경우에는 여전히 카멜 표기법을 사용하나, 작성속도를 위해 단축어를 사용하려고 시도하고 있습니다.

> 왠지 C 프로그래밍은 그래줘야 할 것같은 느낌이 듭니다.

이런 경우 소스의 가독성이 높지 않아 일관적인 변수명을 패턴화해서 사용하는 것이 추후에 리뷰를 할 때 유리해 보입니다.

그렇기 때문에, 자주 사용하는 용어에 대한 변수명 또한 어느정도 정하고 사용하는 것이 좋을 거 같습니다.



이번에 연습을 하면서 느낀 여러가지 변수명에 대한 충돌 또는 명명에 대한 고민거리를 아래 적어보았습니다.

- `for(...)` 구문에 사용하는 `i`  와 배열의 index 로 사용하는 `i` 그리고 입력값으로 사용하는 `i`

- 반복 횟수의 `c` 와 입력 횟수의 `c` 
- 부분합의 `sum` 와 최종 합의 `sum`



이런 것들은 그때 그때 다르게 변수명을 정의하면 되지만, 빠른 리뷰를 위해선 자주 겹치는 변수명은 사전에 규칙을 가지고 명명하는 것이 좋을 거 같습니다.



## 범위 정하기

(나중에 업데이트)

- inbound 와 outbound

## 재귀함수 파라미터 설정하기

(나중에 업데이트)

- 초기값 설정
- 최종값 설정

## 기능 테스트 고민하기

(나중에 업데이트)

- 재귀함수에서 특정 지점에 대한 디버깅

## 초기화 비용에 대해 관대해지기

(나중에 업데이트)

- 배열 초기화



## 용어 정리하기

(나중에 업데이트)

- 알고리즘 용어 정리하기
  - Optimal Substrxucture
  - Heapify - Heap sort
  - Edge Relaxation - Dijkstra algorithm



