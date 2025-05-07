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

![image](https://github.com/user-attachments/assets/bcd334d4-8c9b-4ebc-88ee-2c300d9837d2)

- **HTTP (80)** — Permite que o Load Balancer envie requisições web para a EC2.  
- **SSH (22)** — Garante acesso remoto seguro, preferencialmente via Bastion Host ou IP fixo.  
- **NFS (2049)** — Necessário para montar o volume EFS e armazenar arquivos do WordPress.

### 📤 OUTBOUND RULES

| Tipo        | Porta | Destino     | Motivo                                                 |
|-------------|-------|-------------|---------------------------------------------------------|
| All traffic | All   | 0.0.0.0/0 (via NAT) | Permite atualizações, download de pacotes, acesso ao RDS etc. |

![image](https://github.com/user-attachments/assets/0740743e-7357-491f-8aa5-4656fbed3199)

- O tráfego de saída via NAT Gateway permite atualizações e comunicação com outros serviços da AWS.


## 2. 🛢️ rds_SG (RDS - Banco de Dados - Subnet Privada)

### 📥 INBOUND RULES

| Tipo          | Porta | Origem  | Motivo                        |
|---------------|-------|---------|-------------------------------|
| MySQL/Aurora  | 3306  | ec2_SG  | Permitir acesso do WordPress |

![image](https://github.com/user-attachments/assets/b0779696-5712-4208-b1f8-5badc082b448)

- **MySQL (3306)** — Habilita a conexão da aplicação WordPress ao banco de dados RDS.

### 📤 OUTBOUND RULES

| Tipo          | Porta | Destino | Motivo                                                        |
|---------------|-------|---------|----------------------------------------------------------------|
| MySQL/Aurora  | 3306  | ec2_SG  | Responder requisições (por boas práticas, mesmo sendo stateful) |

![image](https://github.com/user-attachments/assets/0c4f8a19-a588-44a2-9aba-239228124f7e)

- Boa prática configurar explicitamente saída, mesmo sendo gerenciado de forma stateful.


## 3. 📁 efs_SG (EFS - Subnet Privada)

### 📥 INBOUND RULES

| Tipo | Porta | Origem  | Motivo                        |
|------|-------|---------|-------------------------------|
| NFS  | 2049  | ec2_SG  | Permitir montagem via NFS     |

- **NFS (2049)** — Habilita a EC2 a montar o EFS como volume compartilhado.

![image](https://github.com/user-attachments/assets/561ddba1-d65c-474c-a241-5b9d07a81e9e)

### 📤 OUTBOUND RULES

| Tipo | Porta | Destino | Motivo                    |
|------|-------|---------|---------------------------|
| NFS  | 2049  | ec2_SG  | Comunicação bidirecional  |

![image](https://github.com/user-attachments/assets/e33d50a7-cfb7-42a7-8620-776b24e80439)

- Permite a troca de dados contínua entre EC2 e EFS de forma segura e eficiente.

## 4. ⚖️ lb_SG (Classic Load Balancer - Subnet Pública)

### 📥 INBOUND RULES

| Tipo | Porta | Origem     | Motivo                         |
|------|-------|------------|--------------------------------|
| HTTP | 80    | 0.0.0.0/0  | Receber tráfego da internet    |

![image](https://github.com/user-attachments/assets/e74431a9-8a68-43c7-be50-19e52cd636d4)

- **HTTP (80)** — Permite que usuários da internet acessem o site via Load Balancer.

### 📤 OUTBOUND RULES

| Tipo | Porta | Destino | Motivo                                 |
|------|-------|---------|----------------------------------------|
| HTTP | 80    | ec2_SG  | Encaminhar requisições para EC2s       |

![image](https://github.com/user-attachments/assets/e69f2f76-abf1-4560-8c1c-6ffb76039a9e)

- Direciona as requisições dos usuários para as instâncias EC2 que executam o WordPress.


## Virtual Private Cloud(VPC)
- Acesse o Console AWS e vá para a seção VPC.
- Clique em Create VPC e selecione a opção VPC and more.

![image](https://github.com/user-attachments/assets/dfe323a2-60c7-4662-a4b0-158bfda440a4)

- Crie uma VPC com 2 sub-redes públicas e 2 sub-redes privadas.
- Selecione duas Availability Zones (AZs) e um NAT Gateway(1 per AZ).

![image](https://github.com/user-attachments/assets/ba64e675-7c0f-436d-87c8-0ef10c0b2155)

- Finalize a criação clicando em Create VPC.

![image](https://github.com/user-attachments/assets/f9152534-9b53-4ffa-98d3-e119527c1deb)

- Esse deve ser o preview da sua VPC.

