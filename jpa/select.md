#JPA SELECT를 구현해보자.

<br />

```

Under the assumption that the JPA dependency is already added, you can proceed with writing your code.

```

1. gradle
```gradle
If the dependency is not already added, add the script below under the Gradle section.

implementation 'org.springframework.boot:spring-boot-starter-data-jpa'
runtimeOnly 'org.postgresql:postgresql'
```

<br />

2. yaml
```yaml
# database configuration
spring.datasource.url=jdbc:postgresql://localhost:5432/your_database_name
spring.datasource.username=your_username
spring.datasource.password=your_password
spring.jpa.hibernate.ddl-auto=update

## In the operational phase, prevent schema updates with the following script.
### spring.jpa.hibernate.ddl-auto=validate
```

<br />

3. Entity Class
```java
@Entity
@Table(name = "users")
public class User {
  @Id
  @GeneratedValue(strategy = GenerationType.IDENTITY)
  private Long id;

  private String name;
  private String email;

  /* Getters and setters */
}
```

<br />

4. Repository
```java
public interface UserRepository extends JpaRepository<User, Long> {
  /* If additional query methods are needed, declare them here. */
}
```

<br />

5. Controller
```java
@RestController
public class UserController {
  @Autowired
  private UserRepository userRepository;

  @GetMapping("/users")
  public List<User> getUsers() {
    return userRepository.findAll(); /* Select */
  }
}
```
