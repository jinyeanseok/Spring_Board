### ko.co.controller
```
controller의 역할은 웹에서 처리햐야할 데이터를 받고, 이 데이터를 담당할 service를 선택하여 호출
그리고 처리한 데이터를 다음 페이지에서 볼 수 있게 셋팅하며 이동할 페이지를 리턴
```

### ko.co.service
```
service는 데이터를 dao를 통해 넘겨주거나 받으면서 비즈니스 로직을 수행하는 역할을 함
```

### ko.co.dao
```
dao는 DB를 통해 데이터를 조회하거나 수정 삭제 하는 역할을 함
```

### ko.co.vo
```
vo는 DB에 있는 테이블 컬럼 값을 java에서 객체로 다루기 위해 사용
```

### import 자동화
```
메뉴 바에서 [window] - [Perferences] 선택

[Java] - [Editor] - [Save Actions] 선택

가장 상단 부에 Perform the selected actions on save 체크 박스 체크

Apply 누른 후 적용

```

### board/list.jsp
- <c:forEach items="${list}" var = "list">
```
forEach는 받은 ${list}값 만큼 반복해주는 것(자바에서 for문이랑 비슷)
```

```
여기서 ${list}는 BoardController에서 이름을 list로 정한 service.list()를 가져온 것.
```

```
var는 ${list}를 list라는 이름으로 선언 해준 것
```


- <c:out value="${list.bno}" />
```
데이터를 불러 왔으니 뿌려줘야 함
list에 있는 bno를 가져와라 라고 생각하면됨.
```

- forEach와 c:out를 쓰려면?
```
<%@ taglib uri="http://java.sun.com/jsp/jstl/core" prefix="c" %>를 맨위에 작성.
```

- fmt날짜 포맷을 써주려면?
```
<%@ taglib prefix="fmt" uri="http://java.sun.com/jsp/jstl/fmt"%>를 맨위에 작성.
```

### 게시물 조회의 대한 궁금증
```
<select id="read" parameterType="int" resultType="kr.co.vo.BoardVO">
		SELECT	BNO
			  , TITLE
			  , CONTENT
			  , WRITER
			  , REGDATE
		 FROM MP_BOARD
		 WHERE BNO = #{bno}
	</select>
```
- WHERE BNO = #{bno}를 보시면 WHERE에 BNO값을 넣어줘서 제목을 클릭했을때 그 번호에 해당하는 게시물을 조회하게끔 쿼리를 BoardMapper.xml에 추가해줍니다. 