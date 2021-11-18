# AWS_EMR_wordCounter
Counting words from a book using AWS EMR service

## Overview
The goal of this project is to create a fully managed Hadoop ecosystem using AWS EMR service and perform a map reduce job in order to count the occurences of all the words in a book.

In order to do so, the book file will be uploaded to a S3 bucket and then processed by an EMR cluster that will be created for this purpose. After the processing, the results will be stored in the output folder of the S3 bucket. The image below ilustrates the process:
<p align="center"><img src="./overview.png" width="400"></p>

The EMR cluster will perform a map reduce job specified in the mrjob config file. The cluster will be created by the mrjob, so there's no need to configure it manually.

## Steps
* Create the S3 bucket
* Create this folder structure:
  * data/
  * temp/
  * output/
* Create SSH Key for access: 
  * https://console.aws.amazon.com/ec2/ -> Key Pairs -> Create Key Pair
  * Download .pem file
* Obtain both the aws_access_key_id and aws_secret_access_key in order to configure the mrjob:
   * My Security Credentials: https://console.aws.amazon.com/iam/home?region={region}#/security_credentials
   * Access Keys - Create new access key
   * Download the Key
* Create a python virtual environment and install the libraries from the requirements.txt
* Configure the mrjob.conf file with the needed credentials and ssh key
* Run the map reduce job:
  * python3 wordcount.py -r emr -c $PWD/mrjob.conf s3://{bucket}/data/sherlock.txt --output-dir=s3://{bucket}/output/logs1 --cloud-tmp-dir=s3://{bucket}/temp/
