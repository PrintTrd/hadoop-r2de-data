# Special Live : All you need to know about Hadoop

This repository is made for contributing Road to Data Engineer Special Live

## Installation

Host VM for Hadoop on GCP's ssh terminal and setup docker container for use as client
```
 docker container ls
 docker exec -it {CONTAINER ID} /bin/bash #เข้าไปใน container เพื่อรันคำสั่ง
```
Then use Cloudera Manager (Distributer for Hadoop's services packing) -> {EXTERNAL IP}:{PORT}

## Usage

According to the session, a starter packs for starting Hadoop project is avialable within /data.
```
 hadoop fs -cat hdfs:/<directory>/<file> #เรียกดูเนื้อหาในไฟล์
 hadoop fs -put <local_file> hdfs:/<directory>/<file> #อัพโหลดไฟล์ไปที่ hdfs
 hadoop fs -get  hdfs:/<directory>/<file> <local_file> #ดาวน์โหลดไฟล์จาก hdfs
 hadoop fs -cp  hdfs:/<directory>/<file_1> hdfs:/<directory>/<file_1_copy> #คัดลอกไฟล์
 hadoop fs -ls hdfs:/<directory>/ #เรียกดู list of files ใน directory
 hadoop fs -mv  hdfs:/<directory>/<file_1> hdfs:/<directory>/<file_2> #เปลี่ยนชื่อ/ย้ายไฟล์
 hadoop fs -rm  hdfs:/<directory>/<file_1> #ลบไฟล์
 hadoop fs -chown cloudera:cloudera #เปลี่ยนเจ้าของไฟล์
 hadoop fs -chmod 777 hdfs:/<directory>/<file> #กําหนดสิทธิ์ของไฟล์เป็น -rwxrwxrwx
```
1. Upload file
```
 cd /data/file/source
 hadoop fs -mkdir /tmp/file/sink
 hadoop fs -put /data/file/source/customer.csv /tmp/file/sink
```
2. Prepare folders in flume
```
 cd /data/flume/source
 mkdir hbase #Local storages
 mkdir hdfs #Local storages
 hadoop fs -mkdir /tmp/flume/sink #Hadoop storage
```
3. Linked with Cloudera table
```
  hbase shell
> list
> create 'spooled_table', 'spool_cf'
> exiit
```
4. Connect realtime jobs with hdfs and hbase
```
 nohup flume-ng agent -n tier1 -f /data/flume/source/flume_hdfs.conf &
 nohup flume-ng agent -n tier2 -f /data/flume/source/flume_hbase.conf &
 nohup sh /data/flume/src_sys.sh &
 jobs -l #Check job list
 cd hdfs
 ls -lrt #To see text logs
```
(Note) Read file
```
vi /data/flume/src_sys.sh
~ (esc)
:q (quit only) / :wq (save and quit)
```
