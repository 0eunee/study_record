#spring-jpa
> 스프링부트 기반으로 작성합니다.

- 자바 객체 매핑에 따라 테이블 자동 생성
- `pom.xml`에 추가시, 따로 버전을 명시하지 않아도 됨
    + `<parent></parent>`가 존재하기 때문
- **`javax.persistense`**
    + `@Entity`를 클래스에 추가하면 테이블과 매칭된다.
    + `@Id` : 프라이머리 키
    + `@GeneratedValue` : 1씩 자동 증가
    + `@Column` : 컬럼
        * `@Column(nullable=false)` - default는 true이므로 false로 주고 싶으면 명시해줘야 함
        * default 값들을 알고 싶으면 어노테이션 누르고 `F3`
        * 따로 적지 않아도 클래스 안 각각의 값들은 컬럼으로 설정 됨
- `application.properties`에 db정보 세팅
- `public interface ~~~Repository` 또는 `~~~DAO`는 `extends JpaRepository<Entity 선언한 클래스명, 프라이머리키 자료형>`
