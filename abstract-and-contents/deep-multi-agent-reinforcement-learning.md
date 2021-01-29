# Abstract

 드론 컨트롤, 화물 운송과 같은 세상의 많은 문제들은,  부분 관측 가능한\(POMDP : Particially Observable Markov Decision Process\) 상황에서의 Multi-Agent 환경에 놓여있습니다. 더욱이, 더 많은 머신러닝 시스템이 실제 상황에 적용됨에따라, agent는 서로에게 영향을 미치기 시작하고 이를 multi agent로 문제를 정의하는 것에 대한 중요성이 커져만 가고 있습니다. 이 번역본에서는 아래서 설명하는 상황들에 대한 문제를 해결하기 위한 Deep Multi-Agent Reinforcement Learning\(DMARL\)의 method들을 주로 배우게 될 것입니다.

 여기서 주로 다룰 문제는 협력하는\(Collaborate\) 문제 , 소통하는\(Communicate\) 문제, 상호간의 영향을 주는\(Reciprocate\) 문제로 정의합니다. 이 모든 문제에서 공통적으로 쓰이는 테크닉으로는 centralized training, decentralized execution입니다. 학습중엔 모든 state를 볼 수있는 critic이 agent를 올바르게 학습할 수 있도록 돕고, 결과적으로 나오는 policy는 agent 개별의 행동과 지역적인 관찰으로도 충분히 상황을 이해하고 해결할 수 있도록 학습한다는 것입니다. 예를 들면, agent가 학습중에서는 자신의 관찰외에도 시뮬레이터내에서 추가적인 state 정보를 주거나, agent간의 communication을 하도록 돕는 학습 방법입니다. 이는 많은 상황에서 적용 가능하면서 agent의 성능을 높여줄 수 있는 좋은 방법중에 하나로, 현재 많은 MARL method들이 사용하고 있는 테크닉입니다.

 chapter 3에서는 collaborate 상황에서의 common objective를 달성하기 위한 문제들에 대해 기술합니다. 여기서의 어려움 중 하나는 multi-agent 상황에서 어떤 agent의 행동이 reward에 직접 영향을 미쳤는지 입니다\(multi-agent credit assignment\). 모든 agent들의 action은 episode내에서 reward에 영향을 미치기 때문에, 한 agent의 행동에 대한 평가를 분리해서 해내기가 어려움이 있습니다. 여기서는 이런 문제를 풀기 위해Counterfactual Multi-Agent Policy Gradients\(COMA\) 를 제시합니다. COMA에서는 Counterfactual baseline 을 통해 각 agent의 action이 팀내에서 미치는 영향에 대해 평가합니다. 

  chapter 4에서는 agent사이에서의 common knowledge에 대한 중요도에 대해서 다음과 같은 이론으로 정리하여 제시합니다. Multi-Agent Common Knowledge Reinforcement Learning\(MACKRL\)는 agent들의 subgroup들이 서로 같은 common knowledge를 공유하는 계층적인 controllers를 사용합니다. 이렇게 하는 이유는 그룹의 action이 joint된 space를 가지거나 많은 common knowledge를 가진 subgroup에게 기능을 위임하기 위해서입니다.

  chapter 5에서는 MARL 상황에서는 각 agent가 action을 취하는 행동이 environment를 non-stationary하게 만들어 replay buffer를 그대로 사용하는 것은 학습하기 어렵게 만듭니다. 이 때 어떻게 replay buffer를 이용할 수 있을지에 대해 설명합니다. 

  part 1\(chapter 3~5\)까진 agent들이 모두 서로 소통이 없이 decentralized 되어서 action을 취하는 상황에 대해 가정했는데, part 2\(chapter 6~7\)에서는 agent가 communication protocol을 배울 수 있는 세가지 다른 방법을 제시합니다. 

 첫번째 방법으로는 Reinforced Inter-Agent Learning\(RIAL\)가 있습니다. 이는 environment에 영향을 주지 않는 message를 agent끼리 주고받는 방식으로 communication이 이루어집니다.

 두번째 방법으로는 Differentiable Inter-Agent Learning\(DIAL\)입니다. 여기서도 message를 사용하지만, RIAL는 message를 optimization term에 넣어 RIAL보다 섬세하게 communication protocol을 배울 수 있도록합니다.

 세번째 방법으로는 Baysian Action Decoder\(BAD\)를 제시합니다. 이는 agent의 environment에 영향을 주는 action 자체를 communication 방법으로 사용하는 경우로 각각의 agent가 관찰한 불완전한 정보에 대한 정보를 어떻게 활용할 수 있을지에 대해 설명합니다.

위의 part 1과 part 2에서는 모든 agents가 team reward를 최적화했지만 general-sum\(win-win혹은 lose-lose도 가능한\)경우에 대해 part 3에서 설명합니다. 또, 그를 해결할 Learning with Opponents-Learning Awareness\(LOLA\)라는 method를 제시합니다. LOLA에서 agent는 자신의 optimization term에 상대의 policy의 변화를 고려합니다. defact-defact 균형을 이루는 죄수의 딜레마보다, LOLA는 tit-for-tat의 전략을 형성합니다. LOLA는 효과적으로 상호작용을 하면서, 전체적으로 높은 reward를 받는데 집중합니다.

LOLA에서 상대방의 policy를 근사해야하기 때문에 높은 차수의 gradient가 발생하는데 이를 좀더 정확히 근사하기 위해 Infinitely Differentiable Monte-Carlo estimator\(DiCE\)를 소개하는데, 이는 높은 차수의 정확한 gradients를 추정하는 방법으로 LOLA에 적용되었을 때 성능을 개선시키는 것을 보였습니다.

