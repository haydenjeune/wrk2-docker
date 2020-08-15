# wrk2-docker

This image contains the [giltene/wrk2](https://github.com/giltene/wrk2) CLI tool for performance testing.

## Usage

The entrypoint for this image is the `wrk2` binary.

To run tests with 1 thread, 5 connections, 10 requests per second, for 15s, with a request defined in request.lua (as below)

```bash
$ cat request.lua
wrk.method = "POST"
wrk.body   = '{ ... some request JSON }'
wrk.headers["Content-Type"] = "application/json"
```

```bash
docker run -rm -v "$(pwd)"/request.lua:/data/request.lua haydenjeune/wrk2:latest -t1 -L -c5 -R10 -d15s -s /data/request.lua http://localhost/your_request_endpoint
```

Note that the `request.lua` file is mounted inside the `/data` directory of the container via bind mount.
