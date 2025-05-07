## Conclusão

- O projeto Wordpress_AWS teve como principal objetivo demonstrar a implantação de uma aplicação WordPress utilizando a infraestrutura da Amazon Web Services (AWS). Através da automação com o AWS CloudFormation, foi possível provisionar e configurar recursos essenciais como EC2, RDS, VPC, Auto Scaling, Load Balancer e EFS, compondo uma arquitetura escalável, resiliente e segura para hospedagem web.

- A realização prática deste projeto permitiu compreender melhor os conceitos de infraestrutura como código, automação em nuvem e os benefícios da escalabilidade dinâmica. Além disso, reforçou a importância de seguir boas práticas de segurança e gestão de recursos em ambientes de produção.

## Observações

- É importante seguir uma sequência lógica na criação da infraestrutura, iniciando pela rede (VPC, sub-redes), depois o banco de dados (RDS) e por fim a instância EC2 com o WordPress. Isso garante que todos os serviços consigam se comunicar corretamente.

- Ao configurar permissões para as instâncias e serviços, deve-se garantir que apenas o necessário esteja habilitado, evitando permissões excessivas que possam comprometer a segurança da aplicação.

- O banco de dados precisa estar com as portas liberadas no grupo de segurança e o endpoint corretamente referenciado no wp-config.php. Erros nessa etapa impedem a instalação e o funcionamento do WordPress.

- O ponto de montagem do EFS precisa estar acessível e corretamente conectado à instância EC2. É importante testar se o sistema de arquivos está ativo e persistindo os dados do WordPress corretamente.

- Para fins de aprendizado, é possível utilizar apenas uma instância EC2. No entanto, para aplicações em produção, recomenda-se configurar o Load Balancer e Auto Scaling para garantir alta disponibilidade e escalabilidade.

## Agradecimentos

- Agradeço sinceramente a você, por dedicar seu tempo à análise deste projeto. Espero que a proposta desenvolvida aqui contribua positivamente para minha formação e para futuras aplicações práticas dentro do campo de computação em nuvem.

- Se notar quaisquer que sejam os erros ou possiveis melhorias, entre em contato comigo, estarei a disposição para fazer mudanças.