# Reactivity 에 대하여

> Vue 를 소개하기 위해서는 Reactivity 가 필수

<br/>

#### 기존 자바스크립트 방식
* 기존 방식에서는 변수의 값을 변경하면 재할당 없이는 바뀐 값이 적용되지 않는다.

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
    <div id="app">
        <!-- hello world -->
    </div>
    <script>
       var div = document.querySelector('#app');
       var str = 'hello world';
       div.innerHTML =str;
       // --> hello world

       str = 'hello world!!!!';
       div.innerHTML = str;
       // --> hello world
    
    </script>
</body>
</html>
```

<br/>

#### Vue 방식

* Vue 의 핵심. `Reactivity` `반응성`
새로운 값을 받을때마다 화면에 보이는 값이 바뀐다. 
데이터의 변화를 library 에서 감지해서 화면에 자동으로 그려주는 것이다.


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

    Object.defineProperty(viewModel,'str',{
        //속성에 접근했을 때의 동작을 정의
        get : function(){
            console.log('접근');
        },
        //속성에 값을 할당했을때의 동작을 정의
        set : function(newValue){
            console.log('할당', newValue);
            div.innerHTML= newValue; 
        }
    })
    </script>
</body>
</html>
```
 
 
 
** object.defineProperty()**
객체의 동작을 재정의하는 api 이다.

>_문법_
 Object.defineProperty(`대상객체`, `객체의 속성`, {
           `정의할 내용`
       } );