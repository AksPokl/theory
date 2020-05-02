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
