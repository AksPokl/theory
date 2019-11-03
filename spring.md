IoC - набор рекомендаций для написания слабо связанного кода 

Внедрение зависимости (Dependency injection, DI) — прямая реализация IoC, процесс предоставления внешней зависимости программному компоненту. 

ApplicationContext — реализация IOC спрингом (AOP, BeanPostProcessor auto registration)

Bean Factory — это базовая версия IOC контейнера

Термин Bean в Spring используется для ссылки на любой компонент, управляемый контейнером.

ApplicationContext - это главный интерфейс в Spring-приложении, который предоставляет информацию о конфигурации приложения. Он доступен только для чтения во время выполнения, но может быть перезагружен при необходимости и поддержке приложением. 

@Bean используется в конфигурационных классах Spring. Он используется для непосредственного создания бина.

@Component используется со всеми классами, которыми должен управлять Spring. Когда Spring видит класс с @Component, Spring определяет этот класс как кандидата для создания bean.

В @ComponentScan вы указываете пакеты, которые должны сканироваться. Spring будет искать бины не только в пакетах для сканирования, но и в их подпакетах.

BeanDefinition – это объект, который хранит в себе информацию о бине.

При старте приложения, в IoC контейнер попадут бины, которые имеют scope Singleton (устанавливается по-умолчанию), остальные же создаются, тогда когда они нужны (prototype, request, session).

BeanPostProcessor:
- postProcessorBeforeInitialization(Object bean, String beanName);
- postProcessorAfterInitialization(Object bean, String beanName);

BeanPostProcessor gives you a way to do some operations before creating the spring bean and immediately after creating the spring bean.

Между вызовами методов postProcessorBeforeInitialization и postProcessorAfterInitialization происходит вызов init-метода, если он есть.

Жизненный цикл бина:
- Instantiate Spring создает экземпляр компонента.
- populate propeties  Spring внедряет значения и ссылки на компоненты в свойства данного компонента.
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

