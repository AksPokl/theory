Внедрение зависимости (Dependency injection, DI) — процесс предоставления внешней зависимости программному компоненту. 

Термин Bean в Spring используется для ссылки на любой компонент, управляемый контейнером.

@Component Preferable for component scanning and automatic wiring.
@Bean annotation returns an object that spring should register as bean in application context (custom declaration).

BeanDefinition – это объект, который хранит в себе информацию о бине.
При старте приложения, в IoC контейнер попадут бины, которые имеют scope Singleton (устанавливается по-умолчанию), остальные же создаются, тогда когда они нужны (prototype, request, session).

BeanPostProcessor:
- postProcessorBeforeInitialization(Object bean, String beanName);
- postProcessorAfterInitialization(Object bean, String beanName);

Между вызовами методов postProcessorBeforeInitialization и postProcessorAfterInitialization происходит вызов init-метода, если он есть.

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

