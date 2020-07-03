><h3>@RequestBody / @ModelAttribute / @RequestParam 정리</h3>
>
- @RequestBody
    1. 클라이언트가 전송하는 Http 요청의 Body내용을 Java Object로 변환시켜주는 역할
    2. Body가 존재하지 않는 Get 방식의 메소드에는 에러가 발생, 반드시 POST 요청과 함께 사용
    3. Json이나 XML과 같은 형태의 데이터를 Jackson등의 MessageConverter를 활용하여 Java Object로 변환한다.
    4. Parameter로 받은 데이터들을 자바 객체로 1:1로 매칭시켜주는 @ModelAttribute와 차이가 있다.
    5. **POST방식으로 Json 형태로 넘겨온 데이터를 객체로 바인딩하기 위해 사용**
***
- @ModelAttribute
    1. 클라이언트가 전송하는 여러 파라미터들을 1대1로 객체에 바인딩하여 다시 View로 넘겨서 출력하기 위해 사용되응 오브젝트
    2. 매핑시키는 파라미터의 타입이 객체의 타입과 일치하는지를 포함한 다양한 검증(Validation) 작업이 추가적은로 진행
    3. int형의 변수에 String 형을 넣으면 BindException 발생
    4. 여러개의 파라미터를 바로 자바빈 객체로 매핑시킨다.
    5. JSP에서 Form 태그를 통해 전달받은 파라미터들을 객체로 바인딩 시키는 경우 사용<br>
    <pre>
    @ModelAttibute는 바인딩 시키는 어떤 데이터를 set 해주는 Setter 함수가 없다면 매핑 되지 않는다.
    @RequestBody는 요청받은 데이터를 변환시키는 것이기 떄문에, Setter 함수가 없어도 매핑이 된다.</pre>
***
- @RequestParam
    1. 요청 파라미터를 메소드에서 1:1로 받기 위해서 사용한다.
    2. 기본적으로 반드시 해당 파라미터가 전송되어야 한다.
    3. 반드시 필요한 데이터인가?를 나타내는 required의 값이 default로 true로 되어 있어 해당 파라미터가 전송되지 않으면 400 error를 유발
    4. 반드시 필요한 변수가 아니라면 required값을 false로 설정 할 수 있고, default로 받을 값도 설정할 수 있다.
    5. @RequestParam(value = "파라미터명", required="boolean", defaultValue="값")의 형식
***
-  예제 코드<br>

[모델 객체]
```java
public class StudentVO {
    private int index;
    private String name;
    private String gender;
    
    public int getIndex() {
        return index;
    }
    public void setIndex(int index) {
        this.index = index;
    }
    
    public String getName() {
        return name;
    }
    public void setName(String name) {
        this.name = name;
    }
    
    public String getGender() {
        return gender;
    }

    public void setGender(String gender) {
        this.gender = gender;
    }
}
```
[컨트롤러]
```java
@Controller
@RequestMapping(value = "/student")
@Log4j2
public class StudentController {

    @PostMapping(value = "/requestBody")
    public ResponseEntity requestBody(@RequestBody StudentVO studentVO){
        // @RequestBody는 Json으로 받은 요청을 MessageConverter를 통해 Java 객체로 변환시킨다.
        log.info(StudentVO.getContents());
        return ResponseEntity.ok(studentService.add(studentVO));
    }
    
    @PostMapping(value = "/modelAttribute")
    public String modelAttribute(Model model, @ModelAttribute StudentVO studentVO){
        // @ModelAttribute는 Form태그를 통해 전송받은 파라미터들을 Java 객체로 매핑시킨다.
        // 만약 studentVO에 contents에 대한 Setter함수가 없다면 매핑을 시키지 못하고, 항상 null을 갖게 된다.
        log.info(studentVO.getContents());
        model.addAttribute("studentVO", studentService.add(studentVO));
        return "/views/student/detail";
    }
    
    @GetMapping(value = "/list")
    public ResponseEntity requestParam(@RequestParam(value = "searchKeyWord1", required = false) String searchKeyWord1, @RequestParam(value = "writer", defaultValue = "gildong") String searchKeyWord2){
        List<StudentVO> studentList;

        // searchKeyWord1는 required가 false이기 때문에 없을 수도 있다.
        if(searchKeyWord1 != null){
            studentList = studentService.findAllStudentBySearchKeyWord(searchKeyWord1);
        } else {
            studentList = studentService.findAllStudent();
        }
        // 반면에, searchKeyWord2는 required가 true이기 때문에 반드시 요청 파라미터로 존재해야 한다.
        log.info(searchKeyWord2);

        return ResponseEntity.ok(studentList);
    }
}
```

추가 정리해보기 : Controller에서 다양한 타입으로 request 받기
https://sjh836.tistory.com/143