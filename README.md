## Create the Project Structure

Open Cmd

```
mkdir <project-name>

cd <project-name>

mkdir docker, postgres, data-generator, .github/workflows, kafka-debezium, consumers

ni docker-airflow.dockerfile -ItemType file

ni README.md -ItemType file

ni dockerfile-compose.yml -ItemType file

ni .gitignore -ItemType file

ni .env -ItemType file
```

## Run the Docker file create the containers

-- docker compose -f .\docker-compose.yml up -d
