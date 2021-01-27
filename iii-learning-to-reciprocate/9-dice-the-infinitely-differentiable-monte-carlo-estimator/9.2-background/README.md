# 9.2 Background

 random variable $$x $$가 $$ p(x;\theta)$$의 분포를 따른때 다음과 같이 표현합니다. $$x \sim p(x;\theta)$$

그리고 $$f$$는 $$x$$에 의한 함수일 때, 우리는 $$\nabla_\theta\mathbb{E}_x[f(x)]$$를 계산하고 싶은 상황입니다. 이 때, $$\nabla_{\theta}f$$ analytical gradients는 구할 수 없거나 존재하지 않을 때, 다음과 같은 score function estimator를 유도할 수 있습니다.

                                               $$\nabla_\theta\mathbb{E}_x[f(x)] = \mathbb{E}_x[f(x)\nabla_{\theta}\log(p(x;\theta))]$$

 그 이후의 내용은 기본 아이디어를 따온 다음 [Gradient Estimation Using Stochastic Computation Graph](https://arxiv.org/pdf/1506.05254.pdf)를 읽으시면 도움이 될 수 있습니다. 

 만약 $$x$$가 $$\theta$$의 값에 deterministic function이고, 다른 random variable $$z$$로 이루어진다면 이는 $$x(z,\theta)$$로 표현가능하고, 

                                                   $$\nabla_\theta\mathbb{E}_z[f(x(z,\theta)] = \mathbb{E}_z[\nabla_\theta f(x(z,\theta))]$$ 

로 표현할 수 있습니다. 이는 단순한 수식변환이지만 모든 $$z$$에 대해 $$\theta$$의 연속 함수일 때만 필요충분조건으로 성립합니다. 또한 이는 다음과 같이 나타낼 수 있습니다.

                                  $$\frac{\partial}{\partial \theta}\mathbb{E}_{z\sim p(\cdot;\theta)}[f(x(z,\theta))] =  \frac{\partial}{\partial \theta}\int p(\cdot;\theta)f(x(z,\theta))dz$$

                                                                                $$= \int  \frac{\partial p(\cdot;\theta)}{\partial \theta}f(x(z,\theta)) + p(\cdot;\theta)\frac{\partial f(x(z,\theta))}{\partial \theta} dz $$

                                                                                $$= \int  \frac{\partial p(\cdot;\theta)}{\partial \theta}f(x(z,\theta)) + p(\cdot;\theta)\frac{\partial f(x(z,\theta))}{\partial \theta} dz $$

                                                                                  $$ = \mathbb{E}_{z\sim p(\cdot;\theta)}[(\frac{\partial}{\partial \theta}\log{p(z;\theta)})f(x(z,\theta))+\frac{\partial f(x(z,\theta))}{\partial \theta}]$$





