Atomics реализуют "Compare and Set operation".
Ex:
```private volatile long value;

public final long get() {
    return value;
}

public final long getAndAdd(long delta) {
    while (true) {
        long current = get();
        long next = current + delta;
        if (compareAndSet(current, next))
            return current;
    }
}
``` 

Метод compareAndSet представляет из себя механизм оптимистичной блокировки и позволяет изменить значение value, только если оно равно ожидаемому значению (т.е. current).

Если же значение value было изменено в другом потоке, то оно не будет равно ожидаемому значению. Следовательно метод compareAndSet вернет значение false, что приведет к новой итерации цикла while в методе getAndAdd. Т.е. новое значение value будет перезачитано в переменную current, после чего будет произведено сложение и новая попытка записи получившегося значения (т.е. next).
