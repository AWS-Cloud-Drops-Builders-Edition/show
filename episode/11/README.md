# Episódio 01, Temporada 02 - [NA PRÁTICA] Construindo uma aplicação Serverless com IA generativa DO ZERO - Parte 1

[![YouTube video thumbnail](./thumb.jpg)](https://bit.ly/cdbe-s02e01)
**[&#x25b6; Assista agora no Youtube!](https://bit.ly/cdbe-s02e01)**

Bem-vindo(a) ao primeiro episódio da segunda temporada do AWS Cloud Drops Builders Edition!

Nesta temporada nós vamos construir uma aplicação Serverless completa com IA generativa DO ZERO! Desde o caso de uso, até a utilização dos dados para tomada de decisão. Vamos explorar temas como utilizar o Amazon Q Developer para escrever código, prompts, fazer chamadas ao Amazon Bedrock, definir a Infraestrutura, automatizar testes, organizar projetos, definir a arquitetura da solução, dentre outros. 

Esta é a temporada perfeita para você que está começando com desenvolvimento de software na AWS e se interessa em IA generativa.

Bóra Buildar!

## O que mencionamos durante o episódio

- [Amazon Q Developer](https://aws.amazon.com/q/developer/)
- [PartyRock](https://partyrock.aws/)
- [AWS CDK](https://aws.amazon.com/cdk/)

## 🤖 Conversando com o Amazon Q Developer

#### O que pedimos?

> We will create an application from scratch in a program on the AWS LATAM YouTube channel. This application will consist of a web interface (frontend) where users can enter data, and a backend.
> - The main functionality is that users will describe how they're feeling, and the application will generate a recipe for a non-alcoholic drink using generative AI.
> - In addition to the recipe, the software will also generate an impactful image of the recipe, also using generative AI.
> - Users will indicate their dietary restrictions based on available ingredients. Therefore, we will store all user choices to ensure we have this information in case an audit is needed.
> - This application will run at technology events as a way to gauge how people are feeling about the event. The number of drinks needed may vary, from none to 2,000, depending on the event. The client application will run on a touchscreen, and each drink will be requested individually.
> - We will use JavaScript for the frontend and Python for the backend.
> - Users will receive the recipe and recipe image via two QR codes that will appear at the end of the recipe generation process.
> - Bartenders will receive the recipes via an email determined by their team. We will use SendGrid to send the emails.

#### Resposta do Claude 3 Sonnet (via PartyRock)

>- Hospede o código front-end em um bucket S3 e use o AWS Amplify para implantação e hospedagem estática.
Utilize o AWS Amplify para configurar o serviço de hospedagem web e CDN (CloudFront).
>- Crie um domínio personalizado (exemplo: drinkgenerator.com) usando o Amazon Route 53. 
>- Use o AWS Lambda para executar o código Python que gerará as receitas e imagens usando IA generativa.
>- Crie uma API Gateway para expor o Lambda como um endpoint API para o frontend.
>- Use o Amazon DynamoDB para armazenar as escolhas e restrições dos usuários.
>- Configure o AWS Step Functions para orquestrar o fluxo de geração de receitas e imagens. 
>- Utilize o AWS Lambda para gerar os QR Codes das receitas e imagens.
>- Armazene as imagens geradas no Amazon S3. 
>- Integre o AWS Lambda com o SendGrid para enviar e-mails com as receitas para os bartenders. 
>- Use o AWS Auto Scaling para escalar automaticamente as instâncias do Lambda com base na demanda.
>- Implante o frontend em múltiplas regiões da AWS usando o CloudFront para alta disponibilidade.
>- Configure o DynamoDB com réplicas globais para alta disponibilidade dos dados. 
>- Use o Amazon CloudWatch para monitorar a saúde dos serviços e configurar alertas.
>- Habilite o AWS X-Ray para rastreamento e análise de desempenho.
>- Envie logs para o Amazon CloudWatch Logs ou Amazon S3.
>- Essa é uma arquitetura de alto nível que atende aos requisitos fornecidos. Nas próximas etapas, fornecerei instruções detalhadas sobre como configurar e provisionar cada componente mencionado acima.

#### Resposta do Amazon Q Developer

> To build the application you described, we can leverage various AWS services and technologies. Here's a high-level architecture and the services we could use:
>
> Frontend: 
>
>- AWS Amplify or Amazon S3 to host the static website
>- AWS AppSync or Amazon API Gateway to expose a GraphQL or REST API for the backend
>- React or Angular for building the user interface
>
> Backend:
>
>- AWS Lambda to run serverless Python functions
>- Amazon DynamoDB or Amazon RDS to store user preferences and choices
>- Amazon SageMaker or Amazon Bedrock to integrate with generative AI models for recipe and image generation
>- Amazon SNS or Amazon SQS to queue recipe requests for processing
>- AWS Secrets Manager to securely store SendGrid API credentials
>- Amazon CloudWatch for monitoring and logging
>- AWS CloudFormation or AWS CDK for infrastructure as code
>- AWS IAM for access management and security
>
> Workflow:
>
>- User enters their preferences and dietary restrictions on the frontend.
>- Frontend sends a request to the backend API (API Gateway/AppSync).
>- API triggers a Lambda function to store user data in DynamoDB and enqueue a recipe request in SNS/SQS.
>- Another Lambda function is triggered by the SNS/SQS queue to generate the recipe and image using SageMaker/Bedrock models.
>- The generated recipe and image are stored in an S3 bucket, and QR codes are generated for them.
>- The QR codes are returned to the frontend for display.
>- A separate Lambda function sends the recipe to the appropriate bartender team via SendGrid.
>- This architecture allows for scalability, separation of concerns, and easy integration with AWS services. You can use AWS CodePipeline for continuous deployment and AWS CloudFormation/CDK for infrastructure as code.
>
>Note: For the actual implementation, you'll need to provision and configure these services, write the application code, and integrate the generative AI models. Additionally, you'll need to consider security best practices, such as using AWS Cognito for user authentication and AWS KMS for data encryption.

#### O que pedimos?

>For IaC, between AWS CDK and AWS SAM, which one is the best option for us?

#### Resposta do Amazon Q Developer

>When choosing between AWS CDK and AWS SAM for infrastructure as code (IaC) in your project, consider the following factors:
> 
> AWS CDK (Cloud Development Kit):
>- Allows you to define your infrastructure using familiar programming languages like Python, JavaScript/TypeScript, Java, C#, and Go.
>- Provides a higher-level abstraction over AWS resources, making it easier to define and compose complex infrastructure patterns.
>- Supports multiple programming paradigms (object-oriented, functional, etc.) and allows for code reuse through modules and libraries.
>- Offers better integration with CI/CD pipelines and development workflows.
>- Provides better support for testing and validation of infrastructure code.
>- Has a steeper learning curve compared to AWS SAM, as it requires knowledge of the programming language and AWS CDK constructs.
>
> AWS SAM (Serverless Application Model):
>
>- Uses a simplified syntax based on AWS CloudFormation templates (JSON or YAML).
>- Primarily focused on serverless applications and architectures, making it easier to define and deploy serverless resources like Lambda functions, API Gateway, and DynamoDB.
>- Has a lower learning curve for developers familiar with CloudFormation templates.
>- Provides a streamlined workflow for local testing and debugging of serverless applications using the SAM CLI.
>- May be more limited in terms of advanced infrastructure patterns and code reuse compared to AWS CDK.
>- Given the requirements of your project, which involves a frontend, backend, and integration with generative AI models, AWS CDK might be a better choice for the following reasons:
>- Programming Language Support: Since you plan to use JavaScript for the frontend and Python for the backend, AWS CDK supports both languages natively, making it easier to define and manage your infrastructure code alongside your application code.
>- Complex Infrastructure Patterns: Your application involves multiple components (API Gateway, Lambda, DynamoDB, SageMaker, etc.) and integrations, which may require more complex infrastructure patterns. AWS CDK provides a higher-level abstraction and better support for composing and reusing infrastructure patterns.
>- Integration with CI/CD: AWS CDK integrates well with CI/CD pipelines, allowing you to test and validate your infrastructure code as part of your development workflow.
>- Scalability and Future Growth: While your initial requirements may be focused on serverless components, AWS CDK provides broader coverage of AWS services, making it easier to scale and extend your infrastructure as your application grows.
>- However, if your team has significant experience with AWS CloudFormation templates and prefers a more declarative approach, AWS SAM could be a viable option, especially if your application remains focused on serverless architectures.
>
> Ultimately, the choice between AWS CDK and AWS SAM should consider your team's skills, the complexity of your infrastructure, and the long-term scalability and maintainability requirements of your application.

#### O que pedimos?

> Regarding the frontend, we are unsure about which technology to use, our team is proficient in JavaScript. What other options would you like us to consider?

#### Resposta do Amazon Q Developer

> Since your team is proficient in JavaScript, it would be a natural choice for the frontend development of this project. JavaScript is a widely adopted language for building modern web applications and has a vast ecosystem of libraries and frameworks to choose from.
>
> However, it's always good to explore alternative options and consider their potential benefits and trade-offs. Here are some alternatives to JavaScript that you could consider for the frontend:
>
>- TypeScript: TypeScript is a superset of JavaScript that adds optional static typing, which can help catch errors during development and improve code maintainability. It's particularly useful for larger projects and teams, as it provides better tooling support and code documentation. TypeScript is a popular choice for building complex web applications and is well-supported by many JavaScript frameworks and libraries.
>
>- React: React is a JavaScript library for building user interfaces, developed and maintained by Facebook. It uses a component-based architecture and a virtual DOM for efficient rendering. React is widely adopted and has a large community, making it a solid choice for building the frontend of your application.
>
>- Angular: Angular is a comprehensive framework for building web applications, developed and maintained by Google. It follows a more opinionated approach and provides a structured way of building applications. Angular has a steeper learning curve compared to React but offers a more comprehensive set of features out of the box.
>
>- Vue.js: Vue.js is a progressive JavaScript framework that is designed to be incrementally adoptable. It combines the best features of Angular and React, making it a lightweight and flexible option for building user interfaces. Vue.js has a growing community and is often praised for its ease of learning and integration with other libraries.
>
>- Svelte: Svelte is a relatively new component framework that takes a different approach to building user interfaces. Instead of using a virtual DOM, it compiles components into highly optimized JavaScript code during the build process. This can result in smaller bundle sizes and improved performance, especially for larger applications.
>
>- WebAssembly: While not a direct alternative to JavaScript, WebAssembly is a low-level bytecode format that can be used to run code written in languages like C, C++, and Rust in web browsers. It can potentially offer performance benefits for certain types of computationally intensive tasks, but it may not be suitable for building the entire frontend of your application.
>
> When considering these alternatives, you should evaluate factors such as your team's familiarity with the technology, the learning curve, performance requirements, community support, and the availability of third-party libraries and tools. Additionally, consider the long-term maintainability and scalability of the chosen technology, as well as its compatibility with the backend and other components of your application.
>
> Ultimately, if your team is already proficient in JavaScript and comfortable with its ecosystem, sticking with JavaScript and a popular framework like React or Vue.js could be a pragmatic choice for this project.

## 🫰 Dívida técnica

- Criar o projeto básico do frontend
- Criar o desenho da arquitetura conforme susgestões do Amazon Q Developer

## Onde aprender mais

[AWSome Generative Drink App (Github)](https://bit.ly/awsome-generative-drink-app)