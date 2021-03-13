# the-met-collection
🖼️ An implementation of Apache Hadoop to count the unique objects in every curatorial department of The Met collection

### Overview
This project uses the Hadoop MapReduce framework along with the [Hadoop BigQuery Connector](https://github.com/GoogleCloudDataproc/hadoop-connectors) to count the number of unique exhibit types in every deparment of The MET collection. The data are sourced from the Objects table in [The Met Public Domain Art Works dataset](https://console.cloud.google.com/marketplace/product/the-metropolitan-museum-of-art/the-met-public-domain-art-works) that is hosted in Google BigQuery.

### Maven Project Directory 
This project was built around Apache Maven to manage the Java app dependencies. The `pom.xml` file is a configuration file that contains the information required to build the package dependencies (in this case the Hadoop and BigQuery clients), as well as relocate some of the packages. Keep in mind, the version of the Hadoop client declared in the pom.xml file must be identical to the one run by your cluster. If in doubt, run `$ Hadoop version` from the command line of your instance to identify the hadoop version.

    .
    ├── pom.xml
    ├── src                   
        ├── main
            ├── java
                ├── met_objects
                    ├── CountArtObjects.java
 
