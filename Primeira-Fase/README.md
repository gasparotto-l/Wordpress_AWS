## Descrição
- Antes de começarmos de criar nossa EC2, EFS, RDS. É importante criarmos as estruturas essenciais para o funcionamento dessa aplicacão. Criarmos nessa seção todos os security groups e a VPC.

## Security Groups

## 1. 🖥️ EC2_SG (Instâncias EC2 - WordPress - Subnet Privada)

### 📥 INBOUND RULES

| Tipo | Porta | Origem   | Motivo                          |
|------|-------|----------|---------------------------------|
| HTTP | 80    | lb_SG    | Receber tráfego do Load Balancer |
| SSH  | 22    | Seu IP   | Acesso para manutenção     |
| NFS  | 2049  | efs_SG   | Montagem do EFS                 |

- **HTTP (80)** — Permite que o Load Balancer envie requisições web para a EC2.  
- **SSH (22)** — Garante acesso remoto seguro, preferencialmente via Bastion Host ou IP fixo.  
- **NFS (2049)** — Necessário para montar o volume EFS e armazenar arquivos do WordPress.

### 📤 OUTBOUND RULES

| Tipo        | Porta | Destino     | Motivo                                                 |
|-------------|-------|-------------|---------------------------------------------------------|
| All traffic | All   | 0.0.0.0/0 (via NAT) | Permite atualizações, download de pacotes, acesso ao RDS etc. |

- O tráfego de saída via NAT Gateway permite atualizações e comunicação com outros serviços da AWS.


## 2. 🛢️ rds_SG (RDS - Banco de Dados - Subnet Privada)

### 📥 INBOUND RULES

| Tipo          | Porta | Origem  | Motivo                        |
|---------------|-------|---------|-------------------------------|
| MySQL/Aurora  | 3306  | ec2_SG  | Permitir acesso do WordPress |

- **MySQL (3306)** — Habilita a conexão da aplicação WordPress ao banco de dados RDS.

### 📤 OUTBOUND RULES

| Tipo          | Porta | Destino | Motivo                                                        |
|---------------|-------|---------|----------------------------------------------------------------|
| MySQL/Aurora  | 3306  | ec2_SG  | Responder requisições (por boas práticas, mesmo sendo stateful) |

- Boa prática configurar explicitamente saída, mesmo sendo gerenciado de forma stateful.


## 3. 📁 efs_SG (EFS - Subnet Privada)

### 📥 INBOUND RULES

| Tipo | Porta | Origem  | Motivo                        |
|------|-------|---------|-------------------------------|
| NFS  | 2049  | ec2_SG  | Permitir montagem via NFS     |

- **NFS (2049)** — Habilita a EC2 a montar o EFS como volume compartilhado.

### 📤 OUTBOUND RULES

| Tipo | Porta | Destino | Motivo                    |
|------|-------|---------|---------------------------|
| NFS  | 2049  | ec2_SG  | Comunicação bidirecional  |

- Permite a troca de dados contínua entre EC2 e EFS de forma segura e eficiente.



## 4. ⚖️ lb_SG (Classic Load Balancer - Subnet Pública)

### 📥 INBOUND RULES

| Tipo | Porta | Origem     | Motivo                         |
|------|-------|------------|--------------------------------|
| HTTP | 80    | 0.0.0.0/0  | Receber tráfego da internet    |

- **HTTP (80)** — Permite que usuários da internet acessem o site via Load Balancer.

### 📤 OUTBOUND RULES

| Tipo | Porta | Destino | Motivo                                 |
|------|-------|---------|----------------------------------------|
| HTTP | 80    | ec2_SG  | Encaminhar requisições para EC2s       |

- Direciona as requisições dos usuários para as instâncias EC2 que executam o WordPress.



## Virtual Private Cloud(VPC)
- Acesse o Console AWS e vá para a seção VPC.
- Clique em Create VPC e selecione a opção VPC and more.
- Crie uma VPC com 2 sub-redes públicas e 2 sub-redes privadas.
- Selecione duas Availability Zones (AZs) e um NAT Gateway(1 per AZ).
- Finalize a criação clicando em Create VPC.

IMAGEM

