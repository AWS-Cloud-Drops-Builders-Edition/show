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

- Esta é uma decisão tem mais relação com as características da sua organização do que com qualquer outro aspecto técnico. 

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

Ao longo tempo nós temos usando pip em nossos projetos e inclusive usamos pip no projeto que originou esta demo e rodou no HackTown 2024.

Durante a fase de estudos para construir esta temporada, decidimos explorar algumas alternativas e chegamos no Poetry. Para nós, brilham a configuração em um único arquivo e o maior determinismo no gerenciamento das dependências.

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

O Pydantic também foi uma escolha pragmática, pois ele se tornou uma escolha popular para escrever testes em Python devido à sua facilidade de uso, recursos abrangentes e suporte da comunidade.

Algumas funcionalidades que destacamos como úteis, para acelerar o desenvolvimento:

- Sistema de Fixtures: O Pytest possui um sistema de fixtures flexível e poderoso para lidar com operações de *setup* e *teardown*, compartilhamento de dados de teste e gerenciamento de recursos.

- Testes parametrizados: Isso permite que você execute o mesmo teste com diferentes entradas (inputs) de forma fácil. Com testes parametrizados, você pode escrever um único caso de teste e fornecer múltiplos conjuntos de dados de entrada como parâmetros. O Pytest então executará esse teste uma vez para cada conjunto de dados fornecido. Isso é muito útil quando você precisa testar uma função ou método com uma variedade de entradas diferentes, em vez de duplicar o código de teste para cada entrada.

- O Pytest pode descobrir e executar automaticamente os testes em seu projeto sem exigir que você mantenha suítes de testes separadas. Especificamente, o Pytest segue algumas convenções para encontrar os testes em seu código:

    - Ele procura por arquivos cujos nomes começam com "test_" ou terminam com "_test.py".

    - Dentro desses arquivos, ele procura por funções cujos nomes começam com "test_".

    - Também reconhece classes começando com "Test" como classes de teste, e qualquer método nessas classes começando com "test_" como um método de teste.

Essa capacidade de descoberta automática de testes economiza muito trabalho, pois você não precisa configurar explicitamente quais testes devem ser executados. Basta seguir as convenções de nomenclatura e o Pytest encontrará e executará seus testes automaticamente. Isso torna o processo de escrever e executar testes muito mais simples e produtivo, especialmente em projetos maiores com muitos testes espalhados.

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

Você deve fornecer uma pasta de assets quando estiver construindo uma Lambda Layer ou Lambda Function com AWS CDK. Ele remove a pasta superior e pega o conteúdo.

Se fornecêssemos a pasta 'lambda' como a pasta raiz, teríamos problemas de importação ao invocar a função, já que as importações em nossa função Lambda contêm 'lambda.x.y', da mesma forma que reside no repositório.

Para resolver esse problema, temos uma etapa de construção que é executada durante o processo de deployment. Ela copia a pasta 'lambda' do nível raiz para uma nova pasta de nível raiz, a '.build'.

Dessa forma, quando o CDK pega o conteúdo da lambda dessa nova pasta de nível superior, ele também pega a pasta superior 'lambda' (ou qualquer outro nome que seja definido por você) e as importações permanecem válidas.

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