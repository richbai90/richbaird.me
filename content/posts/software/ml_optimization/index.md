---
title: "Optimizing Memory in Machine Learning: List vs Numpy Pre-allocation"
date: 2023-07-10T21:25:38-06:00
draft: false
menu:
  sidebar:
    name: Machine Learning Optimization
    identifier: ml_optimization
    parent: software
    weight: 10
hero: hero.jpg
---

## Introduction

In many machine learning applications, data handling is done using lists, which are then converted into numpy arrays. This practice can be memory inefficient, especially when dealing with large datasets. Below, I illustrate the problem and provide a solution using numpy pre-allocation. I will also discuss other considerations for reducing the memory footprint of machine learning applications. These considerations are especially important when dealing with large datasets.

## The Problem

Let's take an example of data pre-processing with a list:

```python
pre_processed = []
for item in my_dataset:
    process(item)
    pre_processed = pre_processed.append(item) # Creates a new object in memory

arr = np.array(pre_processed)
```
Here, we are processing the data and storing it in a Python list. After processing the entire dataset, we convert the list into a numpy array. This approach is problematic because it requires twice the memory: once for the list and then again for the array. Furthermore, if the list never goes out of scope, the memory is never freed, leading to massive wastes of memory when dealing with large datasets.

## The Solution
A more efficient approach is to pre-allocate a numpy array and fill it directly during processing. Below is a simplified example of this.

```python
# Preallocate a numpy array
data_dim = 3 # Let's assume our data has 3 dimensions (features)
pre_processed = np.zeros((len(my_dataset), data_dim))

for idx, item in enumerate(my_dataset):
    process(item) # Do any processing here
    pre_processed[idx] = item # In place modification of the numpy array
```
In this revised code, we allocate a numpy array with a shape that matches our expected output before processing the data. Then, during processing, we directly update the numpy array with the processed data in place. In place means that a new object is not created as is the case with the concat method. This eliminates the need for the intermediate Python list and therefore, significantly reduces the memory footprint.

Numpy arrays have the added advantage of being stored contiguously in memory which allows for efficient in-place modifications and eliminates the large overhead associated with Python lists.

## Other Considerations
In addition to pre-allocating the numpy array, there are other ways to reduce the memory footprint of the array.
Here are a few other considerations depending on the application.

### Data Types
By default, python treats all numerical values as float64, which requires 8 bytes of memory per number. It may be bennefitical to specify the data type of the array if we know that our value will require less precision. This can be done by passing the `dtype` argument to the `np.zeros` function. For example, if we know that our data will be integers, we can specify `dtype=np.int32`. This will further reduce the memory footprint of the array by using the smallest data type that can represent our data.

### Scope
Programming languages like python will hold onto all the data it cannot guarantee will not be used again. This means that if we have a variable that is not explicitly deleted, it will remain in memory. This is especially problematic when dealing with large datasets. To avoid this, it is best practice to contain the data processing in a function. This way, the data will be freed from memory once the function returns. If this is not possible, we can explicitly delete the variable using the `del` keyword. For example, we can delete the `pre_processed` variable from the previous example by adding `del pre_processed` after the `arr = np.array(pre_processed)` line.

### Chunking
Sometimes datasets may be too large to hold contiguously in memory. In these cases, we can process the data in chunks. This can be done by reading the data in chunks and processing each chunk individually. Then, we can write the processed data to disk and repeat the process for the next chunk. This approach is especially useful when dealing with large datasets that cannot fit in memory.
<br>
<br>
<pre><small><a href="https://www.vecteezy.com/free-vector/artificial-intelligence">Artificial Intelligence Vectors by Vecteezy</a></small></pre>