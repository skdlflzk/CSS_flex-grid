# Flex 와 Grid


## CSS Flex
flexible box , flexbox

레이아웃 배치 전용.
float 이나 inline-block보다 강력 / 편리.
flex만 가능한 ui가 있고, flex가 간단하다.

플렉스 레이아웃을 위한 기본 html

```html
<div class="container">
	<div class="item">hellofle><<div/>
	<div class="item">abc<div/>
	<div class="item">helloflex<div/>
<div/>
```


각 아이템이 플렉스 규칙에 따라 배치
 - 컨테이너에 적용하는 속성?

```css
display:flex;
```

float랑 비슷하게 보인다.

flex는 내용물의 width 만큼만 차지함.

 - 장점?
 
float은 자기 컨텐치만큼만 늘어남
flex는 컨테이너의 높이에 맞게 늘어남.

```html
inline-flex;
```
-> inline은 자기가 가진 만큼만 늘어나게 됨.

[display:flex;]

내용물

<--

-->

[display:inline-flex;]다음 내용물 <- 옆으로 나란히. 요 차이임.


*** 

## 축?

| 축 | 의미 |
|---|:---:|
|`main axis`| flex item 방향 축, 메인 축 (가로 세로 변경 가능) |
|`cross axis`| main과 수직인 축, 교차축 |



* 메인 축 방향 바꾸기?


**flex-direction: xxx;**

| 값 |방향 | 예 |
|---|---|:---:|
|`row`| ->>> |[[내][용][물] _ _ _ ]|
|`row-reverse`|  <<<- |[ _ _ _ [물][용][내]]|
|`column`| v |  |
|`column-reverse`| ^|  |

rtl 언어(아랍어 할때 row-reverse)

* 줄넘김 처리?

**flex-wrap:xxx;**


기본은 내용물이 부모가 작아도 버티기 nowrap  
(float은 컨테이너가 줄어들면 자동 줄맞춤  
부모가 내용물보다 작으면 아래로 이동하기 wrap  


(* 메인축 방향을 바꾸는 flex-wrap과 flex-direction을 같이 쓰는 법? flex-flow)

팁 - 플렉스박스, 그리드 세려면 firefox 개발자도구 검사기-레이아웃을 확인
```html
<style>
	@media (min-width:600px){
	}
</style>
```

 - @media? 
화면조건에 맞는 css를 적용할 수 있는데, 모바일같은 좁은 화면서는 아래처럼 정렬가능.

```html
<style>
	.flex-container{
		display:flex;
		flex-direction:column;
	}
	@media (min-width:600px){
		.flex-container{
			display:flex;
			flex-direction:row;
		}
		.flex-item{
			flex:1;
		}
	}
</style>
```

display block으로 하는거랑 무슨 차이인가?
=>  유연하다구

---

## 전체 아이템 정렬

 |  <= 이건 길쭉 오뎅  
ㅡ|ㅡ|ㅡ|ㅡㅡㅡㅡ  <= 이건 오뎅 꼬치  

메인축 - 꼬치에 오뎅을 꽂는 방향.  
교차축 - 길쭉 오뎅의 방향  
임을 염두에 두자

justify? 메인축 방향으로 꼬치 방향정렬
align? 수직축 방향으로 길쭉 오뎅 방향 정렬

 - 꼬치를 어떻게 꽂을 거냐?

**justify-content:xxx;**


| 값 | 설명 | 예 |
|:---|---|:---:|
|`flex-start(default)`| 메인축 방향대로 정렬 |[[내][용][물] _ _ _]|
|`flex-end`|끝방향으로 밀기|[ _ _ _ [내][용][물]] **<=>** row-reverse  	[ _ _ _ [물][용][내]]|
|`space-between`| |[[내] _ _ _ [용] _ _ _[물]]|
|`space-around`|	|[ _ [내] _ _ [용] _ _ [물] _ ]|
|~~`space-evenly`~~|(ie, edge지원 안함!)|[ _ [내] _ [용] _ [물] _ ]|



 - 오뎅 하나의 모양은 어떻게 되어있냐?
 
 **align-items:xxx;**
 
| 값 | 설명 |
|:---|---|
|`stretch(기본)`|float과의 차이. 컨테이너에 맞춰서 늘림|
|`flex-start`|늘리지않고 내용물 크기만큼 상단(첫아이템 위치) 에 정렬|
|`flex-end`|늘리지 않고 하단(마지막 아이템 위치) 정렬|
|`flex-center`|늘리지않고 중앙정렬|
|`flex-baseline`|Text 하단에 맞춤 (잘 안쓰인다.)|

 - 여러행 정렬?

***align-content:xxx;***

아래 2개 오뎅판이 있다.  
1.  첫번째 판  

ㅡㅡㅡㅡㅡㅡㅡㅡㅡ  
ㅡ|ㅡ|ㅡ|[ㅡㅡ  _ _ _ _  ]|  == 오뎅 꼬치 with nowrap  
  
  
ㅡㅡㅡㅡㅡㅡㅡㅡㅡ  
  
2. 두번째 판  

ㅡㅡㅡㅡㅡㅡㅡㅡㅡ  
  
ㅡ|ㅡ|ㅡㅡㅡㅡ  
|[ㅡㅡㅡ]|ㅡㅡ  == 오뎅 꼬치 with wrap  
  
ㅡㅡㅡㅡㅡㅡㅡㅡㅡ  


> 여러 행이라는 것은, 꼬치길이보다 오뎅이 큰 경우
> 다른 꼬치로 이동한 상황을 말하는 것.
> 즉, flex-wrap:nowrap인 기본 세팅에서는 적용이 되지 않는다.
>  flex-wrap:wrap으로 설정되어 부모 컨테이너보다 items 총합 크기가 더 커서 아래로 내려간 경우의 정렬 방식을 정의하는  속성

| 값 | 설명 | 예|
|:---|---|---|
|`stretch(기본)`|align-items가 stretch인 경우 오뎅판에 오뎅을 쭉 늘려서 채워놓음| |
|`flex-start`|align-items가 flext-xxx으로 내용물을 맞춘경우 오뎅판의 상단(첫아이템위치)에 정렬|위 첫번째 오뎅판의 경우|
|`flex-end`|늘리지 않고 하단(마지막 아이템 위치) 정렬| |
|`space-between`| | | 
|`space-around`| | |

--- 

###정리해보면 **플렉스 박스 배치 방법 4가지***

1. flex-direction: row-reverse;
2. justify-content: flex-start;
3. align-items:	flex-baseline;
4. align-content: space-between; (flex-wrap:wrap; 조건 필수)


---

## flex 아이템에 적용하는 속성

 - 아이템의 기본 크기?

**flex-basis**

아이템이 가지는 기본 크기. != width, height 의미가 다르다.  
flex-direction:row 라면 가로의 너비가 되고 flex-column이면 세로 높이가 되는 것.  

```css
flex-basis:auto; /*기본은 auto - 너비에 맞춤*/
flex-basis:100px;  
```

  
 - 유연하게 늘리기?

**flex-grow**

```css
flex-grow:0; /*기본 0 ~ N*/ 
```
숫자의 의미?  
아이템들의 flex-basis를 제외한 여백 부분을 flex-grow에 지정된 숫자의 비율로 나눈다  
```css
{flex-grow:1;}
```
이면 1 / 1이므로 꽉채우기


```css
.flex-item:nth-child(1){
	flex-grow:1;
}
.flex-item:nth-child(2){
	flex-grow:2;
}
.flex-item:nth-child(1){
	flex-grow:1;
}
```
이면 1/4 , 2/4, 1/4로  

[[내123456 _ ] [용 _  _ ] [물 _ ]] <= 여백이 1:2:1 이라는 것.

 - 유연하게 줄이기?

**flex-shrink**

flex-grow와 세트.  
기본 flex-shrink : 1;

ex) 화면이 이동하는데 특정 아이템이 줄어드는것을 원하지 않을때
```css
.flex-item:nth-child(1){flex-shrink:0;width:100px}
.flex-item:nth-child(2){flex-grow:1;}
```

[쉬링크0 _ _ _][그로우1 _ _ _ _ _ _ _ _ _ _ _ _ _]  
화면이 반으로 축소되면?  
[쉬링크0 _ _ _][그로우1 _ _ _ ]  


- flex-grow, flex-shrink, flex-basis 위 속성을 한번에?

**flex: n n x;**

flex : [flex-grow] + [flex-shrink] + [flex-basis];

```css
flex:1;
/* flex-grow:1;flex-shrink:1;flex-basis:0%*/ 
```
혹은
```css
flex: 1 1 auto;
flex: 1 500px;  /* flex-shrink는 없어도 flex-basis 가 500px임을 의미*/
```

flex는 아이템 크기가 커져도 강제로 맞추지는 않는다.  
-> 이런 경우에는 그냥 width:20% 등으로 맞출것.

> flex 아이템에 width만 쓴다는것? 유연함/유동성을 포기하는것이다.

