# 8.4 Experimental Setup

이번 section에서는 NL과 LOLA agent들에 대한 비교를 합니다. 8.4.1 에서는 2개의 대표적인 infinitely iterated game인 iterated prisoners dilemma와 iterated  matching pennies에 대해 실험합니다. 각 환경은 step마다 각 agent의 한 action만을받고, 이에 대한 각 agent의 discounted future return을 받게 됩니다. 8.4.2에선 Coin Game을 하는데, 이는 좀 더 어려운 환경입니다. 각 step마다 agent는 일련의 action을 취해야하지만, discounted future reward가 정확히 계산되지 않을 수 있습니다. 

 LOLA를 사용한 policy gradient 실험은 off-line learning으로, agent들은 많은 병렬화된 환경에서 최근의 policies를 가지고 학습하게 됩니다. policies는 각 episode마다 변하지않고 유지되며, episode와 episode사이에서 학습이 이루어집니다. 

