## Testes 
### Testando o Auto-Scaling
- No console da Aws, fui até as intanciais, e dei terminated em ambas as 2 criadas.
- Conforme o esperado elas foram criadas novamente e funcionando.
- Observe na imagem:
![image](https://github.com/user-attachments/assets/6dc6fff7-f6f1-4c13-a7e9-15ec3aeae253)


### Acessando o site e se cadastrando
- Acessamos o site utilizando o Dns do Load Balancer.
- Faça configuração do Wordpress conforme indicado. 

![image](https://github.com/user-attachments/assets/03e515ac-343f-47e4-82c5-df3aa80bc211)

- Faça seu cadastro na plataforma
- Utilizando suas informações, é claro.

![image](https://github.com/user-attachments/assets/729ea211-7dc7-45e8-bcab-8ec19df7224d)

- Cadastrado, agora basta acessar!

![image](https://github.com/user-attachments/assets/8b188a15-f720-410d-a413-a7b236c24ee9)

### Crie um post 
- Na pagina inicial de dashboard do wordpress crie um post, e vamos testar a persistencia de dados nesse post.

![image](https://github.com/user-attachments/assets/baac0ddf-a5cc-41b2-9e40-56a7c2862fe7)

- Pagina criada, derrube e instancia e veja se o conteudo do seu post se manteve na pagina do wordpress
- Se sim, então sua persistencia de dados funciona.

![image](https://github.com/user-attachments/assets/cfe2cf68-5a3d-4cae-b1d3-da890ef90425)

- No meu caso funcionou.

## CloudWatch(EXTRA)
- Configure um cloudwatch para verificar o uso de cpu

- Selecione o Auto Scaling Group criado e acesse Automatic scaling > Create dynamic scaling policy.

- Configure da seguinte maneira:
    - Policy type: Simple scaling.
    - Scaling policy name: personalize com um nome.
    - Take the action: selecione Add, com valor 2.

- Navegue até a seção ClouWatch, em Alarms, clique em In alarm e depois em Create alarm.

![image](https://github.com/user-attachments/assets/af4f03a8-9aac-4570-aa8b-b54c40069afa)

- Clique em Select metric > EC2 > By Auto Scaling Group.

- Selecione a métrica CPUUtilization e clique em Select metric.

![image](https://github.com/user-attachments/assets/9a6cde34-6a8e-4363-ae74-dd27411243ac)

- Em Whenever CPUUtilization is..., selecione Greater/Equal e digite 80 em than....

- Em Notification, clique em Remove para excluir a notificação.

- Clique em Auto Scaling action, selecione o Auto Scaling Group criado.

![image](https://github.com/user-attachments/assets/4dee72e0-7e87-41cd-8bc8-3dff39610927)

- Dê um nome para o alarme e finalize clicando em Create alarm.

![image](https://github.com/user-attachments/assets/2e53e59b-57a4-4634-aa34-9030caa9996d)

- Preview do alarme do cloudwatch

![image](https://github.com/user-attachments/assets/f609384a-f4d0-41e0-b9a3-41a904f590d2)

- Alarme criado, espere o status de OK.

![image](https://github.com/user-attachments/assets/7104489d-2dc6-42bd-b515-ded1910eb1fe)

- Agora temos um alarme de cloudwatch criado.