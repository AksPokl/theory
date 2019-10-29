Внедрение зависимости (Dependency injection, DI) — процесс предоставления внешней зависимости программному компоненту. 

Термин Bean в Spring используется для ссылки на любой компонент, управляемый контейнером.

ApplicationContext - это главный интерфейс в Spring-приложении, который предоставляет информацию о конфигурации приложения. Он доступен только для чтения во время выполнения, но может быть перезагружен при необходимости и поддержке приложением. 

@Component Preferable for component scanning and automatic wiring.
@Bean annotation returns an object that spring should register as bean in application context (custom declaration).

BeanDefinition – это объект, который хранит в себе информацию о бине.
При старте приложения, в IoC контейнер попадут бины, которые имеют scope Singleton (устанавливается по-умолчанию), остальные же создаются, тогда когда они нужны (prototype, request, session).

BeanPostProcessor:
- postProcessorBeforeInitialization(Object bean, String beanName);
- postProcessorAfterInitialization(Object bean, String beanName);

BeanPostProcessor gives you a way to do some operations before creating the spring bean and immediately after creating the spring bean.

Между вызовами методов postProcessorBeforeInitialization и postProcessorAfterInitialization происходит вызов init-метода, если он есть.

Жизненный цикл бина:
- Instantiate
- populate propeties
- setBeanName if BeanNameAware implemented
- setBeanFactory if BeanFactoryAwere implemented
- pre-initialization BeanPostProcessor
- after properties set
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

