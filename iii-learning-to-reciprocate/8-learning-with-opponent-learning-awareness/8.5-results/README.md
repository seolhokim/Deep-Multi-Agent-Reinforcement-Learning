# 8.5 Results

이번 section에서는 실험적인 결과를 보입니다. 특히 LOLA-Ex와 NL--Ex의 비교와 LOLA-PG와 NL-PG의 비교를 중점적으로 보시면 됩니다. 이 때, 다음의 질문에 관해 답을 얻는 것을 겨냥해 실험하였습니다.

1. LOLA-Ex agents들은 NL-Ex와 비교해 어떻게 다르게 행동하는지?
2. policy gradient update를 할 때, LOLA-PG와 NL-PG는 어떻게 행동하는지?
3. LOLA-Ex agent는 어떻게 공정하게 평가할 것인지?
4. LOLA-PG agent는 스케일을 키울 수 있는지?
5. LOLA-PG는 opponent의 modeling에 대한 정보가 없어져도 행동을 유지하는지?
6. LOLA agents는 테일러 근사에 좀더 높은 차수를 사용하면 더 정확해지는지?

처음부터 세번째 질문까지는 8.5.1에 정리되어있고, 그다음 두개는 8.5.2, 마지막은 8.5.3에 정리되어있습니다.

