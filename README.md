CLC SDK (for go!) [![Build Status](https://travis-ci.org/mikebeyer/clc-sdk.svg?branch=master)](https://travis-ci.org/mikebeyer/clc-sdk) [![Coverage Status](https://coveralls.io/repos/mikebeyer/clc-sdk/badge.svg?branch=master&service=github)](https://coveralls.io/github/mikebeyer/clc-sdk?branch=master)
======

Insallation
---------------------

```
$ go get github.com/mikebeyer/clc-sdk
$ make deps
$ make test
```


Configuration
-------
The SDK supports two helpers for creating your configuration 

Reading from the environment

```go
config := api.EnvConfig()
```

Reading from a file


```go
config, _ := api.FileConfig("./config.json")

```

Examples
-------
To create a new server

```go
client := clc.New(api.EnvConfig())

server := server.Server{
		Name:           "server",
		CPU:            1,
		MemoryGB:       1,
		GroupID:        "GROUP-ID",
		SourceServerID: "UBUNTU-14-64-TEMPLATE",
		Type:           "standard",
	}

resp, _ := client.Server.Create(server)
```

Check status of a server build

```go
resp, _ := client.Server.Create(server)

status, _ := client.Status.Get(resp.GetStatusID())
```

Async polling for complection

```go
resp, _ := client.Server.Create(server)

poll := make(chan *status.Response, 1)
service.Status.Poll(resp.GetStatusID(), poll)

status := <- poll
```

License
-------
This project is licensed under the [Apache License v2.0](http://www.apache.org/licenses/LICENSE-2.0.html).