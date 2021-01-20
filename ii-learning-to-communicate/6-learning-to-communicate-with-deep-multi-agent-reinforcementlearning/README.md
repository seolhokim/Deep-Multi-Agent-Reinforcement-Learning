# 6. Learning to Communicate with Deep Multi-Agent ReinforcementLearning

지금까지 agent끼리 어떤 특별한 communication이 없는 MARL의 해결에 대해 집중하였습니다. 하지만, communication은 MARL에서 해결되어야 할 매우 중요한 문제라는 것에는 의견이 없을 것입니다. 이를 해결하기 위해 아직도 많은 연구들이 진행되고 있지만 아직도 많은 물음이 남아있고 토론이 진행중입니다. 

최근 몇 십년간의 Neural Network의 비약적인 발전으로 인해 이러한 토론에서 새로운 시각이 등장했는데, 어떻게 agent가 협력하기 위해 communication protocol을 발견할 수 있을까? 무엇이 agent들에게 그런 능력을 제공할 수 있을까? communication을 배우는 agent의 성공 또는 실패에서 얻을 수 있는 통찰력은 무엇인가? 등이 있습니다.

이번 chapter에서는 이러한 물음에 대해 답하기 위한 첫걸음을 뗍니다. 첫째로 communication이 필요한 MARL 벤치마크를 제안하고, 그 것을 해결할 알고리즘들을 제안하고, 마지막으로 어떻게 그 알고리즘이 배울수 있었는지, 혹은 학습하는데 실패했는지에 대해 분석합니다.

여기선 fully cooperative하고, partially observable하고 sequential multi-agent decision making problems한 일들을 고려합니다. 

* 모든 agent는 같은 discounted sum of reward를 공유하고 이를 maximize하는 것이 목표입니다.
* 어떤 agent도 환경에 주어진 Markov state를 관측할 수 없지만, 각자 agent가 이와 상관관계가 있는 자신 개인의 observation을 가집니다.
* 각 agent는 environment에 영향을 주는 action을 취하고, 각 agent는 그들의 동료 agent들과 제한된 cheap-talk channel을 통해 문제를 해결합니다.

결과적으로 환경의 부분 관측한 특성과, communication할 때 제한된 특성에 의해 agent는 협력하기 위해 어떻게 communication을 진행할지에 대해 배우게 됩니다.

이전처럼, centralized learning, decentralized execution방식을 택하는데, 이는 학습할 때는 agent끼리 communication하는 것이 학습동안에는 centralized algorithm을 통해 제한되지않고 execution때 배운 communication channel을 이용하는 것을 의미합니다. 모든 실제 문제를 이처럼 centralized learning, decentralized execution방식으로 해결할 수 없겠지만, 많은 분야에서 이를 적용하고 통용되고 있습니다.

이러한 문제를 해결하기 위해 두가지 방식을 제안하는데, 첫째로, Reinforced inter-agent learning\(RIAL\)가 있습니다. 이는 부분 관측을 해결하기 위해 DRQN algorithm을 사용하고, IQL을 사용하며, 모든 agent끼리의 parameter를 sharing하는 특성을 가집니다.

두번째로, Differentiable inter-agent learning\(DIAL\)을 제시하는데, 이는 centralized learning은 그냥 parameter sharing하는 것보다 더 학습을 개선시킬 수 있다고 보았습니다. 그래서 communication이 단순히 end-to-end로 sharing된 agent 그룹 안에서 일어나는게 아닌, agent끼리 개별로 어떻게 communication을 할지를 배우게 됩니다. 그리하여 message를 통한 communication 접근 방식은 centralized training동안 agent끼리의 message가 넘어다니며, bottleneck을 연결하는 작업으로 여겨집니다. 이는 agent끼리 gradient가 직접 통하지 않고, gradient가 communication channel을 통해  agent사이에서 end-to-end로 학습될 수 있는 시스템을 만들기 위해 흐릅니다.

그리고 실험적으로 설명했던 방식들이 여기서 세운 벤치마크를 해결하고 종종 우아한 communication protocols을 만드는 것도 볼 수 있었습니다. 이 저자가 알기로는 이는 communication protocol을 Neural Network로 해결하기 위한 첫번째 시도로알고있고, 이 결과는 centralized learning이 communication protocol을 배우는데 효과적인 툴임을 알립니다. 마지막으로 experimental section에서 communication을 배우기 위한 필수적인 엔지니어링적인 요소를 연구해놓았습니다.

