IoC - набор рекомендаций для написания слабо связанного кода 

Внедрение зависимости (Dependency injection, DI) — прямая реализация IoC, процесс предоставления внешней зависимости программному компоненту. 
- DI через конструктор считается самым лучшим способом, т.к. для него не надо использовать рефлексию.
- DI через поле не рекомендуется использовать, т.к. для этого применяется рефлексия, снижающая производительность.
- DI через конструктор может приводить к циклическим зависимостям. Чтобы этого избежать, можно использовать ленивую инициализацию бинов или DI через сеттер.


ApplicationContext — реализация IOC спрингом (AOP, BeanPostProcessor auto registration), главный интерфейс в Spring-приложении, который предоставляет информацию о конфигурации приложения. Он доступен только для чтения во время выполнения, но может быть перезагружен при необходимости и поддержке приложением. 

Bean Factory — это базовая версия IOC контейнера, это пул объектов, где они создаются и управляются конфигурацией. 

Термин Bean в Spring используется для ссылки на любой компонент, управляемый контейнером.

@Bean используется в конфигурационных классах Spring. Он используется для непосредственного создания бина.

@Component используется со всеми классами, которыми должен управлять Spring. Когда Spring видит класс с @Component, Spring определяет этот класс как кандидата для создания bean.

В @ComponentScan вы указываете пакеты, которые должны сканироваться. Spring будет искать бины не только в пакетах для сканирования, но и в их подпакетах. В java -> @ComponentScan @Configuration и пустой класс. 

BeanDefinition – это объект, который хранит в себе информацию о бине.

При старте приложения, в IoC контейнер попадут бины, которые имеют scope Singleton (устанавливается по-умолчанию), остальные же создаются, тогда когда они нужны (prototype, request, session).

BeanPostProcessor:
- postProcessorBeforeInitialization(Object bean, String beanName);
- postProcessorAfterInitialization(Object bean, String beanName);

BeanPostProcessor gives you a way to do some operations before creating the spring bean and immediately after creating the spring bean.
(на данном этапе экземпляр бина уже создан и идет его донастройка)

BeanFactoryPostProcessor работает над описаниями бинов или конфигурационными метаданными перед тем, как бин будет создан.

Жизненный цикл бина:
- Instantiate (Spring создает экземпляр компонента).
- populate propeties  Spring внедряет зависимости
- setBeanName if BeanNameAware implemented
- setBeanFactory if BeanFactoryAwere implemented
- setApplicationContext if ApplicationContextAware implemented 
- pre-initialization BeanPostProcessor
- after properties set after all bean properties have been set.
- custom init-method
- post-initialization BeanPostProcessor

Существует четыре вида связывания в спринг:
- autowire byName,
- autowire byType,
- autowire by constructor,
- autowiring by @Autowired and @Qualifier annotations

Interceptor:
- preHandle
- postHandle
- afterCompletion (после того как ответ сформирован)

Как закрыть applicationContext:
- зарегестрировать shutdownHook через AbstractApplicationContext
- вызвать метод close через AbstractApplicationContext
- Web: через ConextLoaderListener 

@RestController объединяет в себе аннотации @Controller и @ResponseBody

Если у бина скоуп прототайп и он вызывается из синглтона - будет возвращен тот же объект
Если у бина скоуп синглтон и он вызывается из прототайпа - будет возвращен тот же объект

Когда вы вызываете метод без @Transactional внутри блока транзакции, родительская транзакция будет продолжать новый метод.

Когда spring bean получается из контекста приложения, он будет прокси bean (не оригинальным bean)
Прокси не перехватывает вызовы внутри объекта - перехватывает вызовы объекта из других объектов. 
Т.е если вызвать метод внутри которого метод, который помечен @Transactional -> вызов метода -  создание proxy - прокси не перехватывает вызовы внутри объекта - метод не транзакционный
Как обойти?
в методе достать бин из контекста - и на нем вызвать транзакционный метод

Если в траназкционном методе вызвать другой траназкционный метод:
В связи с тем, что для поддержки транзакций через аннотации используется Spring AOP, в момент вызова method1() на самом деле вызывается метод прокси объекта. Создается новая транзакция и далее происходит вызов method1() класса MyServiceImpl. А когда из method1() вызовем method2(), обращения к прокси нет, вызывается уже сразу метод нашего класса и, соответственно, никаких новых транзакций создаваться не будет

Прокси это специальный объект, который имеет такие же публичные методы как и бин, но у которого есть дополнительная функциональность. 
Два вида прокси:
- JDK-proxy — динамическое прокси. API встроены в JDK. Для него необходим интерфейс
- CGLib proxy — не встроен в JDK. Используется когда интерфейс объекта недоступен


