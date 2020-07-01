><h2>Package 생성하기</h2>
<pre>
패키지 : 자바의 가장 기본이 되는 "클래스(class)"를 구분하는 최소 분류 단위이다
</pre>
- 패키지는 'a.b.c.d'의 형태로 생성된다.
    1. '마침표(.)를 구분자로 하여 생성하며 파일 시스템에서는 '마침표(.)'가 폴더가 된다.
    2. 왼쪽에서 오른쪽으로 갈수록 상위 카테고리에서 하위 카테고리로 분류된다.
    3. 관심사별로 패키지를 만들어 클래스들을 관리한다.
    4. 클래스의 중복은 패키지와 클래스명이 같은 경우에 발생한다.
    
- 클래스의 중복
    1. 패키지명이 같은 경우 클래스명이 같은 클래스를 생성할 수 없다.
    2. 패키지명이 다를 경우 클래스명이 같은 클래스를 생성할 수 있다.
    3. 프로젝트에서는 외부에서 만들어진 클래스를 같이 사용하는 경우가 많으며 클래스 중복의 방지를 위해<br>
    패키지명의 depth를 'a.b.c.d'와 같이 일반적으로 4단계 이상으로 권장한다.
    
   