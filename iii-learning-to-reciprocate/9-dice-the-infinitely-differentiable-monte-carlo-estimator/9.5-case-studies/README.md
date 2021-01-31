# 9.5 Case Studies

 이번 chapter의 가장 큰 contribution은 SCG에서 어느 차수의 gradient를 얻든 정확한 추정을 할 수 있도록 하는 방법론에 대한 것 이지만, 여기서 몇 개의 실험을 통해 이를 증명하려고 합니다. 이전 chapter에서 실험했던 IPD환경을 그대로 사용하는데, 이는 nontrivial하지만, value function을 analytic하게 계산도 가능한\(gradient estimation에 대한 검증이 필요하므로\) 장점이있습니다.  또한, 다른 agent의 learning step을 자신의 optimization term에 넣어서 해결할 수 있는 문제중에 하나이기 때문에 일리가 있습니다.

