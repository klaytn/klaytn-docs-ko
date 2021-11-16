# Porting Ethereum Contract <a id="porting-ethereum-contract"></a>

대부분의 경우 Klaytn에서 이더리움 컨트랙트를 수정 없이 사용할 수 있습니다. 
그러나 다음 두 가지 문제에 유의하셔야 합니다.

{% hint style="success" %}
NOTE: Baobab 네트워크의 경우, 블록 번호 `#75373312`부터 protocol upgrade가 활성화되었습니다.
Cypress 메인넷은 다음 버전부터 protocol upgrade가 적용됩니다.
{% endhint %}

## Solidity Support <a id="solidity-support"></a>

Klaytn is currently compatible with **Istanbul** Ethereum Virtual Machine (EVM) version.
Backward compatibility is not guaranteed with other EVM versions on Klaytn.
Thus, it is highly recommended to compile Solidity code with the Istanbul target option. 
Please refer to [how to set the EVM version of solc](https://solidity.readthedocs.io/en/latest/using-the-compiler.html#setting-the-evm-version-to-target).


An example command is shown below:

```
$ solc --evm-version istanbul contract.sol
```

## 분리된 키 쌍 <a id="decoupled-key-pairs"></a>

Klaytn [decouples key pairs from addresses](../klaytn/design/accounts.md#decoupling-key-pairs-from-addresses). If user [updates account](../klaytn/design/transactions/basic.md#txtypeaccountupdate), the private key for a specific account is replaced with another one. Most cases this will not affect your business logic. However if your business logic includes ecrecover, you should consider using validateSender. For more details, refer to [here](precompiled-contracts/precompiled-contracts-previous.md).