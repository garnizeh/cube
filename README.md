# What is this?
This is the implementation of the book Build an Orchestrator in Go (Tim Boring)

## Docker client version
If the client complains about the docker API version, just run the command and set the API to the version needed:
```
export DOCKER_API_VERSION=1.44
```
## Run local
```
CUBE_WORKER_HOST=localhost CUBE_WORKER_PORT=5555 CUBE_MANAGER_HOST=localhost CUBE_MANAGER_PORT=5556 go run main.go
```

## Worker API

### list all tasks
```
curl -v localhost:5555/tasks
```

### add new task
```
curl -v --request POST \
  --header 'Content-Type: application/json' \
  --data '{
    "ID": "266592cd-960d-4091-981c-8c25c44b1018",
    "State": 2,
    "Task": {
      "State": 1,
      "ID": "266592cd-960d-4091-981c-8c25c44b1018",
      "Name": "test-chapter-5-1",
      "Image": "strm/helloworld-http"
    }
  }' \
localhost:5555/tasks
```

### delete a task
```
curl -v --request DELETE "localhost:5555/tasks/266592cd-960d-4091-981c-8c25c44b1018"
```

### read stats
```
curl localhost:5555/stats|jq .
```

## Manager API

### list all tasks
```
curl -v localhost:5556/tasks
```

### add new task
```
curl -v --request POST --header 'Content-Type: application/json' --data @task.json localhost:5556/tasks
```

### delete a task
```
curl -v --request DELETE "localhost:5556/tasks/6be4cb6b-61d1-40cb-bc7b-9cacefefa60c"
```

### read stats
```
curl localhost:5556/stats|jq .
```