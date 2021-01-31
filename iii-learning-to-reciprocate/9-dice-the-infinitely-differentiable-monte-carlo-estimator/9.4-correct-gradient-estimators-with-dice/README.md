# 9.4 Correct Gradient Estimators with DiCE

이번 section에서는 이를 모두 해결할 Infinitely Differentiable Monte-Carlo Estimator\(DiCE\)를 소개합니다. 이는 SCG에서 어떤 차수의 미분도 정확하게 계산할 수 있는 실용적인 알고리즘입니다. 특정 차수의 미분을 하기 위해 가장 간단한 방법은 9.3.1에 나온 방법을 재귀적으로 계속 사용하면 되겠지만, 이는 두 가지 결점을 가지고 있습니다. 첫번째로 gradient를 이렇게 정의하는 것이 auto-diff library에 적용하기 힘들다는 점입니다. 둘째로, 단순하게 gradient estimator를 구하면 $$ \nabla_{\theta}f(x;\theta) \neq g(x;\theta)$$이기 때문에 제대로 업데이트되지 않습니다. 

 시작전에 앞에서 정의한 것과 같이 $$ \mathcal{L} = \mathbb{E}[\sum_{c\in\mathcal{C}}c]$$를 SCG에서의 objective로 정의하고 시작합니다. 이때 모든 의존성을 만족하는 gradient estimator는 다음과 같이 표현할 수 있습니다. 

                      $$\nabla_\theta\mathcal{L} = \mathbb{E}[\sum_{c\in\mathcal{C}}(c\sum_{w\in \mathcal{W}_c}\nabla_\theta\log p(w|\mathrm{DEPS}_w)+ \nabla_\theta c(\mathrm{DEPS}_c))] \cdots (1)$$

$$ \mathcal{W}_c$$는 stochastic nodes에 속하고, cost nodes에 영향을 끼치면서 $$\theta$$에 영향을 받는 모든 node를 의미합니다.ancestors node에 잘 조건화되었다고 가정하고 이제부터 DEPS의 표기에 대해 생략해서 표기하겠습니다.

 이전 부터 소개했지만, DiCE에서는 높은 차수의 미분을 정확하게 하기 위해 MagicBox $$\square$$라는 operator를 사용하고, input으로는 stochastic nodes $$\mathcal{W}$$, 그리고 아래와 같은 두가지 성질을 가지고 있습니다. 

* $$\square (\mathcal{W}) \rightarrow 1$$
* $$\nabla_{\theta}\square(\mathcal{W})=\square (\mathcal{W})\sum_{w \in \mathcal{W}}\nabla_{\theta}\log(p(w;\theta))$$

첫번째 성질의 $$\rightarrow$$는 평가한다\(evaluates to\)라는 의미로 모든 gradient의 같음을 의미하는 full equality\(=\)와는 대조적입니다. auto-diff에서는 이를 forward pass evaluation의 의미로 사용합니다.

 두번째 성질은 $$\square$$를 사용해서 sample이 어디서 sampling됐는지 그 분포에 대한 의존성을 보입니다.\($$w$$에 대한 확률 합 형태가 됩니다.\) 그리고 미분하면 log likelihood trick을 이용해 log형태로 나타난 것입니다. 이는 이 성질을 만족하면 첫번째 성질은 쉽게 만족할 수 있습니다. \(총 확률 합이 1이므로\)

 두번째 특성을 만족한다면, $$ \mathcal{L} = \mathbb{E}[\sum_{c\in\mathcal{C}}c] $$인 objective에 대해 다음같이 표현할 수 있습니다.

                                                                         $$ \mathcal{L}_\square = \sum_{c\in\mathcal{C}}\square(\mathcal{W}_c)c \ \ (\because \square(\mathcal{W}_c) \rightarrow 1)$$

이 $$\mathcal{L}_{\square}$$을 가지고 어떻게 정확하게 고차미분을 할 수 있는지에 대해 증명해보겠습니다.

                                         $$\bm{\mathrm{Theroem 1.\ \ \ \ \ \ }} \mathbb{E}[\nabla^n_{\theta}\mathcal{L}_\square] \rightarrow \nabla^n_\theta\mathcal{L},\forall n \in \{0,1,2,\cdots \}$$

 모든 cost nodes $$c \in \mathcal{C}$$에 대해 다음과 같이 정의하겠습니다. 

                                                         $$\ \ \ \ \  c^0 \ \ \ = \ \ \ \ \ \ c \\ \mathbb{E}[c^{n+1}] = \nabla_\theta\mathbb{E}[c^n]$$

 즉 $$c^n$$는 objective $$\mathbb{E}[c]$$의 n차 미분값입니다.

 다음으로 $$c^n_{\square} $$은 $$c^n\square(\mathcal{W}_{c^n})$$인데, magicbox operator의 첫번째 특성으로 인해, $$ \square \mathcal{W}_c^n$$은 1이 되어, $$c^n_\square \rightarrow c^n$$임을 알았습니다. 이를 통해, $$c^n_\square$$또한 objective의 n번째 미분값이랑 같다는 의미가 됩니다. 그렇다면, 마지막으로 $$\nabla_{\theta}c^n_\square = c^{n+1}_\square$$임을 보이면 n차 미분 전체에 대해 magicbox operator로 구할 수 있고, 그것이 실제 미분값과 같다는 의미가 됩니다. 

                                                                    $$\nabla_\theta c^n_\square = \nabla_\theta(c^n\square(\mathcal{W}_{c^n}))$$

                                                                    $$= c^n\nabla_\theta\square(\mathcal{W}_{c^n})+ \nabla_\theta (\mathcal{W}_{c^n}) \square c^n$$

                                                                    $$= c^n\square(\mathcal{W}_{c^n})(\sum_{w\in\mathcal{W}_{c^n}}\nabla_\theta\log(p(w;\theta)))+ \square(\mathcal{W}_{c^n}) \nabla_\theta c^n$$

                                                                    $$= \square(\mathcal{W}_{c^n}) (\nabla_\theta c^n+c^n\sum_{w\in\mathcal{W}_{c^n}}\nabla_\theta\log(p(w;\theta))) \cdots (9.4.4)$$

                                                                    $$ \square(\mathcal{W}_{c^{n+1}})c^{n+1} = c^{n+1}_\square \cdots (9.4.5)$$

 이 때, \(9.4.4\)에서 \(9.4.5\)로갈 때, 두가지 테크닉이 필요합니다. 첫번째로, $$ \mathcal{L} = \mathbb{E}[c^n]$$의 형태를 본문 위\(1\)형태로 변환해 사용하는 것입니다. 그렇게 되면 다음과 같이 표현할 수 있습니다.

                                                    $$ c^{n+1} = \nabla_{\theta}c^n + c^n \sum_{w \in \mathcal{W}_{c^n}}\nabla_\theta \log p(w;\theta)$$

 이를 자세히 보면 \(9.4.4\)의 표현과 같음을 알 수 있습니다. 둘 째로, $$\mathcal{W}_{c^n}$$과 $$\mathcal{W}_{c^{n+1}}$$은 같은 stochastic nodes를 가리키고있을 것이므로, $$\mathcal{W}_{c^n} =\mathcal{W}_{c^{n+1}}$$이 자명합니다. 

