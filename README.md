# Master-s-Degree-project
For Master's Degree Project I worked on machine learning on the edge.
Use case of project was to achieve real-time demography analytics using computer vision on Nvidia Jetson TX2 device.

The project is described in more details in the presentation and whitepaper which are provided in this repo.

## Arhitecture 

System contains three submodules:
 1. Machine learning on the edge on Jetson
 2. Real-time analytics submodule on central server
 3. MLOps submodule

![alt text](https://github.com/DusanBucan/Master-s-Degree-project/blob/main/ML%40Edge%20using%20Jetson%20device.png)



## First submodule was implemented using Python programing language and

OpenCV, TensorFlow, Kafka-producer.
Input of first submodules is image from Jetson camera. 
People detection is implemented using YOLOv5 model.
Gender prediction is implemented using mtCNN for face detection and
custom CNN for gender classification based on detected face on image.

People detection and gender classification informations are wrapped in 
massages and sent to Kafka message broker on central server.

During development code-style was validated using flake8, mypy.



## Second submodule performs real-time analytics on Kafka stream data.

All components of this submodule are run as Docker containers.
I have tried Kafka Connect, Spark, Flink stream processing tools, and
decided to use Flink.

Stream processing application reads messages from Kafka message broker
and calculates average people count and average men/women
count in one minute time window. Stream processing application writes processed data to
output topics. From output topics Kafka Connect reads messages and makes 
records in PostgreSQL database. Apache Superset visualizes data written in PostgreSQL database.



## MLOps submodule implements model versioning using MLFlow tool.

TensorFlow container is used for model training.
Training metrics are saved inside PostgreSQL using MLFlow server and
trained models are saved in MinIO object storage.

