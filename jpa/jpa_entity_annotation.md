# Entity annotation 전략

<br /><br />

* 무분별한 어노테이션 사용의 문제
---

```java
@Getter
@Setter              // 문제 1. 객체가 무분별하게 변경될 가능성 있음
@NoArgsConstructor   // 문제 2. 기본 생성자의 접근 제어자가 불명확함
@Builder
@AllArgsConstructor  // 문제 3. 객체 내부의 인스턴스 멤버들을 모두 가지고 있는 생성자를 생성
@Entity
public class {entity_name} { // ... }
```

<br /><br /><br />

1. @Setter 사용을 지양한다.

```
Setter는 그 의도가 분명하지 않고,
객체를 언제든지 변경할 수 있는 상태가 되어서 객체의 안전성을 보장받기 힘들다.
특히 엔티티에서는 @Setter를 사용 시 해당 변경 가능성이 어디서 누구에 의해 발생했는지 추적하기가 힘들어진다.
```

<br /><br /><br />

2. @NoArgsConstructor(access = AccessLevel.PROTECTED)로 변경

```
기본 생성자(NoArgsConstructor)의 접근 제어를 PROCTECTED 로 설정하면,
아무런 값도 갖지 않는 의미 없는 객체의 생성을 막을 수 있다.
즉 무분별한 객체 생성에 대해 한번 더 체크할 수 있다.
```

```java
// @NoArgsConstructor(access = AccessLevel.PROTECTED) 
Entity entity = new Entity(); // 컴파일 에러 발생
```

```
이때, "의미있는 객체" 생성을 위해 @Builder을 사용할 수 있다.

@Builder를 사용하는 방법은 총 2가지인데,
1) 클래스에 @Builder 사용
2) 생성자에 @Builder 사용

이는 다음 @AllArgsConstructor를 쓰지 않아야 하는 것과 관련이 있다.
```

<br /><br /><br />

3. @AllArgsConstructor를 사용하지 않기

```
만약 해결 2의 방법1(클래스에 @Builder를 붙이기)을 사용,
클래스 레벨에서 @Builder와 @NoArgsConstructor를 함께 쓰면 오류가 발생한다.

이를 해결하기 위해서는 모든 필드를 가지는 생성자를 만들어주어야 하는데,
@AllArgsConstructor도 같이 써주게 된다.

하지만 @AllArgsConstructor은 너무 위험하다.
클래스에 존재하는 모든 필드에 대한 생성자를 자동으로 생성하는데,
인스턴스 멤버의 선언 순서에 영향을 받기 때문에 변수의 순서를 바꾸면
생성자의 입력 값 순서도 바뀌게 되어,
검출되지 않는 치명적인 오류를 발생시킬 수 있다.
```

```
그래서
해결 2의 방법2(생성자에 @Builder 사용)를 사용하여
@AllArgsConstructor를 쓰는 일이 없도록 한다.
```

<br /><br /><br />

* 리팩토링 후 코드 비교
---

```java
@Getter
@NoArgsConstructor(access = AccessLevel.PROTECTED)
@Entity
public class {entity_name} {

    @Id
    @Column(name = "id", nullable = false)
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    private String name;

    private String email;

    @ManyToOne(fetch = FetchType.Lazy)
    @JoinColum(name = "team_id")
    private Team team;

    @Enumerated(EnumType.STRING) // Enum타입 객체를 쓸때 반드시 String타입으로 바꿔주고 DB 필드에 어노테이션을 붙여준다.
    private Role role;

    // 생성자에 @Builder 적용
    @Builder
    public Member(String name, String email, Role role) {
        this.name = name;
        this.email = email;
        this.role = role;
    }
}
```

<br /><br /><br />

* TIP
---

```
* Builder default 사용법

초기화 시 특정 필드를 초기화하고 싶다면,
사용하는 @Builder 속성 어노테이션 내 .Default를 붙인다.
```

```java
@ToString
@NoArgsConstructor
@AllArgsConstructor
@Builder
public class {name} {

    @Builder.Default
    private String name = "test";
    private String nickname;

    @Builder.Default
    private List<PojoTwo> pojoTwos = new ArrayList<PojoTwo>();

}

{name}(name=test, nickname=codej625, pojoTwos=[])
{name}(name=test, nickname=chordj625, pojoTwos=[])
```
