
# MyBank Kafka ETL Pipeline Demo

## 1) To run the docker images
  * cd docker/
  * docker-compose up  

This will spin up kafka, zookeeper , kafka connect, ksqldb, schema registry and the source and target dbs. Kafka Connect JDBC connector and Avro Converter are included and added to the Debezium Kafka Connect Image.

## 2) Setting up the Source DB
* docker exec -it bank_source_db psql -U postgres
* alter system set wal_level to 'logical';  (restart bank_source_db container after this)
* CREATE TABLE INSURANCE_PAYMENTS (
	payment_id SERIAL PRIMARY KEY,
	notes text,
	total FLOAT,
	beneficiary_id INTEGER,
	insurance_id INTEGER,
	insurance_type INTEGER	);

## 3) Check the postman collection 

**MyBank Kafka Cluster Connect Setup.postman_collection.json**  
This collection contains examples of source, sink , KSQLDB Stream and Table based on this setup. 

Alternatively a GUI like Conduktor can be used to create the components of the streaming.
https://docs.conduktor.io/desktop/conduktor-first-steps/install/
