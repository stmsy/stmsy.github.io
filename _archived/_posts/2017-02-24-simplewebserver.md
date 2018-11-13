---
title: Truly Simple Web Server
---

## Simple Web Server From Command Line

In case you want to make quickly a web server for test use, I think the following command should be a great help

```shell
(echo "HTTP/1.1 200 OK"; date; echo "Test OK") | netcat -l -p 8080
```

assuming the port 8080 is not used by any application in the machine.
