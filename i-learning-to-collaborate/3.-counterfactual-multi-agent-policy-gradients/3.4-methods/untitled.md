# 3.4.2.1 baseline lemma

이번 chapter에서는 $$g = \mathbb{E}_\pi[\sum_a{\nabla_{\theta}\log{\pi^a(u^a|\tau^a)A^a(s,\bold{u})}}] = 0$$임을 증명해볼 예정입니다. $$ b$$baseline으로 사용하기 위해서 unbiased함을 보여야하므로 꼭 짚고넘어가는 것이 좋습니다. 

이 $$g$$는 다음과 같이 정의 가능합니다.

                                                        $$ g = \mathbb{E}_\pi[\sum _a{\nabla{\theta}\log{\pi^a(u^a|\tau^a)A^a(s,\bold{u})}}]$$ 

                                                              $$ A^a(s,\bold{u}) = Q(s,\bold{u})-b(s,\bold{u}^{-a})$$

그렇다면, baseline $$b$$에 대한 $$g$$는 $$ g_b = -\mathbb{E}_\pi[\sum _a{\nabla{\theta}\log{\pi^a(u^a|\tau^a)b^a(s,\bold{u^{-a}})}}]$$로 나타낼 수 있습니다. 이는 state distribution이 ergodic하다면, stationary distribution $$d$$를 사용해 summation form으로 다음과 같이 나타낼 수 있습니다.

               $$ g_b  = -\sum_s{d^\pi(s)}\sum _a\sum_{\bold{u}^{a}}{\bm{\pi}(\bold{u}^{a}|\bm{\tau})}{\nabla{\theta}\log{\pi^a(u^a|\tau^a)b^a(s,\bold{u^{-a}})}}$$ 

                    $$  = -\sum_s{d^\pi(s)}\sum _a\sum_{\bold{u}^{-a}}{\bm{\pi}(\bold{u}^{-a}|\bm{\tau}-a)}\sum_{u^a}{\pi^a(u^a|\tau^a)}{\nabla{\theta}\log{\pi^a(u^a|\tau^a)b^a(s,\bold{u^{-a}})}}$$

                    $$  = -\sum_s{d^\pi(s)}\sum _a\sum_{\bold{u}^{-a}}{\bm{\pi}(\bold{u}^{-a}|\bm{\tau}-a)}\sum_{u^a}{\nabla\pi^a(u^a|\tau^a)}{b^a(s,\bold{u}^{-a}})$$

                    $$  = -\sum_s{d^\pi(s)}\sum _a\sum_{\bold{u}^{-a}}{\bm{\pi}(\bold{u}^{-a}|\bm{\tau}-a)}{b^a(s,\bold{u}^{-a}}){\nabla1}$$

                    $$= 0$$





 

