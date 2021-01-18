# Deep Multi-Agent Reinforcement Learning



![](.gitbook/assets/marl_00.png)

![Hits](https://hits.seeyoufarm.com/api/count/incr/badge.svg?url=https://kilmya1.gitbook.io/deep-multi-agent-reinforcement-learning/)



안녕하세요. 김설호입니다. 이번에 COMA로 유명해진 Foerster의 박사학위 논문을 번역해보는 시간을 가져보았습니다. 누군가 "Multi-Agent RL을 배우고 싶은데 이게 최선이야?" 했을 때, 이 글은 아닐 수 있습니다. 하지만 좀 더 본질적으로, "이런식으로 번역한걸 보는 것이 정말 의미가 있어?" 했을 때 저는 충분히 Yes라고 생하고 있습니다.

 혼자 논문을 즐겨 읽는 저로서 항상 아쉬웠던 점은 내가 지금 이해한 것에 대해 다른 사람은 어떻게 생각할까에 대한 해소가 힘들었던 점입니다. 그렇기에 누군가가 제가 남겨논 발자취를 보며 즐겁게 공부해나갔으면 좋겠습니다.

 우리가 비동기적으로 만나서 함께 같은 공부를 하고있다는 사실은 같아도, 과거의 배움은 각자 다른 길을 걸어왔을 것입니다. 다양한 의견들을 존중하고, 틀린 표현들은 바로잡아주면 감사하겠습니다.

 "이 thesis가 MARL의 정도냐" 했을 때, 이 질문에 대답은 완전히 No라고 생각합니다. 하지만, 애초에 어느 학문의 길에도 정도는 없다고 생각합니다. 제가 생각했을 때, 충분히 MARL가 직면하고 있는 문제점들과, 이를 해결하기 위한 노력들에 대해 이해할 수 있었고, 나름 친절해서 저는 좋았다고 생각합니다.

내용은 [이곳](https://ora.ox.ac.uk/objects/uuid:a55621b3-53c0-4e1b-ad1c-92438b57ffa4)에서 확인 가능합니다. permission을 얻은상태이고, 단기간에 빠르게 완성하기 위해 많은 부족한 부분이 존재하는데 유의해서 읽어주셨으면 좋겠습니다.



Written by Jakob N. Foerster

Translated by [Seolho Kim](https://seolhokim.github.io/about/)



