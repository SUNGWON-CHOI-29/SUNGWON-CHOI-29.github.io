---
layout: post
title: Medium - Meaningful Names In Code
description: >
  <a href="https://medium.com/better-programming/how-to-create-meaningful-names-in-code-20d7476537d4">원문 링크 - Daan</a>
author: author

---

Trend 파악을 Medium 기고문 요약 포스팅 - 코딩 할 때 의미있는 변수명을 짓는 방법

![500x400](https://cdn-images-1.medium.com/max/1600/1*OLAqSUqkqFec5ueSCdnt8A.png)

개발자로서 당신은 코딩을 할 때 적절한 이름을 사용하는 데에 많은 시간을 쏟을 것이다.
명명하는 것은 어디에나 있다. 당신은 파일과 클래스들과 메소드들과 변수들에 이름을 붙일 것이다.

우리가 작명하는 것에 그렇게 많은 시간을 들이는 것은 그만큼 중요한 것이기 때문이다.
이 기사에서는 좋은 작명 방법에 대한 몇 가지 간단한 법칙을 소개하려고 한다.

## Use Names Which Reveal Intention
의도가 명확히 드러나도록 작명하는 것이 좋다.

만약 이름에 코멘트가 필요하다면 그것은 의도를 나타내는 이름이 아니다.

~~~php
//Not good Name
private $s; // Time in seconds


//Much better Name
private $days_since_creation;
private $elapsed_time_in_seconds;
private $seconds_since_last_modifie


//Hard to figure out what this function does
function getList() {
    $list1 = [];

    foreach ($this->the_list as $x) {
        if ($x % 2 != 0) {
            $list1[] = $x;
        }
    }
  }
//Instead of getList, it's better to name as getOddNumbers
~~~

## Avoid Disinformation

좋은 작명은 코드의 의미를 애매하게 하는 잘못된 암시를 피해야 합니다.

예를 들어 객체의 타입이 List가 아니라면 productList라는 변수명은 피해야 합니다.

products라는 변수명이 훨씬 명확합니다.

그리고 대문자 'O'와 소문자 'l'을 변수명에 쓰는 것도 바람직 하지 않습니다.

왜냐하면 숫자 0과 1처럼 보이기 때문이죠

그리고 한눈에 이름을 모두 파악할 수 있도록 너무 긴 이름은 피하도록 합시다.

예를 들면 SomeMethodForEfficientHandlingOfFiles 와

SomeMethodForEfficientStorageOfFiles 처럼 말이죠

## Make Meaningful Distinctions

의미로 구분을 할 수 있게 작명을 합시다.

숫자를 뒤에 붙이는 작명은 좋은 방식이 아닙니다. 정보를 전달하지도 않고 코딩한 사람의 의도를

전달하지 못하기 때문입니다. 예시를 봅시다.

~~~php
public function duplicateArray($arr1, &$arr2) {
  foreach ($arr1 as $key => $value) {
    $arr2[$key] = $value;
  }
}
~~~

arr1과 arr2는 source와 destination으로 작명되는 것이 훨씬 낫습니다.

## Use Names You Can Pronounce

만약 당신이 이름을 발음할 수 없다면 당신은 회의할 때 바보처럼 보일 수 밖에 없습니다.

그리고 프로그래밍은 사회적 활동의 일부이기 때문에 이것은 실제로 문제가 됩니다.

모든 사람이 변수를 보고 바로 발음할 수 있는 것을 사용하는 것이 좋습니다.

당신의 회사에서 매우 중요한 축약어인 xsq 라는 변수명이 있다고 생각해봅시다.

"Hey, what about that variable eks ess kjew?"

"You mean the access queue?"

어떠너 개발자들은 변수를 한단어로 발음하려고 하기도 합니다. 다른 사람들은 스펠링을

읽는데 반해서요,

## Use Searchable names

한 글자로 된 변수는 어디에 있는지 찾기 쉽지 않기 때문에 문제가 됩니다.

상수를 바로 쓰는 것도 이따금 문제가 됩니다. 매직넘버를 쓰는 것 보다 MAX_BLOCKS_DISPLAYED와 같이 대체해서 쓰도록 합시다.

한 글자 변수를 사용하는 유일한 경우는 짧은 메소드 안에서 지역변수로 사용될 때 입니다.

## Member Prefixes

제발 숫자를 접두사로 쓰지마세요

예를 들어 어떤 개발자들은 private 멤버들에게 모두 언더바를 붙이기도 합니다.

그러지 마세요.

당신의 클래스들과 메소드는 작기 때문에 이런 접두사들을 쓰지 않아도 됩니다.

이것을 대체하기 위해서 IDE에서 해당 영역의 변수들을 색깔을 달리하는 방식을 쓰세요

## Summary

* 코딩 시에 작명하는 것은 매우 중요하다
* 위의 간단한 규칙을 참고하며 변수 등에 이름을 지을 때 주의하자
