Docker — это платформа, которая предназначена для разработки, развёртывания и запуска приложений в контейнерах.

Преимущества использования Docker:
- Минимальное потребление ресурсов — контейнеры не виртуализируют всю операционную систему (ОС), а используют ядро хоста и изолируют программу на уровне процесса. 
Последний потребляет намного меньше ресурсов локального компьютера, чем виртуальная машина.
- Скоростное развертывание — вспомогательные компоненты можно не устанавливать, а использовать уже готовые docker-образы (шаблоны). 
- Удобное скрытие процессов — для каждого контейнера можно использовать разные методы обработки данных, скрывая фоновые процессы.
- Работа с небезопасным кодом — технология изоляции контейнеров позволяет запускать любой код без вреда для ОС.
- Простое масштабирование — любой проект можно расширить, внедрив новые контейнеры.
- Удобный запуск — приложение, находящееся внутри контейнера, можно запустить на любом docker-хосте.
- Оптимизация файловой системы — образ состоит из слоев, которые позволяют очень эффективно использовать файловую систему.

Docker Engine («Движок» Docker) — ядро механизма Докера. «Движок» отвечает за функционирование и обеспечение связи между основными Docker-объектами (реестром, образами и контейнерами).

Компоненты Docker:
- Docker-демон (Docker-daemon) — сервер контейнеров, входящий в состав программных средств Docker. Демон управляет Docker-объектами (сети, хранилища, образы и контейнеры). 
Демон также может связываться с другими демонами для управления сервисами Docker.
- Docker-клиент (Docker-client / CLI) — интерфейс взаимодействия пользователя с Docker-демоном. Клиент и Демон — важнейшие компоненты «движка» Докера (Docker Engine). 
Клиент Docker может взаимодействовать с несколькими демонами.
- Docker-образ (Docker-image) — файл, включающий зависимости, сведения, конфигурацию для дальнейшего развертывания и инициализации контейнера.
- Docker-файл (Docker-file) — описание правил по сборке образа, в котором первая строка указывает на базовый образ.
Последующие команды выполняют копирование файлов и установку программ для создания определенной среды для разработки.
- Docker-контейнер (Docker-container) — это легкий, автономный исполняемый пакет программного обеспечения, который включает в себя все необходимое для запуска приложения: 
код, среду выполнения, системные инструменты, системные библиотеки и настройки.
- Том (Volume) — эмуляция файловой системы для осуществления операций чтения и записи. 
Она создается автоматически с контейнером, поскольку некоторые приложения осуществляют сохранение данных.
- Реестр (Docker-registry) — зарезервированный сервер, используемый для хранения docker-образов. 
