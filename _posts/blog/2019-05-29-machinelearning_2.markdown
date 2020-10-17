---
layout: post
title:  "Machine Learning (part 2)"
date:   2019-05-29
categories:  machine learning


---


## Machine learning algorithm categorization

The goal of using a machine learning algorithm is to uncover patterns and to use the machine to automate tasks that conventional algorithms hardly can handle. Here are some of the things a machine learning algorithm can help you achieve: 

* categorization/classification 
* prediction
* clustering

Machine learning is broadly categorized into two main categories: supervised learning and unsupervised learning. 



### Supervised learning

Supervised learning means you feed labeled/pre-categorized data into the learning algorithm to "teach" the machine the pattern so it can learn from the labeled examples. The classic examples of supervised learning include email spam detection,hand-written postal code recognition and traditional regression prediction.

Typical steps of using a supervised learning algorithm involve the following:

 1.Separate your existing data into two sets: training dataset and testing dataset. The training dataset is used to to feed into the learning algorithm to "train" to the algorithm to recognize the pattern. The testing dataset is the data that is intentionally being "on-hold" and NOT going to be feeding into the algorithm for training. 

 2.Feed the training dataset into the learning algorithm to train the algorithm to recognize the pattern. The training dataset defines the parameters of the  learning algorithm. 

 3.Now run the testing dataset that you have intentionally put on hold in step 1 on the "trained" algorithm you get from step 2 and compare the results you get from the algorithm with the original labels to see how the algorithm performs. If the  accuracy is good, it means your learning algorithm is doing a good job and ready to use. If not, you need to fine-tune the algorithm and do something different to fix it.  

For example, suppose you are using a supervised learning algorithm to label email spam. First you get a bunch of emails and manually label them one by one as spam or not. You then randomly segment your emails into training dataset and testing dataset. The typical practice is you put 80% of your data as the training dataset and keep 20% as the testing dataset. Then you use a learning algorithm called [naive bayes](https://en.wikipedia.org/wiki/Naive_Bayes_spam_filtering) to train the algorithm with the training dataset. After you have trained the algorithm with your training set, you then run the testing dataset through the trained algorithm and see how accurate the algorithm performs.



### Unsupervised learning

Unsupervised learning does not involve pre-labeled data. Generally speaking, unsupervised learning is much harder than supervised learning. A typical use case of unsupervised learning is clustering. In a clustering use case, you feed some data with no pre-defined labels into the algorithm, then let the algorithm try to group the data into "clusters" so data with similar properties are grouped under the same cluster. One example of the most common clustering learning algorithm is called [K-means](https://en.wikipedia.org/wiki/K-means_clustering).

Another example of unsupervised learning algorithm is neural network, which is closely related to the topic on deep learning, which I will discuss in the next post.Deep learning is the fastest growing field right now that is driving the magnificent progress in machine learning.



