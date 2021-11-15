# Event Emit


> 하위 컴포넌트에서 상위 컴포넌트로 이벤트를 올리는 방법

<br/>

**v-on: `하위컴포넌트 이벤트 이름`=`상위컴포넌트메소드명`**

하위 컴포넌트 이벤트가 발생했을 때 상위컴포넌트의 메서드가 실행된다.
<br/>



```
<body>
    <div id="app">
<!--

        event emit
        하위에서 상위 컴포넌트 : 이벤트를 올린다. event emit

        하위 컴포넌트 이벤트가 발생했을 때 상위컴포넌트의 메서드가 실행된다.
        <app-header v-on:하위 컴포넌트에서 발생한 이벤트 이름="상위컴포넌트의 메서드 이름"></app-header>

-->

        <app-header v-on:pass="logText"></app-header>
    </div>

    <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
    <script>

        var appHeader = {
                        //버튼을 클릭하면 passEvent 라는 메소드를 실행하겠다.
            template : '<button v-on:click="passEvent">click me</button>',
            methods :{
                passEvent : function (){ //메소드함수 passEvent 생성
                    this.$emit('pass'); // 위쪽에 보내는 이벤트 이름 pass 정의
                }
            }
        }

            new Vue({
                el: '#app',
                components: {
                    'app-header' : appHeader

                },
                methods:{
                    logText:function (){ // 이벤트 이름 logText 정의
                        console.log('hi!');
                    }
            });

    </script>
</body>
```



<br/>
<br/>

* appHeader 컴포넌트의 template 에 `v-on:click` 이벤트를 넣어, appHeader 클릭 시 `passEvent` 메소드를 실행시킨다.

* passEvent 메소드는 emit 으로 `pass`를 전달한다.

* ` <app-header v-on:pass="logText"></app-header>`
  app-header 에서 `pass` emit 이 상위 컴포넌트 `Root`의 메소드 `logText`를 실행시킨다.

* `new Vue` 인스턴스 생성에 methods `logText`가 정의되어 있다.
  <br/>

> 실행결과  :
`<app-header>` 클릭 시 콘솔창에 'hi' 가 찍힌다.

<br/>

![](https://images.velog.io/images/mk928000000/post/746aec53-602c-4d95-b70c-ead5ec03f537/event2.PNG)

***
<br/>
<br/>

###  연습 )
> 버튼을 클릭할 때마다 Vue 에 정의된 데이터 num 이 1씩 증가하게 만들어보자

 ```
 <div id="app">
        <app-content v-on:add="addNumber"></app-content>
    </div>
<script>

var appContent = {
            template: '<button v-on:click="increase">add</button>',
            methods : {
                increase : function(){
                    this.$emit('add')
                }
            }
        }
        
new Vue({
                el: '#app',
                components: {
                    'app-content': appContent

                },
                methods:{
                    addNumber:function(){ //메소드함수 addNumber 정의
                        this.num++; 
                        console.log(this.num);
                    }
                },
                data : {
                    num:10
                }
           });
 </script>
```
<br/>

* appContent 컴포넌트의 template 에서 v-on:click 을 통해 `increase` 메소드를 실행시킨다. `increase` 실행 때 emit 으로 `add` 가 발생한다.

* ` <app-content v-on:add="addNumber"></app-content>`
  `add` emit 이 상위컴포넌트의 메소드 `addNumber` 를 실행시킨다.

* new Vue 에 정의된 메소드 `addNumber` 가 실행되면서 내부 함수가 new Vue 의 data `num` 을 증가시키고 콘솔창에 값을 찍는다.
  <br/>


> 실행결과 :
`<app-content>` 버튼을 클릭할 때마다 콘솔창에 11부터 1씩 증가된 값이 찍힌다.

<br/>

![](https://images.velog.io/images/mk928000000/post/db8018cf-b1bf-49db-a001-53524efdd36a/event3.PNG)
