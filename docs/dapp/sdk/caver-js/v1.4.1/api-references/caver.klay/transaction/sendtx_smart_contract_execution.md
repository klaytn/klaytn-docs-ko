# Smart Contract Execution

## sendTransaction \(SMART\_CONTRACT\_EXECUTION\) <a id="sendtransaction-smart_contract_execution"></a>

```javascript
caver.klay.sendTransaction(transactionObject [, callback])
```

Sends a [Smart Contract Execution](../../../../../../../klaytn/design/transactions/basic.md#txtypesmartcontractexecution) transaction to the network.

**매개변수**

sendTransaction의 매개 변수는 트랜잭션 객체 및 콜백 함수입니다.

| 명칭                | 타입       | 설명                                                                                                             |
|:----------------- |:-------- |:-------------------------------------------------------------------------------------------------------------- |
| transactionObject | Object   | 전송하려는 트랜잭션 객체.                                                                                                 |
| callback          | Function | \(optional\) Optional callback, returns an error object as the first parameter and the result as the second. |

` SMART_CONTRACT_EXECUTION`  트랜잭션 오브젝트 구조는 다음과 같습니다.

| 명칭       | 타입        | 설명                                                                                                                                                                        |
|:-------- |:--------- |:------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 형식       | String    | 트랜잭션 타입. "SMART\_CONTRACT\_EXECUTION"                                                                                                                                 |
| from     | String    | 이 트랜잭션 발신자의 주소입니다.                                                                                                                                                        |
| to       | String    | 배포 된 스마트 컨트랙트의 address.                                                                                                                                                   |
| value    | Number \ | String \| BN \| BigNumber | \(optional\) The value transferred for the transaction in peb. 전송된 KLAY를 받기 위해서는, 이 트랜잭션이 호출하는 컨트랙트 함수가 'payable'이어야 합니다. 생략하면 0으로 설정됩니다. |
| gas      | Number    | The maximum amount of gas willing to pay for the transaction \(unused gas is refunded\).                                                                                |
| gasPrice | Number    | \(optional\) Gas price provided by the sender in peb. gasPrice는 Klaytn 노드에 설정된 unitPrice와 같아야 합니다.                                                                      |
| 논스       | Number    | \(optional\) Integer of a nonce. 생략하면 `caver.klay.getTransactionCount` 값으로 caver-js가 설정합니다.                                                                             |
| data     | String    | 스마트 컨트랙트의 입력 데이터.                                                                                                                                                         |

**리턴값**

`callback`은 32바이트 트랜잭션 해시를 반환합니다.

`PromiEvent`: 프로미스(promise)가 조합된 이벤트 이미터(event emitter). 트랜잭션 영수증이 준비되면 resolve 됩니다. 추가로 다음 이벤트가 발생할 수 있습니다.

* `"transactionHash"`는 `String`를 반환: 트랜잭션을 보내고 트랜잭션 해시가 준비된 직후에 발생.
* `"receipt"`는 `Object`를 반환: 트랜잭션 영수중이 중비되면 발생.
* `"error"`는 `Error`를 반환: 전송 중 에러가 발생하면 발생. 가스 부족 에러(out-of-gas)가 발생한 경우 두 번째 인자는 트랜잭션 영수증입니다.

**예시**

```javascript
const account = caver.klay.accounts.wallet.add('0x{private key}')

// Calling smart contract function

// using the promise
caver.klay.sendTransaction({
    type: 'SMART_CONTRACT_EXECUTION',
    from: account.address,
    to: '0x1d389d91886fd0af55f44c56e1240eb6162ddff8',
    data: '0x6353586b0000000000000000000000001d389d91886fd0af55f44c56e1240eb6162ddff8',
    gas: '300000',
    value: '0x174876e800',
})
.then(function(receipt){
    ...
});

// using the event emitter
caver.klay.sendTransaction({
    type: 'SMART_CONTRACT_EXECUTION',
    from: account.address,
    to: '0x1d389d91886fd0af55f44c56e1240eb6162ddff8',
    data: '0x6353586b0000000000000000000000001d389d91886fd0af55f44c56e1240eb6162ddff8',
    gas: '300000',
    value: '0x174876e800',
})
.on('transactionHash', function(hash){
    ...
})
.on('receipt', function(receipt){
    ...
})
.on('error', console.error); // 가스 부족 에러(out-of-gas)가 발생한 경우 두 번째 인자는 트랜잭션 영수증입니다.
```

## sendTransaction \(FEE\_DELEGATED\_SMART\_CONTRACT\_EXECUTION\) <a id="sendtransaction-fee_delegated_smart_contract_execution"></a>

```javascript
caver.klay.sendTransaction(transactionObject [, callback])
```

Sends a [Fee Delegated Smart Contract Execution](../../../../../../../klaytn/design/transactions/fee-delegation.md#txtypefeedelegatedsmartcontractexecution) transaction to the network.

**매개변수**

sendTransaction의 매개 변수는 트랜잭션 객체 및 콜백 함수입니다.

| 명칭                | 타입       | 설명                                                                                                             |
|:----------------- |:-------- |:-------------------------------------------------------------------------------------------------------------- |
| transactionObject | Object   | 전송하려는 트랜잭션 객체.                                                                                                 |
| callback          | Function | \(optional\) Optional callback, returns an error object as the first parameter and the result as the second. |

`FEE_DELEGATED_SMART_CONTRACT_EXECUTION` 트랜잭션 오브젝트 구조는 다음과 같습니다.

| 명칭       | 타입        | 설명                                                                                                                                                                        |
|:-------- |:--------- |:------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 형식       | String    | 트랜잭션 타입. "FEE\_DELEGATED\_SMART\_CONTRACT\_EXECUTION"                                                                                                             |
| from     | String    | 이 트랜잭션 발신자의 주소입니다.                                                                                                                                                        |
| to       | String    | 배포 된 스마트 컨트랙트의 address.                                                                                                                                                   |
| value    | Number \ | String \| BN \| BigNumber | \(optional\) The value transferred for the transaction in peb. 전송된 KLAY를 받기 위해서는, 이 트랜잭션이 호출하는 컨트랙트 함수가 'payable'이어야 합니다. 생략하면 0으로 설정됩니다. |
| gas      | Number    | The maximum amount of gas willing to pay for the transaction \(unused gas is refunded\).                                                                                |
| gasPrice | Number    | \(optional\) Gas price provided by the sender in peb. gasPrice는 Klaytn 노드에 설정된 unitPrice와 같아야 합니다.                                                                      |
| 논스       | Number    | \(optional\) Integer of a nonce. 생략하면 `caver.klay.getTransactionCount` 값으로 caver-js가 설정합니다.                                                                             |
| data     | String    | 스마트 컨트랙트의 입력 데이터.                                                                                                                                                         |

A transaction object of type `FEE_DELEGATED_SMART_CONTRACT_EXECUTION` with the above structure or an `RLP-encoded transaction` of type `FEE_DELEGATED_SMART_CONTRACT_EXECUTION` can be used as a parameter in [caver.klay.accounts.signTransaction](../../caver.klay.accounts.md#signtransaction) for sender and in [caver.klay.accounts.feePayerSignTransaction](../../caver.klay.accounts.md#feepayersigntransaction) for fee payer.

수수료 납부자가 트랜잭션 발신자가 서명한 RLP 인코딩된 트랜잭션에 서명하고 이를 네트워크로 전송하려면 다음 구조로 오브젝트를 정의하고 `caver.klay.sendTransaction`을 호출하세요.

| 명칭                   | 타입     | 설명                      |
|:-------------------- |:------ |:----------------------- |
| feePayer             | String | 트랜잭션 수수료 납부자의 주소.       |
| senderRawTransaction | String | 발신자가 서명한 RLP 인코딩된 트랜잭션. |

**리턴값**

`callback`은 32바이트 트랜잭션 해시를 반환합니다.

`PromiEvent`: 프로미스(promise)가 조합된 이벤트 이미터(event emitter). 트랜잭션 영수증이 준비되면 resolve 됩니다. 추가로 다음 이벤트가 발생할 수 있습니다.

* `"transactionHash"`는 `String`를 반환: 트랜잭션을 보내고 트랜잭션 해시가 준비된 직후에 발생.
* `"receipt"`는 `Object`를 반환: 트랜잭션 영수중이 중비되면 발생.
* `"error"`는 `Error`를 반환: 전송 중 에러가 발생하면 발생. 가스 부족 에러(out-of-gas)가 발생한 경우 두 번째 인자는 트랜잭션 영수증입니다.

**예시**

```javascript
const sender = caver.klay.accounts.wallet.add('0x{private key}')
const feePayer = caver.klay.accounts.wallet.add('0x{private key}')

// using the promise
const { rawTransaction: senderRawTransaction } = await caver.klay.accounts.signTransaction({
  type: 'FEE_DELEGATED_SMART_CONTRACT_EXECUTION',
  from: sender.address,
  to:   '0xe56a7260015ad92dd48a305ed232090e51e02391',
  data: '0x6353586b0000000000000000000000001d389d91886fd0af55f44c56e1240eb6162ddff8',
  gas:  '300000',
  value: caver.utils.toPeb('1', 'KLAY'),
}, sender.privateKey)

caver.klay.sendTransaction({
  senderRawTransaction: senderRawTransaction,
  feePayer: feePayer.address,
})
.then(function(receipt){
    ...
});

// using the event emitter
const { rawTransaction: senderRawTransaction } = await caver.klay.accounts.signTransaction({
  type: 'FEE_DELEGATED_SMART_CONTRACT_EXECUTION',
  from: sender.address,
  to:   '0xe56a7260015ad92dd48a305ed232090e51e02391',
  data: '0x6353586b0000000000000000000000001d389d91886fd0af55f44c56e1240eb6162ddff8',
  gas:  '300000',
  value: caver.utils.toPeb('1', 'KLAY'),
}, sender.privateKey)

caver.klay.sendTransaction({
  senderRawTransaction: senderRawTransaction,
  feePayer: feePayer.address,
})
.on('transactionHash', function(hash){
    ...
})
.on('receipt', function(receipt){
    ...
})
.on('error', console.error); // 가스 부족 에러(out-of-gas)가 발생한 경우 두 번째 인자는 트랜잭션 영수증입니다.
```

## sendTransaction \(FEE\_DELEGATED\_SMART\_CONTRACT\_EXECUTION\_WITH\_RATIO\) <a id="sendtransaction-fee_delegated_smart_contract_execution_with_ratio"></a>

```javascript
caver.klay.sendTransaction(transactionObject [, callback])
```

Sends a [Fee Delegated Smart Contract Execution With Ratio](../../../../../../../klaytn/design/transactions/partial-fee-delegation.md#txtypefeedelegatedsmartcontractexecutionwithratio) transaction to the network.

**매개변수**

sendTransaction의 매개 변수는 트랜잭션 객체 및 콜백 함수입니다.

| 명칭                | 타입       | 설명                                                                                                             |
|:----------------- |:-------- |:-------------------------------------------------------------------------------------------------------------- |
| transactionObject | Object   | 전송하려는 트랜잭션 객체.                                                                                                 |
| callback          | Function | \(optional\) Optional callback, returns an error object as the first parameter and the result as the second. |

`FEE_DELEGATED_SMART_CONTRACT_EXECUTION_WITH_RATIO`  트랜잭션 오브젝트 구조는 다음과 같습니다.

| 명칭       | 타입        | 설명                                                                                                                                                                        |
|:-------- |:--------- |:------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 형식       | String    | 트랜잭션 타입. "FEE\_DELEGATED\_SMART\_CONTRACT\_EXECUTION\_WITH\_RATIO"                                                                                            |
| from     | String    | 이 트랜잭션 발신자의 주소입니다.                                                                                                                                                        |
| to       | String    | 배포 된 스마트 컨트랙트의 address.                                                                                                                                                   |
| value    | Number \ | String \| BN \| BigNumber | \(optional\) The value transferred for the transaction in peb. 전송된 KLAY를 받기 위해서는, 이 트랜잭션이 호출하는 컨트랙트 함수가 'payable'이어야 합니다. 생략하면 0으로 설정됩니다. |
| gas      | Number    | The maximum amount of gas willing to pay for the transaction \(unused gas is refunded\).                                                                                |
| gasPrice | Number    | \(optional\) Gas price provided by the sender in peb. gasPrice는 Klaytn 노드에 설정된 unitPrice와 같아야 합니다.                                                                      |
| 논스       | Number    | \(optional\) Integer of a nonce. 생략하면 `caver.klay.getTransactionCount` 값으로 caver-js가 설정합니다.                                                                             |
| data     | String    | 스마트 컨트랙트의 입력 데이터.                                                                                                                                                         |
| feeRatio | Number    | 트랜잭션 수수료 납부자의 부담 비율입니다. 이 값이 30이면, 트랜잭션 수수료의 30%를 트랜잭션 수수료 납부자가 지불합니다. 나머지 70%는 트랜잭션 발신자가 지불합니다. 수수료 비율의 범위는 1 ~ 99이며, 이 범위를 벗어나면 트랜잭션이 수락되지 않습니다.                        |

A transaction object of type `FEE_DELEGATED_SMART_CONTRACT_EXECUTION_WITH_RATIO` with the above structure or an `RLP-encoded transaction` of type `FEE_DELEGATED_SMART_CONTRACT_EXECUTION_WITH_RATIO` can be used as a parameter in [caver.klay.accounts.signTransaction](../../caver.klay.accounts.md#signtransaction) for sender and in [caver.klay.accounts.feePayerSignTransaction](../../caver.klay.accounts.md#feepayersigntransaction) for fee payer.

수수료 납부자가 트랜잭션 발신자가 서명한 RLP 인코딩된 트랜잭션에 서명하고 이를 네트워크로 전송하려면 다음 구조로 오브젝트를 정의하고 `caver.klay.sendTransaction`을 호출하세요.

| 명칭                   | 타입     | 설명                      |
|:-------------------- |:------ |:----------------------- |
| feePayer             | String | 트랜잭션 수수료 납부자의 주소.       |
| senderRawTransaction | String | 발신자가 서명한 RLP 인코딩된 트랜잭션. |

**리턴값**

`callback`은 32바이트 트랜잭션 해시를 반환합니다.

`PromiEvent`: 프로미스(promise)가 조합된 이벤트 이미터(event emitter). 트랜잭션 영수증이 준비되면 resolve 됩니다. 추가로 다음 이벤트가 발생할 수 있습니다.

* `"transactionHash"`는 `String`를 반환: 트랜잭션을 보내고 트랜잭션 해시가 준비된 직후에 발생.
* `"receipt"`는 `Object`를 반환: 트랜잭션 영수중이 중비되면 발생.
* `"error"`는 `Error`를 반환: 전송 중 에러가 발생하면 발생. 가스 부족 에러(out-of-gas)가 발생한 경우 두 번째 인자는 트랜잭션 영수증입니다.

**예시**

```javascript
const sender = caver.klay.accounts.wallet.add('0x{private key}')
const feePayer = caver.klay.accounts.wallet.add('0x{private key}')

// using the promise
const { rawTransaction: senderRawTransaction } = await caver.klay.accounts.signTransaction({
  type: 'FEE_DELEGATED_SMART_CONTRACT_EXECUTION_WITH_RATIO',
  from: sender.address,
  to:   '0xe56a7260015ad92dd48a305ed232090e51e02391',
  data: '0x6353586b0000000000000000000000001d389d91886fd0af55f44c56e1240eb6162ddff8',
  gas: '300000',
  value: caver.utils.toPeb('1', 'KLAY'),
  feeRatio: 30,
}, sender.privateKey)

caver.klay.sendTransaction({
  senderRawTransaction: senderRawTransaction,
  feePayer: feePayer.address,
})
.then(function(receipt){
    ...
});

// using the event emitter
const { rawTransaction: senderRawTransaction } = await caver.klay.accounts.signTransaction({
  type: 'FEE_DELEGATED_SMART_CONTRACT_EXECUTION_WITH_RATIO',
  from: sender.address,
  to:   '0xe56a7260015ad92dd48a305ed232090e51e02391',
  data: '0x6353586b0000000000000000000000001d389d91886fd0af55f44c56e1240eb6162ddff8',
  gas: '300000',
  value: caver.utils.toPeb('1', 'KLAY'),
  feeRatio: 30,
}, sender.privateKey)

caver.klay.sendTransaction({
  senderRawTransaction: senderRawTransaction,
  feePayer: feePayer.address,
})
.on('transactionHash', function(hash){
    ...
})
.on('receipt', function(receipt){
    ...
})
.on('error', console.error); // 가스 부족 에러(out-of-gas)가 발생한 경우 두 번째 인자는 트랜잭션 영수증입니다.
```

