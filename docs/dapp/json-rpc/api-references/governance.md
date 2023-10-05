---
description: >-
  Klaytn 거버넌스와 관련한 API입니다.
---

# governance <a id="namespace-governance"></a>

네트워크 거버넌스를 위해 Klaytn은 다음과 같이 `governance` namespace의 API를 제공합니다.

Klaytn에는 세 가지 거버넌스 모드가 있습니다.
* `none`: 네트워크에 참여하는 모든 노드는 환경설정을 변경할 권리가 있습니다.
* `single`: 오직 하나의 특정 노드가 환경설정을 변경할 권리를 가집니다.
* `ballot`: 의결권이 있는 모든 노드가 환경설정 변경에 투표할 수 있습니다. 전체 의결권 중 절반 이상이 모이면 해당 의제는 통과됩니다.

거버넌스 모드 종류에 따라 제안자는 단위 가격, 최소 예치 금액 등 네트워크 파라미터에 대해 투표할 수 있습니다. 제안자가 되기 위해서 노드는 최소 기준 이상의 KLAY를 예치해야 합니다. 자격이 있는 노드들은 블록을 제안할 권리를 가지지만, 실제 제안자로 선정될 확률은 예치 금액에 따라 결정됩니다.

특정 기간 동안의 제안자 선정 슬롯(기회)의 수를 결정하기 위해 예치금 비율을 계산할 때 숫자 반올림으로 인해 노드에 슬롯이 한 개도 부여되지 않을 수 있습니다. 하지만 최소 기준 KLAY를 예치한 자격있는 노드에게는 슬롯이 보장됩니다.

노드가 자격이 없을 경우, 즉 노드가 충분한 양의 KLAY를 예치하지 않는다면, 블록을 제안하거나 검증할 기회가 주어지지 않을 것입니다.

**주의 사항**
- 거버넌스 노드는 예외적으로 `single` 모드에서 항상 자격이 있습니다.
- 블록이 제안될 때 투표가 이루어집니다. 이 투표는 블록이 제안된 주기를 포함한 두 주기 이후에 반영됩니다. 예외적으로 addValidator/removeValidator만 즉시 적용됩니다.
## governance_vote <a id="governance_vote"></a>

`vote` 메서드는 새로운 투표를 제출합니다. 거버넌스 모드에 의거하여 노드가 의결권을 가지는 경우 투표할 수 있습니다. 그렇지 않으면 오류 메시지가 반환되고 투표는 무시됩니다.

**Parameters**

- `Key` : 변경하고자 하는 환경설정의 이름입니다. 키는 `domain.field`의 형식으로 되어 있습니다.
- `Value` : 각 키에 대한 다양한 형태의 값입니다.

| Key                                 | Description                                                                                                                                                                                                                                                                                       |
| ----------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `"governance.governancemode"`       | `STRING`. 세 거버넌스 모드 중 하나입니다. `"none"`, `"single"`, `"ballot"` 등 세 가지 모드 중 하나를 선택합니다.                                                                                                                                                                                                              |
| `"governance.governingnode"`        | `ADDRESS`. 거버넌스를 통제하는 특정 노드의 주소입니다. 거버넌스 모드가 `"single"`인 경우에만 해당합니다. 예를 들어, `"0xe733cb4d279da696f30d470f8c04decb54fcb0d2"`입니다.                                                                                                                                                                    |
| `"governance.unitprice"`            | `NUMBER`. 가스당 가격입니다. 예를 들어, `25000000000`입니다.                                                                                                                                                                                                                                                     |
| `"governance.addvalidator"`         | `ADDRESS`. 새로운 검증자 후보의 주소입니다. 예를 들어, `0xe733cb4d279da696f30d470f8c04decb54fcb0d2`입니다.                                                                                                                                                                                                             |
| `"governance.removevalidator"`      | `ADDRESS`. 제거될 검증자의 주소입니다. e.g., `0xe733cb4d279da696f30d470f8c04decb54fcb0d2`                                                                                                                                                                                                                     |
| `"governance.deriveshaimpl"`        | `NUMBER`. Policy to generate the transaction hash and receipt hash in a block header. See [here](https://github.com/klaytn/klaytn/blob/v1.10.0/blockchain/types/derive_sha.go#L34) for available options. e.g., `2` (DeriveShaConcat)                                                             |
| `"governance.govparamcontract"`     | `ADDRESS`. Address of the GovParam contract. e.g., `0xe733cb4d279da696f30d470f8c04decb54fcb0d2`                                                                                                                                                                                                   |
| `"istanbul.epoch"`                  | `NUMBER`. A period in which votes are gathered in blocks. When an epoch end, all votes which haven't been passed will be cleared. e.g., `86400`                                                                                                                                                   |
| `"istanbul.committeesize"`          | `NUMBER`. The number of validators in a committee.(`sub` in chain configuration) e.g., `7`                                                                                                                                                                                                        |
| `"reward.mintingamount"`            | `STRING`. Amount of Peb minted when a block is generated. Double quotation marks are needed for a value. e.g., `"9600000000000000000"`                                                                                                                                                            |
| `"reward.ratio"`                    | `STRING`. Distribution rate for a CN/KGF/KIR separated by `"/"`. The sum of all values has to be `100`. e.g., `"50/40/10"` meaning CN 50%, KGF 40%, KIR 10%                                                                                                                                       |
| `"reward.kip82ratio"`               | `STRING`. Distribution ratio of the block proposer to stakers separated by `"/"`. The sum of all values has to be `"100"`. See [KIP-82](https://github.com/klaytn/kips/blob/master/KIPs/kip-82.md) for further details. e.g., `"20/80"` means that the proposer takes 20% while stakers take 80%. |
| `"reward.useginicoeff"`             | `BOOL`. Use the Gini coefficient or not. `true`, `false`                                                                                                                                                                                                                                          |
| `"reward.deferredtxfee"`            | `BOOL`. The way of giving transaction fee to a proposer. If true, it means the tx fee will be summed up with block reward and distributed to the proposer, KIR and KGF. If not, all tx fee will be given to the proposer. `true`, `false`                                                         |
| `"reward.minimumstake"`             | `STRING`. Amount of Klay required to be a CN (Consensus Node). Double quotation marks are needed for a value. e.g., `"5000000"`                                                                                                                                                                   |
| `"kip71.lowerboundbasefee"`         | `NUMBER`. The lowest possible base fee. See [KIP-71](https://github.com/klaytn/kips/blob/main/KIPs/kip-71.md) for further details. e.g., `25000000000`                                                                                                                                            |
| `"kip71.upperboundbasefee"`         | `NUMBER`. The highest possible base fee. e.g., `750000000000`                                                                                                                                                                                                                                     |
| `"kip71.gastarget"`                 | `NUMBER`. The block gas that base fee wants to achieve. The base fee increases when parent block contains more than gas target, and decreases when parent block contains less than gas target. e.g., `30000000`                                                                                   |
| `"kip71.basefeedenominator"`        | `NUMBER`. Controls how fast base fee changes. e.g., `20`                                                                                                                                                                                                                                          |
| `"kip71.maxblockgasusedforbasefee"` | `NUMBER`. The maximum block gas perceived in base fee calculation. e.g., `60000000`                                                                                                                                                                                                               |


**Return Value**

| Type   | Description  |
| ------ | ------------ |
| String | 투표 제출 결과입니다. |

**Example**

```javascript
> governance.vote ("governance.governancemode", "ballot")
"Your vote was successfully placed."

> governance.vote ("governance.governingnode", "0x12345678990123456789901234567899012345678990")
"Your vote was successfully placed."

> governance.vote("istanbul.epoch", 604800)
"Your vote was successfully placed."

> governance.vote("governance.unitprice", 25000000000)
"Your vote was successfully placed."

> governance.vote("istanbul.committeesize", 7)
"Your vote was successfully placed."

> governance.vote("reward.mintingamount", "9600000000000000000")
"Your vote was successfully placed."

> governance.vote("reward.ratio", "40/30/30")
"Your vote was successfully placed."

> governance.vote("reward.useginicoeff", false)
"Your vote was successfully placed."

// If wrong data are given
> governance.vote("reward.ratio", 100)
"Your vote couldn't be placed. Please check your vote's key and value"

> governance.vote("governance.governingnode", 1234)
"Your vote couldn't be placed. Please check your vote's key and value"

// when `governancemode` is "single" and the node is not `governingnode`
> governance.vote("governance.governancemode", "ballot")
"You don't have the right to vote"
```


## governance_showTally <a id="governance_showtally"></a>

`showTally` 속성은 거버넌스 투표의 현재 집계를 제공합니다. 집계된 찬성률을 백분율로 나타냅니다. 50%가 넘으면 해당 의제는 통과됩니다.

**Parameters**

None

**Return Value**

| Type  | Description                |
| ----- | -------------------------- |
| Tally | 각 표의 가중치를 고려한 찬성률의 백분율입니다. |

**Example**

```javascript
> governance.showTally
[{
    ApprovalPercentage: 36.2,
    Key: "unitprice",
    Value: 25000000000
}, {
    ApprovalPercentage: 72.5,
    Key: "mintingamount",
    Value: "9600000000000000000"
}]
```


## governance_totalVotingPower <a id="governance_totalvotingpower"></a>

`totalVotingPower` 속성은 CN들이 보유한 의결권 합계를 나타냅니다. 각 CN은 1.0 ~ 2.0의 의결권을 가집니다. `"none"`, `"single"` 거버넌스 모드에서는 `totalVotingPower` 속성을 통해 제공하는 정보가 없습니다.

**Parameters**

None

**Return Value**

| Type  | Description             |
| ----- | ----------------------- |
| Float | 총 의결권 또는 오류 메시지를 반환합니다. |

**Example**

```javascript
// In "ballot" governance mode
> governance.totalVotingPower
32.452

// In "none", "single" governance mode
> governance.totalVotingPower
"In current governance mode, voting power is not available"
```


## governance_myVotingPower <a id="governance_myvotingpower"></a>

`myVotingPower` 속성은 노드가 보유한 의결권을 나타냅니다. The voting power can be 1.0 ~ 2.0. In `"none"`, `"single"` governance mode, `totalVotingPower` don't provide any information.

**Parameters**

None

**Return Value**

| Type  | Description               |
| ----- | ------------------------- |
| Float | 노드의 의결권 또는 오류 메시지를 반환합니다. |

**Example**

```javascript
// In "ballot" governance mode
> governance.myVotingPower
1.323

// In "none", "single" governance mode
> governance.myVotingPower
"In current governance mode, voting power is not available"
```


## governance_myVotes <a id="governance_myvotes"></a>

`myVotes` 속성은 투표 주기 동안의 투표 정보를 나타냅니다. 사용자의 노드가 새로운 블록을 생성할 때 각 투표가 블록에 저장됩니다. 현재 투표 주기가 종료되면 이 정보는 사라집니다.

**Parameters**

None

**Return Value**

| Type      | Description                                                                                                                                                                                                      |
| --------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Vote List | Node's Voting status in the epoch<br>- `BlockNum`: The block number that this vote is stored<br>- `Casted`: If this vote is stored in a block or not<br>- `Key/Value`: The content of the vote |

**Example**

```javascript
> governance.vote("governance.governancemode", "ballot")
"Your vote was successfully placed."

> governance.myVotes
[{
    BlockNum: 403,
    Casted: true,
    Key: "governance.governancemode",
    Value: "ballot"
}]

```

## governance_getChainConfig <a id="governance_getchainconfig"></a>

The `getChainConfig` returns the chain configuration at a specific block. If the parameter is not set, it returns the chain configuration at the latest block.

**Parameters**

| Type                | Description                                                                                                                                                                |
| ------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| QUANTITY &#124; TAG | Integer or hexadecimal block number, or the string `"earliest"`, `"latest"` or `"pending"` as in the [default block parameter](klay/block.md#the-default-block-parameter). |

{% hint style="success" %}
NOTE: The block number can be larger than the latest block number, in which case the API returns the tentative value based on the current chain state. The future governance parameters are subject to change via additional governance votes or GovParam contract state changes.
{% endhint %}

**Return Value**

| Type | Description                                   |
| ---- | --------------------------------------------- |
| JSON | Chain configuration at the given block number |

**Example**

```javascript
> governance.getChainConfig()
{
  chainId: 1001,
  deriveShaImpl: 0,
  ethTxTypeCompatibleBlock: 86513895,
  governance: {
    govParamContract: "0x84214cec245d752a9f2faf355b59ddf7f58a6edb",
    governanceMode: "single",
    governingNode: "0x99fb17d324fa0e07f23b49d09028ac0919414db6",
    kip71: {
      basefeedenominator: 20,
      gastarget: 30000000,
      lowerboundbasefee: 25000000000,
      maxblockgasusedforbasefee: 60000000,
      upperboundbasefee: 750000000000
    },
    reward: {
      deferredTxFee: true,
      kip82ratio: "20/80",
      minimumStake: 5000000,
      mintingAmount: 6400000000000000000,
      proposerUpdateInterval: 3600,
      ratio: "50/40/10",
      stakingUpdateInterval: 86400,
      useGiniCoeff: true
    }
  },
  istanbul: {
    epoch: 604800,
    policy: 2,
    sub: 22
  },
  istanbulCompatibleBlock: 75373312,
  koreCompatibleBlock: 111736800,
  londonCompatibleBlock: 80295291,
  magmaCompatibleBlock: 98347376,
  unitPrice: 250000000000
}
```

## governance_chainConfig <a id="governance_chainconfig"></a>

The `chainConfig` property provides the latest chain configuration. This is equivalent to `chainConfigAt()` with an empty parameter.

{% hint style="warning" %}
`governance_chainConfig` API will be deprecated since Klaytn v1.11 (see [klaytn#1783](https://github.com/klaytn/klaytn/pull/1783)). Use <a href="#governance_getchainconfig">`governance_getChainConfig`</a> instead.

NOTE: the RPC API will be deprecated since v1.11. However, the `governance.chainConfig` property in the Klaytn JavaScript console is removed since Klaytn v1.10.2.
{% endhint %}

{% hint style="success" %}
NOTE: In versions earlier than Klaytn v1.10.0, this API returned the initial chain configuration. However, due to its confusing name, it is updated since Klaytn v1.10.0. To query the initial chain configuration, use `chainConfigAt(0)` instead.
{% endhint %}

**Parameters**

None

**Return Value**

| Type | Description                 |
| ---- | --------------------------- |
| JSON | Current chain configuration |

**Example**

```javascript
> governance.chainConfig
{
  chainId: 1001,
  deriveShaImpl: 2,
  governance: {
    govParamContract: "0x0000000000000000000000000000000000000000",
    governanceMode: "ballot",
    governingNode: "0xe733cb4d279da696f30d470f8c04decb54fcb0d2",
    kip71: {
      basefeedenominator: 20,
      gastarget: 30000000,
      lowerboundbasefee: 25000000000,
      maxblockgasusedforbasefee: 60000000,
      upperboundbasefee: 750000000000
    },
    reward: {
      deferredTxFee: true,
      kip82ratio: "20/80",
      minimumStake: 5000000,
      mintingAmount: 6400000000000000000,
      proposerUpdateInterval: 3600,
      ratio: "50/40/10",
      stakingUpdateInterval: 20,
      useGiniCoeff: false
    }
  },
  istanbul: {
    epoch: 20,
    policy: 2,
    sub: 1
  },
  istanbulCompatibleBlock: 0,
  koreCompatibleBlock: 0,
  londonCompatibleBlock: 0,
  magmaCompatibleBlock: 0,
  unitPrice: 25000000000
}
```

## governance_chainConfigAt <a id="governance_chainconfigat"></a>

The `chainConfigAt` returns the chain configuration at a specific block. If the parameter is not set, it returns the chain configuration at the latest block.

{% hint style="warning" %}
`governance_chainConfigAt` API will be deprecated since Klaytn v1.11 (see [klaytn#1783](https://github.com/klaytn/klaytn/pull/1783)). Use <a href="#governance_getchainconfig">`governance_getChainConfig`</a> instead.
{% endhint %}

**Parameters**

| Type                | Description                                                                                                                                                                |
| ------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| QUANTITY &#124; TAG | Integer or hexadecimal block number, or the string `"earliest"`, `"latest"` or `"pending"` as in the [default block parameter](klay/block.md#the-default-block-parameter). |

{% hint style="success" %}
NOTE: The block number can be larger than the latest block number, in which case the API returns the tentative value based on the current chain state. The future governance parameters are subject to change via additional governance votes or GovParam contract state changes.
{% endhint %}

**Return Value**

| Type | Description                                   |
| ---- | --------------------------------------------- |
| JSON | Chain configuration at the given block number |

**Example**

```javascript
> governance.chainConfigAt()
{
  chainId: 1001,
  deriveShaImpl: 2,
  governance: {
    govParamContract: "0x0000000000000000000000000000000000000000",
    governanceMode: "ballot",
    governingNode: "0xe733cb4d279da696f30d470f8c04decb54fcb0d2",
    kip71: {
      basefeedenominator: 20,
      gastarget: 30000000,
      lowerboundbasefee: 25000000000,
      maxblockgasusedforbasefee: 60000000,
      upperboundbasefee: 750000000000
    },
    reward: {
      deferredTxFee: true,
      kip82ratio: "20/80",
      minimumStake: 5000000,
      mintingAmount: 6400000000000000000,
      proposerUpdateInterval: 3600,
      ratio: "50/40/10",
      stakingUpdateInterval: 20,
      useGiniCoeff: false
    }
  },
  istanbul: {
    epoch: 20,
    policy: 2,
    sub: 1
  },
  istanbulCompatibleBlock: 0,
  koreCompatibleBlock: 0,
  londonCompatibleBlock: 0,
  magmaCompatibleBlock: 0,
  unitPrice: 25000000000
}
```

## governance_nodeAddress <a id="governance_nodeaddress"></a>

The `nodeAddress` property provides the address of the node that a user is using. It is derived from the nodekey and used to sign consensus messages. And the value of `"governingnode"` has to be one of validator's node address.

**Parameters**

None

**Return Value**

| Type    | Description               |
| ------- | ------------------------- |
| ADDRESS | 20 BYTE address of a node |

**Example**

```javascript
> governance.nodeAddress
"0xe733cb4d279da696f30d470f8c04decb54fcb0d2"
```

## governance_getParams <a id="governance_getparams"></a>

The `getParams` returns governance parameters at a specific block.

**Parameters**

| Type                | Description                                                                                                                                                                |
| ------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| QUANTITY &#124; TAG | Integer or hexadecimal block number, or the string `"earliest"`, `"latest"` or `"pending"` as in the [default block parameter](klay/block.md#the-default-block-parameter). |

{% hint style="success" %}
NOTE: The block number can be larger than the latest block number, in which case the API returns the tentative value based on the current chain state. The future governance parameters are subject to change via additional governance votes or GovParam contract state changes.
{% endhint %}

**Return Value**

| Type | Description           |
| ---- | --------------------- |
| JSON | governance parameters |

**Example**

```javascript
> governance.getParams(89)
{
  governance.deriveshaimpl: 2,
  governance.governancemode: "single",
  governance.governingnode: "0x99fb17d324fa0e07f23b49d09028ac0919414db6",
  governance.govparamcontract: "0x0000000000000000000000000000000000000000",
  governance.unitprice: 25000000000,
  istanbul.committeesize: 22,
  istanbul.epoch: 604800,
  istanbul.policy: 2,
  kip71.basefeedenominator: 20,
  kip71.gastarget: 30000000,
  kip71.lowerboundbasefee: 25000000000,
  kip71.maxblockgasusedforbasefee: 60000000,
  kip71.upperboundbasefee: 750000000000,
  reward.deferredtxfee: true,
  reward.kip82ratio: "20/80",
  reward.minimumstake: "5000000",
  reward.mintingamount: "9600000000000000000",
  reward.proposerupdateinterval: 3600,
  reward.ratio: "34/54/12",
  reward.stakingupdateinterval: 86400,
  reward.useginicoeff: true
}
```

## governance_itemsAt <a id="governance_itemsat"></a>

The `itemsAt` returns governance parameters at a specific block.

{% hint style="warning" %}
`governance_itemsAt` API will be deprecated since Klaytn v1.11 (see [klaytn#1783](https://github.com/klaytn/klaytn/pull/1783)). Use <a href="#governance_getparams">`governance_getParams`</a> instead.
{% endhint %}

**Parameters**

| Type                | Description                                                                                                                                                                |
| ------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| QUANTITY &#124; TAG | Integer or hexadecimal block number, or the string `"earliest"`, `"latest"` or `"pending"` as in the [default block parameter](klay/block.md#the-default-block-parameter). |

{% hint style="success" %}
NOTE: In versions earlier than Klaytn v1.7.0, only integer block number, the string `"earliest"` and `"latest"` are available.
{% endhint %}

{% hint style="success" %}
NOTE: The block number can be larger than the latest block number, in which case the API returns the tentative value based on the current chain state. The future governance parameters are subject to change via additional governance votes or GovParam contract state changes.
{% endhint %}

**Return Value**

| Type | Description      |
| ---- | ---------------- |
| JSON | governance items |

**Example**

```javascript
> governance.itemsAt(89)
{
  governance.deriveshaimpl: 2,
  governance.governancemode: "single",
  governance.governingnode: "0x7bf29f69b3a120dae17bca6cf344cf23f2daf208",
  governance.govparamcontract: "0x0000000000000000000000000000000000000000",
  governance.unitprice: 25000000000,
  istanbul.committeesize: 13,
  istanbul.epoch: 30,
  istanbul.policy: 2,
  kip71.basefeedenominator: 20,
  kip71.gastarget: 30000000,
  kip71.lowerboundbasefee: 25000000000,
  kip71.maxblockgasusedforbasefee: 60000000,
  kip71.upperboundbasefee: 750000000000,
  reward.deferredtxfee: true,
  reward.kip82ratio: "20/80",
  reward.minimumstake: "5000000",
  reward.mintingamount: "9600000000000000000",
  reward.proposerupdateinterval: 30,
  reward.ratio: "34/54/12",
  reward.stakingupdateinterval: 60,
  reward.useginicoeff: true
}
```

## governance_pendingChanges <a id="governance_pendingchanges"></a>

The `pendingChanges` returns the list of items that have received enough number of votes but not yet finalized. At the end of the current epoch, these changes will be finalized and the result will be in effect from the epoch after next epoch.

**Parameters**

None

**Return Value**

| Type      | Description                                           |
| --------- | ----------------------------------------------------- |
| Vote List | Currently pending changes composed of keys and values |

**Example**
```javascript
> governance.pendingChanges
{
  reward.minimumstake: "5000000",
  reward.useginicoeff: false
}
```

## governance_votes <a id="governance_votes"></a>

The `votes` returns the votes from all nodes in the epoch. These votes are gathered from the header of each block.

**Parameters**

None

**Return Value**

| Type      | Description                                               |
| --------- | --------------------------------------------------------- |
| Vote List | Current votes composed of keys, values and node addresses |

**Example**
```javascript
> governance.votes
[{
    key: "reward.minimumstake",
    validator: "0xe733cb4d279da696f30d470f8c04decb54fcb0d2",
    value: "5000000"
}, {
    key: "reward.useginicoeff",
    validator: "0xa5bccb4d279419abe2d470f8c04dec0789ac2d54",
    value: false
}]
```

## governance_idxCache <a id="governance_idxcache"></a>
The `idxCache` property returns an array of current idxCache in the memory cache. idxCache contains the block numbers where governance change happened. The cache can have up to 1000 block numbers in memory by default.

**Parameters**

None

**Return Value**

| Type         | Description                                    |
| ------------ | ---------------------------------------------- |
| uint64 array | Block numbers where governance change happened |

**Example**
```javascript
> governance.idxCache
[0, 30]
```

## governance_idxCacheFromDb <a id="governance_idxcachefromdb"></a>
The `idxCacheFromDb` returns an array that contains all block numbers on which a governance change ever happened. The result of `idxCacheFromDb` is the same or longer than that of `idxCache`

**Parameters**

None

**Return Value**

| Type         | Description                                          |
| ------------ | ---------------------------------------------------- |
| uint64 array | Every block numbers where governance change happened |

**Example**
```javascript
> governance.idxCacheFromDb
[0, 30]
```

## governance_itemCacheFromDb <a id="governance_itemcachefromdb"></a>
The `itemCacheFromDb` returns the governance information stored in the given block. If no changes were stored in the given block, the function returns `null`.

**Parameters**

| Type   | Description                                                      |
| ------ | ---------------------------------------------------------------- |
| uint64 | A block number to query the governance change made in the block. |

**Return Value**

| Type | Description                                    |
| ---- | ---------------------------------------------- |
| JSON | Stored governance information at a given block |

**Example**
```javascript
> governance.itemCacheFromDb(0)
{
  governance.governancemode: "single",
  governance.governingnode: "0xe733cb4d279da696f30d470f8c04decb54fcb0d2",
  governance.unitprice: 25000000000,
  istanbul.committeesize: 1,
  istanbul.epoch: 30,
  istanbul.policy: 2,
  reward.deferredtxfee: true,
  reward.minimumstake: "5000000",
  reward.mintingamount: "6400000000000000000",
  reward.proposerupdateinterval: 3600,
  reward.ratio: "50/40/10",
  reward.stakingupdateinterval: 20,
  reward.useginicoeff: false
}
```
## governance_getStakingInfo <a id="governance_getstakinginfo"></a>

The `getStakingInfo` returns staking information at a specific block. The result includes the following information.
- `BlockNum`: 예치 정보가 조회되는 블록 번호
- `CouncilNodeAddrs`: 컨센서스 노드 주소
- `CouncilRewardAddrs`: 관련 노드들의 블록 보상이 제공되는 주소
- `CouncilStakingAddrs`: 관련된 노드들이 예치를 위해 배포하는 컨트랙트 주소
- `CouncilStakingAmounts`: 관련 노드들이 예치하는 KLAY 액수
- `Gini`: 지니 계수
- `KIRAddr`: KIR 컨트랙트 주소
- `PoCAddr`: The contract address of KGF. PoC is the previous name of KGF.
- `UseGini`: 지니 계수 사용 여부를 나타내는 boolean 값

Note that the order of all addresses and the staking amounts are matched.

**Parameters**

| Type                | Description                                                                                                                                                         |
| ------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| QUANTITY &#124; TAG | Integer of a block number, or the string `"earliest"`, `"latest"` or `"pending"`, as in the [default block parameter](./klay/block.md#the-default-block-parameter). |

**Return Value**

| Type | Description         |
| ---- | ------------------- |
| JSON | Staking information |

**Example**

```javascript
> governance.getStakingInfo("latest")
{
  BlockNum: 57801600,
  CouncilNodeAddrs: ["0x99fb17d324fa0e07f23b49d09028ac0919414db6", "0x571e53df607be97431a5bbefca1dffe5aef56f4d", "0xb74ff9dea397fe9e231df545eb53fe2adf776cb2", "0x5cb1a7dccbd0dc446e3640898ede8820368554c8", "0x776817c0ef3d06d794cf01ae9afa33d7397b9b40", "0xc180ca565b34b5b63877674f5fe647e7da079022", "0x03497f51c31fe8b402df0bde90fd5a85f87aa943"],
  CouncilRewardAddrs: ["0xb2bd3178affccd9f9f5189457f1cad7d17a01c9d", "0x6559a7b6248b342bc11fbcdf9343212bbc347edc", "0x82829a60c6eac4e3e9d6ed00891c69e88537fd4d", "0xa86fd667c6a340c53cc5d796ba84dbe1f29cb2f7", "0x6e22cbe2b8bbd1df9f1d3c8ebae6d7ff5414a734", "0x24e593fb29731e54905025c230727dc28d229f77", "0x2b2a7a1d29a203f60e0a964fc64231265a49cd97"],
  CouncilStakingAddrs: ["0x12fa1ab4c3e17c1c08c1b5a945c864c8e8bf707e", "0xfd56604f1a20268ff7a0eab2ab48e25ee1e0f653", "0x1e0f6aaa9baa6081dc4910a854eebf8854c262ab", "0x5e6988415ebe0f6b088f5a676003ba60f572875a", "0xbb44998c2af35b8faee694cffe216558056d747e", "0x68cba498b7175cde9de08fc2e85ad3e9c8caefa8", "0x98efb31eeccafe35d53a6926e2a54c0858d9eebc"],
  CouncilStakingAmounts: [5000000, 5000000, 5000000, 5000000, 5000000, 5000000, 5000000],
  Gini: 0,
  KIRAddr: "0x716f89d9bc333286c79db4ebb05516897c8d208a",
  PoCAddr: "0x2bcf9d3e4a846015e7e3152a614c684de16f37c6",
  UseGini: true
}
```

## governance_ getRewardsAccumulated<a id="governance_getRewardsAccumulated"></a>
Returns the rewards information accumulated within the given block range `[first, last]`.

{% hint style="success" %}
NOTE: The block range should be less than 604800 (about 7 days) to protect endpoints from the resource exhaustion.
{% endhint %}

**Parameters**

| Type                | Description                                                                                                                                                                                                             |
| ------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| QUANTITY &#124; TAG | Accumulation start (first) block number, inclusive. Integer of a block number, or the string `"earliest"`, `"latest"` or `"pending"`, as in the [default block parameter](./klay/block.md#the-default-block-parameter). |
| QUANTITY &#124; TAG | Accumulation end (last) block number, inclusive. Integer of a block number, or the string `"earliest"`, `"latest"` or `"pending"`, as in the [default block parameter](./klay/block.md#the-default-block-parameter).    |

**Return Value**

| Type | Description         |
| ---- | ------------------- |
| JSON | Rewards information |

**Example**

```javascript
> governance.getRewardsAccumulated(123400489,123416489)
{
    "jsonrpc": "2.0",
    "id": 1,
    "result": {
        "firstBlockTime": "2023-05-29 15:11:27 +0900 KST",
        "lastBlockTime": "2023-05-29 19:38:11 +0900 KST",
        "firstBlock": 123400489,
        "lastBlock": 123416489,
        "totalMinted": 102406400000000000000000,
        "totalTxFee": 1012877568458206944160,
        "totalBurntTxFee": 1012877568458206944160,
        "totalProposerRewards": 10240640000000000224014,
        "totalStakingRewards": 40962559999999999775986,
        "totalKFFRewards": 20481280000000000000000,
        "totalKCFRewards": 30721920000000000000000,
        "rewards": {
            "0x04185389ec237dba242888a5a28b5555d011a223": 341760000000000007476,
            "0x064ce4c3e8409a544ce91245f9f8cfc33bde8925": 341158409421920578070,
            "0x0bb09aab5276ae532e33caf69d00a624adbc3fdf": 4692517369325951639990,
            "0x0c41cce8ddaea235f97745a13207421dca7340fa": 341158442792400102695,
            "0x179679457f93094a4e7186abcb2089661e92fc22": 4670094563747132209866,
            "0x186de0382923086f73367bab16af09aeda4e54bf": 3344700808386003997995,
            "0x1a147924d0489fccf53471904dc271b9d20157a4": 812253494122089774069,
            "0x24e593fb29731e54905025c230727dc28d229f77": 341120033370479516086,
            "0x2b2a7a1d29a203f60e0a964fc64231265a49cd97": 405647783029499903389,
            "0x2fd3ff6e4ead7430ea25bab5e5b2b073492b7e6e": 4179365177477290146362,
            "0x4b87df856044f2580ca62f44f6e15121d7ebcc91": 943429290876805235278,
            "0x5459c9591c3c3f260eff1a538d84610015332c91": 399791330615756805978,
            "0x54e8bc489cee5ab638920cc80160d8095df846b1": 1342241347422787927227,
            "0x5ed9914689a2fafb55a0c99a1c10d2f911d37734": 1150518010638720583027,
            "0x5f1dbd747996d8d31e2ab0317be7ffffd155522a": 507972397569861326690,
            "0x75239993ac422a4e6a7441d5ab47ed6e91faf306": 9708690430353790307357,
            "0x758476368db33864b704f41cc63b8460f8e7d39a": 719558444429276229872,
            "0x85d82d811743b4b8f3c48f3e48a1664d1ffc2c10": 20481280000000000000000,
            "0x999999999939ba65abb254339eec0b2a0dac80e9": 2546664690927360639974,
            "0xac7f6f8a63733877a78917dc798ed7693095be7b": 976294207626140822860,
            "0xadb287e1f8405f085c740e791a3914f9b07acae0": 4834561973146129955927,
            "0xb89a760eb082dbae4f334a9374fa32e7b077e00d": 341120033370479516086,
            "0xbb121974208b9282e72cb0da7f48d8ae14dba954": 477271623157965876433,
            "0xc8e7053dc17bce47d2317718734ef087be40a023": 533654318603814390326,
            "0xcd7cd61f0b221a61405640b8ba10f1455cce6d51": 1153716971545888984956,
            "0xda5609a74470689a3b51cb53ee3c499b0f54f31a": 401005661421389210969,
            "0xdbd3fbdc9e1965855b773a4746f27165b787fe3c": 1153644257271028044532,
            "0xdc7dda990c08513962d5ae6dfb195b1f6879bfaf": 1954666498718499702479,
            "0xdd4c8d805fc110369d3b148a6692f283ffbdccd3": 30721920000000000000000,
            "0xdedbab7de9551a2bee78792638af67d59b8675c6": 1285976941809533886160,
            "0xe3d49ffc285c668425b2966b683776f632859efa": 714216865143954209314,
            "0xf786c3720a10cb48c8f12d0ac2086dcf227c7cde": 588428623678048468557
        }
    }
}
```
