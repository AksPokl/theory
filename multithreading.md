
Mutex (lock) and monitor:
Mонитор – это концепция синхронизации, которая позволяет потокам иметь взаимное исключение и возможность ожидания (блокировки), пока не будет выполнено определенное состояние. У монитора также есть механизм оповещения других потоков о достижении их состояния. 
Монитор состоит из объекта блокировки (mutex, lock) и условной переменной (примитив синхронизации, обеспечивающий блокирование одного или нескольких потоков до момента поступления сигнала от другого потока о выполнении некоторого условия или до истечения максимального промежутка времени ожидания).

Each object in Java is associated with a monitor, which a thread can lock or unlock.

CopyOnWrite коллекции: - Все операции по изменению коллекции (add, set, remove) приводят к созданию новой копии внутреннего массива. Тем самым гарантируется, что при проходе итератором по коллекции не кинется ConcurrentModificationException. Следует помнить, что при копировании массива копируются только референсы (ссылки) на объекты (shallow copy), т.ч. доступ к полям элементов не thread-safe. CopyOnWrite коллекции удобно использовать, когда write операции довольно редки

ConcurrentHashMap<K, V>   — В отличие от Hashtable и блоков synhronized на HashMap, данные представлены в виде сегментов, разбитых по hash'ам ключей. В результате, для доступ к данным лочится по сегментам, а не по одному объекту. В дополнение, итераторы представляют данные на определенный срез времени и не кидают ConcurrentModificationException. 

Blocking Queues:
 - Blocking queues provide blocking put and take methods. If the queue is full, put blocks until space becomes available; if the queue is empty, take blocks until an element is available. 
 

Synchronizers:

Синхронизаторы – вспомогательные утилиты для синхронизации потоков, которые дают возможность разработчику регулировать и/или ограничивать работу потоков и предоставляют более высокий уровень абстракции, чем основные примитивы языка (мониторы).

- Semaphore. Чаще всего, семафоры необходимы, когда нужно ограничить доступ к некоторому общему ресурсу. В конструктор этого класса (Semaphore(int permits) или Semaphore(int permits, boolean fair)) обязательно передается количество потоков, которому семафор будет разрешать одновременно использовать заданный ресурс.



Executors:

- Callable<V> - Расширенный аналог интерфейса Runnable для асинхронных операций. Позволяет возвращать типизированное значение и кидать checked exception. Несмотря на то, что в этом интерфейсе отсутсвует метод run(), многие классы java.util.concurrent поддерживают его наряду с Runnable.

volatile принуждает использовать единственный экземпляр переменной, но не гарантирует атомарность. Например, операция count++ не станет атомарной просто потому что count объявлена volatile. C другой стороны class AtomicInteger предоставляет атомарный метод для выполнения таких комплексных операций атомарно, например getAndIncrement() – атомарная замена оператора инкремента, его можно использовать, чтобы атомарно увеличить текущее значение на один. Похожим образом сконструированы атомарные версии и для других типов данных.