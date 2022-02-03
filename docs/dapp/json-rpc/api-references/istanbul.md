---
description: '>- APIs related to the namespace "istanbul".'
---

# Namespace istanbul <a id="namespace-istanbul"></a>

`istanbul` 네임스페이스는 합의 관련된 함수를 제공합니다.

## istanbul_getSnapshot <a id="istanbul_getsnapshot"></a>

특정 블록 넘버에서 상태 스냅샷을 반환합니다. 상태 스냅샷은 번호/해시, 검증자, 스냅샷 블록의 거버넌스 투표 등의 정보를 포함하고 있습니다.

**Parameters**

| 이름    | 타입                  | 설명                                                                                                                            |
| ----- | ------------------- | ----------------------------------------------------------------------------------------------------------------------------- |
| 블록 번호 | QUANTITY &#124; TAG | 정수 형태의 블록 번호나 [default block parameter](./klay/block.md#the-default-block-parameter)에 정의된 `"earliest"`, `"latest"` 같은 문자열입니다. |

**리턴값**

`객체` - 헤더 객체, 또는 블록이 없는 경우 `error`를 반환합니다.

| 이름 | 타입 | 설명 | | Epoch | 64-byte DATA | 해당 블록 다음부터 보류 중인 표결을 체크포인트 및 리셋합니다. | | Number | 64-byte DATA | 스냅샷이 생성된 블록 번호입니다. | | Number | 64-byte DATA | 스냅샷이 생성된 블록 번호입니다. | | ValSet | 64-byte DATA | 현재 검증자 목록입니다. | | Policy | 64-byte DATA | | | CommiteeSize | 64-byte DATA | | | Votes | 64-byte DATA | 연대기 순으로 정렬된 표결입니다. | | Tally | 64-byte DATA | 재계산을 방지하기 위한 현재 표 합산입니다. |

**예시**

```shell
// Request
$ curl -H "Content-Type: application/json" --data '{"jsonrpc":"2.0","method":"istanbul_getSnapshot","params":["latest"],"id":1}' http://localhost:8551
// Response
{"jsonrpc":"2.0","id":1,"result":{"epoch":604800,"number":3228602,"hash":"0xc03aa058e9e248fee12e12302d0f1ba9a97873765146ae5e2429b78af826a1da","votes":[],"tally":[],"validators":["0x571e53df607be94731a5qqefca1dffe5aek45g3e", ... ],"policy":2,"subgroupsize":22,"rewardAddrs":[...],"votingPower":[1000,1000,1000,1000],"weight":[0,0,0,0],"proposers":["0x5cb1a7dccbd0dc446e3640898ede8820368554c8", ... ],"proposersBlockNum":3225600}}
```

## istanbul_getSnapshotAtHash <a id="istanbul_getsnapshotAtHash"></a>

특정 블록 해시의 스냅샷을 반환합니다.

**Parameters**

| 이름         | 타입            | 설명                   |
| ---------- | ------------- | -------------------- |
| block hash | 32바이트 크기 DATA | The hash of a block. |

**리턴값**

[istanbul_getSnapshot](#istanbul_getsnapshot)를 확인하세요.

**예시**

```shell
// Request
$ curl -H "Content-Type: application/json" --data '{"jsonrpc":"2.0","method":"istanbul_getSnapshotAtHash","params":["0xc03aa058e9e248fee12e12302d0f1ba9a97873765146ae5e2429b78af826a1da"],"id":1}' http://localhost:8551
// Response
{"jsonrpc":"2.0","id":1,"result":{"epoch":604800,"number":3228602,"hash":"0xc03aa058e9e248fee12e12302d0f1ba9a97873765146ae5e2429b78af826a1da","votes":[],"tally":[],"validators":["0x571e53df607be94731a5qqefca1dffe5aek45g3e", ... ],"policy":2,"subgroupsize":22,"rewardAddrs":[...],"votingPower":[1000,1000,1000,1000],"weight":[0,0,0,0],"proposers":["0x5cb1a7dccbd0dc446e3640898ede8820368554c8", ... ],"proposersBlockNum":3225600}}
```


## istanbul_getValidators <a id="istanbul_getvalidators"></a>

특정 블록 번호의 검증자 목록을 반환합니다.

**Parameters**

| 이름    | 타입                  | 설명                                                                                                                            |
| ----- | ------------------- | ----------------------------------------------------------------------------------------------------------------------------- |
| 블록 번호 | QUANTITY &#124; TAG | 정수 형태의 블록 번호나 [default block parameter](./klay/block.md#the-default-block-parameter)에 정의된 `"earliest"`, `"latest"` 같은 문자열입니다. |

**리턴값**

| 이름  | 타입            | 설명             |
| --- | ------------- | -------------- |
| 검증자 | 20바이트 크기 DATA | 검증자의 주소 목록입니다. |

**예시**

```shell
// Request
$ curl -H "Content-Type: application/json" --data '{"jsonrpc":"2.0","method":"istanbul_getValidators","params":["latest"],"id":1}' http://localhost:8551
// Response
{"jsonrpc":"2.0","id":1,"result":["0x571e53df607be94731a5qqefca1dffe5aek45g3e", ... ]}
```

## istanbul_getValidatorsAtHash <a id="istanbul_getvalidatorsathash"></a>

주어진 블록 해시에서의 승인된 검증자 목록을 반환합니다.

**Parameters**

| 이름         | 타입            | 설명                   |
| ---------- | ------------- | -------------------- |
| block hash | 32바이트 크기 DATA | The hash of a block. |

**리턴값**

[istanbul_getValidators](#istanbul_getvalidators)를 참고하세요.

**예시**

```shell
// Request
$ curl -H "Content-Type: application/json" --data '{"jsonrpc":"2.0","method":"istanbul_getValidatorsAtHash","params":["0xc03aa058e9e248fee12e12302d0f1ba9a97873765146ae5e2429b78af826a1da"],"id":1}' http://localhost:8551
// Response
{"jsonrpc":"2.0","id":1,"result":["0x571e53df607be94731a5qqefca1dffe5aek45g3e", ... ]}
```

## istanbul_candidates <a id="istanbul_candidates"></a>

노드가 지지하고 투표하려고 하는 현재 후보자들을 반환합니다.

**Parameters**

없음

**리턴값**

| account | 20-byte DATA | 후보자의 주소입니다. | | auth | boolean | 후보자의 승인 상태를 나타내는 값입니다. |

**예시**

```shell
// Request
$ curl -H "Content-Type: application/json" --data '{"jsonrpc":"2.0","method":"istanbul_candidates","params":[],"id":1}' http://localhost:8551           
// Response
{"jsonrpc":"2.0","id":1,"result":{"0x571e53df607be94731a5qqefca1dffe5aek45g3e":true}}
```

## istanbul_propose <a id="istanbul_propose"></a>

검증자가 관철시키고자 하는 새로운 승인 후보를 추가합니다.

**Parameters**

| 이름      | 타입            | 설명                     |
| ------- | ------------- | ---------------------- |
| account | 20바이트 크기 DATA | 후보자의 주소입니다.            |
| auth    | boolean       | 후보자의 승인 상태를 나타내는 값입니다. |

**리턴값**

없음

**예시**

```shell
// Request
$ curl -H "Content-Type: application/json" --data '{"jsonrpc":"2.0","method":"istanbul_propose","params":["0x571e53df607be94731a5qqefca1dffe5aek45g3e", true],"id":1}' http://localhost:8551 
// Response
{"jsonrpc":"2.0","id":1,"result":null}
```

## istanbul_discard <a id="istanbul_discard"></a>

현재 후보자를 탈락시키고, 검증자가 더 이상 투표하지 못하도록 합니다.

**Parameters**

| 이름      | 타입            | 설명          |
| ------- | ------------- | ----------- |
| account | 20바이트 크기 DATA | 후보자의 주소입니다. |

**리턴값**

없음

**예시**

```shell
// Request
$ curl -H "Content-Type: application/json" --data '{"jsonrpc":"2.0","method":"istanbul_discard","params":["0x571e53df607be94731a5qqefca1dffe5aek45g3e"],"id":1}' http://localhost:8551 
// Response
{"jsonrpc":"2.0","id":1,"result":null}
```

## istanbul_getTimeout <a id="istanbul_getTimeout"></a>

이스탄불 config 타임아웃을 반환합니다. 기본값은 10000ms이며, 이를 초과할 시 timeoutEvent가 전송됩니다. CN의 경우 timeoutEvent는 currentRound, preparesSize, 그리고 로그될 commitsSize를 포함합니다.


**Parameters**

없음

**리턴값**

| 이름      | 타입  | 설명              |
| ------- | --- | --------------- |
| timeout | int | config 타임아웃입니다. |

**예시**

```shell
// Request
$ curl -H "Content-Type: application/json" --data '{"jsonrpc":"2.0","method":"istanbul_getTimeout","params":[],"id":1}' http://localhost:8551 
// Response
{"jsonrpc":"2.0","id":1,"result":10000}
```