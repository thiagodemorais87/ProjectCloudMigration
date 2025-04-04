![banner](https://vetores.org/d/compass-uol.svg)
# Introdução

Este trabalho marca a conclusão do estágio Scholarship na Compass UOL. Ao longo do programa, exploramos conceitos essenciais de tecnologia, segurança e desenvolvimento, colocando em prática conhecimentos fundamentais. O projeto é um reflexo do nosso aprendizado e comprometimento, evidenciando tanto nossas habilidades técnicas quanto as metodologias aplicadas no ambiente profissional.

## Case

A empresa fictícia está enfrentando um crescimento acelerado em seu E-commerce, tornando a infraestrutura atual incapaz de lidar com a alta demanda de acessos e compras. Para solucionar esse problema, a empresa TI SOLUÇÕES INCRÍVEIS alocou um time de dentro dos estúdios de Dev Sec Ops, para solucionar o desafio.
A equipe da TI SOLUÇÕES INCRÍVEIS foi designada para realizar uma consultoria no caso de uma migração para a **AWS do seu serviço completo** (todas as maquinas on-premise clonadas para cloud), da empresa Fast Engineering S/A, garantindo maior escalabilidade, segurança e eficiência na infraestrutura, onde a solução atual de arquitetura da empresa não está atendendo mais a alta demanda de acessos e compras, assim sendo este o requisito principal do projeto. 
Posteriormente, após toda a migração para a AWS, como segunda etapa, foi solicitado a modernização com kubernetes: com a aplicação das melhores práticas de arquitetura em Cloud Computing para otimização e escalabilidade.

## Objetivo

O objetivo deste projeto é realizar a migração da infraestrutura on-premise para a AWS, com foco na escalabilidade e segurança, através de uma abordagem ‘lift-and-shift’, seguida da modernização para Kubernetes com microserviços Docker.

## Benefícios para o Cliente

- **Redução de Custos**: Migração para a AWS reduz custos operacionais com hardware e manutenção.

- **Maior Performance**: Infraestrutura escalável e otimizada melhora a experiência do usuário final.

- **Alta Disponibilidade**: Implementação de balanceamento de carga e auto scaling reduz tempo de inatividade.

- **Segurança Aprimorada**: Uso de AWS IAM, WAF, GuardDuty e KMS para proteção contra ameaças.

- **Eficiência e Agilidade**: Kubernetes permite a rápida implantação e escalabilidade dos serviços.

## Riscos e Mitigação

- **Falhas de Rede**: Implementação de replicação de dados e redundância entre zonas de disponibilidade.

- **Perda de Dados**: Estratégias de backup automatizado e replicação em múltiplas regiões.

- **Segurança**: Monitoramento contínuo e aplicação de políticas rigorosas de controle de acesso.

- **Plano de Rollback**: Implementação de estratégias de Blue/Green Deployment e Canary Releases para minimizar riscos em caso de falha durante a migração.

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
- **Segurança:** AWS IAM, AWS WAF, AWS GuardDuty, AWS Shield Advanced e Grupos de Segurança AWS.

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

![Image](https://github.com/user-attachments/assets/95680b7c-5afc-4e5b-ba66-29ad6c50b43b)

Diagrama da Arquitetura
![Image](https://github.com/user-attachments/assets/0a6a5e3d-3154-4a34-b8bf-f22950bebcd6)

## Como serão garantidos os requisitos de Segurança?

- **AWS IAM**: Configure usuários e permissões de acesso.
- **AWS WAF**: Proteja o aplicativo contra ataques como SQL Injection e XSS.
- **CloudWatch**: Monitore logs, métricas e eventos do ambiente AWS, configurando alarmes para detectar atividades suspeitas ou falhas no sistema.
- **Security Groups**: Controle o tráfego permitido para as instâncias EC2.
- **AWS Key Management Service (KMS)**: Utilize o KMS para gerenciar chaves de criptografia de forma segura, protegendo dados sensíveis armazenados em S3, RDS, EBS, e outros serviços.
- **AWS GuardDuty**: Implementação de monitoramento contínuo de ameaças, com integração ao AWS Security Hub para uma visão centralizada de segurança e alertas automáticos via CloudWatch e SNS.
- **VPC Flow Logs**: Para monitorar tráfego dentro da sua VPC e detectar acessos não autorizados.
- **RDS Automatic Backups**: Para recuperação de banco de dados em caso de ataque.
- **AWS Systems Manager**: Para acesso seguro a instâncias EC2 sem necessidade de SSH.

## Quais atividades são necessárias para a migração?

As fases do processo de migração estão sintetizadas a seguir para tornar o entendimento mais claro. Cada etapa apresenta um panorama das atividades envolvidas. 

### Migração de Servidores e APIs para AWS EC2 com Application Migration Service

Este processo detalha os passos para a migração de servidores utilizando o **AWS Application Migration Service** (MGN). Ele envolve a instalação do agente de replicação, sincronização dos dados, testes de aceitação e a execução do cutover final para garantir uma transição segura e eficiente para a infraestrutura da AWS.

1. Inicializar o AWS Application Migration Service na região de destino.
2. Instalar o AWS Replication Agent no servidor de origem.
3. Após a instalação do agente, é necessário aguardar a conclusão da sincronização inicial, que realiza a replicação em nível de bloco do servidor de origem para o servidor de replicação na área de preparação.
4. Lançar instâncias de teste. Após a sincronização inicial, é possível iniciar uma máquina de destino no Modo de Teste, permitindo a realização de testes de aceitação e a verificação do funcionamento correto do ambiente migrado.
5. Realizar testes de aceitação nos servidores. Após testar com sucesso a instância de teste, finalize o teste e exclua a instância.
6. Configurar ações pós-lançamento (se necessário).
7. Aguardar a janela de cutover.
8. Verificar se há atraso (lag).
9. Parar todos os serviços operacionais no servidor de origem.
10. Lançar uma instância de cutover. Iniciar a máquina de destino no Modo de Cutover, iniciando o processo final de migração.
11. Confirmar que a instância de cutover foi lançada com sucesso e, em seguida, finalizar o cutover.
12. Arquivar o servidor de origem.

### Migração do Banco de Dados com AWS DMS

1. Criar uma instância de replicação do AWS DMS antes de configurar os endpoints.
2. Criar um Endpoint de Origem no AWS DMS apontando para o banco MySQL atual.
3. Criar um Endpoint de Destino para o novo banco no Amazon RDS.
4. Configurar uma Tarefa de Migração com opção de Full Load + CDC (Change Data Capture) para replicação contínua.
5. Iniciar a migração e monitorar no AWS DMS Console.
6. Validar a integridade dos dados e realizar o switch para o novo banco.
7. Estimativa de três dias (72 horas) para a migração.


## Como será realizado o processo de backup?

- O RDS realiza backups contínuos do banco de dados dentro do período de retenção configurado.
- Os arquivos estáticos armazenados no S3 são versionados e seguem um ciclo de vida.
- Implementação de snapshots regulares das instâncias ECS e backup automatizado do EKS.

## Qual é o custo da infraestrutura na AWS (AWS Calculator)?

### Amazon RDS MySQL Multi-AZ
- Database Engine: MySQL Deployment Option: Multi-AZ 
- Instance Type: db.m5.large (3 vCPUs, 8 GB RAM – ajustado para suportar os 10 GB de RAM mencionados)
- Storage: 500GB (GP2 SSD)
- Usage: 730 horas/mês (24/7 por 1 mês)
- Backup: Backups automáticos com retenção de 7 dias
- **Custo:**  452,31 USD/mês

### Frontend (EC2)

- Instance Type: t3.medium (1 vCPU, 4 GB RAM – ajustado para os 2 GB mencionados)
- Number of Instances: 2 (para alta disponibilidade)
- **Custo:**  61,54 USD/mês

### Backend (EC2) 
- Instance Type: t3.large (2 vCPUs, 8GB RAM – ajustado para 4GB mencionados)
- Number of Instances: 2 (alta disponibilidade)
- **Custo:**  122,27 USD/mês 

### ALB
- Frontend: 5 GB/hora
- Backend: 1 GB/hora
- **Custo:** 45,63 USD + 22,27 USD = 67,90 USD/mês

### S3
- Storage Class: Standard
- Storage Amount: 5 GB
- Requests: 1.000 PUTs e 10.000 GETs (estimativa conservadora).
- **Custo:**   0,12 USD/mês 

### Migração

- Custos da migração do banco de dados (t3.large)
    - 10.51 USD
- Custos de armazenamento DMS
    - 57.50 USD

### Estrutura

- Custo mensal:
    - 704,14 USD
- Custo total anual:
    - 8.449,68 USD

![Image](https://github.com/user-attachments/assets/aee6d490-c112-4be2-84e9-b7c56efc5afb)


---

## ETAPA 2: MODERNIZAÇÃO COM KUBERNETES

## Quais atividades são necessárias para a migração?

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

AWS EC2

AWS ALB

AWS RDS

AWS S3

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
- **Security Groups**: controlam o tráfego permitido para as instâncias EC2 e restringem o tráfego externo para o cluster.
- **AWS Key Management Service (KMS)**: gerencia chaves de criptografia de forma segura, protegendo dados sensíveis armazenados em S3, RDS, EBS, e outros serviços.

Visando que o projeto está em produção, serão adicionadas camadas extras de proteção e segurança:

Segurança de Containers e Kubernetes:  

- **PodSecurity Policies e RBAC**: controlam o acesso e as permissões de execução dentro do cluster Kubernetes, assegurando que os pods tenham permissões mínimas e evitando o uso de práticas inseguras (como containers executando como root).
- **Escaneamento de Imagens de Containers (Trivy, Clair)**: garante que as imagens de containers estejam livres de vulnerabilidades conhecidas antes de serem implantadas no Kubernetes.

**Ameaças Internas e Zero Trust**

- **Network Policies no Kubernetes**: Implemente políticas de rede para garantir que apenas os pods autorizados possam comunicar entre si. Isso minimiza os riscos de movimento lateral em caso de comprometimento de um pod.
- **Segurança de API (API Gateway + Rate Limiting)**: Proteja suas APIs com um **API Gateway**, implemente **rate limiting** para evitar abuso e **autenticação/autorização** (OAuth, JWT).

**Segurança de Rede**

- **AWS Shield (Proteção contra DDoS)**: Ative o AWS Shield para proteger suas aplicações de ataques de negação de serviço distribuída (DDoS).
- **VPC com subnets privadas**: Configure sua infraestrutura de rede de forma que os componentes sensíveis (como bancos de dados) fiquem em subnets privadas e inacessíveis diretamente pela internet.

## Como será realizado o processo de Backup?

- O RDS realiza backups contínuos do banco de dados dentro do período de retenção configurado.
- Os arquivos estáticos armazenados no S3 serão versionados e seguirão um ciclo de vida.

## Qual o custo da infraestrutura na AWS (AWS Calculator)?

### Amazon RDS MySQL Multi-AZ
- Database Engine: MySQL Deployment Option: Multi-AZ 
- Instance Type: db.m5.large (3 vCPUs, 8GB RAM – ajustado para suportar os 10GB de RAM mencionados)
- Storage: 500GB (GP2 SSD)
- Usage: 730 horas/mês (24/7 por 1 mês)
- Backup: Backups automáticos com retenção de 7 dias
- **Custo:**  452,31 USD/mês (Mesmo do lift-and-shift)

### Amazon EKS (Elastic Kubernetes Service)
- Cluster EKS: 1 cluster Number of Instances: 2 (para alta disponibilidade)
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

## Duração e Cobrança

- **Fase 1**: Migração para AWS (3 meses)
- **Fase 2**: Modernização com Kubernetes (4 meses)

- **Desenvolvedor** – R$ 150 a R$ 400/hora (tempo estimado: 3 a 7 meses)

## Treinamento
- Com a migração do e-commerce concluída, capacitar a equipe do e-commerce da "Fast Engineering S/A"é o próximo passo para garantir o sucesso na AWS. Um treinamento focado permitirá que a empresa gerencie a infraestrutura com autonomia, resolva incidentes com agilidade e otimize o ambiente continuamente. Isso reduz a dependência de suporte externo e maximiza o retorno do investimento, mantendo os custos sob controle.

- Isso pode ser feito com videoaulas da Udemy, como "AWS, na prática!", para aprendizado prático, e a certificação "AWS Certified Cloud Practitioner", que oferece uma base sólida em conceitos de nuvem via AWS Skill Builder. O plano incluiria assistir aos cursos da Udemy e, em 4-6 semanas, preparar-se para o exame de certificação. Essa capacitação, proposta pela "TI SOLUÇÕES INCRÍVEIS", garantiria autonomia e eficiência na operação da AWS.


## Suporte
- Após a migração "lift-and-shift" para a AWS, a "TI Soluções Incríveis" oferecerá suporte robusto à "Fast Engineering S/A", garantindo a estabilidade do e-commerce com validação rápida do MySQL, React e APIs, configuração otimizada do Elastic Load Balancer e instâncias EC2/RDS para suportar a demanda, além de monitoramento contínuo via CloudWatch; nos primeiros 90 dias, disponibilizaremos assistência 24/7 para resolver problemas e minimizar interrupções, complementada por orientação prática à equipe no uso do AWS Management Console, assegurando uma transição confiável rumo à modernização.




## Conclusão

Este projeto tem como objetivo garantir uma migração segura e eficiente da infraestrutura on-premise para a AWS, adotando serviços gerenciados para aprimorar desempenho, escalabilidade e segurança. O processo ocorre em duas fases: inicialmente, a estrutura atual é replicada na nuvem por meio de serviços como AWS MGN, RDS, EC2 e DMS; posteriormente, a aplicação é modernizada com EKS e microserviços Docker, tornando-a mais eficiente e flexível.

A implementação segue boas práticas de segurança, incorporando IAM, WAF, criptografia com KMS e políticas específicas para Kubernetes, garantindo um ambiente protegido contra ameaças. Além disso, a estimativa de custos permite um planejamento financeiro detalhado, proporcionando maior previsibilidade nos investimentos e evitando custos inesperados.

Com essa abordagem estruturada, a migração reduz a complexidade operacional e prepara a infraestrutura para acompanhar o crescimento futuro da aplicação, assegurando alto desempenho, confiabilidade e escalabilidade.

Com a modernização em Kubernetes, a aplicação estará mais ágil, resiliente e facilmente escalável, garantindo que a empresa esteja preparada para suportar picos de demanda com maior eficiência.

---
