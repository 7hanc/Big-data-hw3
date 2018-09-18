# Big-data (hw3+hw4)

# Homework 3 (Spark MapReduce programming)

> Goal
* Practice Spark MapReduce programming on Hadoop platform. You may choose either one program language from Java, Scala, and Python to implement your program on Spark.
>> Dataset
* Taxi data: http://www.nyc.gov/html/tlc/html/about/trip_record_data.shtml
> Question
* Q1: Implement a MapReduce program to count occurrences of each word in the attached article (IhaveaDream.txt).
  * A: Show the top 20 most frequent occurring words and their counts.
  * B: According to the word counting result, can you summarize this article by using some keywords? Show at least three keywords you choose and the reason of choosing these words.
* Q2: Implement a MapReduce program to calculate the average number of passengers in one trip for each "Payment_type" in 2015 NYC Yellow Taxi trip data. In NYC Taxi data, the "Passenger_count" is a driver-entered value. Explain how you deal with the data loss issue.
* Q3: For each of the above task 1 and 2, compare the execution time on local worker and yarn cluster. Also, give some discussions on your observation.
***
Answer 1:   
Step1: upload txt file to hdfs.   
`hdfs dfs -put /home_il/s31tsm40/IhaveaDream.txt hw.txt`   
Step2: turn to spark environment   
`spark-shell \\ will turn to "scala>"`   
Step3: open txt file which is in hdfs   
`val textFile = sc.textFile("hw.txt")`   
Step4: use mapreduce method to count the words   
`val counts = textFile.flatMap(line => line.split(" ")).map(word => (word, 1)).reduceByKey(_+_)`   
Step5: save the result to the directory   
`counts.saveAsTextFile("output")`   
Step6: download the “output” directory to the localhost   
`hdfs dfs -get output /home_il/s31tsm40`   
![a](https://i.imgur.com/wAEGcWF.jpg])

# Homework 4 (Build a predictive framework)

> Goal
* Build a predictive framework, which is able to predict "WeatherDelay" of all flights in 2008. This work should use the data from 2003 to 2007 as training including validation and 2008 as testing.
>> Dataset
* Airline on-time performance dataset: http://stat-computing.org/dataexpo/2009/
> Question
* Q1: Explain the predictive framework you designed.
  * Feature: “Month” and “DayofMonth” 
  * Algorithms: Linear regression.
* Q2: Explain how method you use to validate your model when training.
  * Use cross-validation to validate my model 
  * The method of cross validation: K-fold   
### The answer of Q1 and Q2 -> hw4.py
* Q3: Show the evaluation results of validation in training and prediction in testing  by following those evaluation metric:
<table>
　<tr>
    <td> </td>
　  <td>average MAE</td>
    <td>average RMSE</td>
　</tr>
 <tr>
    <td>validation in training</td>
　  <td>1.612427</td>
    <td>5.016839</td>
　</tr>
 <tr>
    <td>prediction in testing</td>
　  <td>1.495521</td>
    <td>9.243812</td>
　</tr>
</table>
