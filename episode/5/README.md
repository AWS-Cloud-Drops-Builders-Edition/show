# Episódio 6 - Ajustando LLMs com Parameter efficient fine-tunning (PEFT)

[![YouTube video thumbnail](./thumb.jpeg)](https://www.youtube.com/watch?v=18eWp6ceP4k)
**[&#x25b6; Assista agora no Youtube!](https://www.youtube.com/watch?v=18eWp6ceP4k)**

Como vimos no último episódio, o ajuste de LLMs é computacionalmente intensivo. O ajuste fino completo requer memória não apenas para armazenar o modelo, mas vários outros parâmetros que são necessários durante o processo de treinamento. Mesmo que o seu computador possa suportar o tamanho do modelo, que agora é da ordem de centenas de gigabytes para os modelos maiores, você também deve ser capaz de alocar memória para vários componentes adjacentes e memória temporária durante todo o processo de treinamento. Esses componentes adicionais podem ser muitas vezes maiores que o modelo e podem rapidamente se tornar grandes demais para serem manuseados em hardware de uso geral. 

Neste episódio, veremos alternativas ao ajuste fino completo, utilizando o Parameter efficient fine-tuning (PEFT), para utilizar técnicas que atualizam apenas um pequeno subconjunto de parâmetros. 

## O que mencionamos durante o episódio

## 🐛 Bugs em produção

## 🫰 Dívida técnica

## Onde aprender mais

* [Código utilizado neste episódio (guithub)](https://github.com/AWS-Cloud-Drops-Builders-Edition/s01e06)
* [PartyRocket - build web apps with gen AI](https://partyrock.aws/u/mza/pDK3iF1kb/PartyRocket-build-web-apps-with-gen-AI/snapshot/xKLiQfwHd)
* [AWS re:Invent 2023 - Keynote with Dr. Werner Vogels](https://www.youtube.com/watch?v=UTRBVPvzt9w)
* [HELM is a living benchmark to evaluate Language Models more transparently](https://crfm.stanford.edu/helm/latest/)
* [Este artigo apresenta o GLUE, uma referência para avaliar modelos em diversas tarefas de compreensão de linguagem natural (NLU) e enfatiza a importância de sistemas NLU gerais aprimorados](https://openreview.net/pdf?id=rJ4km2R5t7)
* [Este artigo apresenta o SuperGLUE, um benchmark projetado para avaliar o desempenho de vários modelos de PNL em uma série de tarefas desafiadoras de compreensão de linguagem](https://super.gluebenchmark.com/)
* [Este artigo apresenta e avalia quatro medidas diferentes (ROUGE-N, ROUGE-L, ROUGE-W e ROUGE-S) no pacote de avaliação de resumo ROUGE, que avalia a qualidade dos resumos comparando-os com resumos ideais gerados por humanos](https://aclanthology.org/W04-1013.pdf)
* [Este artigo apresenta um novo teste para medir a precisão multitarefa em modelos de texto, destacando a necessidade de melhorias substanciais para alcançar a precisão de nível especializado e abordar o desempenho desequilibrado e a baixa precisão em assuntos socialmente importantes](https://arxiv.org/pdf/2009.03300.pdf)
* [O artigo apresenta o BIG-bench, um benchmark para avaliar modelos de linguagem em tarefas desafiadoras, fornecendo insights sobre escala, calibração e preconceito social](https://arxiv.org/pdf/2206.04615.pdf)


[![AWS PartyRock](../../images/partyrock.jpeg)](https://partyrock.aws/)
**[Bóra construir uma aplicação baseada em IA](https://partyrock.aws/)**

[![Generative AI with LLMs](../../images/Generative%20AI%20with%20LLMs.jpeg)](https://www.deeplearning.ai/courses/generative-ai-with-llms/)
**[DeepLearning.AI](https://www.deeplearning.ai/courses/generative-ai-with-llms/)**
