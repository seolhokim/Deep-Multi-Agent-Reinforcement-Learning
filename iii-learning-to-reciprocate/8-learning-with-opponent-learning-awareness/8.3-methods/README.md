# 8.3 Methods

이번 Section에서는 naive learner로 시작해서 LOLA까지 알아보도록 하겠습니다. agent가 Expected discounted reward sum의 정확한 hessian을 얻을 수 있는 상황에 대해 8.3.2에서 정의하고, 그렇지 못할 때에 대해 8.3.3에서 정의합니다. 8.3.4에선 opponent의 modeling에 대해 모를 때를 가정한 상황에 대해 정의하고, 8.3.5에서는 상대의 Expected discounted reward sum을 1차 근사가 아닌 더 정확하게 근사했을 때에 대해 얘기합니다.

