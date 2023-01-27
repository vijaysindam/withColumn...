# withColumn...

package pack

import org.apache.spark._
import org.apache.spark.sql._
import org.apache.spark.sql.functions._
import org.apache.spark.sql.types._
import org.apache.spark.sql.Row
import org.apache.spark.SparkConf
import org.apache.spark.sql.SparkSession


object obj {
  
  def main(args:Array[String]) : Unit = {
    
    val conf = new SparkConf().setAppName("ES").setMaster("local[*]")
    val sc = new SparkContext(conf)
    sc.setLogLevel("ERROR")
    val spark = SparkSession.builder().getOrCreate()
    import spark.implicits._
    
    
    val df = spark.read.format("csv").option("header","true")
    .load("file:///c:/data/dt.txt")
  
  df.show()
  
  val fdf = df.withColumn("tdate",expr("split (tdate,'-')[2]"))
              .withColumnRenamed("tdate", "year")
              .withColumn("status",expr("case when spendby = 'cash' then 1 else 0 end"))
  
  
  
  fdf.show()

  
  
  
  
  
  
  }
  
    
    
    
    
    
    
    
    
    
    

  
  
  
  
  
  
}
