Spring Security offers several options for configuring a user store, including these:
- An in-memory user store
- A JDBC-based user store
- An LDAP-backed user store 
- A custom user details service


OAuth 2.0 — протокол авторизации, позволяющий выдать одному сервису (приложению) права на доступ к ресурсам пользователя на другом сервисе.

OpenID Connect - это простой слой идентификации, созданный поверх протокола OAuth 2.0

Аутентификация - это процесс проверки учётных данных пользователя (логин/пароль). 
Авторизаци - это проверка прав пользователя на доступ к определенным ресурсам.

Spring Security использует Spring AOP proxy, которые наследуются от класса AbstractSecurityInterceptor.

SecurityContext — дефолтная реализация Spring Security содержащая объект Authentication. Он позволяет получать и устанавливать объект Authentication.

Authentication представляет следующие свойства:

Коллекцию полномочий выданных принципалу
Данные для удостоверения пользователя(логин, пароль)
Details — доп. информация, если она нужна. Может быть равно null
Принципал
Authentication flag — boolean переменная, которая показывает успешно ли прошел проверку принципал

SecurityContextHolder — содержит и предоставляет доступ к SecurityContext в приложении. 
