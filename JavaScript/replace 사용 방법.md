><h2>자바스크립트 특정문자 바꾸기</h2>

<pre>
    자바스크립트에서 replace 메서드를 사용하면 첫 번째 문자만 치환이 되고 작동을 멈춘다.
    ※String 클래스에서 replaceAll 메서드를 추가하면 쉽게 문자를 치환 할 수 있다. 
</pre>
***
<h3>[ 방법 1. String prototype 메서드 추가 ]</h3>

```javascript
   //replaceAll prototype 선언
   String.prototype.replaceAll = function(org, dest) {
       return this.split(org).join(dest);
   }

   //replaceAll 사용
   var str = "Hello World";
   str = str.replaceAll("o","*");
   alert(str); 
```

- <code>str = str.split("o");</code>
- 출력 : ["Hell", " W", "rld"] 해당 문자로 배열이 만들어진다.
- <code>str = str.join("*");</code>
- 출력 : [Hell* W*rld] 배열을 해당 문자로 합친다.

<br>

<h3>[ 방법 2. 정규식 사용 ]</h3>

```javascript
    var str = "Hello World";
    str = str.replace(/o/g,"*");
    alert(str);
```

- <code>replace(/o/g,"*")</code> : o를 *로 전체 치환 한다.
- <code>replace(/o/gi,"*")</code> : o를 *로 대/소문자 구분 없이 전체 치환 한다.
- <code>g</code> : 발생할 모든 pattern에 대한 전역 검색
- <code>i</code> : 대소문자 구분 안함
- 정규식에서 사용하는 특수문자 <code>. ^ ( ) </code>를 치환할 때는 escape(\) 문자를 붙여 주어야 한다.
- <code>str = "Hello World.";</code> ==> <code>str = str.replace(/\./, "!");</code> ==> 출력 : <code>Hello World!</code>

