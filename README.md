# Desafio-DIO
Repositório criado durante o bootcamp Code Girls para documentar conhecimentos adquiridos


# O que são *Regions* e *Availability Zones*

- Regions são áreas geográficas, onde estão localizados os data centers, isolados entre si. 
- Availability Zones são o conjunto de data centers isolados fisicamente e interconectados para prover baixa latência, além de tolerância a falhas.

  ## Não esquecer:
  Quando se cria uma conta na AWS, não se deve utilizar a root account. Você deve criar um novo perfil com permissões de ADMIN e utilizá-lo para fazer todas as outras ações que não requerem o uso da conta root. A mesma também deve estar protegida pelo MFA (Multi Factor Authenticator)
  

# Diferenças entre nuvem pública, privada e híbrida

- Nuvem pública: Um ou mais provedores de serviços que são utilizados por múltiplos clientes, reduzindo o custo na oferta dos mesmos. O cliente não precisa investir em infraestrutura já que o serviço é "compartilhado"

- Nuvem privada: Exclusivo para o cliente, sendo uma estrutura específica para o mesmo, seu próprio data center e infraestrutura. Existe mais controle da infraestrutura e segurança nas mãos do cliente

- Nuvem Híbrida: O equilibrio entre os dois tipos, onde o cliente possui seu datacenter exclusivo, mas também utiliza de um provedor que é compartilhado globalmente

# Principio da responsabilidade compartilhada

Na AWS tanto o cliente, quanto a própria AWS tem responsabilidades quando se trata da nuvem. Existe uma divisão equilibrada (dependendo do serviço) quando se pensa no tipo de infraestrutura adotada, mas na maioria dos casos, a AWS é responsável pelo físico (Data centers, alimentação, internet e segurança física), enquanto o cliente é responsável por tudo que insere na nuvem (dados, certificados e a proteção dos mesmos com principios de segurança oferecidos pela AWS). 

# IAAS, PAAS, SAAS

- IAAS: Infraestrutura como Serviço
  Cliente gerencia instalações de updates de software, escolhe memória e capacidades de suas máquinas (EC2), tendo um maior controle da infraestrutura.
  ex: EC2
  
- PAAS: Plataforma como Serviço
  Cliente não gerencia instalações, mas ainda precisa cuidar de seus dados e aplicações que sobe para a nuvem, sem se preocupar com infraestrutura.
  ex: Elastic Beanstalk, 
  
- SAAS: Software como Serviço
  Cliente não precisa focar em nada além do que inserir seus dados para utilizar o serviço, todas as responsabilidades de infraestrutura e gestão ficam para a AWS.
  ex: Email, Quicksight

# IAM - Identity Access Management 

Serviço onde você pode setar permissões e políticas para um usuário, grupo ou recursos.

- Autenticação:
  Seu usuário e senha, a verificação de permissão para logar naquele recurso.
  ex: quando você loga no console da AWS, a verificação que é feita antes do seu login, confere se você está autenticado corretamente para entrar naquele site.
  
- Autorização:
  Suas permissões, a autorização para acesso ou visualização de determinado recurso.
  ex: ao tentar excluir um bucket, ocorre a verificação de acesso, para entender se você possui permissão para tal ação.

- Usuário: Individuo ou conta que irá realizar acesso aos recursos
- Grupo: Conjunto de usuários, que podem estar sob uma política nesse grupo
- Políticas: Conjunto de regras, geralmente em um arquivo JSON, informando todas permissões e proibições que um usuário, grupo ou recurso possa ter. (É possível utilizar políticas já existentes e criadas pela AWS, como também criar suas próprias políticas baseadas em regras de negócio pessoais.)
- Roles: Permissão que um recurso pode assumir para realizar um trabalho sem precisar de outros acessos. O serviço assume aquela role que contém todas as permissões no momento necessário, sem ter acesso em outros momentos sem necessidade.

  ### ATENÇÃO

**Um usuário pode pertencer a vários grupos, mas um grupo não pode estar inserido dentro de outro**

# Controle de Gastos e Alertas

Para manter um controle efetivo dos gastos na nuvem, é possível criar alertas e orçamentos baseados no que você pode gastar. Além de todos os outros serviços que monitoram gastos e sugerem melhorias, você pode criar um alerta definindo um valor 'x' que não pode ser ultrapassado quando utiliza os recursos AWS. 

# Formas de acesso aos recursos AWS 
Atualmente existem 3 formas de acesso aos recursos AWS: 

- Console: Uma forma mais visual e mais amigável para quem não entende de programção, é basicamente o que se vê ao acessar o site da AWS.
- CLI / Cloudshell: A Command Line Interface é o terminal onde se insere comandos para acessar e gerenciar seus recursos através de código similares aos que usamos no Githhub. No caso do Cloudshell, diferente da CLI tradicional, você não precisa realizar nenhuma instalação já que o mesmo é um recurso totalmente online no console da AWS. 
- SDK: É um framework, como um pacote onde você pode interligar sua aplicação à AWS através de código. 

# EC2 = Elastic Compute Cloud

São como máquinas virtuais na AWS, onde você pode hospedar e executar seus aplicativos, escolhendo poder de computação, armazenamento e outros.
Nessas máquinas você ainda configura sua rede, através das VPCS, Subnets e Security Groups, da mesma forma feita no on-premises, mas simplificado. 
Como EC2 é um IAAS, existem mais responsabilidades do cliente ao se administrar essa máquina, realizando updates de software, cuidando das redes, segurança e etc.

- As EC2 possuem várias categorias: Otimizadas para computação (Ex: C6), Machine Learning (P2), Armazenamento (H1), Memória (R6)

  ## Terminologia dos tipos de instâncias

  O nome das instâncias geralmente é composto pelo seu tipo; que inclui a série, geração e opções, além de seu tamanho (micro, large, etc)  

 <img width="774" height="409" alt="image" src="https://github.com/user-attachments/assets/3b781692-83ba-42b6-9e4c-221c30199812" />


  ## Otimização de recursos

  Na nuvem é sempre recomendado que se desligue ou exclua serviços que não estão sendo utilizados. É possível ainda escalar esses recursos baseado na necessidade. 
  - É possível escalar horizontal ou verticalmente, de forma manual ou automática.
    **Vertical** : Se aumenta ou diminui a capacidade de um recurso, por ex: adicionar mais memória ou processamento de uma máquina específica.
    **Horizontal** : Se aumenta ou diminui a quantidade de recursos, por ex: adicionar mais EC2 em um caso de largo acesso as máquinas. Passando de uma máquina para 3 por exemplo. 

  ## Tipos de compra de EC2

  # On-demand: conforme sua necessidade, não existe um contrato por um tempo determinado. São cobradas em taxas fixas por horas, para cargas de trabalho que não podem ser interrompidas.
  # Reservadas: assim como o nome, você reserva aquela instância por pelo menos um ano, é mais barata que a on-demand mas requer compromisso. 
  # Spot: oferecem até 90% de desconto, mas podem ser encerradas a qualquer momento, havendo apenas um aviso 2 minutos antes. É ideal para cargas que possam ser interrompidas. 


# Amazon EBS - Elastic Block Storage 

  É o armazenamento em blocos, que pode ser anexado a uma instância EC2. É possível anexar múltiplos EBS a uma instância, desde que estejam na mesma zona de disponibilidade. Além de que o EBS possui armazenamento persistente, ou seja, mesmo que a instância seja desligada, os dados não serão perdidos. Sempre bom lembrar desse ponto no caso de exclusão da instância, caso o EBS também não seja excluido, continuará havendo cobranças.

  ## Snapshots EBS - São como "fotos" tiradas de determinado momento da sua máquina para realizar um backup. É possível configurar a frequeência que os mesmos serão feitos. Os instantâneos EBS são armazenados no S3 e para fins de DR (Disaster Recovery) podem ser armazenados em regiões distintas. 

  ### Diferença AMI x Snapshot:

  - AMI é a imagem de toda sua infraestrutura daquela máquina, seu sistema, aplicações, configurações, redes e etc. (Além do próprio EBS que está anexado na instância).
  - EBS é apenas a imagem daquele volume que foi anexado a instância, ou seja, tudo que foi guardado naquele volume. 

# Amazon S3 - Simple Storage Service

  Armazenamento de objetos na nuvem, popularmente chamados de buckets, essas unidades permitem armazenamento com alta disponibilidade. O S3 possui algumas categorias de armazenamento, baseadas no tempo que aqueles objetos serão guardados e quão frequentemente ou não serão acessados. O S3 foi desenvolvido para entregar ate 11 9's de durabilidade, garantindo que seu arquivo armazenado nesse serviço permanecerá seguro e disponível.

  ## S3 Standard - Classe de armazenamento padrão, a mais cara. Utilizada para acessos frequentes e a recuperação de arquivos é praticamente imediata.
  ## S3 Intelligent Tiering - Essa classe monitora o padrão de acesso dos objetos e os move automaticamente para classes compatíveis com o acesso. 
  ## S3 Infrequent Access - Classe de armazenamento para objetos que não são muito acessados, mas precisam ser recuperados rapidamente. 
  ## S3 One Zone -  Objetos são armazenados em apenas uma zona de disponbilidade, mais barato, mas caso ocorram problemas naquela zona, você pode perder seus objetos.
  ## S3 Glacier Instant Retrieval - objetos que raramente são acessados, mas precisam ser recuperados rapidamente. Os objetos ficam disponiveis em tempo real
  ## S3 Glacier Flexible Retrieval - objetos que raramente são acessados, mas podem ser recuperados em questões de minutos. Não ficam disponíveis em tempo real 
  ## S3 Glacier Deep Archive - classe para arquivamento de objetos, quase nunca são acessados e podem ser recuperados em um tempo maior. 

  ### O S3 possui regras de *lifecycle* ou ciclo de vida, onde você pode setar uma quantidade de tempo x, onde o objeto fará transição para uma classe mais barata ou será excluído. 

# DRAWIO - Fluxograma utilizando S3 e Lambda

  Imaginando uma situação onde:
  o usuário faz o upload de uma imagem através da CLI para um bucket ->
  Esse upload trigga a função lambda para processamento -> 
  armazena a foto processada em um novo bucket -> 
  armazena os metadados da foto no dynamodb. 



<img width="840" height="691" alt="Dio Diagram drawio" src="https://github.com/user-attachments/assets/23097f7d-e535-4513-abec-7da893789f67" />


  



