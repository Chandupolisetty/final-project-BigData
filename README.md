# final-project-BigData

Commands and a notebook about processing text data using Spark and Python.

## Author:

- [Chandrakanth Polisetty](https://github.com/Chandupolisetty)

## Resource for Text Data:

- [https://www.gutenberg.org/files/65114/65114-0.txt](https://www.gutenberg.org/files/65114/65114-0.txt)

## Tools and Languages:
- Databricks Cloud Environment.
- Spark Processing Engine.
- PySpark.
- Python Programming Language.


## Commands used:

- The import urllib.request library is used to import the data directly form the URL.


```
import urllib.request
stringInURL = "https://www.gutenberg.org/files/6130/6130-0.txt"
urllib.request.urlretrieve(stringInURL, "/tmp/finaProject_data.txt")
```

```
dbutils.fs.mv("file:/tmp/finaProject_data.txt", "dbfs:/data/finaProject_data.txt")
```

```
final_RDD = sc.textFile("dbfs:/data/finaProject_data.txt")
```
```
textRDD = final_RDD.flatMap(lambda line : line.lower().strip().split(" "))
```
```
Final_word_count_RDD = IKVPairsRDD.reduceByKey(lambda acc, value: acc+value)
```
```
final_results = Final_word_count_RDD.map(lambda x: (x[1], x[0])).sortByKey(False).take(25)
print(final_results)
```
```
results = Final_word_count_RDD.collect()
print(results)
```
## Charting the results:

- We use pandas, matplotlib seaborn to chart the results.

```
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns
from collections import Counter
 
source = 'The Project Gutenberg eBook of The Wonders of Optics, by Fulgence Marion'
title = 'Top Words in ' + source
xlabel = 'Count'
ylabel = 'Words'
 
# create Pandas dataframe from list of tuples
df = pd.DataFrame.from_records(results, columns =[xlabel, ylabel]) 
print(df)
 
# create plot (using matplotlib)
plt.figure(figsize=(10,3))
sns.barplot(xlabel, ylabel, data=df, palette="Paired").set_title(title)
```

