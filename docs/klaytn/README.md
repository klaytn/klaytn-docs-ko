# Overview <a id="overview"></a>

클레이튼은 엔터프라이즈급 안정성을 목표로 고도로 최적화된, BFT 알고리즘 기반 퍼블릭 블록체인입니다. 주요 디자인 목표는 다음과 같습니다.

- 즉각적인 완결성
- 실제 사용 사례에서 문제 없는 높은 TPS
- Blockchain 애플리케이션 실행 비용 절감
- 사용자의 진입 장벽을 낮춤
- 산업계의 블록체인 기술 도입 촉진

클레이튼은 2019년 6월 27일에 다음과 같은 사양으로 메인넷 [Cypress](https://scope.klaytn.com/)을 출시했습니다.

- 1초의 블록 생성 및 확인(Confirm) 시간
- 초당 4,000 건의 트랜잭션
- 이더리움 1/10 수준의 낮은 가스비
- EVM(이더리움 가상머신)을 구동하여 솔리디티 컨트랙트 실행을 지원함
- 세계적으로 평판이 높은 19개 기업이 모여 최초의 클레이튼 거버넌스 카운슬을 결성하고 컨센서스 노드 운영을 시작함. 컨센서스에 참여하는 노드 개수 현황은 [Klaytnscope](https://scope.klaytn.com/)에서 볼 수 있습니다.
- 50개 이상의 초기 서비스 파트너가 클레이튼에서 블록체인 애플리케이션을 출시하려고 준비

## 클레이튼: 개관 <a id="klaytn-the-big-picture"></a>

Klaytn은 역할 및 목적에 따라 세 개의 논리적 서브네트워크로 분할할 수 있습니다. 아래 그림은 Klaytn 생태계의 대략적인 구조를 보여줍니다.

![클레이튼 생태계 및 논리적 서브 네트워크 (CCN, ENN, SCN)](images/klaytn_network_overview.png)

### 코어 셀 네트워크(CCN) <a id="core-cell-network-ccn"></a>

CCN은 엔드포인트 노드(EN)를 통해 제출된 트랜잭션을 확인하고 실행하는 코어 셀(CC, Core Cell)로 구성됩니다. CCN은 네트워크 전체에서 블록을 생성하고 전파합니다.

### 엔드포인트 노드 네트워크(ENN) <a id="endpoint-node-network-enn"></a>

ENN은 주로 트랜잭션을 생성하고, RPC API 요청을 처리하며, 서비스체인의 데이터 요청을 처리하는 엔드포인트 노드(EN)로 구성됩니다.

### 서비스체인 네트워크(SCN) <a id="service-chain-network-scn"></a>

SCN은 탈중앙화 애플리케이션(dApp)에 의해 독립적으로 운영되는 보조 블록체인들로 구성된 클레이튼 서브네트워크입니다. 서비스 체인은 EN을 통해 메인 체인에 연결됩니다.

**코어 셀 네트워크**와 **엔드포인트 노드 네트워크**은 클레이튼 메인체인과 메인넷을 구성합니다. 블록체인 애플리케이션은 클레이튼 메인 체인인 Cypress에서 실행하거나 자체적인 블록체인인 **서비스체인**에서 작동할 수 있습니다. 높은 TPS와 설정 변경이 가능한 네트워크 정책을 가진 전용 실행 환경을 원한다면 서비스체인을 사용하는 것을 추천합니다.

> 애플리케이션을 위한 서비스 체인을 설정하려면 [서비스 체인의 설치 및 운영 가이드](./../installation-guide/deployment/service-chain/getting-started/README.md)를 읽어보세요.

## 클레이튼 네트워크 토폴로지 <a id="klaytn-network-topology"></a>

이 장에서는 클레이튼 메인체인의 네트워크 토폴로지에 대해 설명합니다. 네트워크 성능을 최적화하기 위해 역할 기반 노드 유형에 따라 계층화된 네트워크 아키텍처가 구현되었습니다.

### 역할 기반 노드 유형 <a id="role-based-node-types"></a>

클레이튼 메인체인 네트워크 토폴로지를 살펴보기 전에 다양한 유형의 클레이튼 노드를 알아보겠습니다.

#### 코어 셀(CC): 컨센서스 노드(CN) + 프록시 노드(PN) <a id="core-cell-cc-consensus-node-cn-proxy-node-pn"></a>
코어 셀 (CC) 은 하나의 <strong>컨센서스 노드 (CN)<strong>와 두 개의 <strong>프록시 노드 (PNs)<strong>로 구성됩니다. 합의 노드는 블록 생성 프로세서에 참여하고, 프록시 노드는 네트워크에 인터페이스를 제공합니다. PN은 트랜잭션 요청을 합의 노드로 전송하고 블록을 엔드포인트 노드로 전파합니다.

> Core Cell Operator가 되기에 관심이 있다면, [Core Cell의 설치 및 운영 가이드를 읽어보세요](./../installation-guide/deployment/core-cell/installation-guide/before-you-install.md).

#### 엔드포인트 노드 (EN) <a id="endpoint-node-en"></a>

Klaytn 네트워크의 엔드포인트로서, RPC API 요청을 처리하고 서비스 체인과의 데이터 전송을 담당합니다.

> 애플리케이션을 위한 엔드포인트 노드를 설정하려면, [엔드포인트 노드의 설치 및 운영 가이드](./../installation-guide/deployment/endpoint-node/README.md)를 읽어보세요.

#### 부트노드 <a id="bootnode"></a>

부트노드는 Klaytn이 새로운 노드가 네트워크에 등록하고 다른 노드와 연결할 수 있도록 도와주는 특별한 유형의 노드입니다. CN 부트노드는 CNN 내부에 위치해 있고 공개되지 않은 반면, PN과 EN 부트노드는 공개적으로 볼 수 있습니다.  PN 부트노드는 허가된 PN만 등록할 수 있게 하고, 적합한 PN들이 EN과 연결될 수 있도록 합니다.  EN 부트노드는 EN들에게 어떤 PN에 연결해야 하는지에 대한 정보를 제공합니다. <0>

### 계층화된 네트워크 <a id="tiered-networks"></a>

CN, PN, 그리고 EN은 각각 논리적 네트워크를 형성하며, 이는 컨센서스 노드 네트워크 (CNN), 프록시 노드 네트워크 (PNN), 그리고 엔드포인트 노드 네트워크 (ENN) 입니다.

아래의 그림은 Klaytn 메인넷의 전체 토폴로지를 보여주며, 여기에서 코어 셀 네트워크 (CCN) 은 컨센서스 노드 네트워크 (CNN) 과 프록시 노드 네트워크 (PNN) 으로 더 세분화됩니다. 엔드포인트 노드 네트워크 (ENN) 는 PNN에 직접 연결된 주변 네트워크로도 표시됩니다.

![Klaytn Main Chain Physical Topology and Tiered Architecture (CNN, PNN, and ENN)](images/klaytn_network_node.png)


#### 컨센서스 노드 네트워크<a id="consensus-node-network-cnn"></a>

CN들은 CNN이라고 불리는 자체적으로 완전 연결망(full-mesh network) 을 형성합니다. CNN은 WAN(wide area network) 상에서 BFT를 적용하고, 각 CN이 충분한 성능 수준에서 BFT 합의를 수행하기 위해 [엄격한 하드웨어와 네트워크 리소스 요구 사항](./../installation-guide/deployment/core-cell/system-requirements.md)을 충족해야 합니다.

#### 프록시 노드 네트워크 (PNN) <a id="proxy-node-network-pnn"></a>

PNN은 PN(프록시 노드) 들로 구성됩니다. 일반적으로, PN들은 이웃하는 코어 셀에 있는 하나의 PN과만 연결을 유지합니다. 피어 연결의 수는 네트워크 구성에 따라 변경될 수 있습니다.

#### 엔드포인트 노드 네트워크 (ENN) <a id="endpoint-node-network-enn"></a>

가장 바깥쪽의 하위 네트워크인 ENN은 서로 연결된 EN(엔드포인트 노드) 들만으로 구성되며, 일부 PN에도 연결됩니다.


## 블록 생성 및 전파 <a id="block-generation-and-propagation"></a>

블록 생성과 전파 설계는 사용되는 합의 알고리즘과 함께 블록체인 플랫폼의 지연 시간을 줄이는 데 중요한 역할을 합니다.

### 블록 생성 주기 <a id="block-generation-cycle"></a>

클레이튼에서의 '라운드'는 블록 생성 주기입니다.</3> 각 라운드마다 새로운 블록을 생성하며, 바로 다음에 새로운 라운드가 시작됩니다. Klaytn은 각 라운드가 대략 1초가 되도록 목표를 설정하고 있지만, 블록 생성 간격은 네트워크 트래픽과 노드 운영 상태에 영향을 받을 수 있습니다.

#### 제안자와 위원회 선택 <a id="proposer-and-committee-selection"></a>

각 라운드에서 Klaytn은 무작위로 하지만 결정론적으로 블록을 생성할 제안자로 컨센서스 노드 (CN) 를 선택하고, 그 라운드에 대한 위원회로 CN 그룹을 선택합니다. Klaytn은 제안자나 위원회의 선택에 직접 관여하지 않습니다. 대신 각 CN은 가장 최근의 블록 헤더에서 파생된 난수를 사용하여 이 라운드에 대해 선택되었는지(또는 선택되지 않았는지) 증명하는 암호화 작업을 수행합니다. 위원회의 크기는 비잔틴 공격에 대한 저항력이 있어야 합니다. 만약 CNN의 크기가 작다면, 모든 CN(제안자 제외)은 위원회 멤버로 선택될 자격이 있습니다.

#### 블록 제안 및 검증 <a id="block-proposal-and-validation"></a>

선택되면 제안자는 모든 CN에게 그 라운드의 선택 증명(즉, 제안자의 공개 키로 검증 가능한 암호화 증명)을 전송합니다. 그 후에는, 해당 라운드의 위원회로 선택된 CN들이 제안자에게 자신의 선택 증명을 응답하여 새로 제안될 블록을 누구에게 전송할지 알립니다. 제안자는 그 후에 자신의 트랜잭션 풀에서 트랜잭션들을 선택하고 이를 정렬하여 블록을 생성합니다. 마지막으로, 제안자는 위원회와 합의를 실행하여 새롭게 생성된 블록을 승인하고 확정합니다. Klaytn은 계속해서 더 높은 보안성과 효율성을 달성하기 위해 합의 알고리즘을 개선할 계획입니다.

### 블록 전파 <a id="block-propagation"></a>

제안된 블록은 위원회 구성원의 3분의 2 이상으로부터 서명을 받아야만 성공적으로 확정됩니다.</3> 위원회가 합의에 도달하면, 새로운 블록은 모든 CN에게 전파되고 컨센서스 라운드가 종료됩니다. 새로운 블록이 모든 CN에게 전파되면, 새롭게 생성된 블록의 정보는 PNN을 통해 ENN에 블록 헤더와 바디 데이터를 전달함으로써 모든 Klaytn 네트워크 참가자에게 제공될 수 있습니다.

## 공개 및 공개 검증 <a id="public-disclosure-and-open-validation"></a>

Klaytn 네트워크의 서비스 제공자와 사용자는 블록 생성 결과를 자유롭게 검증하고 CN 위원회가 적절한 절차에 따라 블록을 생성했는지 확인할 수 있습니다. 이러한 검증에는 블록 헤더에 위원회 서명의 3분의 2 이상을 포함하는지 확인하는 작업이 포함됩니다. 모든 CN들은 공개 검증을 지원해야 하며, 그들의 공개 키(블록에 서명하는 데 사용됨)를 공개적으로 접근 가능한 공간(예: 블록 헤더)에 게시해야 합니다. 공개 검증은 투명성을 증진시키고 검열을 방지하며 악의적인 행동을 예방합니다.

## 블록과 트랜잭션을 위한 분리된 전파 채널 (멀티채널 전파) <a id="separated-propagation-channels-for-blocks-and-transactions-multichannel-propagat"></a>

네트워크의 지연 시간은 그 정체도에 크게 영향을 받습니다. 네트워크의 처리량이 일정하다고 가정할 때, 트랜잭션의 증가는 네트워크의 지연 시간이 비례적으로 지연됩니다. 지연 시간은 dApps에서 중요한 문제입니다. 레거시 모바일 앱이나 웹 서비스의 일반적인 사용자들은 몇 초 이상의 응답 시간을 참을 수 없으며, 블록체인 서비스도 더 높은 사용자 인내를 가정할 이유가 없습니다.

Klaytn은 네트워크의 지연 문제를 처리하기 위해 멀티 접근 방식을 채택합니다. 트랜잭션과 블록에 대한 별도의 전파 채널을 할당함으로써, Klaytn 네트워크는 높은 트랜잭션 수로 인한 심각한 정체 상황에서도 새로 생성된 블록을 적시에 전파할 수 있습니다. 이렇게 함으로써 Klaytn은 그 네트워크의 dApps이 간헐적인 네트워크 트래픽 급증에도 불구하고 최종 사용자의 요청에 신속하게 응답할 수 있도록 보장합니다.

## 블록 보상 <a id="block-rewards"></a>

각 라운드마다 블록 보상(6.4개의 새로 생성된 KLAY와 블록을 처리하기 위해 지불된 트랜잭션 수수료의 합계) 이 미리 설정된 분배 비율에 따라 네트워크 참가자에게 분배됩니다. 새로 생성된 블록의 제안자는 CN에게 주어질 보상의 100%를 받을 것이며, 위원회는 보상을 받지 않을 것입니다. 제안자로 선택될 확률은 CN이 플랫폼에 스테이킹한 KLAY의 양에 영향을 받는다는 것에 유의해야 합니다. 즉, 더 많은 KLAY를 투자한 CN은 확률적으로 더 많은 보상을 받을 것입니다. 블록 보상 분배의 자세한 내용은 [Klaytn Token Economy](design/token-economy.md) 섹션에서 찾을 수 있습니다.
