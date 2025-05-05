## Descrição
- Antes de começarmos de criar nossa EC2, EFS, RDS. É importante criarmos as estruturas essenciais para o funcionamento dessa aplicacão. Criarmos nessa seção todos os security groups e a VPC.

## Security Groups

### 🖥️ EC2 Pública

#### INBOUND RULES

| TIPO | INTERVALO DE PORTAS | ORIGEM     |
|------|----------------------|------------|
| SSH  | 22                   | Meu IP     |
| HTTP | 80                   | 0.0.0.0/0  |

- SSH (porta 22) — Permite acesso via terminal apenas a partir do seu IP, garantindo maior segurança.  
- HTTP (porta 80) — Libera acesso público à aplicação web hospedada na EC2.

#### OUTBOUND RULES

| TIPO           | INTERVALO DE PORTAS | DESTINO     |
|----------------|----------------------|-------------|
| Todo o tráfego | Tudo                 | 0.0.0.0/0   |

- Permite que a EC2 acesse a internet (downloads, APIs externas etc).

---

### 🔒 EC2 Privada

#### INBOUND RULES

| TIPO           | INTERVALO DE PORTAS | ORIGEM                      |
|----------------|----------------------|-----------------------------|
| SSH            | 22                   | SG da EC2 Pública           |
| NFS            | 2049                 | SG do EFS                   |
| HTTP           | 80                   | SG do ELB                   |
| MYSQL/Aurora   | 3306                 | SG do RDS                   |

- SSH — Permite acesso somente pela EC2 pública (bastion host).  
- NFS — Permite que a EC2 use o sistema de arquivos EFS.  
- HTTP — Permite comunicação do Load Balancer com a aplicação.  
- MySQL — Permite conexão da EC2 privada ao banco de dados RDS.

#### OUTBOUND RULES

| TIPO           | INTERVALO DE PORTAS | DESTINO       |
|----------------|----------------------|----------------|
| HTTP           | 80                   | 0.0.0.0/0       |
| MYSQL/Aurora   | 3306                 | SG do RDS       |
| NFS            | 2049                 | SG do EFS       |
| Todo o tráfego | Tudo                 | 0.0.0.0/0       |

- Libera conexões da EC2 com internet e recursos internos como banco de dados e armazenamento.

---

### 🛢️ RDS

#### INBOUND RULES

| TIPO         | INTERVALO DE PORTAS | ORIGEM            |
|--------------|----------------------|-------------------|
| MYSQL/Aurora | 3306                 | SG da EC2 Privada |

- Garante que apenas a EC2 privada tenha acesso ao banco, evitando acessos indevidos.

#### OUTBOUND RULES

| TIPO           | INTERVALO DE PORTAS | DESTINO     |
|----------------|----------------------|-------------|
| Todo o tráfego | Tudo                 | 0.0.0.0/0   |

- Permite saída do RDS para resolver DNS, atualizações e outras necessidades internas.

---

### 📁 EFS

#### INBOUND RULES

| TIPO | INTERVALO DE PORTAS | ORIGEM            |
|------|----------------------|-------------------|
| NFS  | 2049                 | SG da EC2 Privada |

- Permite que a EC2 privada monte e acesse o volume EFS.

#### OUTBOUND RULES

| TIPO           | INTERVALO DE PORTAS | DESTINO     |
|----------------|----------------------|-------------|
| Todo o tráfego | Tudo                 | 0.0.0.0/0   |

- Permite que o EFS responda e mantenha conexões com a EC2.

---

### ⚖️ ELB (Load Balancer)

#### INBOUND RULES

| TIPO | INTERVALO DE PORTAS | ORIGEM     |
|------|----------------------|------------|
| HTTP | 80                   | 0.0.0.0/0  |

- Permite que qualquer cliente da internet envie requisições HTTP ao ELB.

#### OUTBOUND RULES

| TIPO | INTERVALO DE PORTAS | DESTINO    |
|------|----------------------|------------|
| HTTP | 80                   | 0.0.0.0/0  |

- Permite que o ELB encaminhe requisições para as instâncias EC2 privadas.


## Virtual Private Cloud(VPC)



## EC2 com User-Data

### Iniciando uma Instancia EC2

### 