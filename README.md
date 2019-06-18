1) create database into Mysql with name "jwtappdemo"


В сервисе можно юзать другой сервис. (не знаю можно ли в сервисе юзать другой дао, по сути - это неправильно, чтобы в сервисе юзать другой дао).


1) реалищовать свой JwtUserDetailsService
	имплементировать UserDetailsService (security)
	перегразить loadUserByUsername(String username) и верунть JwtUser, реализацию UserDetails

2) Создвть JwtUser реализовав UserDetails
	переопределить все методы.
	добавить поля
		id
		username
		firstname
		lastname
		password
		email
		enabled
		lastPasswordResetDate
		Collection<? extends GrantedAuthority> authorities

3)  реализовать  JwtUserFacroty для создания JwtUser
4) Создать JwtAuthenticationExeption extends authenticationException
5) Реализовать JwtTokenProvider - класс, который будет как раз таки генерить токен.
	поставить на нём аннотацию @Componet
	Добавить в класс secret-значение
	добавить в класс значение validInMilliseconds.

	написать соответствующие методы:
			createtoken(Object data)
			Authentication getAuthentication(String token)
			getUsername(String token)
			boolean validateToken(String token)
			String resolveToken(HttpServletRequest request)

6) Дбавить класс jwtTokenFilter extends GenericFilterBean
	 сделать исплементацию doFilter()

7) написать JwtConfigurer extends SecurityConfigurerAdapter<DefaultSecurityFilterChain> - класс предназначенный для того, чтобы переопределить стандартное поведение spring-security, добавив свой собственный фильтр конфигурации.
	добавить jwtTokenProvider
	переопределить метод configure(HttpSecurity httpSecurity)

8) Пишем наш SecurityConfig унаследовавшишь от WebSecurityConfigAdapter
	Ложим туда JwtTokenProvider
	переопрделям метод AuthenticationManager authenticatonManageBean()
		return super.authenticationManagerBean()
	ставим аннотацию Bean над методом
	переопределяем методо configure (HttpSecurity http)
		прописываем кастомную реализацию
			смотри реалицацию в примере.




GrantedAuthority - интерфейс, для реализации прав доступа.
SimpleGrantedAuthority - простейшая реализация интерфейса GrandesAuthority, содержит String поле 'role'





видео: https://www.youtube.com/watch?v=yRnSUDx3Y8k
пример гитхаба: https://github.com/proselytear/jwtappdemo
аналогичный пример: https://medium.com/@hantsy/protect-rest-apis-with-spring-security-and-jwt-5fbc90305cc5

Как реализуется Oath spring security:
1) реализовать authentication endpoint
2)



