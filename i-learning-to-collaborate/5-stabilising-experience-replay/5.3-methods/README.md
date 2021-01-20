# 5.3 Methods



이 chapter에서는 Replay Memory를 MARL에 적용할 수 있는 두가지 효과적인 방법을 제시합니다.

* 첫째로, Replay Memory내의 data를 off-environment data로 취급하는 것입니다. off policy에서는 policy에 의해 등장하는 state distribution의 차이 때문에 Importance Sampling을 사용했다면, 이번에는 agent 입장에서의 다른 agent들의 joint action에 대해 distribution이 달라져 그에 대한 Importance Sampling을 진행합니다. 
* 둘째로, Hyper Q-learning에 의해 영감을 받은 접근법을 소개하는데, 이는 각 agent가 다른 agent의 policy들을 관찰하며 추정하여 non-stationary를 피합니다. 반면에 Q-function의 space가 커질 때 이를 감당할 수 없는데, 여기서는 작은 차원의 fingerprint를 이전의 한계를 해결합니다.

