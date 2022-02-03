# 메타마스크 연동 <a id="connecting-metamask"></a>

> **참고**: MetaMask는 주로 이더리움 지갑으로서 사용되지만, 동일한 주소 구조를 지닌 Klaytn과도 호환 가능합니다. Klaytn은 브라우저 익스텐션 지갑 [Kaikas](../developer-tools/README.md#kaikas)도 지원합니다. 따라서 Remix를 제외하면 MetaMask와 거의 동일한 기능을 제공합니다.

## 1단계: 메타마스크 설치하기 <a id="install-metamask"></a>

* Chrome 웹브라우저 기준으로 설명합니다. ([**크롬 설치하기**](https://www.google.com/intl/en_us/chrome/))

* Chrome 확장 프로그램 탭에서 [**MetaMask 확장 프로그램**](https://chrome.google.com/webstore/detail/metamask/nkbihfbeogaeaoehlefnkodbefgpgknn?hl=en)을 추가합니다.

  > **참고:** 다른 브라우저를 사용하는 경우 별도 설치가 필요할 수 있습니다.

* Chrome 검색 바 오른쪽 아이콘을 클릭하면 메타마스크를 실행시킬 수 있습니다.

## 2단계: 메타마스크 지갑 생성 <a id="generate-a-metamask"></a>

![Create a Wallet](./img/new-to-metamask.png)

* [지갑 생성] 버튼을 클릭합니다.
* 암호를 생성합니다.
* 12개의 단어로 구성된 시드 구문이 주어지면 이를 안전한 곳에 적습니다.

  > **참고:** 해당 구문을 알아야만 지갑 복구가 가능합니다. 타인에게 노출 시 계정의 자금을 모두 잃을 수 있습니다. 그렇기에 시드 구문은 수기로 적어두거나 외부 연결이 차단된 장치에 기록하기를 권장합니다.

![Seed phrase and Wallet](./img/metamask-secret-backup.png)

## 3단계: Klaytn 네트워크 연결 <a id="connect-to-klaytn-network"></a>

* 이더리움 메인넷 상태인 네트워크 탭을 클릭해 [맞춤형 RPC]를 선택합니다.

* 연결할 Klaytn 체인의 EN 정보를 입력합니다.

  * Cypress
    * 네트워크 이름: Klaytn Cypress
    * 새 RPC URL: (기본값: [https://public-node-api.klaytnapi.com/v1/cypress](https://public-node-api.klaytnapi.com/v1/cypress))
    * 블록 탐색기 URL: [https://scope.klaytn.com/](https://scope.klaytn.com/)
    * 체인 ID: 8217
  * Baobab
    * 네트워크 이름: Klaytn Baobab
    * 새 RPC URL: [https://api.baobab.klaytn.net:8651](https://api.baobab.klaytn.net:8651) (Default: [http://localhost:8551](http://localhost:8551/))
    * 블록 탐색기 URL: [https://baobab.scope.klaytn.com/](https://baobab.scope.klaytn.com/)
    * 체인 ID: 1001
  * 공통
    * 통화 기호: KLAY


* [Save]를 클릭하면 Klaytn Cypress 네트워크가 추가됩니다.

![Network Setup and Custom RPC](./img/metamask-add-cypress-1.png) ![Network Setup and Custom RPC](./img/metamask-add-cypress-2.png)

## 4단계: KLAY 보내기 <a id="send-klay"></a>
**Note:** KLAY를 보내기 위해서는 트랜잭션을 발생시켜야 하며, 이 과정은 KLAY를 요구합니다. Klaytn Baobab 네트워크를 사용하는 경우, KLAY가 부족할 시 이 단계를 따르세요.

* 우측 상단 아이콘 탭에서 [Create Account]을 클릭하여 새로운 계정을 생성합니다.
* 계정 주소를 복사합니다.

![계정 주소를 복사하세요.](./img/metamask-copy-address.png)

* 드롭다운 메뉴에서 첫 번째 계정으로 전환합니다.
* [Send]에서 받을 계정 주소와 KLAY 수량을 입력한 후 [Next]을 클릭하여 송금을 진행합니다. > **Note:** Klaytn의 가스비는 고정되어 있습니다. 임의적으로 가스비를 변경할 경우 트랜잭션이 실패할 수 있습니다. [Activity] 탭에서 거래 내역을 확인할 수 있습니다.

![거래 내역](./img/metamask-send-klay.png)

## Klaytn Baobab 네트워크 - 트랜잭션을 위한 KLAY 충전<a id="obtain-klay-to-make-a-transaction"></a>
> **참고:** 예제는 테스트넷(Baobab)의 Public EN으로 네트워크에 연결하였습니다. 테스트 시에는 Baobab을 사용하세요.

* [Save]을 클릭하면 Klaytn Baobab 네트워크가 추가됩니다.

![Network Setup and Custom RPC](./img/metamask-add-baobab.png)

* Klaytn Wallet의 연동 상태를 확인하기 위해서는 송금에 사용될 KLAY가 필요합니다.
* 우측 상단 아이콘 아래 탭에서 [Account details]를 클릭합니다.
* [Export Private Key]를 클릭하여 개인 키를 획득합니다.

![개인 키 내보내기](./img/metamask-obtain-private-key.png)

* Baobab 테스트넷에서는 [**Klaytn Faucet**](https://baobab.wallet.klaytn.com/access?next=faucet)을 이용하여 테스트에 필요한 KLAY를 받을 수 있습니다.
* Klaytn Wallet에서 개인 키를 입력한 후 [Access] 버튼을 클릭해 로그인합니다. (개인 키 앞에 0x를 기입합니다.)
* [Run Faucet] 버튼을 클릭하세요. 5 테스트넷 KLAY가 전송되고 잔액이 업데이트됩니다. Faucet 기능은 계정당 1일 1회, 24시간마다 한 번씩 실행할 수 있습니다.

![계정 로그인과 KLAY Faucet](./img/metamask-klay-faucet.png)

* 메타마스크로 돌아와 보유 KLAY를 확인합니다.
* Klaytn Baobab 네트워크의 경우 Step 4를 따르세요.

![Balance](./img/metamask-klay-received.png)