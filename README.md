# Micro template of the STELLA infrastructure

This repository provides interested experimenters with a template for integrating their ranking and recommendation systems into the [STELLA infrastructure](https://stella-project.org/). 
Currently, the infrastructure supports two different types of submission. 
Experimenters can choose to submit pre-computed runs with TREC run file syntax *OR* use this repository in order to integrate their system as a micro-service into the [STELLA App](https://github.com/stella-project/stella-app).
In contrast to pre-computed results, these dockerized systems can deliver more comprehensive search result since they are not limited to pre-selected queries or items.

## Development notes

As a starting point we provide a web-service based on [flask](https://palletsprojects.com/p/flask/) in [`app.py`](./app.py). **The classes in [`systems.py`](./systems.py) need to be adapted**.
Of course, experimenters are not restricted to use Flask or Python at all as long as the resulting Docker containers implement the required REST endpoints and deliver technically correct responses.

For ranking systems the following endpoint has to be implemented:

**GET** `container_name/ranking?query=<string:qstr>&page=<int:pnum>&rpp=<int:rppnum>`

For recommending datasets this endpoint has to be implemented:

**GET** `container_name/recommendation/datasets?itemid=<string:itemidstr>&page=<int:pnum>&rpp=<int:rppnum>`  

For recommending publications this endpoint has to be implemented:

**GET** `container_name/recommendation/publications?itemid=<string:itemidstr>&page=<int:pnum>&rpp=<int:rppnum>`

**Requirements:** The submitted system has run in a single Docker container and this repository should be self-contained. As a starting point, please have a look at the [Dockerfile](./Dockerfile). 

## Testing

Before registering your ready-to-be-evaluated system, make sure you run the tests provided in [`test/`](./test).
Beside unit tests, we provide Python scripts to build, run, stop and remove the Docker images/containers.
Once the Docker container is started run either `test_ranking`, `test_recommendation_datasets`, or `test_recommendation_publications`.

## Data

Datasets can be retrieved after registration. Experimenters can choose to implement their system with datasets provided by LIVIVO or GESIS.
Recommendation systems are going to be deployed at GESIS, whereas ranking systems at LIVIVO.

## Register

In order to get access and submit systems, experimenters have to [register](https://stella-project.org/). More information on the procedure will follow soon.