# 프로파일링<a id="profiling"></a>

## debug_blockProfile <a id="debug_blockprofile"></a>

입력으로 받은 기간 동안의 블록 프로파일링을 설정하고 프로파일 데이터를 디스크에 씁니다. 가장 정확한 정보를 위해 프로파일 속도는 1입니다. 속도를 다르게 설정하려면, [debug_writeBlockProfile](#debug_writeblockprofile)를 사용하여 속도를 설정하고 프로파일을 수동으로 작성합니다.

| Client  | Method Invocation                                              |
|:-------:| -------------------------------------------------------------- |
| Console | `debug.blockProfile(file, seconds)`                            |
|   RPC   | `{"method": "debug_blockProfile", "params": [string, number]}` |

**Parameters**

| Name    | Type   | Description            |
| ------- | ------ | ---------------------- |
| file    | string | 프로파일링 결과 파일의 이름입니다.    |
| seconds | int    | 초 단위로 표현된 프로파일링 기간입니다. |

**Return Value**

None

**Example**

Console
```javascript
> debug.blockProfile("block.profile", 10)
null
```
HTTP RPC
```shell
$ curl -H "Content-Type: application/json" --data '{"jsonrpc":"2.0","method":"debug_blockProfile","params":["block.profile", 10],"id":1}' https://public-en-baobab.klaytn.net
{"jsonrpc":"2.0","id":1,"result":null}
```


## debug_cpuProfile <a id="debug_cpuprofile"></a>

입력으로 받은 기간 동안의 CPU 프로파일링을 설정하고 프로파일 데이터를 디스크에 씁니다.

| Client  | Method Invocation                                            |
|:-------:| ------------------------------------------------------------ |
| Console | `debug.cpuProfile(file, seconds)`                            |
|   RPC   | `{"method": "debug_cpuProfile", "params": [string, number]}` |

**Parameters**

| Name    | Type   | Description                            |
| ------- | ------ | -------------------------------------- |
| file    | string | The filename for the profiling result. |
| seconds | int    | The profiling duration in seconds.     |

**Return Value**

None

**Example**

Console
```javascript
> debug.cpuProfile("block.profile", 10)
null
```
HTTP RPC
```shell
$ curl -H "Content-Type: application/json" --data '{"jsonrpc":"2.0","method":"debug_cpuProfile","params":["block.profile", 10],"id":1}' https://public-en-baobab.klaytn.net
{"jsonrpc":"2.0","id":1,"result":null}
```

## debug_mutexProfile <a id="debug_mutexprofile"></a>

nsec (nanosecond)에 대한 뮤텍스(mutex) 프로파일링을 시작하고 파일에 프로파일 데이터를 기록합니다. It uses a profile rate of 1 for most accurate information. 다른 속도를 원하는 경우, 속도를 설정하고 수동으로 프로파일을 작성하세요.

| Client  | Method Invocation                                              |
|:-------:| -------------------------------------------------------------- |
| Console | `debug.mutexProfile(file, seconds)`                            |
|   RPC   | `{"method": "debug_mutexProfile", "params": [string, number]}` |

**Parameters**

| Name    | Type   | Description                            |
| ------- | ------ | -------------------------------------- |
| file    | string | The filename for the profiling result. |
| seconds | int    | The profiling duration in seconds.     |

**Return Value**

None

**Example**

Console
```javascript
> debug.mutexProfile("mutex.profile", 10)
null
```
HTTP RPC
```shell
$ curl -H "Content-Type: application/json" --data '{"jsonrpc":"2.0","method":"debug_mutexProfile","params":["mutex.profile", 10],"id":1}' https://public-en-baobab.klaytn.net
{"jsonrpc":"2.0","id":1,"result":null}
```


## debug_isPProfRunning <a id="debug_ispprofrunning"></a>

pprof HTTP 서버가 실행 중이면 `true`를 반환하고, 그렇지 않으면 `false`를 반환합니다.

| Client  | Method Invocation                                  |
|:-------:| -------------------------------------------------- |
| Console | `debug.isPProfRunning()`                           |
|   RPC   | `{"method": "debug_isPProfRunning", "params": []}` |

**Parameters**

None

**Return Value**

| Type | Description                                                 |
| ---- | ----------------------------------------------------------- |
| bool | pprof HTTP 서버가 실행 중이면 `true`를 반환하고, 그렇지 않으면 `false`를 반환합니다. |

**Example**

Console
```javascript
> debug.isPProfRunning()
false
```

HTTP RPC
```shell
$ curl -H "Content-Type: application/json" --data '{"jsonrpc":"2.0","method":"debug_isPProfRunning","params":[],"id":1}' https://public-en-baobab.klaytn.net
{"jsonrpc":"2.0","id":1,"result":true}
```


## debug_setBlockProfileRate <a id="debug_setblockprofilerate"></a>

Go루틴 블록 프로파일 데이터 수집 속도(샘플/초)를 설정합니다. 0이 아닌 값으로 설정하면 블록 프로파일링을 활성화하고, 0으로 설정하면 중단합니다. [debug_writeBlockProfile](#debug_writeblockprofile)을 사용하여 수집한 프로파일 데이터를 쓸 수 있습니다.

| Client  | Method Invocation                                             |
|:-------:| ------------------------------------------------------------- |
| Console | `debug.setBlockProfileRate(rate)`                             |
|   RPC   | `{"method": "debug_setBlockProfileRate", "params": [number]}` |

**Parameters**

| Name | Type | Description              |
| ---- | ---- | ------------------------ |
| rate | int  | (샘플/초)로 표현된 프로파일링 속도입니다. |

**Return Value**

None

**Example**

Console
```javascript
> debug.setBlockProfileRate(1)
null
```
HTTP RPC
```shell
$ curl -H "Content-Type: application/json" --data '{"jsonrpc":"2.0","method":"debug_setBlockProfileRate","params":['3'],"id":1}' https://public-en-baobab.klaytn.net
{"jsonrpc":"2.0","id":1,"result":null}
```


## debug_startCPUProfile <a id="debug_startcpuprofile"></a>

무기한으로 CPU 프로파일링을 진행하고, 입력으로 받은 파일에 그 결과를 작성합니다.

| Client  | Method Invocation                                         |
|:-------:| --------------------------------------------------------- |
| Console | `debug.startCPUProfile(file)`                             |
|   RPC   | `{"method": "debug_startCPUProfile", "params": [string]}` |

**Parameters**

| Name | Type   | Description         |
| ---- | ------ | ------------------- |
| file | string | 프로파일링 출력 파일의 이름입니다. |

**Return Value**

None

**Example**

Console

```javascript
> debug.startCPUProfile("cpu.profile")
null
```
HTTP RPC
```shell
$ curl -H "Content-Type: application/json" --data '{"jsonrpc":"2.0","method":"debug_startCPUProfile","params":["cpu.profile"],"id":1}' https://public-en-baobab.klaytn.net
{"jsonrpc":"2.0","id":1,"result":null}
```


## debug_stopCPUProfile <a id="debug_stopcpuprofile"></a>

CPU 프로파일링을 중단합니다.

| Client  | Method Invocation                                  |
|:-------:| -------------------------------------------------- |
| Console | `debug.stopCPUProfile()`                           |
|   RPC   | `{"method": "debug_stopCPUProfile", "params": []}` |

**Parameters**

None

**Return Value**

None

**Example**

Console
```javascript
> debug.stopCPUProfile()
null
```
HTTP RPC
```shell
$ curl -H "Content-Type: application/json" --data '{"jsonrpc":"2.0","method":"debug_stopCPUProfile","params":[],"id":1}' https://public-en-baobab.klaytn.net
{"jsonrpc":"2.0","id":1,"result":null}
```


## debug_startPProf <a id="debug_startpprof"></a>

pprof HTTP 서버를 시작합니다.  실행 중인 pprof 서버는 아래를 통해 접근할 수 있습니다. (기본 설정의 경우, localhost:6060으로 설정됩니다.)
- http://localhost:6060/debug/pprof (pprof 결과)
- http://localhost:6060/memsize/ (메모리 크기 리포트)
- http://localhost:6060/debug/vars (측정 수치)

| Client  | Method Invocation                                            |
|:-------:| ------------------------------------------------------------ |
| Console | `debug.startPProf(address, port)`                            |
|   RPC   | `{"method": "debug_startPProf", "params": [string, number]}` |

**Parameters**

| Name    | Type   | Description                                              |
| ------- | ------ | -------------------------------------------------------- |
| address | string | (선택 사항) pprof HTTP 서버의 리스너 인터페이스입니다.(기본 설정: "127.0.0.1") |
| port    | int    | (선택 사항) pprof HTTP 서버의 리스너 포트입니다.(기본 설정: 6060)           |

**Return Value**

None

**Example**

Console
```javascript
# To start the pprof server at 127.0.0.1:6060
> debug.startPProf()
null

# To start the pprof server at localhost:12345
> debug.startPProf("localhost", 12345)
null
```

HTTP RPC
```shell
# To start the pprof server at localhost:6060
$ curl -H "Content-Type: application/json" --data '{"jsonrpc":"2.0","method":"debug_startPProf","params":["localhost", 6060],"id":1}' https://public-en-baobab.klaytn.net
{"jsonrpc":"2.0","id":1,"result":null}
```


## debug_stopPProf <a id="debug_stoppprof"></a>

pprof HTTP 서버를 중단합니다.

| Client  | Method Invocation                             |
|:-------:| --------------------------------------------- |
| Console | `debug.stopPProf()`                           |
|   RPC   | `{"method": "debug_stopPProf", "params": []}` |

**Parameters**

None

**Return Value**

None

**Example**

Console
```javascript
> debug.stopPProf()
null
```

HTTP RPC
```shell
$ curl -H "Content-Type: application/json" --data '{"jsonrpc":"2.0","method":"debug_stopPProf","params":[],"id":1}' https://public-en-baobab.klaytn.net
{"jsonrpc":"2.0","id":1,"result":null}
```


## debug_writeBlockProfile <a id="debug_writeblockprofile"></a>

입력으로 받은 파일에 Go루틴 블록 프로파일링을 작성합니다.

| Client  | Method Invocation                                           |
|:-------:| ----------------------------------------------------------- |
| Console | `debug.writeBlockProfile(file)`                             |
|   RPC   | `{"method": "debug_writeBlockProfile", "params": [string]}` |

**Parameters**

| Name | Type   | Description                            |
| ---- | ------ | -------------------------------------- |
| file | string | The filename for the profiling output. |

**Return Value**

None

**Example**

Console
```javascript
> debug.writeBlockProfile("block.profile")
null
```
HTTP RPC
```shell
$ curl -H "Content-Type: application/json" --data '{"jsonrpc":"2.0","method":"debug_writeBlockProfile","params":["block.profile"],"id":1}' https://public-en-baobab.klaytn.net
{"jsonrpc":"2.0","id":1,"result":null}
```


## debug_writeMemProfile <a id="debug_writememprofile"></a>

입력으로 받은 파일에 할당 프로파일을 작성합니다.  프로파일링 속도는 이 API로 설정할 수 없으며, 커맨드라인에서 `--memprofilerate` 플래그를 사용하여 설정해야 합니다.

| Client  | Method Invocation                                         |
|:-------:| --------------------------------------------------------- |
| Console | `debug.writeMemProfile(file)`                             |
|   RPC   | `{"method": "debug_writeMemProfile", "params": [string]}` |

**Parameters**

| Name | Type   | Description                            |
| ---- | ------ | -------------------------------------- |
| file | string | The filename for the profiling output. |

**Return Value**

None

**Example**

Console
```javascript
> debug.writeMemProfile("mem.profile")
null
```
HTTP RPC
```shell
$ curl -H "Content-Type: application/json" --data '{"jsonrpc":"2.0","method":"debug_writeMemProfile","params":["mem.profile"],"id":1}' https://public-en-baobab.klaytn.net
{"jsonrpc":"2.0","id":1,"result":null}
```

## debug_writeMutexProfile <a id="debug_writemutexprofile"></a>

Writes a goroutine blocking profile to the given file.

| Client  | Method Invocation                                           |
|:-------:| ----------------------------------------------------------- |
| Console | `debug.writeMutexProfile(file)`                             |
|   RPC   | `{"method": "debug_writeMutexProfile", "params": [string]}` |

**Parameters**

| Name | Type   | Description                            |
| ---- | ------ | -------------------------------------- |
| file | string | The filename for the profiling output. |

**Return Value**

None

**Example**

Console
```javascript
> debug.writeMutexProfile("mutex.profile")
null
```
HTTP RPC
```shell
$ curl -H "Content-Type: application/json" --data '{"jsonrpc":"2.0","method":"debug_writeMutexProfile","params":["mutex.profile"],"id":1}' https://public-en-baobab.klaytn.net
{"jsonrpc":"2.0","id":1,"result":null}
```
