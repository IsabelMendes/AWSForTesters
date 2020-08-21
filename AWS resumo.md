# Amazon WebService: resumo da arquitetura

## AWS API Gateway

Usando API Gateway , você pode criar APIs do RESTful e WebSocket que habilitam aplicativos de comunicação bidirecionais em tempo real. O API Gateway dá suporte a cargas de trabalho com conteiners e sem servidor, além de aplicativos da Web.

### Autorização da AWS



### Chaves de API

O API Gateway ajuda a gerenciar o ecossistema de quem poderá acessar suas APIs, através de chaves de acesso.

É possível a criação de chaves API Gateway, definir permissões de acesso para cada chave e distrubuí-las a desenvolvedores externos.

O uso de chaves é totalmente opcional e deve ser habilitado para cada método.

## AWS Lambda

Aplicações serveless tem chamado a atenção em arquitetura de sistemas, por possibilitarem:

- Execução de pequenas funções, sem a necessidade de grandes infraestruturas;
- Custo de infraestrutura ociosa;
- Escalabilidade para atender muitas requisições ao mesmo tempo;
- Facilidade de instalação de novas funções.



## AWS DynamoDB

É um bando de dados não relacional, que se basea em documentos e estruturas de chave-valor. Possui operações de acesso extremamente rápidas em qualquer escala. Também oferece:

- Agendamento de backup;
- Recuperação de dados;
- Mecanismos que possibilitam avisar a aplicação em caso de mudança de registros;
- Alta performance para operação de escrita e leitura;
- Mecanismo para exclusão automática de registros.

## AWS SQS

Mecanismo de filas para troca de mensagens dos serviços da AWS, como por exemplo estabelecimento de comunicação entre as aplicações. Características:

- Garatia de entrega de pelo menos 1 mensagem;
- Possui mecanismos para evitar inversão na ordem das mensagens.

## AWS CloudWatch

Serviço de monitoramento e gerenciamento:

- Visualização de logs gerados por outros recursos e aplicações;
- Gráficos de métricas como consumo de memória e processamento;
- Visualização de eventos;
- Informações concentradas em um único lugar. 

# O que posso testar/monitorar em cada serviço

## API Gateway

- Latência
- Erro 4XX: Campos vazios
- Erro 5XX: Id com string
- API calls: quantidades de invocações

## Lambda Products

- Quantidade de invocações
- Duração
- Taxa de erros e sucesso

## Lambda Products no CloudWatch

- Logs de invocações recentes em segundos
- Invogações por memória: quanto gastei de memória?
- Log de uma invocação de criação de produto

## Tabela no DDB Product

- Capacidade de leitura e escrita na tabela
- 1 unidade = 4 Kbytes da dados
- Latência de get e put (post)
- Produto na tabela
- Editando na tabela: Não cria eventos

## SQS

- As mensagens que foram criadas pelo Lambda Product através dos eventos, entram no SQS e são consumidas pelo Lambda Product Event Consumer.
- Imagine um filtro de água. 

## Tabela no DDB Events

- São inseridos todos os eventos da aplicação
- Exemplo: tudo o que aconteceu com o produto de Id=5

## Arquitetura incompleta - parte 1

- Como a mensagem chega na fila?
- No código, classe do Evento devo procurar os parâmetros da mensagem
  - Id: deve ser int
  - Código: string
  - Event: CREATED
  - Tempo: data + hora

- Na tabela do Evento:
  - Filtar pelo Id
  - Ver o log no CloudWatch
  - Criamos o evento e não o produto

## Arquitetura incompleta - parte 2

- No Lambda Product faremos um get no produto:
  - quando busco o produto, um evento deverá ser criado
  - Esse evento deverá ter o Id do usuário. 
  - Criar o Json.







