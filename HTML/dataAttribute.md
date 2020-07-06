><h3>data-* 속성</h3>


<pre>표준이 아닌 속성이나 추가적인 DOM 속성, Node.setUserData()과 같은 다른 조작을 하지 않고도,
의미론적 표준 HTML 요소에 추가 정보를 저장할 수 있도록 해줍니다.</pre>

***
[사용법]
- 어느 엘리먼트에나 <code>data-</code>로 시작하는 속성은 무엇이든 사용 가능
- 화면에 안 보이게 글이나 추가정보를 엘리먼트에 담아 노을 수 있다.
<br>

***

[HTML 문법]
```html
<article
  id="electriccars"
  data-columns="3"
  data-index-number="12314"
  data-parent="cars">
...
</article>
```
***
[JavaScript에서 접급하기]
- HTML 이름과 함께 getAttribute() 사용
- 표준은 더 간단한 방법 사용 가능 : DOMStringMap은 dataset 속성을 통해 읽기 가능
- <code>dataset</code>객체를 통해 <code>data</code>속성을 가져오기 위해서는 속성 이름의 <code>data-</code> 뒷부분 사용<br>
  ※대시들은 camelCase로 변환!!

```javaScript
var article = document.getElementById('electriccars');
 
article.dataset.columns // "3"
article.dataset.indexNumber // "12314"
article.dataset.parent // "cars"
```
***
[CSS에서 접근하기]
- <code>data</code>속성은 순 HTML 속성이기 때문에 CSS에서도 접근 가능
```CSS
article::before {
  content: attr(data-parent);
}
```
- CSS의 <strong>속성 선택자</strong>도 데이터에 따라 스타일을 바꾸는데 사용할 수 있다.
```CSS
article[data-columns='3'] {
  width: 400px;
}
article[data-columns='4'] {
  width: 600px;
}
``` 
***
- 데이터 속성들은 게임 점수와 같이 계속 변하는 정보도 저장 할 수 있다
- IE10 이하를 지원하기 위해서는 getAttribute()를 통해 데이터 속성에 접근
