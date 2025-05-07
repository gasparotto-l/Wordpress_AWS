## RDS
- Agora crie o banco de dados, para isso siga os passos abaixo:

#### Primeiro Passo
- Selecione standard create
- Selecione MySQL

![image](https://github.com/user-attachments/assets/ce1eb8c7-971f-4117-bad6-aaca43b1909f)

- Selecione a Engine version, eu escolhi a 8.4.5, por ser a mais recente.
- Selecione Free Tier(queremos gastar o minímo)

![image](https://github.com/user-attachments/assets/f92a855c-3136-494f-b597-a6c90935d9b3)

- Agora selecione single-AZ DB

![image](https://github.com/user-attachments/assets/c3c0a91d-8773-48ef-8410-9efe16471b2a)

- De um nome identificação para o DB.
- Configure suas credenciais assim como mostrado.

![image](https://github.com/user-attachments/assets/d1fd3051-103b-492b-a786-9c78d28dfc8d)

- Selecione db.t3.micro
- Selecione general purpose gp3

![image](https://github.com/user-attachments/assets/eb975410-363d-4745-a8bb-bd4885b1f750)

- Siga as configurações da minha imagem
- Use o sg criado para rds anteriormente.

![image](https://github.com/user-attachments/assets/846eb901-74fe-485a-a345-c56d27017a83)

- Use a porta padrão de banco de dados 3306
- Utilize database authentication

![image](https://github.com/user-attachments/assets/ab141585-3238-436a-85e7-b3b00ce60f5a)

- De um nome inicial para seu database, isso é essencial para evitar erros.
- Vamos precisar desse nome para nosso user-data.

![image](https://github.com/user-attachments/assets/ac195562-3f4f-46fb-9fea-1e714cb9b292)


## EFS
- Agora vamos criar nosso EFS:
    - Selecione regional
    - Selecione Bursting
    - Selecione General Purpose

![image](https://github.com/user-attachments/assets/f2a147ab-fb8c-47eb-a73b-9a1f73b85145)

- Selecione sua VPC criada anteriormente
- Selecione em ambas os security groups da EFS já criados.

![image](https://github.com/user-attachments/assets/7c55a5e2-fcf1-422e-a6eb-9a72ed2d852d)
