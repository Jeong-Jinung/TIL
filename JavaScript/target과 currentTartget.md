><h4>event.target 과 event.currentTartget의 차이점

<br>

<pre>event.target</pre>
- 버블링의 가장 마지막에 위치한 최하위의 요소를 반환
- 즉 클릭된 요소를 기준으로 사용하는 경우 사용
```html
<div onclick="checkTarget();">
    <p>click test</p>
    <span>test</span>
</div>
```
- 이 경우 <code>div</code>에 이벤트를 걸어도 <code>span</code>태그를 클릭하면, 클릭된 <code>element</code>를 가져옴.

***

<pre>event.currentTarget</pre>
- 이벤트가 바인딩된 요소를 반환
```html
<div onclick="checkTarget();">
    <p>click test</p>
    <span>test</span>
</div>
```
- <code>span</code>태그를 클릭해도 이벤트가 바인딩 된 <code>div</code> 태그를 반환


