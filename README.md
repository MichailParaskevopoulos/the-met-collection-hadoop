# The MET Collection
🖼️ An implementation of Apache Hadoop to count the unique objects in every curatorial department of The Met collection using tools available on the Google Cloud Platform.

### Overview
This project executes a MapReduce job with the [Hadoop BigQuery Connector](https://github.com/GoogleCloudDataproc/hadoop-connectors) to count the number of unique exhibit types in every deparment of The MET collection. The data are sourced from the Objects table in [The Met Public Domain Art Works dataset](https://console.cloud.google.com/marketplace/product/the-metropolitan-museum-of-art/the-met-public-domain-art-works) that is hosted on Google BigQuery.

### Maven Project Directory 
This project was built around Apache Maven to manage the Java app dependencies. The `pom.xml` file is a configuration file that contains the information required to build the package dependencies (in this case the Hadoop and BigQuery clients), as well as relocate some of the packages. Keep in mind, the version of the Hadoop client declared in the `pom.xml` file should match the one run by your cluster. If in doubt, run `$ Hadoop version` from the command line of your instance (or Dataproc Cluster if you are using GCP) to identify the hadoop version. Finally, you can check the latest version of your dependencies at the [Maven Central Repository](https://search.maven.org/).

    .
    ├── pom.xml                                    # Configuration file for Apache Maven
    ├── src                   
    ├    ├── main
    ├        ├── java
    ├            ├── met_objects                   # Main package name
    ├                ├── CountArtObjects.java      # Java project source code 
    ├── target
         ├── met-object-count-0.0.1.jar            # JAR file 
                    
### Running Hadoop Jobs on Google Dataproc

1. Compile the Java class files in your local machine using Maven (or another Java project management tool)
   
2. Copy the JAR file to the Cloud Storage bucket of your project:

        $ gsutil cp /home/usr/my_Maven_project/target/met-object-count-0.0.1.jar gs://${PROJECT}/hadoop_job_files

3. Create a Dataproc cluster:

        $ gcloud dataproc clusters create ${CLUSTER_NAME} \
            --worker-machine-type n1-standard-4 \
            --num-workers 0 \
            --image-version 2.0.5-debian10 \
            --region ${REGION} \
            --max-idle=30m 

4. Submit a Hadoop job to the Dataproc cluster:

        $ gcloud dataproc jobs submit hadoop \
            --jar gs://${PROJECT}/hadoop_job_files/met-object-count-0.0.1.jar \
            --cluster ${CLUSTER_NAME} \
             

