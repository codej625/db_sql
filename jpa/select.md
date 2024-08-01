# JPA SELECT 구현

<br /><br />

```
동작 순서만 확인하는 예시이다.
접속 데이터베이스는 PostgreSQL이라는 전제로 한다.
(예시에서는 Service layer를 제외)
```

<br /><br /><br />

1. gradle

```gradle
// 의존성 추가
implementation 'org.springframework.boot:spring-boot-starter-data-jpa'
runtimeOnly 'org.postgresql:postgresql'
```

<br /><br /><br />

2. yaml

```yaml
# Database configuration
  datasource:
    url: jdbc:postgresql://192.168.0.152:5432/{database_name}
    username: {user_name}
    password: {user_password}
    driver-class-name: org.postgresql.Driver

  # Jpa
  jpa:
    open-in-view: false
    hibernate:
      # 스키마를 삭제하고 다시 생성한다.
      ddl-auto: create
      # 스키마를 변경하지 않는다.
      # ddl-auto: none
      # 스키마를 변경된 엔티티에 맞게 업데이트한다.
      # ddl-auto: update

    show-sql: true
    properties:
      hibernate:
      format_sql=true:
```

<br /><br /><br />

3. Entity Class

```java
@Entity
@Table(name = {table_name})
public class {method_name} {
  @Id
  @GeneratedValue(strategy = GenerationType.IDENTITY)
  private Long id;

  private String name;
  private String email;

  // Getters and setters
}
```

<br /><br /><br />

4. Repository
```java
public interface {interface_name} extends JpaRepository<User, Long> {}
```

<br /><br /><br />

5. Controller
```java
@RestController
public class {controller_name} {

  @Autowired
  private {interface_name} {variable_name};

  @GetMapping({path})
  public ResponseEntity<T> {controller_method_name}() {
  
    Entity entity = userRepository.findAll(); // All select

    return new ResponseEntity<>(entity, HttpStatus.OK);
  }
}
```
