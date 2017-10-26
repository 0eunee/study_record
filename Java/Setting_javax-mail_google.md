# javax.mail 발신자를 구글메일로 사용할 때의 설정 방법
- 명시할 프로퍼티
  + [스택오버플로우 질문글](https://stackoverflow.com/questions/15378133/could-not-connect-to-smtp-host-smtp-gmail-com-port-465-response-1) 참조
  ```java
  props.put("mail.smtp.user", "메일보내는아이디@gmail.com");
  props.put("mail.smtp.host", "smtp.gmail.com");
  props.put("mail.smtp.port", "465");
  props.put("mail.smtp.starttls.enable", "true");
  props.put("mail.smtp.auth", "true");
  props.put("mail.smtp.socketFactory.port", "465");
  props.put("mail.smtp.socketFactory.class", "javax.net.ssl.SSLSocketFactory");
  props.put("mail.smtp.socketFactory.fallback", "false");
  ```
- 보낼 구글 메일로 로그인 한 후 밑 링크의 step1을 따라야 보내짐
  + [Read Gmail messages on other email clients using IMAP](https://support.google.com/mail/answer/7126229)
- 사용한 소스 (기존에 있던 소스에 `prop.put`만 수정함)
  + 컨트롤러에서 호출
  ```java
  HtmlTransfer htl = new HtmlTransfer(메일주소, 보낼 데이터);
  htl.mailSend();
  ```
  + 유틸 클래스
  ```java
  public class HtmlTransfer {
    private String from;
    private String to;
    private String sendData;

    public HtmlTransfer(String to, String sendData) {
      this.from = "메일보내는아이디@gmail.com";
      this.to = to;
      this.sendData = sendData;
    }

    public void mailSend(){
      if(from == null || to == null) {
        System.out.println("usage : java <from> <to> <filename>");
        System.exit(0);
      }

      try{   
        // 시스템 속성 객체 생성
        Properties props = System.getProperties();

        props.put("mail.smtp.user", "agrtwebmaster@gmail.com");
        props.put("mail.smtp.host", "smtp.gmail.com");
        props.put("mail.smtp.port", "465");
        props.put("mail.smtp.starttls.enable", "true");
        props.put("mail.smtp.auth", "true");
        props.put("mail.smtp.socketFactory.port", "465");
        props.put("mail.smtp.socketFactory.class", "javax.net.ssl.SSLSocketFactory");
        props.put("mail.smtp.socketFactory.fallback", "false");

        // 메일 서버 세션 생성
        Session session = Session.getInstance(props);

        // 메세지 정의
        Message message = new MimeMessage(session);

        // 메일 헤더 설정
        message.setSubject("제목");
        message.setFrom(new InternetAddress(from));
        message.addRecipient(Message.RecipientType.TO, new InternetAddress(to));

        // 메세지 몸체 생성
        BodyPart messageBodyPart = new MimeBodyPart();

        // HTML 데이터 생성
        String htmlText = "";
        htmlText += "html태그 사용하여 메일 내용 작성. 보낼 데이터 있으면" + sendData + "사용해주기";

        // 단순히 텍스트로만 발송할 경우에는 text/html 대신에 text/plain으로 바꾸시면 됩니다.
        message.setContent(htmlText, "text/html; charset=euc-kr");

        // 다양한 종류의 데이터 추가를 위한 객체 생성
        //MimeMultipart multipart = new MimeMultipart("related");

        // 메세지 몸체를 Multipart 객체에 추가
        //multipart.addBodyPart(messageBodyPart);

        // 이미지 메세지 몸체 생성
        //messageBodyPart = new MimeBodyPart();

        // 메세지 몸체에 이미지 첨부
        //DataSource fds = new FileDataSource(filename);

        // 메세지 몸체에 파일 객체 첨부
        //messageBodyPart.setDataHandler(new DataHandler(fds));

        // 파일 이름 설정
        //messageBodyPart.setFileName(filename);

        // 메일 헤더 설정
        message.setHeader("Content-ID", "family");

        // 메세지 몸체를 Multipart 객체에 추가
        // multipart.addBodyPart(messageBodyPart);

        // Multipart 객체를  Message 객체에 추가
        // message.setContent(multipart);

        // 보낸 날짜 설정
        message.setSentDate(new Date());

        // 생성된 메세지 전송
        Transport t = session.getTransport("smtp");
        t.connect("메일보내는아이디@gmail.com", "비밀번호");
        t.sendMessage(message, message.getAllRecipients());
      }
      catch(javax.mail.MessagingException ex) {
        System.out.println("ERROR");
        ex.printStackTrace();
      }
    }
  }
  ```
