# Abstract

 세상의 많은 문제들\(드론 컨트롤, 화물 운송\)은,  부분 관측 가능한\(POMDP : Particially Observable Markov Decision Process\) 상황에서의 Multi-Agent 환경에 놓여있습니다. 이런 환경을 풀어내기 위해선 Multi Agent Reinforcement Learning\(MARL\)에 대한 setting이 필요합니다. 게다가 machine learning system이 실제 상황에 적용되면서 서로에게 영향을 끼치는 상황에서, 효과적으로 문제에 대한 결정을 내리는 문제는 MARL 상황에 귀결됩니다. 이 곳에서는 여러 상황에 대한 Deep Multi-Agent Reinforcement Learning\(DMARL\)에 대한 방법을 평가하고 발전시키는 것을 주로 배우게 될 것입니다.

 이러한 문제에는 협력하는\(Collaborate\) 문제 , 소통하는\(Commuicate\) 문제, 상호간의 문제\(Reciprocate\)가 있습니다. 대부분의 실제 상황에서는 결과적으로 나오는 정책\(policy\)은 agent 개별의 행동과 지역적인 관찰에 의존합니다. 그러나 많은 케이스에서 이런 지역적인 관찰을 중앙에서 통제하는 training을 진행할 수 있습니다. 예를들면, 정책을 학습시키면서 시뮬레이터내에서 추가적인 state 정보를 주거나, agent간의 communication을 하도록 하는 것 입니다.

 첫 장은 collaborate 상황에서의 common objective를 달성하기 위한 challenge 들에 대해 기술합니다. 여기서의 어려움 중 하나는 multi-agent 상황에서 어떤 agent의 행동이 reward에 직접 영향을 미쳤는지 입니다\(multi-agent credit assignment\). 모든 agent들의 action은 episode내에서 reward에 영향을 미치기 때문에, 한 agent의 행동에 대한 평가를 분리해서 해내기가 어려움이 있습니다. 여기서는 이런 문제를 풀기 위해Counterfactual Multi-Agent Policy Gradients\(COMA\) 를 제시합니다. COMA에서는 Counterfactual baseline 을 통해 각자의 agent가 그들의 action이 팀내에서 미치는 영향에 대해 평가합니다. 

 또한, 조정된 action의 common knowledge에 대한 중요도에 대해서 다음과 같은 이론으로 정리하여 제시합니다. Multi-Agent Common Knowledge Reinforcement Learning\(MACKRL\)는 agent들의 subgroup들이 서로 같은 common knowledge를 공유하는 계층적인 controllers를 사용합니다. 이렇게 하는 이유는 그룹의 action이 joint된 space를 가지거나 많은 common knowledge를 가진 subgroup에게 기능을 위임하기 위해서입니다.

 문제를 푸는 핵심의 인사이트는 모든 정책은 여전히 decentralized되어 처리될 수 있다는 점입니다. 모든 agent는 독립적으로 그룹의 common knowledge를 추론할 수 있기 때문입니다. MARL에서는 모든 agent가 동시에 environment에 대해 배우고 이것은 다른 agent들에 대한 간섭에 의해 non-stationary합니다. 이것이 MARL에서의 replay buffer를 사용하는데 어려움을 겪게 만드는데, 이런 문제를 결과적으로 해소하기 위한 \(수집된 시간과 그 당시에 대한 정책의 랜덤성을 고려해서\)replay buffer에서 사용할 수 있는 metadata fingerprint를 제시하고 평가합니다.

지금까지, agent들이 모두 서로 소통이 없이 decentralised 되어서 action을 취하는 상황에 대해 가정했는데, 두번째 파트에서는 agent가  communication protocol을 배울 수 있는 세가지 다른 방법을 제시합다.

첫번째 방법으로는 Differentiable Inter-Agent Learning\(DIAL\)입니다. 여기서는 centralized training을 통해 discrete한 communication channel들 중에 주어진 문제를 잘 풀어낼 수 있는 알맞는 communication protocol을 찾아 구별된 방법\(differentiation\)을 사용합니다.

둘째로는 Reinforced Inter-Agent Learning\(RIAL\)가 있는데, RIAL는 RL을 단순히 protocol을 배우는 수단으로 사용하는 것입니다. 이 방법들은 관찰한 agent들의 행동에 대해 직접적인 이유를 알진 못합니다. 하지만다른 agent의 action을 봤을 때, 즉각적으로 왜 그런 행동이 실행되고, 그것이 state에 대해 무엇을 의미하는가들에 대해 가설을 세울 수 있게 됩니다.

 셋째로는 이러한 인사이트에 영감을 받아 만든, Baysian Action Decoder\(BAD\)가 있습니다. 이는 agents가 직접적으로 Baysian update 근사와 관찰된 action과 communication actions을 통해 communication 방법을 배우면서 다른 agents의 정책을 고려합니다.

위의 두 이론은 모든 agents가 team reward를 최적화하지만 실제로는 다른 agent 끼리 경쟁하는 경우가 있습니다. 이 경우에는 위의 알고리즘들이 안좋은 성능을 보였기 때문에 또다른 알고리즘을 통해 해결하는데 이것을 Learning with Opponents-Learning Awareness\(LOLA\)라고 부릅니다. LOLA에서 agent들은 환경내에 있는 다른 agent들을 염두에 두고 자신에게 유리하게 상대를 행동하도록 하는 policy를 찾습니다.

defact-defact 균형을 이루는 죄수의 딜레마보다, LOLA는 tit-for-tat의 전략을 형성합니다. LOLA는 효과적으로 상호작용을 하면서, 전체적으로 높은 reward를 받는데 집중합니다.

또 Infinitely Differentiable Monte-Carlo estimator\(DiCE\)를 소개하는데, 계산적인 방법인데, 한 agent가 다른 agent의 학습되는 행동을 설명할 때의 gradients를 발생시키는 방법입니다.

LOLA와 DiCE는 모두 광범위한 목적의 목적식을 갖는데, stochastic computation graphs를 추정함으로써, gradient를 발생시키는 역할을 합다.













### Centralised execution vs Decentralised execution

* **Centralised execution**
  * 한 controller가 다른 요소를 모두 제어할 수 있게 되어있음
  * DMARL에서는 agent가 모든 정보를 알고 제어할 수있음을 나타냅니다.
* **Decentralised execution**
  * 낮은 단계의 controller에게 명령권을 줍니다.  
  * DMARL에서는 agent가 자신의 부분적인 정보만을 이용하여 제어함을 말합니다. 

#### 

#### reference:

* [https://www.doctrine.af.mil/Portals/61/documents/Volume\_1/V1-D81-CC-DE.PDF](https://www.doctrine.af.mil/Portals/61/documents/Volume_1/V1-D81-CC-DE.PDF)



