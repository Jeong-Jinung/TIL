><h3>JAVA getClass() 메소드 사용법</h3>
- 현재 참조하고 있는 클래스를 확인할 수 있는 메소드
- A 라는 클래스를 참조하고 있다면 class A 라는 값이 출력된다.

<pre>
    <code>
    public class Test01 {
        public static void main(String[] args) {
        
            ArrayList<String> list = new ArrayList<>();
            
            System.out.println("getClass:::" + list.getClass());
            System.out.println("getName:::" + list.getClass().getName());
        }
      }    
    </code>
</pre>

- getName()과 같이 사용할 수 있다.
- 실행 결과<br>
![캡처](https://user-images.githubusercontent.com/52848296/86305483-b3e6b880-bc4c-11ea-9015-05dcd065eccc.PNG)




