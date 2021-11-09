# Reactivity 코드 라이브러리화

> 즉시실행함수로 Reactivity 코드를 라이브러리화 해 본다. 
Vue의 구동체험이라 생각하자.

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    <div id="app"></div>

    <script>
       var div = document.querySelector('#app');
       var viewModel = {};

       //즉시실행함수.
       //내부의 함수들을 application 로직에 노출되지 않도록 또다른 스코프(유효범위)에 넣어준다.
       //일반적으로 오픈소스 라이브러리들이 이런식으로 관리된다.
       (function(){

            function init(){
            Object.defineProperty(viewModel,'str',{
                //속성에 접근했을 때의 동작을 정의
                get : function(){
                    console.log('접근');
                },
                //속성에 값을 할당했을때의 동작을 정의
                set : function(newValue){
                    console.log('할당', newValue);
                    render(newValue);
                }
            });
            }
    
            function render(value){
                div.innerHTML= value; 
            }
        
            init();

       }());
      
      


    </script>
</body>
</html>
```

#### 즉시실행함수 
* 즉시실행함수 내부의 함수들을 application 로직에 노출되지 않도록 또다른 스코프(유효범위)에 넣어준다.
 * 일반적으로 오픈소스 라이브러리들이 이런식으로 관리된다.


> _문법_       
	( function(){
		함수들 정의
	});
    
    
    
***
    
    
# Vue 의 사용

`chrome vue 확장` 을 설치하면 
  개발자도구에서 Vue 를 볼 수 있다.
  
  jquery 사용처럼 script src 로 vue cdn 을 입력하면 `<script></script>` 태그 안에서 vue 사용이 가능하다.
  
  ```
 <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
  <script>
      new Vue({
        el: '#app',
        data: {
          message: 'Hello Vue.js'
        }
      })
    </script>
   
```

 
***

# 인스턴스 생성

* `인스턴스`는 Vue 로 개발할 때 필수로 생성해야하는 코드이자 단위이다.

`new Vue();`

* 인스턴스를 생성하고 나면 인스턴스 안에 어떤 속성과 api 가 있는지 개발자도구 console 에서 확인할 수 있다.

```
<div id="app">
    <!-- ... -->
</div>

<script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
<script>
    //인스턴스 생성
    var vm = new Vue({
        //body 에서 #app을 가진 태그를 찾아서 인스턴스를 붙이겠다는 의미이다.
        //이걸 붙이는 순간 #app 안에서 vue 의 기능과 속성이 유효해진다.
        el : '#app',
        data : {
            message:'hi'
        }
    });
    //vue 개발자도구의 콘솔창에서 vm 을 입력하면 vm 의 속성과 api 가 출력된다.


</script>
```

<br/>
<br/>

### 왜 인스턴스를 생성자 함수 형태로 만드는가?


* 어떤 함수를 정의하는것이 아니라 **미리 정의한 함수** 를 사용할 수 있기 때문이다.
* Vue 의 사용은 Vue에서 어떤 api 와 속성을 정의해놓고 이것을 재사용하는 패턴이다.

<br/>
<br/>


> 미리 정의해 만든 함수를 사용하는 예시

```
<div id="app">
    <!-- ... -->
</div>

<script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
<script>

//함수명의 첫글자를 대문자로 하는것은 '생성자'를 만든다는 암묵적인 표현이다.
function Vue(){
    this.logText = function(){
        console.log('hello');
    }
}

var vm = new Vue();
vm.logText();
//--> hello 출력

</script>
```

<br/>
<br/>


### 인스턴스의 옵션과 사용

인스턴스에서 사용할 수 있는 속성과 api 는 다음과 같다. 옵션의 자세한 내용은 앞으로의 공부에서 알아보자.

> 
```
new Vue ({
    el: '',
    template: '',
    data: '',
    methods: '',
    created: '',
    watch: '',
});
```

* **공식 문서의 options 사용 방식**
options 객체를 변수로 정의하고 생성자에 담는 방법이다.

```
<script>
var options = {
        el : '#app',
        data : {
            message:'hi'
        },
        methods: {

        },
    };

    var vm = new Vue(options);
</script>
```
<br/>
<br/>

* **객체 리터럴을 통한 options 사용 방식**
`객체`를 통채로 생성자 안에 넣는 방법이다.
객체를 넣었으므로 콤마를 찍어 인자를 늘려감을 인지하자.

```
<script>
   var vm = new Vue({
        el : '#app',
        data : {
            message:'hi'
        },
        created: function(){

        }
    });
</script>
```