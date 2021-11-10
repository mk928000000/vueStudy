# 컴포넌트

> 1. 컴포넌트의 정의
2. 전역컴포넌트와 지역컴포넌트


<br/>
<br/>

### 컴포넌트란?
화면을 영역별로 구분해서 코드를 관리하는 것을 말한다.
예를 들어 위쪽은 헤더, 가운데는 컨텐츠 옆은 사이드로 구분해 관리하는 것이다.

### 컴포넌트의 사용 이유

코드의 반복을 줄이고 기존에 작성한 코드를 최대한 활용하는 것, `재사용성`을 위해서 이다.

> _일단은,_
화면의 영역을 구분해 개발하는 것을 컴포넌트라고 하며,
영역을 구분하면 컴포넌트 간의 관계가 생긴다는 것 까지만 알아두자.

<br/>


### 컴포넌트의 생성
뷰 인스턴스를 생성하면 인스턴스는 자동으로 `<Root> component` 가 된다.
여기에 컴포넌트를 추가로 등록해 보자.

```
<div id="app"></div>

<script>

  	//뷰 인스턴스 생성! 크롬 개발자도구로 보면 <Root> 컴포넌트가 등록된것을 볼 수 있다.
 	new Vue ({
          el: '#app'
	});  

</script>
```
<br/>

#### 방법 1. 전역 컴포넌트 등록방식
> 문법 : 
Vue.component( '컴포넌트 이름' ,  컴포넌트 내용 );
```
<script>
	//<app-header> 라는 태그에 컴포넌트가 등록되었다!
	Vue.component('app-header', {
            template : '<h1>Header</h1>'
        });
</script>
```

`template` 은 컴포넌트가 표현되는 마크업 스타일을 뜻하는 속성이다.
이제 인스턴스의 영역인 #app 에 app-header 라는 태그를 만들면 컴포넌트 내용이 반영되어 화면에 나타난다.


<br/>

```
//뷰 생성자로 등록된 인스턴스영역
<div id="app">
	<app-header></app-header>
</div>
```
![](https://images.velog.io/images/mk928000000/post/5ffe1aee-2c75-4cb6-a270-3fd78b7bfcf7/%EC%BB%B4%ED%8F%AC%EB%84%8C%ED%8A%B80.PNG)


* `<Root>` 태그 하위에 `<appHeader>` 태그가 있음을 확인할 수 있다.
* `<appHeader>` 태그는 컴포넌트의 template 에서 지정한대로 `<h1>` 태그로 작성된 글자 Header 로 화면에 나타난다.

<br/>
<br/>

#### 방법2. 지역 컴포넌트 등록방식
실제 서비스에서 많이 쓰이는 방식이다.
인스턴스 생성 시에 `components` 속성을 이용해 컴포넌트들을 등록한다.

> 문법 : 
 `'컴포넌트 이름' : 컴포넌트 내용` 으로 정의한다.
  `Vue.component('컴포넌트이름', 컴포넌트내용)` 의 구조로 전역 컴포넌트와 동일한 구조.
```
<script>
	 new Vue({
            el: '#app',
            //컴포넌!!츠!!!! s 가 붙는다.
            components: {
                'app-footer' : {
                    template : '<footer>footer</footer>'
                }
            }
        });
</script>
```


<br/>

### 전역 컴포넌트와 지역 컴포넌트의 차이
* 전역 컴포넌트의 문법에서는 `component` 속성 사용
   지역 컴포넌트의 문법에서는 `components` 속성 사용
   <br/>
* 지역 컴포넌트는 특정 컴포넌트 하단에 어떤 컴포넌트가 등록되어있는지 알 수 있다.
이 때문에 서비스를 구현할 때는 일반적으로 지역 컴포넌트로 등록한다.

<br/>
<br/>

### 컴포넌트와 인스턴스의 관계
* `전역 컴포넌트`를 등록하면 생성되는 모든 인스턴스에 `기본`으로 등록된다.
* 지역 컴포넌트는 인스턴스 생성 때마다 새로이 등록해 줘야한다.

```
// 상황 예시

<div id="app">
	<app-header></app-header>
    	<app-footer></app-footer>
</div>

<div id="app2">
	<app-header></app-header>
    	<app-footer></app-footer>
</div>


<script>

Vue.component('app-header',{
	template : '<h1>Header</h1>'
});

new Vue({
	el: '#app',
    components : {
    	'app-footer' : {
        	template : '<footer>footer</footer>'
        }
    }
});

new Vue({
	el: '#app2'
});

</script>
```

* `<app-header>` 는 전역 컴포넌트로 등록되어 #app2 에 등록하지 않았음에도 문제없이 작동된다.
* `<app-footer>` 는 #app 에서 지역 컴포넌트로 등록되어, #app2 에서는 인식할 수 없다.

![](https://images.velog.io/images/mk928000000/post/9ece5933-88c1-4d64-8225-ccb8d60a7c3a/%EC%BB%B4%ED%8F%AC%EB%84%8C%ED%8A%B81.PNG)