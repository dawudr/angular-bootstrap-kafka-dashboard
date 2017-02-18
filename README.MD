# JSConnect Explorer

Angular 4 and Bootstrap 3 dashboard to display live status of data streams from Kafka broker


## Overview

Dashboard to display data ingestion pipeline live status for each incoming data feed.
This is a loosely coupled front-end that will sit on top of dpp-source-adapter backend data services
application. It will display live incoming and allow end-users to monitor data feeds and
build new ingestion pipelines without have write any JSON in the configuration files.

## Running the UI

1. Install npm packages.
2. Run npm start to launch the sample application.


## Configuration files

- domain.config.json - this is the list of the domain for which we can a data feed.
- conf folder - these are the properties for defining the data endpoint source, data connection adapter and sink which is the target to copy data to.


## Docker

There is a docker image to run Kafka broker on your localhost:2181.
To run install docker on your computer. Then run the following commands.

```
docker-compose up
docker-compose down
docker-compose up
docker ps
docker exec -it dppsourceadapters_kafka_1 bash
```

For storeslocation from the storeslocations.conf file create a topic…..

Then in the docker Kafka vm:
Get the port configured in Zookeeper
```
/opt/kafka/config/zooker.properties
```

Run the consumer giving topic…..
```
/opt/kafka_2.10-0.9.0.1/bin/kafka-console-consumer.sh --zookeeper localhost:2181 --topic stores
```

The JSConnect source adpaters code will need to be run to send message to the store topic. We need to write some code to send mock messages to this topic.



## Framework challenges and epics

Build using Bootstrap v3, Node v6, Angular v2.4

Do not use JQuery code.
Stick to Bootstrap style css as close as possible.


### [EPIC] Domain (High priority)

Page to show live pie charts of percentage completion for each data domain status. We should try get status from Kafka broker.
If we can't show percentage completion because data maybe a continuous real time stream we can show a spinner.

Show for each data domain listed in domain.config.json


### [EPIC] Pipelines (High priority)

Shows the pipeline job from source to sink. We show an animated progress bar between the process points if live. Buttons to start job.
Need to find out how Angular can run a command line script. (This is a Java program that start the source adapter jobs).


### [EPIC] Jobs (Low priority)

This is configure time scheduling of the job and submit this to Oozie in Cloudera.


### [EPIC] Sources  (Medium priority)

This is the pipeline designer. GUI to enable end-user to build a new domain configuration file without having to write JSON file in conf/ folder.
This will show:-
- List of Source type e.g REST api, SFTP, Database connection, JMS Queues
- List of Adapters - for read data from different file stream and data formats and compressed files.
- List of Sink - destination to copy the data to e.g Amazon S3 or Kafka broker

Users can select with drop down to build end to end pipeline and that will generate a new .conf file and add an entry to the domain.config.json file.


### [EPIC] Settings  (Medium priority)

This lists configuration files paths because the /conf folder maybe be installed on another path on the linux server environments.
Any other settings here?


### [OTHER]
Any fantastics ideas?

See:-
http://webapplayers.com/inspinia_admin-v2.7/graph_flot.html
http://wrapbootstrap.com/preview/WB0R5L90S


## [LIBRARIES and USEFUL Links]
- KAFKA - https://github.com/confluentinc/kafka-rest-node
- OOZIE - https://oozie.apache.org/docs/4.0.0/WebServicesAPI.html#Job_Information
- Execute command line program from Javascript - http://stackoverflow.com/questions/1880198/how-to-execute-shell-command-in-javascript and https://nodejs.org/api/child_process.html
- Angular Tutorial - https://angular.io/docs/ts/latest/tutorial/
- READ from JSON files - http://crunchify.com/how-to-read-json-object-from-file-in-java/
- BOOTSTRAP fancy menus - http://navnav.co/
