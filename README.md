![banner](https://vetores.org/d/compass-uol.svg)
# Introdução

Este trabalho marca a conclusão do estágio Scholarship na Compass UOL. Ao longo do programa, exploramos conceitos essenciais de tecnologia, segurança e desenvolvimento, colocando em prática conhecimentos fundamentais. O projeto é um reflexo do nosso aprendizado e comprometimento, evidenciando tanto nossas habilidades técnicas quanto as metodologias aplicadas no ambiente profissional.

## Case

A empresa fictícia está enfrentando um crescimento acelerado em seu E-commerce, tornando a infraestrutura atual incapaz de lidar com a alta demanda de acessos e compras. Para solucionar esse problema, a empresa TI SOLUÇÕES INCRÍVEIS alocou um time de dentro dos estúdios de Dev Sec Ops, para solucionar o desafio.
A equpe da TI SOLUÇÕES INCRÍVEIS foi designada para realizar uma consultoria no caso de uma migração para a **AWS do seu serviço completo** (todas as maquinas on-premise clonadas para cloud), da empresa Fast Enginnering S/A, garantindo maior escalabilidade, segurança e eficiência na infraestrutura, onde a solução atual de arquitetura da empresa não está atendendo mais a alta demanda de acessos e compras, assim sendo este o requisito principal do projeto. 
Posteriormente, após toda a migração para a AWS, tendo como a segunda etapa, foi solicitado a modernização com kubernetes: tendo a aplicação das melhores práticas de arquitetura em Cloud Computing para otimização e escalabilidade.

## Objetivo

O projeto visa realizar a migração da infraestrutura atual para a **AWS**, iniciando com um processo de **"lift-and-shift"**, garantindo uma transição rápida e segura, contando com sistema de failover. 

Em seguida, será realizada a **modernização da infraestrutura com Kubernetes**, aplicando as melhores práticas de arquitetura em Cloud Computing. Para saber mais sobre essa segunda etapa, acesse a página dedicada à **modernização com Kubernetes.** 

## Estrutura Atual

Arquitetura de operação utilizada pelo cliente


- **Banco de Dados:** Servidor MySQL (500GB de dados, 10GB de RAM, 3 Core CPU).
- **Frontend:** Servidor React (5GB de dados, 2GB de RAM, 1 Core CPU).
- **Backend:** Servidor com 3 APIs, Nginx como balanceador de carga e armazenamento de arquivos estáticos (5GB de dados, 4GB de RAM, 2 Core CPU).
  
## Estruturas Propostas na AWS

- A migração inicial será feita com mínimas alterações, utilizando os seguintes serviços AWS:

- **Banco de Dados:** Amazon RDS MySQL Multi-AZ.
- **Frontend:** EC2 + Load Balancer.
- **Backend:** EC2 + Load Balancer.
- **Armazenamento de Arquivos:** Amazon S3.
- **Segurança:** AWS IAM, AWS WAF e Grupos de Segurança AWS.

- # ETAPA AS IS

## Quais as ferramentas vão ser utilizadas?

AWS MGN

AWS DMS

AWS-EC2

AWS-ALB

AWS-RDS

AWS-S3

CloudWatch

NAT

EKS

## Qual o diagrama da empresa atual?

![Image](https://github.com/user-attachments/assets/408850c5-12a7-4625-9fdc-8838b106d8c4)

## Qual o diagrama da infraestrutura na AWS?

#### Etapa As-Is

![Image](https://github.com/user-attachments/assets/3e94d503-d9ec-4cf7-a699-831a4907da2e)

#### Etapa Modernizção

![Image](https://github.com/user-attachments/assets/09283004-5d77-4d74-adea-370e6cb0bc84)


## Como serão garantidos os requisitos de Segurança?

- **AWS IAM**: Configure usuários e permissões de acesso.
- **AWS WAF**: Proteja o aplicativo contra ataques como SQL Injection e XSS.
- **CloudWatch**: Monitore logs, métricas e eventos do ambiente AWS, configurando alarmes para detectar atividades suspeitas ou falhas no sistema.
- **Security Groups**: Controle o tráfego permitido para as instâncias EC2.
- **AWS Key Management Service (KMS)**: Utilize o KMS para gerenciar chaves de criptografia de forma segura, protegendo dados sensíveis armazenados em S3, RDS, EBS, e outros serviços.

## Quais atividades são necessária para a migração?

As fases do processo de migração estão sintetizadas a seguir para tornar o entendimento mais claro. Cada etapa apresenta um panorama das atividades envolvidas. Para informações mais detalhadas, há links ao longo da documentação que oferecem uma explicação mais aprofundada de cada fase. Sugerimos a leitura desses materiais para um acompanhamento mais completo.

### Migração de Servidores e APIs para AWS EC2 com Application Migration Service

Este processo detalha os passos para a migração de servidores utilizando o **AWS Application Migration Service** (MGN). Ele envolve a instalação do agente de replicação, sincronização dos dados, testes de aceitação e a execução do cutover final para garantir uma transição segura e eficiente para a infraestrutura da AWS.

1. Inicializar o AWS Application Migration Service na região de destino.
2. Instalar o AWS Replication Agent no servidor de origem.
3. Aguardar a conclusão da sincronização inicial. Após instalar o agente, é necessário aguardar a conclusão do processo de sincronização inicial, que realiza a replicação em nível de bloco do servidor de origem para o servidor de replicação na área de preparação.
4. Lançar instâncias de teste. Após a sincronização inicial, é possível iniciar uma máquina de destino no Modo de Teste, permitindo a realização de testes de aceitação e a verificação do funcionamento correto do ambiente migrado.
5. Realizar testes de aceitação nos servidores. Após testar com sucesso a instância de teste, finalize o teste e exclua a instância.
6. Configurar ações pós-lançamento (se necessário).
7. Aguardar a janela de cutover.
8. Confirmar que não há atraso (lag).
9. Parar todos os serviços operacionais no servidor de origem.
10. Lançar uma instância de cutover. Iniciar a máquina de destino no Modo de Cutover, iniciando o processo final de migração.
11. Confirmar que a instância de cutover foi lançada com sucesso e, em seguida, finalizar o cutover.
12. Arquivar o servidor de origem.

### Banco de dados on-premise para RDS

![Image](https://github.com/user-attachments/assets/92fd40ea-10d8-4d45-bd02-762838e9d1d1)


## Como será realizado o processo de Backup?

- O RDS realiza backups contínuos do banco de dados dentro do período de retenção configurado.
- Os arquivos estáticos armazenados no S3 são versionados e seguem um ciclo de vida.

## Qual o custo da infraestrutura na AWS (AWS Calculator)?

### Migração

Estimativa de três dias (72 Horas) para migração:

- Custos da migração do banco de dados (72 horas de uso t3.large)
    - 10.51 USD
- Custos de armazenamento DMS
    - 57.50 USD

### Estrutura

- Custo mensal
    - 504.22 USD
- Custo total anual
    - 6,050.64 USD

![Image](https://github.com/user-attachments/assets/aee6d490-c112-4be2-84e9-b7c56efc5afb)


---

## ETAPA 2: MODERNIZAÇÃO COM KUBERNETES

## Quais atividades são necessária para a migração?

### 1. Converter estrutura em microserviços docker

- **Identificar componentes do sistema** (ex: backend, frontend, banco de dados, autenticação).
- **Separar funcionalidades monolíticas** em serviços independentes.
- **Criar imagens Docker** para cada serviço.
- **Publicar as imagens** no **Amazon ECR** (Elastic Container Registry).

### **2. Preparar o Cluster Kubernetes**

- Criar um **Cluster EKS** no AWS Management Console ou via CLI.
- Configurar **VPC, sub-redes e Auto Scaling** para os Worker Nodes.

### **Segurança e Configurações Adicionais**

- Configurar **IAM roles** para permissões do EKS.
- Implementar **AWS WAF e Security Groups** para proteção.

## Quais as ferramentas vão ser utilizadas?

AWS MGN

AWS DMS

AWS-EC2

AWS-ALB

AWS-RDS

AWS-S3

CloudWatch

NAT

EKS

CloudFront

ECR

## Qual o diagrama da infraestrutura na AWS?

![Image](https://github.com/user-attachments/assets/09283004-5d77-4d74-adea-370e6cb0bc84)

## Como serão garantidos os requisitos de Segurança?

- **AWS IAM**: configura usuários e permissões de acesso.
- **AWS WAF**: protege o aplicativo contra ataques como SQL Injection e XSS.
- **CloudWatch**: monitora logs, métricas e eventos do ambiente AWS, configurando alarmes para detectar atividades suspeitas ou falhas no sistema.
- **Security Groups**: controla o tráfego permitido para as instâncias EC2, restringir o tráfego externo para o cluster.
- **AWS Key Management Service (KMS)**: gerencia chaves de criptografia de forma segura, protegendo dados sensíveis armazenados em S3, RDS, EBS, e outros serviços.

Visando que o projeto esta em produção, será adicionado camadas extras de proteção e segurança:

Segurança de Containers e Kubernetes:  

- **PodSecurity Policies e RBAC**: Controla o acesso e as permissões de execução dentro do cluster Kubernetes, assegurando que os pods tenham as permissões mínimas e evitando o uso de práticas inseguras (como containers executando como root).
- **Escaneamento de Imagens de Containers (Trivy, Clair)**: Assegura que as imagens de containers estejam livres de vulnerabilidades conhecidas antes de serem implantadas no Kubernetes.

**Ameaças Internas e Zero Trust**

- **Network Policies no Kubernetes**: Implemente políticas de rede para garantir que apenas os pods autorizados possam comunicar entre si. Isso minimiza os riscos de movimento lateral em caso de comprometimento de um pod.
- **Segurança de API (API Gateway + Rate Limiting)**: Proteja suas APIs com um **API Gateway**, implemente **rate limiting** para evitar abuso e **autenticação/autorização** (OAuth, JWT).

**Segurança de Rede**

- **AWS Shield (Proteção contra DDoS)**: Ative o AWS Shield para proteger suas aplicações de ataques de negação de serviço distribuída (DDoS).
- **VPC com subnets privadas**: Configure sua infraestrutura de rede de forma que os componentes sensíveis (como bancos de dados) fiquem em subnets privadas e inacessíveis diretamente pela internet.

## Como será realizado o processo de Backup?

- O RDS realiza backups contínuos do banco de dados dentro do período de retenção configurado.
- Os arquivos estaticos armazenados no S3 serão versionados e seguirão um ciclo de vida

## Qual o custo da infraestrutura na AWS (AWS Calculator)?

- Custo mensal
    - 977.84 USD
- Custo total anual
    - 11,734.08 USD






## Orçamento

A seguir, apresentamos a estimativa de custos para a implementação do projeto. A tabela abaixo detalha os valores correspondentes a cada item necessário para a execução, garantindo maior transparência e controle financeiro.

<img width="762" alt="Image" src="https://github.com/user-attachments/assets/d93c7ef0-cfb5-41ed-88f5-c79995d09f62" />


## Conclusão

Este projeto tem como objetivo assegurar uma migração segura e eficiente da infraestrutura on-premise para a AWS, utilizando serviços gerenciados para aprimorar desempenho, escalabilidade e segurança. O processo ocorre em duas fases: inicialmente, a estrutura atual é replicada na nuvem por meio de serviços como AWS MGN, RDS, EC2 e DMS; posteriormente, a aplicação é modernizada com EKS e microserviços Docker, aumentando sua eficiência e flexibilidade.

A implementação segue boas práticas de segurança, incorporando IAM, WAF, criptografia com KMS e políticas específicas para Kubernetes, garantindo um ambiente robusto contra ameaças. Além disso, a estimativa de custos permite um planejamento financeiro detalhado, proporcionando maior previsibilidade nos investimentos.

Com essa abordagem estruturada, a migração não apenas reduz a complexidade operacional, mas também prepara a infraestrutura para acompanhar o crescimento futuro da aplicação, garantindo alto desempenho e confiabilidade.

---
