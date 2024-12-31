# Adults-Income
Analyze Adult income dataset using Map Reduce Framework

# Hadoop Distributed File System
[cloudera@quickstart ~]$ hdfs dfs -ls /![image](https://github.com/user-attachments/assets/2c14a6c3-9a3e-4097-8bf1-8f8b90a69729)

[cloudera@quickstart ~]$ hdfs dfs -mkdir /adult![image](https://github.com/user-attachments/assets/200d39b9-c83f-4953-8c0a-4ad067ff8c83)

hdfs dfs -put /home/cloudera/Downloads/ADULT.csv/adult![image](https://github.com/user-attachments/assets/19364286-6a61-4b73-8bc2-279178686dd3)

[cloudera@quickstart ~]$ hdfs dfs -cat /adult/ ADULT.csv![image](https://github.com/user-attachments/assets/d37d7bff-c0a3-4054-ba89-ed97928c9dc5)

hadoop jar project.jar income.adultincome /adult/ADULT.csv /output90![image](https://github.com/user-attachments/assets/6907c75c-e6e6-404d-b066-4a12c9f337d5)

hadoop fs -cat /output90/part-r-00000![image](https://github.com/user-attachments/assets/61856831-75a3-4b89-80bf-b3fa70eb19a0)
