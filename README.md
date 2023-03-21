### Fluxo
#### Primeiro fluxo
Scraping -> Tratamento em base histórica -> Vetorização por TFIDF -> Clusterização por MiniBatchKmeans -> Treino para RandomFlorestClassifier
#### Segundo fluxo
Base nova de respostas -> Scrapping -> Tratamento -> Teste para RandomFlorestClassifier 
### Cenário
O código em questão se trata de um projeto realizado em um período de 2 meses ao qual foi designado à mim em meu período de estágio (6meses). A empresa realiza cobranças, via SMS (whatsapp) e e-mail, de grandes instituições financeiras, o objetivo era pegar as respostas das mensagens enviadas e classifica-las para que um analista realizasse a visualização em cima das mensagens mais importantes e respondesse de forma personalizada, de acordo com o que foi pedido/respondido. (O script de SMS decidi não coloca-lo visto que utiliza-se os mesmos modelos utilizados porém com menor tratamento e algumas peculiaridades)

### Desenvolvimento
Foi realizado então o processo de captura em cima de um email ao qual só recebia as respostas das mensagens enviadas, após captura-los, os dados eram tratados de uma forma totalmente personalizada ao contexto que se encontravam e posteiormente levados à um arquivo de clusterização com 19 possibilidades de encaixe, provindos de uma base histórica de 250.000 linhas de respostas classificadas a partir do modelo não supervisionado (MiniBatchKmeans), que previamente foi utilizada de treino pelo modelo RandomForestClassifier e após isso, a base de dados nova, já tratada, era testada pelo modelo supervisionado, utilizando os clusters como classe

Sobre os 19 clusters encontrados na base histórica, aqui estão seus significados:
- 0 = Alega pagamento
- 1 = Alto atrito
- 2 = Desconhece Pessoa
- 3 = Desconhece dívida
- 4 = Interesse em negociar
- 5 = Requer boleto/fatura
- 6 = Promessa de pagamento
- 7 = Recusa pagamento
- 8 = Ok
- 9 = Ameaça litígio
- 10 = Variedade
- 11 = Saudações
- 12 = Sim
- 13 = Requerem outra forma de pagamento
- 14 = Não incomodar
- 15 = Requer cancelamento
- 16 = Lixo (erros)
- 17 = Saber valor de dívida
- 18 = Sem condições

Esse projeto teve curta duração, visto que tive de entender o modelo de negócio, verificar clusterização com diversas formas de tratamento e testar diversos modelos supervisionados e não supervisionados até achar o que obtinha maior acurácia em cada um dos casos. Após esses 2 meses fui movido para outro projeto. 

Caso eu continuasse no projeto, iria realizar a automação e a comunicação entre os arquivos, realizando assim um modelo que poderia ser aplicado semanalmente de forma automática, comunicando assim com o banco de dados da empresa para que obtivesse todos os dados (Sobre email remetente, data, cluster, cpf, entre outros) armazenados com suas referêntes "PK's" para consulta futura, além de possíveis otimizações em cima do script.

OBS: (Não pude explorar a biblioteca "Bert" para NLP pois o computador disponibilizado pela empresa possuia certas limitações quanto à instalações)
