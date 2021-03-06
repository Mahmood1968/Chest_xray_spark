# Chest_xray_spark
This project is design to Diagnose Thoracic Pathology from Chest X-rays with mutiple label written in Spark
Summary
In this notebook, the transfer learning is utilized to predict common Thorax Disease Categories in chest X-ray which is freely available by NIH(National Institutes of Health). Download the dataset by click here. The dataset contains 112120 images in gray scale format which 1024 by 1024. There are 15 different classes and there is apossibility of 14 different diseases to be appeared in all ChestXray images. These kind of images make the problem as multi-class and multi-label. The class labels are NLP(Natural Language Processing) extracted with 90% labelling accuracy. The size of the dataset is around 42GB which made it as a big data with multiple classes and multiple labels.

We have utilized different pre-trained models such as Resnet-50, Densenet-161, Inception-V1 and VGG-16. The chosen pre-trained model is trained from scratch in order to get the fine features of images. The first layer was replaced by 224 by 224 by 3 and the last layer was replaced with fully connected layer with 14 classes. Because of this multiple class and multiple labels problem the activation function is set to be sigmoid and the loss function is binary cross entropy. Due to overfitting, we have used dropout and added L1 and L2 regularization to the output layer.

Environment
Python 2.7 or higher
JDK 8
Apache Spark 2.1.1
Jupyter Notebook 4.1 or spark submit using CLI(Command Line Interface).
BigDL 0.7.0
Analytics zoo 0.4.0
Hardware Infrastructure
Hadoop cluster with at least 4 nodes with driver memory 170GB and executor memory is 170GB.
Download and Install Analytics Zoo and BigDL
Follow the instruction given in here to install and configure BigDL and for analytics zoo follow this link.

Run jupyter Notebook
Run export SPARK_HOME = the root directory of Spark. (Ex: /opt/cloudera/parcels/SPARK2-2.1.0.cloudera2-1.cdh5.7.0.p0.171658/lib/spark2)
Run export ANALYTICS_ZOO_HOME=the folder where you extract the downloaded Analytics Zoo zip package. (Ex: /usr/lib/zoo)
Run the following bash command to start the jupyter notebook. Change parameter settings as you need,
$ANALYTICS_ZOO_HOME/bin/jupyter-with-zoo.sh  \
    --master yarn \
    --num-executors 4 \
    --executor-cores 16 \
    --driver-memory 170g \
    --executor-memory 170g 
Run spark-submit
Run export SPARK_HOME = the root directory of Spark. (Ex: /opt/cloudera/parcels/SPARK2-2.1.0.cloudera2-1.cdh5.7.0.p0.171658/lib/spark2)
Run export ANALYTICS_ZOO_HOME=the folder where you extract the downloaded Analytics Zoo zip package. (Ex: /usr/lib/zoo)
Run the following spark-submit command. Change parameter settings as you need,
$ANALYTICS_ZOO_HOME/bin/spark-submit-with-zoo.sh \
    --master yarn \
    --deploy-mode cluster \
    --num-executors 4 \
    --executor-cores 8 \
    --driver-memory 300g \
    --executor-memory 300g \
    path/to/python_file.py \
    batch_size \
    num_epochs \
    path/to/pretrained model file \
    path/to/dataset \ 
    path/to/save the model
