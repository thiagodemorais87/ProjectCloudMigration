![banner](https://vetores.org/d/compass-uol.svg)
# Introdução

Este trabalho marca a conclusão do estágio Scholarship na Compass UOL. Ao longo do programa, exploramos conceitos essenciais de tecnologia, segurança e desenvolvimento, colocando em prática conhecimentos fundamentais. O projeto é um reflexo do nosso aprendizado e comprometimento, evidenciando tanto nossas habilidades técnicas quanto as metodologias aplicadas no ambiente profissional.

## Case

A empresa fictícia está enfrentando um crescimento acelerado em seu E-commerce, tornando a infraestrutura atual incapaz de lidar com a alta demanda de acessos e compras. Para solucionar esse problema, a empresa TI SOLUÇÕES INCRÍVEIS alocou um time de dentro dos estúdios de Dev Sec Ops, para solucionar o desafio.
A equipe da TI SOLUÇÕES INCRÍVEIS foi designada para realizar uma consultoria no caso de uma migração para a **AWS do seu serviço completo** (todas as maquinas on-premise clonadas para cloud), da empresa Fast Engineering S/A, garantindo maior escalabilidade, segurança e eficiência na infraestrutura, onde a solução atual de arquitetura da empresa não está atendendo mais a alta demanda de acessos e compras, assim sendo este o requisito principal do projeto. 
Posteriormente, após toda a migração para a AWS, como segunda etapa, foi solicitado a modernização com kubernetes: com a aplicação das melhores práticas de arquitetura em Cloud Computing para otimização e escalabilidade.

## Objetivo

O projeto visa realizar a migração da infraestrutura atual para a **AWS**, iniciando com um processo de **"lift-and-shift"**, garantindo uma transição rápida e segura, contando com sistema de failover. 

Em seguida, será realizada a **modernização da infraestrutura com Kubernetes**, aplicando as melhores práticas de arquitetura em Cloud Computing. Para saber mais sobre essa segunda etapa, acesse a página dedicada à **modernização com Kubernetes.** 

## Estrutura Atual

Arquitetura de operação utilizada pelo cliente


- **Banco de Dados:** Servidor MySQL (500GB de dados, 10GB de RAM, 3 Core vCPUs).
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

AWS EC2

AWS ALB

AWS RDS

AWS S3

CloudWatch

NAT

EKS

## Qual o diagrama da empresa atual?

![Image](https://github.com/user-attachments/assets/408850c5-12a7-4625-9fdc-8838b106d8c4)

## Qual o diagrama da infraestrutura na AWS?

#### Etapa As-Is

![image](https://github.com/user-attachments/assets/14149833-8864-44ec-a144-c497326b06e5)


#### Etapa Modernizção

![Image](https://github.com/user-attachments/assets/09283004-5d77-4d74-adea-370e6cb0bc84)


## Como serão garantidos os requisitos de Segurança?

- **AWS IAM**: Configure usuários e permissões de acesso.
- **AWS WAF**: Proteja o aplicativo contra ataques como SQL Injection e XSS.
- **CloudWatch**: Monitore logs, métricas e eventos do ambiente AWS, configurando alarmes para detectar atividades suspeitas ou falhas no sistema.
- **Security Groups**: Controle o tráfego permitido para as instâncias EC2.
- **AWS Key Management Service (KMS)**: Utilize o KMS para gerenciar chaves de criptografia de forma segura, protegendo dados sensíveis armazenados em S3, RDS, EBS, e outros serviços.
- **AWS GuardDuty**: será implementado para monitorar ameaças durante todas as fases do projeto, Durante a migração Lift-and-Shift para detectar acessos suspeitos e eventos maliciosos.


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

### Migração do Banco de Dados com AWS DMS

1.Criar uma instância de replicação do AWS DMS antes de configurar os endpoints.
2.Criar um Endpoint de Origem no AWS DMS apontando para o banco MySQL atual.
3.Criar um Endpoint de Destino para o novo banco no Amazon RDS.
4.Configurar uma Tarefa de Migração com opção de Full Load + CDC (Change Data Capture) para replicação contínua.
5.Iniciar a migração e monitorar no AWS DMS Console.
6.Validar a integridade dos dados e realizar o switch para o novo banco.
7.Estimativa de três dias (72 Horas) para migração.



### Banco de dados on-premise para RDS

![Image](https://github.com/user-attachments/assets/92fd40ea-10d8-4d45-bd02-762838e9d1d1)


## Como será realizado o processo de Backup?

- O RDS realiza backups contínuos do banco de dados dentro do período de retenção configurado.
- Os arquivos estáticos armazenados no S3 são versionados e seguem um ciclo de vida.

## Qual o custo da infraestrutura na AWS (AWS Calculator)?

### Amazon RDS MySQL Multi-AZ
- Database Engine: MySQLDeployment Option: Multi-AZ 
- Instance Type: db.m5.large (3 vCPUs, 8GB RAM – ajustado para suportar os 10GB de RAM mencionados)
- Storage: 500GB (GP2 SSD)
- Usage: 730 horas/mês (24/7 por 1 mês)
- Backup: Backups automáticos com retenção de 7 dias
- **Custo:**  452,31 USD/mês

### EC2 Frontend

- Instance Type: t3.medium (1 vCPU, 4GB RAM – ajustado para 2GB mencionados)
- Number of Instances: 2 (para alta disponibilidade)
- **Custo:**  61,54 USD/mês

### EC2 Backend
- Instance Type: t3.large (2 vCPUs, 8GB RAM – ajustado para 4GB mencionados)
- Number of Instances: 2 (alta disponibilidade)
- **Custo:**  122,27 USD/mês 

### ALB
- Frontend: 5 GB/hora.
- Backend: 1 GB/hora.
- **Custo:**   45,63 USD + 22,27 USD = 67,9/mês

### S3
- Storage Class: StandardStorage Amount: 5GB
- Requests: 1.000 PUTs e 10.000 GETs (estimativa conservadora).
- **Custo:**   0,12 USD/mês 

### Migração

- Custos da migração do banco de dados(t3.Large)
    - 10.51 USD
- Custos de armazenamento DMS
    - 57.50 USD

### Estrutura

- Custo mensal
    - 704.14 USD
- Custo total anual
    - 8.449,68 USD

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
- **AWS GuardDuty**: Garantindo a segurança dos workloads em EKS.

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

### Amazon RDS MySQL Multi-AZ
- Database Engine: MySQLDeployment Option: Multi-AZ 
- Instance Type: db.m5.large (3 vCPUs, 8GB RAM – ajustado para suportar os 10GB de RAM mencionados)
- Storage: 500GB (GP2 SSD)
- Usage: 730 horas/mês (24/7 por 1 mês)
- Backup: Backups automáticos com retenção de 7 dias
- **Custo:**  452,31 USD/mês (Mesmo do lift-and-shift)

### Amazon EKS (Elastic Kubernetes Service)
- Cluster EKS: 1 clusterNumber of Instances: 2 (para alta disponibilidade)
- Worker Nodes: 4 nós EKS (2 por AZ, conforme diagrama). 
- Tipo: t2.medium (2 vCPUs, 4GB RAM – ajustado para o projeto).
- EBS: 10GB por nó (total 40GB)
- **Custo:**  554,80 USD/mês 

### S3
- Storage Class: StandardStorage Amount: 5GB
- Requests: 1.000 PUTs e 10.000 GETs (estimativa conservadora).
- **Custo:**   0,12 USD/mês 

### ALB
- 1 ALB (centralizado para frontend e backend).
- Bytes processados: 6GB/hora (5GB frontend + 1GB backend, conforme Etapa 1).
- Novas conexões: 3/segundo.
- Duração: 1 segundo.Solicitações: 4.5/segundo (1.5 frontend + 3 backend).
- Regras: 5.
- Horas: 730/mês
- **Custo:** 51,47 USD /mês

### Amazon CloudFront
- Tráfego: 100GB/mês (assumindo que CloudFront distribui o conteúdo do frontend e S3).
- Requisições: 1.000.000 (média para um e-commerce).
- **Custo:** 11,50 USD/mês

### AWS WAF
- Web ACLs: 1 (associada ao CloudFront e ALB).
- Regras: 5 (média).
- Requisições: 1.000.000/mês.
- **Custo:** 10,60 USD/mês

### Amazon CloudWatch
- Logs: 5GB/mês (média para EKS, ALB, RDS).
- Métricas: 10 métricas personalizadas (e.g., CPU, memória).
- **Custo:**   8,05 USD/mês

### Amazon ECR (Elastic Container Registry)
- Armazenamento: 1GB (imagens Docker para frontend e backend).
- Transferência: 1GB/mês (push/pull).
- **Custo:**   0,10 USD/mês 

### Estrutura

- Custo mensal
    - 1.088,95 USD
- Custo total anual
    - 13.067,40 USD

![Image](https://github.com/user-attachments/assets/7675317b-c25c-46db-b756-762d8b53a185)


## Conclusão

Este projeto tem como objetivo assegurar uma migração segura e eficiente da infraestrutura on-premise para a AWS, utilizando serviços gerenciados para aprimorar desempenho, escalabilidade e segurança. O processo ocorre em duas fases: inicialmente, a estrutura atual é replicada na nuvem por meio de serviços como AWS MGN, RDS, EC2 e DMS; posteriormente, a aplicação é modernizada com EKS e microserviços Docker, aumentando sua eficiência e flexibilidade.

A implementação segue boas práticas de segurança, incorporando IAM, WAF, criptografia com KMS e políticas específicas para Kubernetes, garantindo um ambiente robusto contra ameaças. Além disso, a estimativa de custos permite um planejamento financeiro detalhado, proporcionando maior previsibilidade nos investimentos.

Com essa abordagem estruturada, a migração não apenas reduz a complexidade operacional, mas também prepara a infraestrutura para acompanhar o crescimento futuro da aplicação, garantindo alto desempenho e confiabilidade.

---
