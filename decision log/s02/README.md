# Temporada 02 - Histórico de decisões de projeto

Este arquivo destina-se a manter o histórico das decisões de nível de projeto que foram tomadas para o projeto que foi construído durante a segunda temporada do [AWS Cloud Drops Builders Edition](https://www.youtube.com/playlist?list=PLQHh55hXC4yrlnKxKDsLPFl5O6sTfXWHu). Nós sabemos que na maior parte das vezes não há apenas uma resposta certa, então vamos compartilhar também os porquês de cada decisão.   

## 20-08-2024

### AWS CDK

🤨 **O que?**

O [AWS CDK](https://aws.amazon.com/pt/cdk/) (Cloud Development Kit) é um framework de código aberto que permite definir infraestrutura de nuvem usando linguagens de programação familiares como TypeScript, Python, Java e .NET. Ele gera templates do AWS CloudFormation a partir do seu código, permitindo que você provisione e gerencie recursos da AWS de uma maneira mais intuitiva e programática. O AWS CDK simplifica o processo de criação e implantação de infraestrutura de nuvem, fornecendo construções e abstrações de alto nível para os serviços da AWS.

🕵️ **Por que?**

Nós usamos o Amazon Q Developer para nos ajudar a tomar esta decisão. Você pode ver parte do diálogo [aqui](https://github.com/AWS-Cloud-Drops-Builders-Edition/show/blob/main/episode/11/README.md).

- Há inúmeras opções para definir infraestrutura como código. Você pode escolher entre AWS SAM, Terraform, Pulumi, AWS CloudFormation, entre outros.

- Nós escolhemos AWS CDK porque gostaríamos de usar Python de ponta a ponta no projeto backend. 

- Esta é uma decisão que tem mais relação com as características da sua organização do que com qualquer outro aspecto técnico. 

### React

🤨 **O que?**

[React](https://react.dev/) é uma biblioteca JavaScript para construção de interfaces de usuário. Ela utiliza uma arquitetura baseada em componentes e um DOM virtual para renderização eficiente. 

🕵️ **Por que?**

Nós usamos o Amazon Q Developer para nos ajudar a tomar esta decisão. Você pode ver parte do diálogo [aqui](https://github.com/AWS-Cloud-Drops-Builders-Edition/show/blob/main/episode/11/README.md).

Aqui vale notar que nós não somos desenvolvedores do Frontend. Sendo assim, nosso principal racional foi o pragmatismo, que nos fez escolher o React por ser tão popular e ter tanto suporte da comunidade. O Vue.js também seria uma escolha na mesma direção.

## 01-10-2024

### Poetry

🤨 **O que?**

[Poetry](https://python-poetry.org/) é uma ferramenta de gerenciamento de dependências e empacotamento para projetos Python. O Poetry visa resolver muitos dos desafios associados às ferramentas tradicionais de gerenciamento de pacotes Python, oferecendo uma abordagem mais moderna e simplificada para o gerenciamento e empacotamento de projetos Python.

🕵️ **Por que?**

Ao longo do tempo nós temos usando pip em nossos projetos e inclusive usamos pip no projeto que originou esta demo e rodou no HackTown 2024.

Durante a fase de estudos para construir esta temporada, decidimos explorar algumas alternativas e chegamos ao Poetry. Para nós, brilham a configuração em um único arquivo e o maior determinismo no gerenciamento das dependências.

- Gerenciamento de Dependências: O Poetry simplifica o processo de gerenciar dependências do projeto, permitindo declarar bibliotecas necessárias em um arquivo pyproject.toml e instalando, atualizando e resolvendo essas dependências.

- Ambientes Virtuais: Cria e gerencia automaticamente ambientes virtuais isolados para cada projeto.

- Lockfile: Utiliza um arquivo lockfile (poetry.lock) para garantir instalações reproduzíveis em diferentes ambientes.

- Resolução de Dependências: Oferece resolução robusta de dependências, evitando conflitos de versões.

- Gerenciamento de Configuração: Usa um único arquivo pyproject.toml para configuração do projeto.

- Builds consistentes: Garante builds consistentes entre diferentes ambientes de desenvolvimento e pipelines de implantação.

### Powertools for AWS Lambda

🤨 **O que?**

[Powertools for AWS Lambda](https://docs.powertools.aws.dev/lambda/python/latest/) é um kit de ferramentas para desenvolvedores projetado para simplificar a implementação das melhores práticas de serverless e aumentar a produtividade dos desenvolvedores ao trabalhar com funções AWS Lambda.

🕵️ **Por que?**

Melhores práticas para todos. Este é o lema do Powertools for AWS Lambda e foi exatamente o que nos fez escolher utilizá-lo neste projeto. Neste caso em particular, vamos usar fortemente a parte de logs estruturados e idempotência. 

- Rastreamento: Ajuda no rastreamento distribuído de manipuladores de funções Lambda e outras funções.

- Logging: Permite logging estruturado com detalhes de contexto do Lambda.

Sem os logs estruturados, o log de uma exceção vai se parecer com isso aqui:

```
[ERROR] ValueError: Não foi possível processar o drink
Traceback (most recent call last):
  File "/var/task/lambda_function.py", line 9, in lambda_handler
    raise ValueError("Não foi possível processar o drink")
```

Este formato dificulta a análise e filtragem de logs, especialmente quando você precisa correlacionar eventos ou depurar problemas em produção.

Com o log estruturado do PowerTools for AWS Lambda temos algo muito mais rico e útil:

```json
{
  "level": "ERROR",
  "location": "lambda_function.lambda_handler:11",
  "message": "Erro ao processar o drink 123",
  "service": "order-service",
  "timestamp": "2025-03-23T19:30:45.123Z",
  "xray_trace_id": "1-65fd1234-abcdef1234567890abcdef12",
  "exception": "Traceback (most recent call last):\n  File \"/var/task/lambda_function.py\", line 9, in lambda_handler\n    raise ValueError(\"Não foi possível salvar o drink\")\nValueError: Não foi possível salvar o drink",
  "lambda": {
    "function_name": "meu-lambda",
    "function_memory_size": "128",
    "function_arn": "arn:aws:lambda:us-east-1:123456789012:function:meu-lambda",
    "request_id": "a1b2c3d4-5678-90ab-cdef-EXAMPLE11111"
  },
  "cold_start": true,
  "event": {
    "drink_id": "123"
  }
}
```

Os benefícios dos logs estruturados incluem:

1. **Pesquisa e filtragem avançadas**: Você pode facilmente filtrar logs por nível, serviço, ID de solicitação ou qualquer outro campo personalizado.

2. **Correlação de eventos**: O ID de rastreamento do X-Ray e o ID de solicitação permitem correlacionar eventos em diferentes serviços.

3. **Contexto enriquecido**: Informações como cold start, detalhes da função Lambda e dados do evento fornecem contexto valioso para depuração.

4. **Integração com ferramentas de observabilidade**: Logs estruturados em formato JSON podem ser facilmente ingeridos por ferramentas como CloudWatch Logs Insights, Elasticsearch ou soluções de terceiros.

5. **Análise automatizada**: Facilita a criação de alertas baseados em padrões específicos ou anomalias nos logs.


- Métricas: Permite a criação de métricas personalizadas usando o CloudWatch Embedded Metric Format (EMF).

Recursos adicionais (dependendo da linguagem):

- Idempotência: Para tornar funções Lambda seguras para repetição.

- Projetado para ajudar a implementar as melhores práticas da AWS Well-Architected para aplicações serverless.

- Fácil integração via gerenciadores de pacotes ou Lambda Layers.

- Permite adoção progressiva de utilitários individuais ou de todo o conjunto.

- Código aberto, permitindo contribuições e melhorias da comunidade.

### Pydantic

🤨 **O que?**

[Pydantic](https://docs.pydantic.dev/latest/) é uma biblioteca Python popular para validação de dados usando anotações de tipo do Python.

🕵️ **Por que?**

Nós precisávamos de uma forma para validar os dados de entrada e saída do nosso projeto e vamos também fazer o parsing das variáveis de ambiente. O Pydantic foi uma escolha pragmática, com base em inúmeros projetos que conseguimos observar o seu uso.   

### pytest

🤨 **O que?**

O [pytest](https://docs.pytest.org/en/stable/) é amplamente utilizado na comunidade Python devido à sua simplicidade, flexibilidade e recursos poderosos. Ele ajuda os desenvolvedores a escrever testes mais fáceis de manter e confiáveis, o que por sua vez leva a um software mais robusto. Sua simplicidade na escrita de testes, combinada com recursos avançados para cenários de teste mais complexos, o torna adequado para projetos de todos os tamanhos e complexidades.

🕵️ **Por que?**

O Pytest também foi uma escolha pragmática, pois ele se tornou uma escolha popular para escrever testes em Python devido à sua facilidade de uso, recursos abrangentes e suporte da comunidade.

Algumas funcionalidades que destacamos como úteis, para acelerar o desenvolvimento:

- Sistema de Fixtures: O Pytest possui um sistema de fixtures flexível e poderoso para lidar com operações de *setup* e *teardown*, compartilhamento de dados de teste e gerenciamento de recursos.

- Testes parametrizados: Isso permite que você execute o mesmo teste com diferentes entradas (inputs) de forma fácil. Com testes parametrizados, você pode escrever um único caso de teste e fornecer múltiplos conjuntos de dados de entrada como parâmetros. O Pytest então executará esse teste uma vez para cada conjunto de dados fornecido. Isso é muito útil quando você precisa testar uma função ou método com uma variedade de entradas diferentes, em vez de duplicar o código de teste para cada entrada.

- O Pytest pode descobrir e executar automaticamente os testes em seu projeto sem exigir que você mantenha suítes de testes separadas. Especificamente, o Pytest segue algumas convenções para encontrar os testes em seu código:

    - Ele procura por arquivos cujos nomes começam com "test_" ou terminam com "_test.py".

    - Dentro desses arquivos, ele procura por funções cujos nomes começam com "test_".

    - Também reconhece classes começando com "Test" como classes de teste, e qualquer método nessas classes começando com "test_" como um método de teste.

Essa capacidade de descoberta automática de testes economiza algum trabalho, pois você não precisa configurar explicitamente quais testes devem ser executados. Basta seguir as convenções de nomenclatura e o Pytest encontrará e executará seus testes automaticamente. Isso torna o processo de escrever e executar testes muito mais simples e produtivo, especialmente em projetos maiores com muitos testes espalhados.

## 29-10-2024

### Boas práticas com AWS CDK

🤨 **O que?**

Nome diferente da stack em um projeto AWS CDK, por desenvolvedor e por branch.

🕵️ **Por que?**

Nomear a stack por desenvolvedor e por branch permite que múltiplos desenvolvedores compartilhem a mesma conta de desenvolvimento e trabalhem em paralelo na mesma stack. O pipeline de CI/CD deve utilizar o seu nome único para remover qualquer chance de conflitos.

### Utilização de Lambda Layers

🤨 **O que?**

Vamos criar e utilizar uma Lambda layer que todas as funções Lambda irão compartilhar.

🕵️ **Por que?**

A intenção aqui é a otimização do processo de deployment, já que todas as nossas funções requerem as mesmas dependências.

Esta layer conterá todas as dependências contidas sa sessão '[tool.poetry.dependencies]' do arquivo 'pyproject.toml'.

Você pode ler mais sobre Lambda Layers [aqui](https://docs.aws.amazon.com/lambda/latest/dg/chapter-layers.html).

### A pasta .build

🤨 **O que?**

Nós vamos utilizar um estágio de build como parte do processo de deployment para copiar o conteúdo das funções Lambdas para uma pasta específica dentro de '.build' e ainda definir o arquivo de dependências que será utilizado para criação da Lambda Layer.

🕵️ **Por que?**

Você deve fornecer uma pasta de assets quando estiver construindo uma Lambda Function com AWS CDK, que desconsidera a pasta informada e pega apenas o conteúdo abaixo dela para levar para dentro da função.

Desta forma, a proposta é mover o código das funções lambda para uma pasta centralizada de maneira a não quebrar as importações. Digamos que seu código está organizado assim (vide estrutura do projeto):

```
service/
└── drink/
    ├── domain_logic/
    ├── handlers/
    ├── integration/
    └── models/
```

Ao importar o schema `DrinkRequest` da pasta models, o import seria algo como:

```
from service.drink.models import DrinkRequest 
```

Se fornecêssemos a pasta ```service``` como a pasta raiz, teríamos problemas de importação ao importar o schema, já que as importações contêm ```service.drink.models```, mas o que estaria dentro da função seria ```drink.models``` (não existiria a pasta ```service```).

```
drink/
 ├── domain_logic/
 ├── handlers/
 ├── integration/
 └── models/
```

Para resolver esse problema, temos uma etapa de construção que é executada durante o processo de deployment. Ela copia recursivamente a pasta ```service``` para uma nova pasta de nível raiz chamada ```lambda```, dentro do diretório ```.build```.

Dessa forma, quando o AWS CDK pega o conteúdo da função lambda dessa nova pasta de nível superior, ele também pega a pasta ```service``` (ou qualquer outro nome que seja definido por você) e todas as importações permanecem válidas.

### O Makefile

🤨 **O que?**

Vamos criar um arquivo makefile para simplificar as tarefas repetitivas no projeto AWS CDK. 

🕵️ **Por que?**

Criar um Makefile para projetos AWS CDK é uma boa prática que oferece vários benefícios:

- Padroniza a execução de tarefas comuns no projeto.
- Simplifica comandos complexos do CDK em targets fáceis de lembrar.
- Automatiza tarefas repetitivas como execução de testes, lint, formatação, synth, deploy e etc....
- Configura o ambiente de desenvolvimento de forma consistente.
- Permite executar testes locais e verificações de qualidade antes do processo de deployment.
- Facilita a integração com pipelines de CI/CD.
- Serve como documentação, listando as operações disponíveis.
- Garante compatibilidade multiplataforma, funcionando em sistemas Unix e Windows.

## 12-11-2024

### pre-commit, formatação e análise estática de código

🤨 **O que?**

Nós vamos configurar algumas verificações para serem executadas automaticamente antes de cada cada commit. Para isso, vamos utilizar um [framework](https://github.com/pre-commit/pre-commit) para manter os hooks de pre-commit.

Com o hook configurado, vamos utilizar três ferramentas:

- [black](https://github.com/psf/black):
    - Formatador de código Python
Aplica um estilo consistente e opinativo. Não é configurável, visando eliminar debates sobre estilo.

- [flake8](https://github.com/pycqa/flake8):
    - Ferramenta de lint para Python
Combina PyFlakes, pycodestyle e Ned Batchelder's McCabe script.
Verifica erros de estilo e lógica.

- [isort](https://github.com/pycqa/isort):
    - Utilitário para ordenar imports em arquivos Python. Organiza imports automaticamente por tipo e ordem alfabética.

🕵️ **Por que?**

- Detectar problemas antes que entrem em seu repositório.
- Garantir automaticamente que todo o código atenda aos padrões estabelecidos.
- Impedir a submissão de código problemático, como declarações de depuração, arquivos grandes ou informações sensíveis.
- Impor consistência em toda a equipe.
- Impor as mesmas verificações de estilo e qualidade de código para todos.
- Eliminar debates sobre estilo, já que todos usam as mesmas ferramentas automatizadas.
- Tornar as revisões de código mais focadas na funcionalidade do que na formatação.
- Permitir a detecção precoce de problemas.
- Eliminar a verificação manual de problemas comuns.

## 26-11-2024

### Estrutura do projeto de backend (AWS CDK)

🤨 **O que?**

Escolhemos uma estrutura de projeto opinativa com uma pasta de infraestrutura (baseada em CDK), uma pasta de testes e uma pasta para os domínios (caso haja mais de um, as subpastas serão responsáveis separá-los).

Estrutura proposta (considere que drink é o nome do domínio)

```
infrastructure/
└── drink/

service/
└── drink/
    ├── domain_logic/
    ├── handlers/
    ├── integration/
    └── models/

tests/
└── drink/
    ├── unit/
    ├── integration/
    └── e2e/
```

🕵️ **Por que?**

Aqui, como em várias outras práticas aplicadas neste projeto, não há certo ou errado. Outras estruturas podem fazer mais sentido para você. Do nosso lado, vemos vantagem em separar o código de infraestrutura do código de domínio, pois isso adiciona clareza de propósito.

A separação por domínios (caso haja mais de um no mesmo projeto) também visa facilitar o entendimento do projeto. 

### Aplicando o Princípio da Responsabilidade Única

🤨 **O que?**

De baixo da pasta service/drink há uma série de subpastas (separadas por domínio).

Estas pastas representam diferentes "camadas", que propõem uma separação de responsabilidades, a fim de evitar a criação de componentes com mais de uma responsabilidade.

- *domain_logic*: é a lógica do negócio
- *handlers*: handlers das funções lambda
- *integration*: código que acessa APIs (serviços da AWS e APIs externas ao serviço)
- *models*: schemas/modelos do pydantic.

🕵️ Por que?

Esta estrutura é totalmente opinativa e visa principalmente separar o código dos manipuladores de função (handlers) da lógica de domínio e sugerir a criação de códigos menos acoplados e mais testáveis.

Principais vantagens:

- Manutenibilidade: Componentes com responsabilidade única são mais fáceis de entender, modificar e manter. Isso reduz o risco de introduzir bugs ao fazer alterações e facilita a evolução do código ao longo do tempo.

- Reutilização de código: Componentes bem definidos e com responsabilidade única têm maior potencial de reutilização em diferentes partes do sistema ou até mesmo em outros projetos, aumentando a eficiência do desenvolvimento.

- Testabilidade: Componentes menores e mais focados são mais fáceis de testar de forma isolada. Isso permite a criação de testes de unidade mais eficazes.

Possíveis desafios:

- Complexidade excessiva (over engineering): Unidades muito pequenas podem levar a um aumento na complexidade.

- Definição de limites: Determinar onde exatamente uma responsabilidade termina e outra começa pode ser subjetivo e desafiador, especialmente em sistemas complexos.

## 14-03-2025

### Metodologia de testes

🤨 **O que?**

Temos testes de unidade, testes de infraestrutura, testes de integração e testes ponta a ponta (E2E).

🕵️ **Por que?**

Cada tipo de teste tem seu uso:

- Testes de unidade verificam pequenas funções e principalmente validações de schemas.

- Testes de infraestrutura são executados antes da implantação; eles verificam se recursos críticos existem e não foram excluídos do template do CloudFormation (que é o resultado do deploy do AWS CDK) por erro ou bug.

- Testes de integração ocorrem após a implantação e geram um evento simulado (mocked events), chamam o manipulador de função na IDE e permitem depurar as funções com pontos de interrupção. 

- Chamamos serviços AWS reais e podemos escolher o que simular para simular falhas e quais recursos chamar diretamente.

- Testes E2E - acionam os recursos que foram implantados na AWS.