``` bash
docker: Error response from daemon: driver failed programming external connectivity on endpoint elated_brown (英数字列): Bind for 0.0.0.0:8888 failed: port is already allocated.
```

解決策：
``` bash
$ docker ps
$ docker kill $CONTAINER_ID

```
[【Docker】port is already allocatedエラーを解決したい](https://teratail.com/questions/212664)