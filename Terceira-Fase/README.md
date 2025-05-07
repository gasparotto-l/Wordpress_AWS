## Launch Template
- Acesse create launch template e vamos configurar
- De um nome e descrição ao seu template
- Selecione guidance para obter dicas caso queira utilizar esse template em um auto scaling group.

![image](https://github.com/user-attachments/assets/5b2ad149-f0db-4d50-9b7f-5744ce3edc3f)

- Agora selecione o sistema operacional que deseja usar na imagem, eu utilizei o Amazon Linux.

![image](https://github.com/user-attachments/assets/42488e90-b514-471f-9fbe-e381f66b6afe)

- Selecione o tipo de instancia, no meu caso foi a t2.micro pra poupar gastos.
- Crie uma Key pair e adicione-a, caso queira acessar a instancia por ssh por quaisquer que sejam os motivos.

![image](https://github.com/user-attachments/assets/091e5fb3-000a-4161-9dec-902c5b2b0e82)

- Selecione essas opções
- Não se esqueça de selecionar nosso sg criado previamente.

![image](https://github.com/user-attachments/assets/e5262166-a6de-47ef-bad5-328a5bffb49a)

- Em configuração adicional adicione seu user data, caso queira utilizar o meu, ele está disponivel nessa pasta da Terceira-Fase.
- Nomeado como: "user-data.sh"

![image](https://github.com/user-attachments/assets/4d6acb0d-3944-4f05-b339-a778d2c47096)

- Feito isso partimos pra proxima etapa.

## Load Balancer
- Primeiro selecione um load balancer do tipo classico, como mostrado na imagem.

![image](https://github.com/user-attachments/assets/d3289b5a-24aa-45f0-9033-bcaca7c2fdfe)

- De um nome para seu LB
- Selecione Internet Facing

![image](https://github.com/user-attachments/assets/aeabe346-edf8-46da-9b56-7ae96e22f72e)

- Selecione a VPC criada anteriormente.
- Marque os dois checkboxes referentes as zonas de disponibilidade.
- Selecione as subnets públicas para essas zonas.

![image](https://github.com/user-attachments/assets/30170d2c-9e94-44e3-af61-67f167bf3b8b)

- Selecione o sg feita para o LB nas etapas anteriores, e configure suas rotas da maneira mostrada na imagem.

![image](https://github.com/user-attachments/assets/346502af-245b-4327-b59c-327a0a13b981)

- Review geral do Load Balancer configurado:

![image](https://github.com/user-attachments/assets/19405a1b-90a2-459a-9b0e-393f46903993)


## Auto Scaling Groups
- Primeiro de um nome para seu auto scaling group
- Depois selecione seu launch template criado anteriormente nessa terceira-fase. 

![image](https://github.com/user-attachments/assets/e4d3e127-8286-42df-9c03-592ea736b7fd)

- Selecione a VPC criada previamente.
- Escolha as duas subnets privadas em zonas diferentes.
    - us-east-1-a <- subnet-private-1
    - us-east-1-b <- subnet-private-2

![image](https://github.com/user-attachments/assets/592035bc-3692-4b8b-aad4-518f4ff6676e)

- Selecione "Attach to an existing load balancer".
- E escolha o load balancer que criarmos anteriormente.

![image](https://github.com/user-attachments/assets/b793d9e5-6081-4412-916a-94e610831244)

- Ative os Health checks para load balancer, isso vai nos ajudar a saber se nossas instancias estão funcionando corretamente ou estão com problemas.

![image](https://github.com/user-attachments/assets/07706e81-e080-4b1a-8bb6-4cd0b859c023)

- Agora vamos configurar a capacidade e escalonamento:
    - Desired capacity: 2
    - Min: 2
    - Max: 4
- Selecionei "no scaling policies" por optar simplicidade e funcionalidade nesse projeto. Porém, caso queira fazer algum teste utilizando politicas de escalonamente, fique a vontade.

![image](https://github.com/user-attachments/assets/f590a994-46aa-403d-a0d6-96a41c73f8f0)

- Siga as configurações mostradas, sem politica e deixando as configurações adicionais em default.
- Ative "Enable group metrics collection within CloudWatch caso queira utilizar o cloudwatch para criar alarmes futuramente

![image](https://github.com/user-attachments/assets/1734e06a-7062-418f-b261-74c42c2eeadc)

- Agora basta criar e aguardar alguns minutos, as instancias serão criadas e projeto estará pronto.
- Confira isso na quarta-fase desse repositorio, lá está os teste e a conclusão final.
- Te vejo lá!

