# Motivação
  Pela primeira vez olhei para a infraestrutura com outros olhos, acho que por que o convivio com os meus colegas me motivou a estudar mais sobre, até por que
o meu conhecimento era básico e vi uma oportunidade de aprender como melhorar o dia a dia dos devs. Como a melhor forma de aprender é ensinando, vou mostrar a vocês a minha jornada.
  
  # Introdução
  É interessante antes de começar a catucar o console da AWS, é bom da uma lida nos principais serviços que ela disponibiliza. Acho que os principais que vamos usar são
    
   - IAM
   - EC2
   - Cloud Front
   - S3
   - VPC
   - Route53
   
 Esses são os principais que vamos usar aqui, vamos evoluindo a nossa infra e passando entre eles de acordo com a nossa necessidade. Então não se preocupe, vou tentar explica de forma simples no que cada ferramenta pode fazer.
 
 
# Setup Inicial
  Para começar os trabalhos precisamos criar uma conta no console da amazon, feito isso vamos começar as configurações iniciais de segurança. Mas já? o que tem de segurança logo no início? A própria amazon recomenda que você crie um usuário administrador e não utilize o root por questões de segurança.
  
## Primeiro desafio
  Agora que estamos logados com o nosso usuário root, precisamos criar um usuário com permissões de administrador.

## Algumas explicações
  A amazon trabalha de uma forma que todo serviço que eles oferecem necessariamente precisa de permissões, então podemos criar permissões únicas para um usuário e   para outro, sendo assim conseguimos manter o escopo da necessidade de cada usuário por exemplo:
    - Um dev precisa apenas acessar um s3 para ler e criar arquivos, porém ele não precisa ver o serviço do <b>EC2</b>
      
  Outro detalhe é quando falamos do <b>IAM</b>, basicamente é um serviço que faz o gerencimento dos usuários e permissões com o objetivo de cada um ter sua         responsabilidade e deixar o login de forma mais segura, controlando quem pode logar no console da aws. 
  Já que as explicações foram feitas, vamos começar.
  
  <hr>
  
## Criar um grupo de usuários
 1. Basicamente criar um grupo vai ajudar para o reaproveitamento de permissões quando criamos outro usuário. Dito isso, vamos criar um grupo chamado <b>Administradores</b>, vamos acessar o serviço do IAM e indo na opção do menu <b>Grupos</b>.
 
 2. Pronto, no próximo passo precisamos colocar a politica necessaria para nossos administradores. Procure a politica chamada <b>AdministratorAccess</b> e confirme.
 
## Adicionar o grupo ao usuário administrador
  1. Beleza, agora vamos colocar o grupo em nosso novo usuário, acesse no menu a opção de <b>Usuários</b>.
  2. Ao adicionar um usuário vamos escolher o nome <b>joaozinho</b>.
  3. A aws vai dar algumas opções de acesso para usuário, caso você queira que um usuário só acesse via API ou CLI, basta selecione a opção <b>Acesso programático
</b>, ai você por que eu vou precisar apenas usar a API? uma boa prática que a gente vai vê lá na frente é que quando eu criar um bucket no <b>s3</b> o cenário ideal é criar um grupo apenas com essa permissão para que ele consiga "enxergar" via API ou CLI.
  4. Para o nosso usuário habilite também a opção de acessar o console da amazon, siga a próximo etapa.
  5. Massa, vamos adicionar as permissões que criamos a esse usuário, selecione o nosso grupo <b>Administradores</b>, siga próxima epata.
  6. Por enquanto, vamos ignorar esse rolê de tags que eu não entendi carai nenhum.
  7. Guarde suas credenciais no coração e vamos para o próximo desafio.
  
## Segundo desafio
   Criar uma VPC com subnets privadas e subnets públicas
