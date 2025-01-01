# Adults-Income
Analyze Adult income dataset using Map Reduce Framework

# Hadoop Distributed File System
[cloudera@quickstart ~]$ hdfs dfs -ls /![image](https://github.com/user-attachments/assets/2c14a6c3-9a3e-4097-8bf1-8f8b90a69729)

[cloudera@quickstart ~]$ hdfs dfs -mkdir /adult![image](https://github.com/user-attachments/assets/200d39b9-c83f-4953-8c0a-4ad067ff8c83)

hdfs dfs -put /home/cloudera/Downloads/ADULT.csv/adult![image](https://github.com/user-attachments/assets/19364286-6a61-4b73-8bc2-279178686dd3)

[cloudera@quickstart ~]$ hdfs dfs -cat /adult/ ADULT.csv![image](https://github.com/user-attachments/assets/d37d7bff-c0a3-4054-ba89-ed97928c9dc5)

hadoop jar project.jar income.adultincome /adult/ADULT.csv /output90![image](https://github.com/user-attachments/assets/6907c75c-e6e6-404d-b066-4a12c9f337d5)

hadoop fs -cat /output90/part-r-00000![image](https://github.com/user-attachments/assets/61856831-75a3-4b89-80bf-b3fa70eb19a0)

# Eclipse java code 
package income;
import org.apache.hadoop.conf.Configuration;
import org.apache.hadoop.fs.Path;
import org.apache.hadoop.io.IntWritable;
import org.apache.hadoop.io.Text;
import org.apache.hadoop.mapreduce.Job;
import org.apache.hadoop.mapreduce.Mapper;
import org.apache.hadoop.mapreduce.Reducer;
import org.apache.hadoop.mapreduce.lib.input.FileInputFormat;
import org.apache.hadoop.mapreduce.lib.output.FileOutputFormat;
import java.io.IOException;

public class adultincome {
	
	// Mapper Class
    public static class incomemapper extends Mapper<Object, Text, Text, IntWritable> {

        private final static IntWritable one = new IntWritable(1);
        private Text country = new Text();

        public void map(Object key, Text value, Context context) throws IOException, InterruptedException {
            // Split the input line into fields
            String[] fields = value.toString().split(",");
            
            // Assuming the dataset has the following columns:
            // ProductID, ProductName, Country, Quantity, Price
            // Country is at index 2 in the split array

            if (fields.length > 2) { // Check if the line has enough fields
                country.set(fields[2].trim()); // Get the country name
                context.write(country, one); // Emit country with a count of 1
            }
        }
    }
    
 // Reducer Class
    public static class incomeReducer extends Reducer<Text, IntWritable, Text, IntWritable> {

        public void reduce(Text key, Iterable<IntWritable> values, Context context) throws IOException, InterruptedException {
            int sum = 0;
         // Sum up all the counts for a country
            for (IntWritable val : values) {
                sum += val.get();
            }

            context.write(key, new IntWritable(sum)); // Emit country and total count
        }
    }
![image](https://github.com/user-attachments/assets/39e35db6-6b53-41eb-84a4-34ccff533155)
