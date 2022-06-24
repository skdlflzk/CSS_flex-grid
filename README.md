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
