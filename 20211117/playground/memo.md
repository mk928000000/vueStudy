# Vue 인스턴스에서의 this

<br/>
<br/>

## 1. javascript 인스턴스에서의 this

> javaScript 인스턴스에서는 내부 함수에서 `this` 를 사용하면 해당 인스턴스를 가리킨다.


```
<script>
  var obj = {
      num : 10,
      getNumber : function(){
        console.log(this.num)}  
        //여기에서의 this 는 obj 를 가리킨다. 그러므로 this의 num 값을 출력
    }
</script>

```

<br/>
<br/>

그러나 vue 인스턴스의 구조를 보면 data 라는 스코프 안에 변수가 선언된다.
그렇다면 methods 스코프안에 선언되는 함수가 this 를 사용하면 data 스코프 내 변수에 접근이 가능한가?

<br/>
<br/>


## 2. vue 인스턴스 내에서의 this



```
<script>

var vm = new Vue({
                el: '#app',
                components: {
                    ...

                },
                methods:{
                    ...,
                    addNumber:function(){
                        ...;
                        console.log(this.num); // <--- 여기에서 this는 ?
                    }

                },
                data : {
                    num:10       // <----- data 스코프 안에 있지만 vue 인스턴스의 변수로 찾아지는가?
                }
            });
</script>
```

<br/>
<br/>

**실행결과 ) **

![](https://images.velog.io/images/mk928000000/post/2765ce60-9fd6-4680-baa8-4a19668220a0/this.PNG)


* javascript 에서 this.num 이 num 값을 인식한 것 처럼,
  vue 의 this.num 도 data 스코프안의 num 값을 인식했다.

  <br/>

> _**결론 ) **_
vue 인스턴스는 javaScript 와 달리 `data 스코프 안에` 변수가 선언되지만,
javaScript 처럼 뷰 인스턴스의 직접적인 변수로 인식한다