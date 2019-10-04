---
layout: post
title: Basic of the JavaScript (1)
description: >
  <a href="https://medium.com/free-code-camp/the-definitive-node-js-handbook-6912378afc6e">학습자료링크</a>
author: author
comments: true
---
<a href="https://flaviocopes.com/javascript-lexical-structure/">JavaScript Lexical Structure</a>

## Unicode
자바스크립트는 유니코드로 작성되었습니다. 이말은 이모지또한 변수이름으로 쓸 수 있다는 것이죠. 더욱 중요한 것은 <a href="https://mathiasbynens.be/notes/javascript-identifiers">일정 규칙</a>만 준수하면 중국어나 일본어 같이 어떤 언어라도 구분자로 사용할 수 있다는 것입니다.

## Semicolons
자바스크립트는 C와 비슷한 문법을 가지고 있습니다. 그리고 많은 예제에서 각 라인마다 세미콜론이 붙어있는 걸 보셨을 수도 있겠네요. 세미콜론은 의무적인 것이 아니고 코드에서 세미콜론을 사용하지 않아도 아무 문제가 없습니다. 최근 세미콜론이 없는 언어를 사용해온 개발자들은 세미콜론 사용을 기피하고 있습니다.

다음과 같이 한 문장을 여러줄에 나눠서 타이핑하는 이상한 짓만 안하시면 됩니다.
```
return
variable
```
아니면 라인의 시작을 대괄호, 중괄호로 시작하지만 않으면 안전할 것입니다. 제 개인적인 취향으로 저는 세미콜론을 사용하지 않기로 했기 때문에 여기 예제에서는 절대 보실 수 없을겁니다.
## White space
자바스크립트는 공백문자를 의미있게 간주하지 않습니다. 공백과 line breaks는 여러분이 좋아하는 대로 추가될 수 있습니다.

일반적으로는 사람들이 자주 사용하는 스타일을 쓰는 것을 좋아하실 겁니다 그리고 linter나 Prettier와 같은 도구를 사용해서 강제할 수 있습니다.

저는 항상 두 단어로 작성하는 것을 좋아합니다.
## Case sensitive
자바스크립트는 대소문자를 구분합니다. something은 Something과 다릅니다. 구분자도 마찬가지 입니다.
## Comments
/\* \*/, // 두 가지 종류의 주석처리 스타일이 있습니다. 처음은 닫기 전까지 여러줄을 주석처리 하며 두번쨰 것은 현재 라인을 주석처리 합니다.
## Literals and Identifiers
우리는 리터럴을 소스코드 내에 작성된 변수로 정의합니다. 예를 들어 숫자, 문자열, 불 변수 그리고 객체 리터럴과 변수 리터럴 같은 구조체를 말합니다.
```
5
'test'
true
['a', 'b']
{color: 'red', shape: 'Rectangle'}
```
식별자는 함수, 객체, 변수를 식별하기 위해 사용되는 문자열입니다. 문자로 시작하거나 '$', '\_'로 시작할 수 있으며 숫자를 포함할 수 있습니다. 유니코드를 사용하면 이모지와 같은 어떤 문자도 사용할 수 있습니다.
```
Test
test
TEST
_test
Test1
$test
```
달러 표시는 DOM요소에 주로 사용됩니다.
## Reserved words
다음의 단어는 언어에서 사용하기 때문에 식별자로 사용할 수 없습니다.
```
break
do
instanceof
typeof
case
else
new
var
catch
finally
return
void
continue
for
switch
while
debugger
function
this
with
default
if
throw
delete
in
try
class
enum
extends
super
const
export
import
implements
let
private
public
interface
package
protected
static
yield
```
<a href="https://flaviocopes.com/javascript-expressions/">JavaScript Expressions</a>
## Arithmetic expressions
수치를 구하기 위한 표현입니다.
```
1 / 2
i++
i -= 2
i * 2
```
## String expressions
문자를 나타내기 위한 표현입니다.
```
'A ' + 'string'
```
## Primary expressions
아래는 리터럴이나 상수 변수들을 조회합니다.
```
2
0.02
'something'
true
false
this // 현재 객체
undefined
i // i 가 변수나 상수일 때
```
다음은 키워드 들입니다.
```
function
class
function* // 함수 생성자
yield // pauser/resumer 생성자
yield* // 또 다른 생성자나 순회자를 위한 대표자
async function* // 비동기 함수 표현
await // 비동기 함수 완료시 pause/resume/wait 함
/pattern/i //정규식
() // 그룹핑
```
## Array and object initializers expressions
```
[] //배열 리터럴
{} //객체 리터럴
[1, 2, 3]
{a: 1, b: 2}
{a: {b: 1}}
```
## Logical expressions
논리 표현은 논리 연산자를 사용하거나 불 값을 바꾸는데 사용됩니다.
```
a && b
a || b
!a
```
## Left-hand-side expressions
```
new // 생성자의 인스턴스 생성
super // 부모의 생성자를 호출
...obj // 스프레드 연산자의 표현
```
## Property access expressions
```
object.property // 객체의 프로퍼티나 메소드를 참조
object[property]
object['property']
```
## Object creation expressions
```
new object()
new a(1)
new MyRectangle('name', 2, {a:4})
```
## Function definition expressions
```
function() {}
function(a,b) { return a * b}
(a, b) => a * b
a => a * 2
() => { return 2}
```
## Invocation expressions
함수나 메소드 호출 문법
```
a.x(2)
window.resize()
```
<a href="https://flaviocopes.com/javascript-types/">JavaScript Types</a>
여러분은 자바스크립트가 타입이 없다고 여러번 들으셨을 수도 있지만 그건 부정확합니다. 변수에 모든 종류의 타입을 할당 할 수 있는 것은 사실이지만 자바스크립트는 타입이 있습니다. 특히나 객체타입과 기본타입을 제공합니다.
## Primitive types
기본 타입들은 넘버/문자열/불변수/심볼이고 특수 타입은 널과 undefined입니다.
## Numbers
내부적으로 자바스크립트는 숫자가 부동소수라도 하나의 숫자타입만 가지고 있습니다.
숫자 리터럴은 소스코드에 숫자를 나타내며 어떻게 쓰여지느냐에 따라서 정수 리터럴 혹은 부동소수점 리터럴로 표현됩니다.
```
10
5354576767321
0xCC // 16진수
```
```
3.14
.1234
5.2e4 // 5.2 * 10^4
```
## Strings
문자열 타입은 캐릭터의 흐름입니다. 소스코드에서 문자열 리터럴로 정의되며 따옴표나 쌍따옴표안에 위치합니다.
```
'A string'
"Another string"
```
문자열은 백래쉬를 이용하여 멀티라인으로 확장될 수 있습니다.
```
"A \
string"
```
문자열은 \\n과 같이 문자가 출력될 때 해석되는 이스케이스 문자를 포함할 수 있습니다. 백래쉬는 따옴표 안에 공백문자를 넣거나 문자 내에 따옴표를 표현하기 위해 사용됩니다.
```
'I\'m a developer'
"A " + "string" //문자열은 + 연산자를 사용하여 붙일 수 있습니다.
```
## Template literals
ES2015에서 소개된 템플릿 리터럴은 문자열 리터럴을 더욱 강력하게 정의할 수 있게 해줍니다.
```
const a_string = 'something'
```
여러분은 어떤 JS 표현이라도 결과에 문자열을 치환하여 포함시킬 수 있습니다.
```
'a string with ${something}'
`a string with ${something+somethingElse}`
'a string with ${obj.something()}'
```
멀티라인 문자열도 쉽게 표현할 수 있습니다.
```
`a string
with
${something}`
```
## Booleans
자바스크립트는 불 표현을 위해 두가지 예약어가 있습니다. true 와 false입니다. ===, <, >와 같은 비교연산자는 불 값을 리턴합니다.

if,while 구문과 다른 컨트롤 구조에서 불린은 흐름을 결정합니다. 그냥 true,false만 받아들이는게 아니라 참이나 거짓을 나타내는 변수도 받아들입니다.
false로 해석되는 거짓 변수들은 다음과 같습니다.
```
0
-0
undefined
null
`` //빈 문자
```
나머지는 모두 참인 변수로 취급됩니다.
## null
널은 값이 없음을 암시하는 특별한 값입니다. 다른 언어에서도 일반적인 개념으로 파이썬에서는 nil이나 None으로 알려진 값이죠.
## undefined
undefined는 해당 변수가 초기화 되지 않았고 값도 없음을 나타냅니다. 리턴 값이 없는 함수들에게서 리턴되며 함수가 매개변수를 받아들이지만 호출 시 세팅되지 않으면 그것이 undefined입니다.

undefined를 탐지하기 위해서 다음과 같이 구성을 해야합니다.
```
typeof variable === 'undefined'
```
## object types
기본타입이 아닌 모든 타입은 객체 타입입니다. 객체타입은 프로퍼티가 있고 프로퍼티에 동작을 하는 메소드가 있습니다.
## How to find the type of variable
어떤 변수라도 할당된 타입이 있습니다. typeof 연산자를 사용해서 타입을 대표하는 문자열을 얻어낼 수 있습니다.
```
typeof 1 === 'number'
typeof '1' === 'string'
typeof {name: 'Flavio'} === 'object'
typeof [1, 2, 3] === 'object'
typeof true === 'boolean'
typeof undefined === 'undefined'
typeof (() => {}) === 'function'
```
왜 typeof가 "function"을 리턴할까요? 자바스크립트는 function 타입이 없습니다. 이것은 typeof의 불규칙한 결과로 그냥 편리함을 위해 해당 값을 리턴하는 것입니다.

<a href="https://flaviocopes.com/javascript-variables/">JavaScript Variables</a>
## Introduction to JavaScript Variables
변수는 구분자에게 할당된 리터럴로 프로그램에서 나중에 조회하거나 사용할 수 있습니다. 자바스크립트의 변수는 타입이 추가로 붙지 않습니다. 한번 특정 리터럴 타입을 변수에게 할당해도 타입에러나 다른 이슈 없이 다음에 어떤 타입으로도 재할당 가능합니다.

이것이 자바스크립트가 때때로 untyped라고 언급되는 이유입니다. 변수는 사용하기 전에 선언되어야 합니다. var, let, const를 사용해서 선언할 수 있으며 이 방법은 변수가 나중에 어떻게 상호작용하는지 차이점을 나타냅니다.
## Using var
ES2015 전까지는 var가 변수를 정의하는 유일한 방법이었습니다.
```
var a = 0
```
var를 추가하지 않는다면 정의되지 않는 값이 할당되어 결과가 달라질 수 있습니다.

요즘 개발환경에서 strict 모드를 켜면 에러를 받게 될 것입니다. 구식 환경에서는 변수를 초기화 하고 전역 객체에게 할당합니다.

여러분이 선언할 때 변수를 초기화하지 않으면 값을 할당할 때까지 undefined 값을 가지게 됩니다.
```
var b // typeof a === 'undefined'
```
여러분은 변수를 여러번 재정의하거나 덮어쓸 수 있습니다.
```
var a = 1
var a = 2
```
여러분은 또한 같은 구문에서 여러개의 변수를 정의할 수 있습니다.
```
var a = 1, b = 2
```
스코프는 변수가 보이는 코드의 영역입니다. var와 함께 함수밖에서 초기화된 변수는 전역 객체에게 할당되며 전역 스코프를 가지며 어디서나 사용할 수 있습니다. var와 함께 함수 내에서 초기화된 함수는 함수 내에서만 사용가능하며 함수 파라미터와 같이 저역 변수로 취급됩니다.

함수 내에 전역변수와 동일한 이름으로 선언된 지역변수는 전역변수를 가리게 됩니다. 블록이 새로운 스코프를 정의하지 않는 다는 것을 이해하는 것이 중요합니다. 새로운 스코프는 오직 함수가 만들어질 때만 생성됩니다. 왜냐하면 var는 블록 스코프가 없지만 함수는 가지고 있기 때문입니다.

함수 내에서는 어디에서 선언되더라도 사용할 수 있습니다. 변수 가 함수 끝에서 선언되었어도 함수 처음부분에서 사용할 수 있습니다. 왜냐하면 자바스크립트는 코드를 실행하기 전에 모든 변수를 탑에 옮겨놓기 때문입니다. 혼동을 막기위해서 변수는 항상 함수의 시작부분에 선언합니다.
## Using let
let은 ES2015의 새로운 피처로 소개되었으며 var의 닫힌 스코프 버전입니다. 스코프가 블록이나 구문, 정의된 표현으로 제한되며 모든 것이 내부 블록에 있습니다.

최근 자바스크립트 개발자들은 아마 let만 사용하고 var는 완전히 사용하지 않을 수 있습니다. let을 함수 밖에서 선언하는 것은 var와는 다르게 전역 변수를 생성하지 않습니다.
## Using const
var/let으로 생성된 변수는 프로그램에서 나중에 변경되거나 재할당 될 수 있습니다. const는 한번 초기화되면 값이 절대 변하지 않습니다.
```
const a = 'test'
```
우리는 a상수에게 다른 리터럴을 할당할 수 없습니다. 만약 a가 값을 변환시키는 메소드를 제공한다면 값을 변환시킬 수 있습니다. const는 불변성을 제공하는 것이 아니라 단지 변하지 않은 값을 조회할 수 있도록 보장합니다. const는 let과 같은 블록 스코프를 가집니다. 요즘 자바개발자들은 나중에 값이 재할당되길 원치 않는 변수들에 대해서는 항상 const를 사용할 것입니다. 왜냐하면 우리는 에러를 낮추기 위해 항상 간단한 구조를 사용해야 하기 때문입니다.
<a href="https://flaviocopes.com/javascript-math-operators/">JavaScript Math Operators</a>
수학 연산자들로 계산을 하는 것은 프로그래밍 언어에서 매우 일반적인 일입니다. 자바 스크립트는 숫자로 작업하는데 도움이 되는 여러 연산자들이 있습니다.
## Addition (+)
```
const three = 1 + 2
const four = three + 1
```
더하기 연산자는 문자열을 연결할 때도 사용됩니다. 그러니까 문자를 사용할 때는 주의를 해 주세요
```
const three = 1 + 2
three + 1 // 4
'three' + 1 // threeq
```
## Subtraction (-)
```
const two = 4 - 2
```
## Division (/)
연산자의 앞부분을 뒷부분으로 나눈 몫을 리턴합니다.
```
const result = 20 / 5 //result === 4
const result = 20 / 7 //result === 2.8571..
```
만약 0으로 나누게 되면 자바스크립트는 에러를 발생시키지 않고 Infinity/-Infinity 값을 리턴합니다.
```
1 / 0 //Infinity
-1 / 0 //-Infinity
```
## Remainder (%)
나머지 연산자는 많은 계산에서 매우 유용합니다.
```
const result = 20 % 5 // result === 0
const result = 20 % 7 // result === 6
```
0으로 나머지 연산을 수행하면 항상 NaN을 리턴합니다(Not a Number)
```
1 % 0 //NaN
-1 % 0 //NaN
```
## Muliplication (\*)
두 숫자를 곱합니다.
```
1 * 2 //2
-1 * 2 //-1
```
## Exponentiation (\*\*)
첫번째 피연산자를 두번째 피연산자의 제곱승으로 표현합니다.
```
1 ** 2 // 1
2 ** 1 // 2
2 ** 2 // 4
2 ** 8 // 256
```
제곱승 연산자(\*\*)는 Math.pow()함수를 사용하는 것과 동일하지만 언어가 아닌 라이브러리 함수로 사용된다는 것입니다.
```
Math.pow(4, 2) == 4 ** 2
```
이 피처는 수학용 자바 응용프로그램을 위한 좋은 추가입니다.
\*\*연산자는 파이썬, 루비, MATLAB,Lua, Perl등 많은 언어에서도 표준화되었습니다.
## Increment (++)
숫자를 증가시킵니다. 단일 연산자로서 숫자 앞에 사용하면 증가된 값을 리턴합니다. 숫자뒤에 붙이는 경우 원래 값을 리턴한 다음 값을 증가 시킵니다.
```
let x = 0
x++ //0
x // 1
++x //2
```
## Decrement (--)
증가연산자와 동일한 작업을 수행하지만 값을 감소시킵니다.
## Unary negation (-)
피연산자의 마이너스 값을 리턴합니다.
## Unary plus (+)
피연산자가 숫자가 아니라면 숫자로 변환을 시도합니다. 피연산자가 숫자라면 아무동작도 하지 않습니다.

<a href="https://flaviocopes.com/javascript-functions/">JavaScript Functions</a>
## Introduction
자바스크립트의 모든 것은 함수에서 일어납니다. 자바는 코드 블록이며 한번 정의되면 여러분이 원할 때마다 실행할 수 있습니다. 함수는 선택적으로 매개변수들을 가질 수 있으며 하나의 값을 리턴합니다. 자바스크립트의 함수는 함수객체라는 특별한 객체입니다. 그들의 강력한 힘의 근원은 그들이 호출될 수 있다는 것이죠. 추가적으로 함수는 일급 클래스 함수로서 변수에 할당될 수 있고 매개변수로 넘겨지거나 리턴 값으로 사용될 수 있습니다.

## Syntax
ES6이전에 구식 문법부터 시작해봅시다. 여기서 사용된 foo와 bar는 무작위 이름으로써 다른 이름으로 대체하세요.
```
function dosomething(foo) {
  //do something
}
```
ES6에서는 정규 함수라고 언급됩니다. 함수는 변수에 할당될 수 있고 함수표현이라고 불립니다.
```
const dosomething = function(foo) {
  //do something
}
```
명명된 함수 표현은 비슷하지만 에러가 발생했을 경우 스택 호출 추적과 함께 사용하면 매우 좋습니다. 함수의 이름을 붙잡고 있기 때문이죠.
```
const dosomething = function dosomething(foo) {
  //do something
}
```
ES6에서는 화살표 함수가 소개되었습니다. 매개변수로 콜백과 같은 인라인 함수와 사용할 때 매우 좋습니다.
```
const dosomething = foo => {
  //do something
}
```

## Parameters
하나의 함수는 한개 이상의 파라미터를 가질 수 있습니다.
```
const dosomething = () => {
  //do something
}

const dosomethingElse = foo => {
  //do something
}

const dosomethingElseAgain = (foo, bar) => {
  //do something
}
```
ES6에서는 함수에서 파라미터의 기본값을 가질 수 있게되었습니다.
```
const dosomething = (foo = 1, bar = 'hey') => {
  //do something
}
```
이 때문에 매개변수를 넘겨주지 않고 함수를 호출할 수 있습니다.
```
dosomething(3)
dosomething()
```
ES2018에서 소개된 파라미터를 위한 trailing쉼표는 파라미터 주변의 쉼표가 없어서 생기는 버그를 줄이는데 도움이 되는 피처입니다.
```
const dosomething = (foo = 1, bar = 'hey') => {
  //do something
}
dosomething(2, 'ho!')
```
여러분은 모든 매개변수를 배열로 래핑할 수 있습니다, 그리고 함수를 호출할 때 스프레드 연산자를 사용할 수 있죠
```
const dosomething = (foo = 1, bar = 'hey') => {
  //do something
}
const args = [2, 'ho!']
dosomething(...args)
```
파라미터가 많이지면 순서를 기억하는 게 어려울 수 있습니다. 객체를 사용해서 비구조화하는 것이 매개변수의 이름을 유지할 수 있게 해줍니다.
```
const dosomething = ({ foo = 1, bar = 'hey' }) => {
  //do something
  console.log(foo) // 2
  console.log(bar) // 'ho!'
}
const args = { foo: 2, bar: 'ho!' }
dosomething(args)
```
## Return values
모든 함수는 리턴값이 있고 기본 리턴값은 undefined입니다.
<center>
<img src="https://flaviocopes.com/javascript-functions/undefined-return-value.png"/>
</center>
모든 함수는 코드가 끝나거나 return 키워드를 실행하는 흐름을 만나면 끝이납니다. 자바스크립트는 return 키워드를 만나면 함수 실행을 종료하고 콜러에게 제어를 넘겨줍니다. 값이 전달되는 경우 그 값은 함수의 결과로 리턴됩니다.

여러분은 오직 하나의 값만 리턴할 수 있습니다. 여러개의 값을 리턴하고 싶다면 객체 리터럴이나 배열을 사용하세요. 그리고 함수 호출 시 <a href="https://flaviocopes.com/es6/#destructuring-assignments">비구조화 할당</a>을 사용하세요

배열을 사용할 때:
<center>
<img src="https://flaviocopes.com/javascript-functions/destructuring-return-array.png"/>
</center>
객체를 사용할 때:
<center>
<img src="https://flaviocopes.com/javascript-functions/destructuring-return-object.png"/>
</center>
## Nested functions
함수는 다른 함수 내부에 정의될 수 있습니다.
```
const dosomething = () => {
  const dosomethingElse = () => {
    //some code here
  }
  dosomethingElse()
  return 'test'
}
```
중첩된 함수의 스코프는 바깥 함수에 해당되며 외부에서 호출될 수 없습니다. 이 의미는 dosomethingElse()가 dosomething() 외부에서는 호출될 수 없다는 것입니다.

```
const dosomething = () => {
  const dosomethingElse = () => {
    //some code here
  }
  dosomethingElse()
  return 'test'
}
dosomethingElse() //ReferenceError: dosomethingElse is not defined
```
이것은 중첩함수를 정의한 외부함수로 스코프를 제한하기 때문에 캡슐화된 코드를 만들 수 있어서 매우 유용합니다. 우리는 함수 내부에 똑같은 중첩함수를 가진 2개의 함수를 생각해 볼 수 있습니다.
```
const bark = () => {
  const dosomethingelse = () => {
    //some code here
  }
  dosomethingelse()
  return 'test'
}


const sleep = () => {
  const dosomethingelse = () => {
    //some code here
  }
  dosomethingelse()
  return 'test'
}
```
이런 경우 가장 중요한 것은 이미 존재하는 함수와 변수들이 함수 외부에서 덮어씌여지는 것에 대해 생각할 필요가 없다는 것입니다.
## Object Methods
객체의 프로퍼티로 사용되는 경우 함수들은 메소드라고 불립니다.
```
const car = {
  brand: 'Ford',
  model: 'Fiesta',
  start: function() {
    console.log(`Started ${this.brand} ${this.model}`)
  },
  stop: () => {
    console.log(`Stopped ${this.brand} ${this.model}`)
  }
}
```
## this in Arrow Functions
객체의 메소드로 함수가 사용될 때 화살표함수와 정규함수의 동작에 중요한 차이가 있습니다. 다음의 예제를 봅시다.
```
const car = {
  brand: 'Ford',
  model: 'Fiesta',
  start: function() {
    console.log(`Started ${this.brand} ${this.model}`)
  },
  stop: () => {
    console.log(`Stopped ${this.brand} ${this.model}`)
  }
}
```
stop() 메소드는 여러분이 원하는 대로 동작하지 않습니다.
<center>
<img src="https://flaviocopes.com/javascript-functions/methods-this.png"/>
</center>
이것은 this를 처리하는 방식이 두 함수가 서로 다르기 때문입니다. 화살표 함수에서 this는 함수 내부 컨텍스트로 제한되며 여기서는 window object를 가리킵니다.
<center>
<img src="https://flaviocopes.com/javascript-functions/methods-this-window.png"/>
</center>
this는 function을 사용하는 주인 객체를 가리킵니다. 이것은 화살표 함수가 객체의 메소드와 생성자로 사용하기엔 적절하지 않다는 것을 의미합니다.(화살표 함수 생성자는 호출될 때 TypeError를 일으킵니다.)
## IIFE, Immediately Invocated Function Expressions
An IIFE는 정의와 동시에 바로 실행되는 함수 입니다.
```
;(function dosomething() {
  console.log('executed')
  })()
```
결과 값을 변수에 할당할 수 있습니다.
```
const something = (function dosomething() {
  return 'something'
  })()
```
함수 선언 후에 따로 호출할 필요가 없기 때문에 매우 편리합니다.
## Function Hoisting
자바스크립트는 여러분의 코드를 실행하기 전에 몇가지 규칙에 따라 순서를 재배치 합니다. 함수는 그들의 영역에서 가장 윗부분으로 끌어올려집니다.
```
dosomething()
function dosomething() {
  console.log('did something')
}
```
<center>
<img src="https://flaviocopes.com/javascript-functions/hoisting-example.png"/>
</center>
내부적으로 자바스크립트는 함수가 호출되기 전에 같은 스코프에 있는 모든 연관된 함수를 옮깁니다.
```
function dosomething() {
  console.log('did something')
}
dosomething()
```
만약 여러분이 명명된 함수 표현을 사용한다면 변수를 사용할 때 뭔가 다른일이 발생합니다. 변수는 정의될 때 상단부로 이동되지만 값은 아닙니다. 함수도 마찬가지죠.
```
dosomething()
const dosomething = function dosomething() {
  console.log('did something')
}
```
이건 동작하지 않을겁니다.
<center>
<img src="https://flaviocopes.com/javascript-functions/hoisting-named.png"/>
</center>
이것은 내부적으로 다음과 같이 동작하기 때문입니다.
```
const dosomething
dosomething()
dosomething = function dosomething() {
  console.log('did something')
}
```
let 정의에서도 동일한 일이 발생하며 var역시 동일하게 동작하지 않지만 다른 에러가 발생합니다.
<center>
<img src="https://flaviocopes.com/javascript-functions/hoisting-var.png"/>
</center>
이것은 var의 정의가 위로 이동한 뒤에 undefined로 초기화되기 때문입니다.

<a href="https://flaviocopes.com/javascript-iife/">JavaScript Immediately-Invoked Function Expressions</a>
즉시호출함수표현(IIFE)는 함수가 만들자마자 실행하는 방법입니다. IIFE는 전역 객체를 건드리지 않고 변수 선언을 독립시키는 쉬운 방법이기 떄문에 매우 유용합니다. 다음은 IIFE의 정의 문법입니다.
```
(function() {
  /* */
  })()
```
IIFE는 화살표 함수로도 잘 정의됩니다.
```
(() => {
  /* */
  })()
```
기본적으로 괄호내부에 함수를 정의하며 뒤에 ()를 추가하여 함수를 실행시킵니다. <b>(\/\* function \*\/)()</b>
위의 래핑하는 괄호들이 실제적으로 함수를 만들어 주는 것이며 내부적으로 표현으로 간주됩니다. 그렇지 않으면 함수 정의가 무효될 것이고 어떤 이름도 사용할 수 없습니다.
<center>
<img src="https://flaviocopes.com/javascript-iife/invalid-function-declaration.png"/>
</center>
함수 정의는 이름을 원하는 반면 함수 표현은 이름을 요구하지 않습니다.

여러분은 호출 괄호를 표현 괄호 내부에 넣을 수도 있습니다. 차이점은 없고 그냥 스타일의 차이입니다.
```
(function() {
  /* */
}())

(() => {
  /* */
}())
```
## Alternative syntax using unary operators
IIFE를 정의하는 기괴한 문법들이 있지만 실제로는 거의 쓰이지 않고 단일 연산자를 사용하는데 의존합니다.
```
-(function() {
  /* */
})() +
  (function() {
    /* */
  })()

~(function() {
  /* */
})()

!(function() {
  /* */
})()
```
화살표 함수로는 동작하지 않습니다.
## Named IIFE
IIFE는 명명된 정규함수도 될 수 있습니다(화살표 함수는 안됩니다). 이것은 IIFE의 특징인 글로벌 스코프에 유출되지 않는 것과 실행 후에 다시 호출될 수 없는 것을 유지합니다.
```
(function doSomething() {
  /* */
})()
```
## IIFEs starting with a semicolon
여러분은 아마 다음과 같은 구문을 보셨을겁니다.
```
;(function() {
  /* */
})()
```
이것은 두 자바스크립트 파일이 암시적으로 연결되는 이슈를 막기위한 것입니다. 자바스크립트가 세미콜론을 요구하지 않으므로 어떤 구문의 마지막과 파일이 연결되어 문법 오류를 일으킬 수도 있습니다. 이 문제는 webpack과 같이 똑똑한 코드 번들러와 함께 사용하면 해결됩니다.

<a href="https://flaviocopes.com/javascript-this/">this</a>
this 키워드는 어디서 사용되느냐에 따라서 값이 달라집니다. 자바스크립트의 이 세세한 부분을 모른다면 많은 두통을 유발할 수 있습니다. 그러니까 5분을 들여서 모든 기법을 익히는 것은 매우 가치가 있을 것입니다.
## this in strict mode
strict 모드에서는 모든 객체 외부에서 this의 값이 undefined입니다. 제가 strict mode라고 한것을 기억하세요. strict mode가 disable이라면(sloppy mode) this는 전역 객체의 값을 가집니다. 따라서 window 컨텍스트를 가지게 됩니다.
## this in methods
메소드는 객체에 달려있는 함수입니다. 다양한 형태를 보실 수 있죠. 다음을 살펴봅시다.
```
const car = {
  maker: 'Ford',
  model: 'Fiesta',

  drive() {
    console.log(`Driving a ${this.maker} ${this.model} car!`)
  }
}

car.drive()
//Driving a Ford Fiesta car!
```
이 경우에 정규 함수를 사용하면 this는 객체에 자동적으로 연결됩니다. 위의 메소드 정의는 drive: function () {...}와 동일합니다만 짧게 줄인겁니다. 다음의 예제도 동일하게 동작합니다.
```
const car = {
  maker: 'Ford',
  model: 'Fiesta'
}

car.drive = function() {
  console.log(`Driving a ${this.maker} ${this.model} car!`)
}

car.drive()
//Driving a Ford Fiesta car!
```
화살표 함수는 내부적으로 바인딩이 되기 때문에 똑같이 동작하지 않습니다.
```
const car = {
  maker: 'Ford',
  model: 'Fiesta',

  drive: () => {
    console.log(`Driving a ${this.maker} ${this.model} car!`)
  }
}

car.drive()
//Driving a undefined undefined car!
```
## Binding arrow functions
화살표 함수에서는 일반함수에서 하는 것 처럼 값을 연결할 수 없습니다. 이것은 화살표 함수가 동작하는 방식 때문에 가능하지 않습니다. this는 어휘적인 연결로 this가 정의된 컨텍스트에서 값이 전달된다는 의미입니다.
## Explicitly pass an object to be used as this
자바스크립트는 여러분이 원하는 객체에 this를 맵핑하는 몇가지 방법을 제공합니다. bind()를 함수 정의단계에서 사용하는 것입니다.
```
const car = {
  maker: 'Ford',
  model: 'Fiesta'
}

const drive = function() {
  console.log(`Driving a ${this.maker} ${this.model} car!`)
}.bind(car)

drive()
//Driving a Ford Fiesta car!
```
이미 존재하는 객체의 메소드에 존재하는 this의 값을 바인딩 할 수도 있습니다.
```
const car = {
  maker: 'Ford',
  model: 'Fiesta',

  drive() {
    console.log(`Driving a ${this.maker} ${this.model} car!`)
  }
}

const anotherCar = {
  maker: 'Audi',
  model: 'A4'
}

car.drive.bind(anotherCar)()
//Driving a Audi A4 car!
```
call() 혹은 apply()를 함수 호출 단계에서 사용할 수도 있습니다.
```
const car = {
  maker: 'Ford',
  model: 'Fiesta'
}

const drive = function(kmh) {
  console.log(`Driving a ${this.maker} ${this.model} car at ${kmh} km/h!`)
}

drive.call(car, 100)
//Driving a Ford Fiesta car at 100 km/h!

drive.apply(car, [100])
//Driving a Ford Fiesta car at 100 km/h!
```
call()이나 apply()로 전달되는 첫 매개변수는 항상 this에 연결됩니다. call()과 apply()의 차이점은 함수에 전달되는 두번째 매개변수가 매개변수 리스트인 배열을 원하는지 하나의 값을 원하는지의 차이입니다.
## The special case of browser event handlers
이벤트 핸들러 콜백에서 this는 이벤트를 받은 HTML 요소를 가리킵니다.
```
document.querySelector('#button').addEventListener('click', function(e) {
  console.log(this) //HTMLElement
}
```
다음과 같이 bind를 사용할 수도 있습니다.
```
document.querySelector('#button').addEventListener(
  'click',
  function(e) {
    console.log(this) //Window if global, or your context
  }.bind(this)
)
```
