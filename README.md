# big-data-course-project

Versions:
hadoop
Spark
elasticsearch
Kibana

1. start environment:

1) Hadoop:
/Users/wesley/important/hadoop-2.9.2/sbin/start-dfs.sh
/Users/wesley/important/hadoop-2.9.2/sbin/start-yarn.sh
2) elasticsearch:
/Users/wesley/important/elasticsearch-6.5.2/bin/elasticsearch

3) kibana:
/Users/wesley/important/kibana-6.5.2-darwin-x86_64/bin/kibana


2. remove all result datas and source datas in hadoop(if exists)

hadoop fs -rm -r /finalProjectData/result
hadoop fs -rm -r /finalProjectData/tmdb_5000_movies.csv
hadoop fs -rm -r /finalProjectData/tmdb_5000_credits.csv

3. add source data to /finalProjectData/

hadoop fs -put /Users/wesley/codes/python/test/tmdb_5000_movies.csv /finalProjectData/
hadoop fs -put /Users/wesley/codes/python/test/tmdb_5000_credits.csv /finalProjectData/

4. run main_data_processor in spark local to get cast_impresssion_data

/Users/wesley/important/spark-2.4.0-bin-hadoop2.7/bin/spark-submit --master local[2] --name spark-local /Users/wesley/codes/bigdatafinal/data_process/main_data_processor.py

5. run write_to_es to write cast_impresssion_data to es

/Users/wesley/important/spark-2.4.0-bin-hadoop2.7/bin/spark-submit --master local[2] --jars elasticsearch-spark-20_2.11-6.5.2.jar /Users/wesley/codes/bigdatafinal/data_process/write_to_es.py

6. open http://0.0.0.0:5601 to check data



some useful command
hadoop fs -ls /finalProjectData/
hadoop fs -get /finalProjectData/result/data_impression.csv /Users/wesley/codes/python/test/
