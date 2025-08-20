---
title: "DevZip의 보안과 관리자 권한 시스템 설계"
parent: 사이드 프로젝트 - DevZip
grand_parent: Projects
layout: default
date: 2025-08-08 20:48:37
---

# DevZip 프로젝트의 보안: 관리자 권한 및 접근 제어 시스템

## 개요

DevZip 프로젝트는 Spring Boot 3.3.1 기반의 웹 분석 플랫폼으로, JWT 기반 인증과 Spring Security를 활용한 세밀한 관리자 접근 제어 시스템을 구현했습니다. 이 글에서는 실제 Spring Boot 환경에서 구현된 보안 메커니즘과 설계 철학을 소개합니다.

## Spring Security 기반 인증 시스템

### 기술 스택
- **Spring Boot 3.3.1**
- **Spring Security**: 인증 및 권한 부여
- **JWT (JSON Web Token)**: 상태 없는 인증
- **JPA/Hibernate**: 사용자 엔티티 관리
- **MySQL**: 사용자 정보 저장

### JWT 설정 (application.properties)
```properties
# JWT 설정
app.jwt.secret=${JWT_SECRET_KEY:defaultSecretKey}
app.jwt.expiration=86400000
app.cors.allowed-origins=http://localhost:3000,https://devzip.cloud
```

### 사용자 엔티티 구현
```java
@Entity
@Table(name = "users")
public class User {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;
    
    @Column(unique = true, nullable = false)
    private String username;
    
    @Column(nullable = false)
    private String password;
    
    @Column(unique = true, nullable = false)
    private String email;
    
    @Enumerated(EnumType.STRING)
    private Role role = Role.USER;
    
    // getters, setters, constructors
}

public enum Role {
    USER, ADMIN
}
```

## Spring Security 설정

### SecurityConfig 클래스
```java
@Configuration
@EnableWebSecurity
@EnableMethodSecurity(prePostEnabled = true)
public class SecurityConfig {
    
    @Autowired
    private JwtAuthenticationEntryPoint jwtAuthenticationEntryPoint;
    
    @Autowired
    private JwtRequestFilter jwtRequestFilter;
    
    @Bean
    public PasswordEncoder passwordEncoder() {
        return new BCryptPasswordEncoder();
    }
    
    @Bean
    public AuthenticationManager authenticationManager(
            AuthenticationConfiguration authConfig) throws Exception {
        return authConfig.getAuthenticationManager();
    }
    
    @Bean
    public SecurityFilterChain filterChain(HttpSecurity http) throws Exception {
        http.csrf(csrf -> csrf.disable())
            .authorizeHttpRequests(authz -> authz
                .requestMatchers("/api/auth/**").permitAll()
                .requestMatchers("/api/log/event").permitAll()
                .requestMatchers("/api/admin/**").hasRole("ADMIN")
                .anyRequest().authenticated()
            )
            .exceptionHandling(ex -> ex
                .authenticationEntryPoint(jwtAuthenticationEntryPoint)
            )
            .sessionManagement(session -> session
                .sessionCreationPolicy(SessionCreationPolicy.STATELESS)
            );
        
        http.addFilterBefore(jwtRequestFilter, UsernamePasswordAuthenticationFilter.class);
        
        return http.build();
    }
}

## JWT 토큰 관리

### JWT 유틸리티 클래스
```java
@Component
public class JwtUtil {
    
    private String secret;
    private long jwtExpiration;
    
    public JwtUtil(@Value("${app.jwt.secret}") String secret,
                   @Value("${app.jwt.expiration}") long jwtExpiration) {
        this.secret = secret;
        this.jwtExpiration = jwtExpiration;
    }
    
    public String generateToken(UserDetails userDetails) {
        Map<String, Object> claims = new HashMap<>();
        // 사용자 역할 정보를 JWT 클레임에 포함
        claims.put("role", userDetails.getAuthorities().iterator().next().getAuthority());
        return createToken(claims, userDetails.getUsername());
    }
    
    private String createToken(Map<String, Object> claims, String subject) {
        return Jwts.builder()
                .setClaims(claims)
                .setSubject(subject)
                .setIssuedAt(new Date(System.currentTimeMillis()))
                .setExpiration(new Date(System.currentTimeMillis() + jwtExpiration))
                .signWith(SignatureAlgorithm.HS512, secret)
                .compact();
    }
    
    public Boolean validateToken(String token, UserDetails userDetails) {
        final String username = getUsernameFromToken(token);
        return (username.equals(userDetails.getUsername()) && !isTokenExpired(token));
    }
}
```

### JWT 인증 필터
```java
@Component
public class JwtRequestFilter extends OncePerRequestFilter {
    
    @Autowired
    private UserDetailsService userDetailsService;
    
    @Autowired
    private JwtUtil jwtUtil;
    
    @Override
    protected void doFilterInternal(HttpServletRequest request, 
                                  HttpServletResponse response, 
                                  FilterChain chain) throws ServletException, IOException {
        
        final String requestTokenHeader = request.getHeader("Authorization");
        
        String username = null;
        String jwtToken = null;
        
        if (requestTokenHeader != null && requestTokenHeader.startsWith("Bearer ")) {
            jwtToken = requestTokenHeader.substring(7);
            try {
                username = jwtUtil.getUsernameFromToken(jwtToken);
            } catch (IllegalArgumentException e) {
                logger.error("JWT Token 획득 실패", e);
            } catch (ExpiredJwtException e) {
                logger.error("JWT Token 만료됨", e);
            }
        }
        
        if (username != null && SecurityContextHolder.getContext().getAuthentication() == null) {
            UserDetails userDetails = this.userDetailsService.loadUserByUsername(username);
            
            if (jwtUtil.validateToken(jwtToken, userDetails)) {
                UsernamePasswordAuthenticationToken authToken = 
                    new UsernamePasswordAuthenticationToken(
                        userDetails, null, userDetails.getAuthorities());
                authToken.setDetails(new WebAuthenticationDetailsSource().buildDetails(request));
                SecurityContextHolder.getContext().setAuthentication(authToken);
            }
        }
        chain.doFilter(request, response);
    }
}
```

## 관리자 API 컨트롤러

### AuthController - 인증 관련 엔드포인트
```java
@RestController
@RequestMapping("/api/auth")
@CrossOrigin(origins = {"http://localhost:3000", "https://devzip.cloud"})
public class AuthController {
    
    @Autowired
    private AuthenticationManager authenticationManager;
    
    @Autowired
    private JwtUtil jwtUtil;
    
    @Autowired
    private UserService userService;
    
    @PostMapping("/login")
    public ResponseEntity<?> login(@RequestBody LoginRequest loginRequest) {
        try {
            authenticationManager.authenticate(
                new UsernamePasswordAuthenticationToken(
                    loginRequest.getUsername(), 
                    loginRequest.getPassword())
            );
        } catch (BadCredentialsException e) {
            throw new BadCredentialsException("잘못된 자격 증명", e);
        }
        
        final UserDetails userDetails = userService
            .loadUserByUsername(loginRequest.getUsername());
        final String token = jwtUtil.generateToken(userDetails);
        
        return ResponseEntity.ok(new JwtResponse(token));
    }
    
    @PostMapping("/register")
    public ResponseEntity<?> register(@RequestBody SignUpRequest signUpRequest) {
        if (userService.existsByUsername(signUpRequest.getUsername())) {
            return ResponseEntity.badRequest()
                .body(new MessageResponse("오류: 사용자명이 이미 사용 중입니다!"));
        }
        
        if (userService.existsByEmail(signUpRequest.getEmail())) {
            return ResponseEntity.badRequest()
                .body(new MessageResponse("오류: 이메일이 이미 사용 중입니다!"));
        }
        
        // 새 사용자 계정 생성 (기본 역할: USER)
        User user = new User(signUpRequest.getUsername(),
                           signUpRequest.getEmail(),
                           passwordEncoder.encode(signUpRequest.getPassword()));
        user.setRole(Role.USER);
        
        userService.save(user);
        
        return ResponseEntity.ok(new MessageResponse("사용자가 성공적으로 등록되었습니다!"));
    }
}
```

### AdminController - 관리자 전용 기능
```java
@RestController
@RequestMapping("/api/admin")
@PreAuthorize("hasRole('ADMIN')")
@CrossOrigin(origins = {"http://localhost:3000", "https://devzip.cloud"})
public class AdminController {
    
    @Autowired
    private UserService userService;
    
    @Autowired
    private EventService eventService;
    
    @GetMapping("/users")
    public ResponseEntity<List<User>> getAllUsers() {
        List<User> users = userService.findAll();
        return ResponseEntity.ok(users);
    }
    
    @PostMapping("/users")
    public ResponseEntity<?> createUser(@RequestBody CreateUserRequest request) {
        if (userService.existsByUsername(request.getUsername())) {
            return ResponseEntity.badRequest()
                .body(new MessageResponse("사용자명이 이미 존재합니다."));
        }
        
        User user = new User();
        user.setUsername(request.getUsername());
        user.setEmail(request.getEmail());
        user.setPassword(passwordEncoder.encode(request.getPassword()));
        user.setRole(request.getRole()); // ADMIN 또는 USER
        
        userService.save(user);
        
        return ResponseEntity.ok(new MessageResponse("사용자가 성공적으로 생성되었습니다."));
    }
    
    @GetMapping("/events")
    public ResponseEntity<Page<Event>> getEvents(
            @RequestParam(defaultValue = "0") int page,
            @RequestParam(defaultValue = "50") int size) {
        
        Pageable pageable = PageRequest.of(page, size);
        Page<Event> events = eventService.findAll(pageable);
        
        return ResponseEntity.ok(events);
    }
    
    @GetMapping("/stats")
    public ResponseEntity<AdminStats> getStats() {
        AdminStats stats = new AdminStats();
        stats.setTotalUsers(userService.count());
        stats.setTotalEvents(eventService.count());
        stats.setActiveUsers(userService.countActiveUsers());
        
        return ResponseEntity.ok(stats);
    }
}
```

## UserDetailsService 구현

### CustomUserDetailsService
```java
@Service
public class CustomUserDetailsService implements UserDetailsService {
    
    @Autowired
    private UserRepository userRepository;
    
    @Override
    @Transactional
    public UserDetails loadUserByUsername(String username) throws UsernameNotFoundException {
        User user = userRepository.findByUsername(username)
            .orElseThrow(() -> new UsernameNotFoundException("사용자를 찾을 수 없습니다: " + username));
        
        return UserPrincipal.create(user);
    }
}

public class UserPrincipal implements UserDetails {
    private Long id;
    private String username;
    private String email;
    private String password;
    private Collection<? extends GrantedAuthority> authorities;
    
    public static UserPrincipal create(User user) {
        List<GrantedAuthority> authorities = List.of(
            new SimpleGrantedAuthority("ROLE_" + user.getRole().name())
        );
        
        return new UserPrincipal(
            user.getId(),
            user.getUsername(),
            user.getEmail(),
            user.getPassword(),
            authorities
        );
    }
    
    @Override
    public Collection<? extends GrantedAuthority> getAuthorities() {
        return authorities;
    }
    
    @Override
    public boolean isAccountNonExpired() { return true; }
    
    @Override
    public boolean isAccountNonLocked() { return true; }
    
    @Override
    public boolean isCredentialsNonExpired() { return true; }
    
    @Override
    public boolean isEnabled() { return true; }
}
```

## 보안 설정 및 CORS

### CORS 설정 (application.properties)
```properties
# CORS 설정
app.cors.allowed-origins=http://localhost:3000,https://devzip.cloud
app.cors.allowed-methods=GET,POST,PUT,DELETE,OPTIONS
app.cors.allowed-headers=*
app.cors.allow-credentials=true

# 세션 보안
server.servlet.session.cookie.secure=true
server.servlet.session.cookie.http-only=true
server.servlet.session.cookie.same-site=strict

# 로깅 설정
logging.level.org.springframework.web=DEBUG
logging.level.org.springframework.security=DEBUG
logging.level.com.hoooon22.devzip=DEBUG
```

## 결론

DevZip 프로젝트의 Spring Boot 기반 보안 시스템은 다음과 같은 특징을 갖습니다:

### 핵심 보안 원칙
- **JWT 기반 무상태 인증**: 확장 가능한 토큰 기반 인증 시스템
- **역할 기반 접근 제어**: `@PreAuthorize` 어노테이션을 활용한 메서드 레벨 보안
- **BCrypt 암호화**: 안전한 비밀번호 해싱 알고리즘 사용
- **CORS 정책**: 명시적 도메인 허용으로 XSS 공격 방지

### 기술적 구현 요소
- **Spring Security 6**: 최신 보안 프레임워크 활용
- **JPA/Hibernate**: 사용자 엔티티 영속성 관리
- **Method Security**: 세밀한 권한 제어
- **Custom UserDetailsService**: 비즈니스 요구사항에 맞는 인증 로직

### 운영 환경 고려사항
- **환경 변수 기반 설정**: 민감한 정보의 안전한 관리
- **페이지네이션 제한**: 대용량 데이터 처리 시 성능 최적화
- **상세한 로깅**: 보안 이벤트 추적 및 감사

지속적인 보안 업데이트와 모니터링을 통해 안전한 웹 분석 플랫폼을 제공합니다.