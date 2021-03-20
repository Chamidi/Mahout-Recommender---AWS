# Mahout-Recommender-AWS
Building a Recommender with Apache Mahout on Amazon Elastic MapReduce (EMR)

**Step 1 : Building up the data set**
```
wget http://files.grouplens.org/datasets/movielens/ml-1m.zip
unzip ml-1m.zip
cat ml-1m/ratings.dat | sed 's/::/,/g' | cut -f1-3 -d, > ratings.csv
```
**Step 2 : Inserting data set to HDFS**

```
hadoop fs -put ratings.csv /ratings.csv
```

**Step 3 : Running the mahout recommender job**

```
mahout recommenditembased --input /ratings.csv --output recommendations --numRecommendations 10 --outputPathForSimilarityMatrix similarity-matrix --similarityClassname SIMILARITY_COSINE

```
**Step 4 : View the results in terminal**

```
 hadoop fs -ls recommendations
 hadoop fs -cat recommendations/part-r-00000 | head
 ```
 **Step 5 : Install required python packages**
 ```
 sudo pip3 install twisted klein redis
 ```
 
**Step 6 : Running Redis Server**
```
wget http://download.redis.io/releases/redis-2.8.7.tar.gz
tar xzf redis-2.8.7.tar.gz
cd redis-2.8.7
make
./src/redis-server &

```

**Step 7 : Creating the web service ( hello.py) and Startting the web server**

```
twistd -noy hello.py &
```
**Step 8 : Testing**

```
curl localhost:8090/37
```

```ruby
Terminate all aws services once the work is over 
```


