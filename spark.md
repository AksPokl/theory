Spark
Spark – это проект Apache, который позиционируется как инструмент для «молниеносных кластерных вычислений». 

Installation:
- brew install scala
- brew install apache-spark
- spark-shell
- export SPARK_HOME=/usr/local/Cellar/apache-spark/2.4.5/libexec 
PYTHONPATH=/usr/local/Cellar/apache-spark/2.4.5/libexec/python/:$PYTHONP$

Run the program:
- ${SPARK_HOME}/bin/spark-submit --class com.spark.airport.Airports --master local target/airport-spark.jar 

Приложение Spark состоит из ведущего процесса, содержащего высокоуровневую логику Spark, и набора процессоров-исполнителей, которые могут быть разбросаны по узлам кластера. Программа Spark работает на узле драйвера и отправляет команды исполнителям. 
 RRD - resilient distributed dataset (неизменяемые распределенные коллекции объектов, хранятся в исполнителях (ведомый узел))
 
Способы создания наборов RDD:
- Путем преобразования существующего RDD
- Из обеъкта SparkContext
- Путем преобразования типа обхектов DataFrame или DataSet (созданного из SparkSession)

SparkContext - соединение между кластером Spark и одним из запущенных приложений Spark. 

Существуют два типа определяемых для наборов RDD функций:
- Действия (actions, функции, возвращающие нечто отличное от набора RDD, включая побочный эффект). Ex: collect, count, reduce, take, sample. Некоторые из этих действий плохо масштабируются, так как могут приводит к ошибкам памяти в драйвере. Лучше использовать действия take, count или reduce, передающие обратно драйверу фиксированный объем данных.
- Преобразования (transformations, функции, возвращающие другой набор)

Схема запуска Spark в распределенной системе:

<img src="https://github.com/AksPokl/theory/blob/master/images/Screen%20Shot%202020-05-02%20at%205.01.42%20PM.png" width="450"/>

Структура задания Spark:
- Задание состоит из этапов, представляющих собой шаги преобразования данных, необходимые для формирования итогового набора RDD. Каждое задание соответсвует одному действию, а действия вызываются драйверной программой приложения Spark.
- Этап состоит из набора задач, каждая из которых означает параллельное вычисление, выполняемое на исполнителе
- Одна задача не может выполняться более чем в одном исполнителе.

RDD – это распределенная коллекция данных, расположенных по нескольким узлам кластера, набор объектов Java или Scala, представляющих данные. RDD работает со структурированными и с неструктурированные данными. Также, как DataFrame и DataSet, RDD не выводит схему загруженных данных и требует от пользователя ее указания.

DataFrame – это распределенная коллекция данных в виде именованных столбцов, аналогично таблице в реляционной базе данных. DataFrame работает только со структурированными и полуструктурированными данными, организуя информацию по столбцам, как в реляционных таблицах. Это позволяет Spark управлять схемой данных.

DataSet – это расширение API DataFrame, обеспечивающее функциональность объектно-ориентированного RDD-API (строгая типизация, лямбда-функции), производительность оптимизатора запросов Catalyst и механизм хранения вне кучи. DataSet эффективно обрабатывает структурированные и неструктурированные данные, представляя их в виде строки JVM-объектов или коллекции. Для представления табличных форм используется кодировщик (encoder).

Как реализуются вычисления:
- RDD-коллекция сериализуется каждый раз, когда Spark требуется распределить данные внутри кластера или записать информацию на диск. Затраты на сериализацию отдельных объектов Java и Scala являются дорогостоящими, т.к. выполняется отправка данных и структур между узлами.
- DataFrame может сериализовать данные в хранилище вне кучи (т.е., в памяти) в двоичном формате, а затем выполнить много преобразований непосредственно в этой памяти без кучи. Это возможно из-за того, что в датафреймах Spark понимает схему данных. Благодаря инструменту Tungsten не требуется использовать сериализацию Java для кодирования данных, т.к. этот механизм явно управляет памятью и динамически генерирует байт-код для оценки выражений. Благодаря динамической генерации байт-кода с сериализованными данными можно выполнить много операций, не требуя десериализации для небольших вычислений.
- DataSet API обрабатывает преобразование между объектами JVM в табличное представление c использованием вышеупомянутого безопасного двоичного формата Tungsten. Это позволяет выполнить операцию с сериализованными данными, эффективно используя память, т.к. предоставляется доступ к индивидуальному атрибуту по требованию без десериализации всего объекта.
