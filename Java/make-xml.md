# xml 형식의 API / 파일 만들기
```java
// 루트 엘리먼트
Document doc = DocumentBuilderFactory.newInstance().newDocumentBuilder().newDocument();
Element rootElement = doc.createElement("company");
doc.appendChild(rootElement);

// staff 엘리먼트
Element staff = doc.createElement("staff");
rootElement.appendChild(staff);

// 속성값 정의
staff.setAttribute("id", "1");

// 닉네임 엘리먼트
Element nickname = doc.createElement("nickname");
nickname.appendChild(doc.createTextNode("Mr.Hong"));
staff.appendChild(nickname);

// salary
Element salary = doc.createElement("salary");
salary.appendChild(doc.createTextNode("100000"));
staff.appendChild(salary);

// XML 파일로 쓰기
TransformerFactory transformerFactory = TransformerFactory.newInstance();
Transformer transformer = transformerFactory.newTransformer();

transformer.setOutputProperty(OutputKeys.ENCODING, "UTF-8");
transformer.setOutputProperty(OutputKeys.INDENT, "yes");
transformer.setOutputProperty(OutputKeys.OMIT_XML_DECLARATION, "yes");
DOMSource source = new DOMSource(doc);
StringWriter writer = new StringWriter();

// 그냥 콘솔로 찍어볼때
//		StreamResult result = new StreamResult(System.out);
// 파일로 내보낼때
//		StreamResult result = new StreamResult(new FileOutputStream(new File(“C:\\file.xml”)));
//		transformer.transform(source, result);

transformer.transform(source, new StreamResult(writer));
String output = writer.getBuffer().toString();

model.addAttribute("result", output);
```
- API로 내보낼 시, 헤더에서 `contentType="text/xml"` 명시
