# What is this?
This is the implementation of the book Build an Orchestrator in Go (Tim Boring)

## Docker client version
If the client complains about the docker API version, just run the command and set the API to the version needed:
```
export DOCKER_API_VERSION=1.44
```
## Run local
```
CUBE_HOST=localhost CUBE_PORT=5555 go run main.go
```

## Client API

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