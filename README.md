# Azure Machine Learning (Bootcamp DIO)

Este repositório foi criado para poder registrar o passo a passo feito no projeto **Trabalhando com Machine Learning na Prática no Azure ML** do [Bootcamp Microsoft Azure AI Fundamentals](https://www.dio.me/bootcamp/microsoft-azure-ai-fundamentals), por meio da plataforma [DIO](https://www.dio.me).

## Etapas realizadas durante o projeto

A seguir irei descrever brevemente quais foram as etapas necessárias a serem realizadas para poder realizar o laboratório do projeto por meio da plataforma da [Microsoft Azure](https://azure.microsoft.com/pt-br).

### Criação da Conta no Microsoft Azure

Para poder seguir as etapas do projeto, que foram exemplificadas por meio dos vídeos da [Valéria Baptista](https://www.linkedin.com/in/valeriabaptista), e também por meio deste [tutorial](https://microsoftlearning.github.io/mslearn-ai-fundamentals/Instructions/Labs/01-machine-learning.html), primeiro. é necessário registrar na Azure com uma conta de teste gratuita, com o período de 30 dias e com 200 dólares em forma de créditos disponibilizados por meio dessa conta.

### Criando um Workspace no Azure Machine Learning
#### Grupo de Recursos
Com a conta criada, selecionei o recurso do Azure Machine Learning, selecionei minha subscrição e criei um grupo de recursos, para poder ser utilizado neste e nos futuros projetos do bootcamp.
#### Possibilidades do Azure ML
Com o deploy feito do recurso, selecionei para poder explorar o recurso, e consequentemente para abrir o estúdio do Azure ML, onde por ele posso selecionar qual tipo de tarefa desejo realizar, criar automações, utilizar notebooks, entre outros recursos.
Com o workspace selecionado, escolhi para poder criar um novo trabalho de ML Automatizado.

### Construindo um Tarefa de Machine Learning Automatizada
#### Escolha dos dados e tipo de tarefa
Após a configuração inicial, no qual preenche os dados básicos sobre o trabalho e o experimento, fui para a etapa de selecionar o tipo da tarefa e quais dados pretendia usar, que selecionei o tipo de regressão, consultando/consumindo os dados de uma tabela por meio de um arquivo disponível da web, disponibilizado pela própria Microsoft no tutorial citado acima. Com as delimitações feitas para reconhecer os padrões do arquivo CSV que está sendo consumido os dados, foi feito uma checagem para validar se as variáveis e os valores estavam adequados com o que está preenchido na tabela. Após a validação, prosseguimos para a etapa de configuração das tarefas.
##### Métricas e Limites
Na configuração, foi delimitado qual coluna da tabela seria escolhida como a coluna de destino para a tarefa, além de selecionar qual métrica seria utilizada pela IA para poder realizar a análise/predição das informações, assim como escolher quais modelos são permitidos, e os valores limites para a tarefa poder ser realizada e concluída, como Máximo de Avaliações, Máximo de Nós, Tempo Limite do Experimento, entre outros valores. Por fim, seleciona-se qual tipo de validação deseja utilizar, com suas configurações, variando pelo tipo escolhido, e se há a necessidade de usar algum dado de teste.
##### Escolha da VM e confirmação da tarefa
Por fim, seleciona-se qual recurso de computação será usado para executar o trabalho de treinamento, o que inclui o tipo de computação, tipo de máquina virtual, tamanho dessa máquina e quantas instâncias serão utilizadas. Com o valores preenchidos, aparece uma tela para revisão das informações, e tudo estando dentro dos conformes, pode-se Enviar o trabalho de treinamento.

A seguir temos um print do resultado da minha replicação desta tarefa descrita acima:
![image](https://github.com/NichZilli/azure-machine-learning-bootcamp-dio/assets/61953808/3ace4fe3-35fc-4eae-a488-5a55c6f6be8c)

### Testando o modelo gearado pelo Endpoint
#### Métricas
Com a tarefa finalizada, temos acesso as métricas geradas a partir do modelo de dados que foi consumido, no qual podemos visualizar todos os cálculos que foram gerados a partir dos dados, como a variância, média, mediana, entre outros valores, assim como dois gráficos, em que o primeiro apresenta um comparativo do valor real com o valor da predição, e o segundo um histograma da coluna de dados selecionada posteriormente na configuração, no caso, a *residuals*. A seguir, temos umas imagens para ilustrar os gráficos e os valores calculados:
![image](https://github.com/NichZilli/azure-machine-learning-bootcamp-dio/assets/61953808/1464735b-53d2-4c33-81e4-3507046f5f7c)
![image](https://github.com/NichZilli/azure-machine-learning-bootcamp-dio/assets/61953808/387b3fe3-2299-46bf-83ca-d00d3da47a56)
![image](https://github.com/NichZilli/azure-machine-learning-bootcamp-dio/assets/61953808/84faaf51-22d2-4e19-8704-0d01f4e1f2fd)
#### Teste por meio de um Endpoint
Depois da análise das métricas apresentadas acima, podemos realizar um teste do modelo gerado a partir de um endpoint por meio da plataforma, no qual esse teste pode ser visualizado de múltiplas maneiras, o que inclui: uso/visualização do teste por meio de um endpoint de uma API REST ou por meio de uma URI de um endpoint estilizado pelo Swagger (ou OpenAPI).

Tendo em vista, foi realizado um teste sobre o modelo de dados gerado, a partir de um input do formato JSON, com os seguintes valores:
```json
 {
   "Inputs": { 
     "data": [
       {
         "day": 1,
         "mnth": 1,   
         "year": 2022,
         "season": 2,
         "holiday": 0,
         "weekday": 1,
         "workingday": 1,
         "weathersit": 2, 
         "temp": 0.3, 
         "atemp": 0.3,
         "hum": 0.3,
         "windspeed": 0.3 
       }
     ]    
   },   
   "GlobalParameters": 1.0
 }
```

Com o input correto, cliquei em "Testar" para poder visualizar o resultado a partir dos valores que inseri como entrada, e o resultado gerado está no arquivo `predict-rentals-endpoint-output.json` dentro desse repositório, no qual gerou a seguinte saída:

```json
{
  "Results": [
    344.22922757258226
  ]
}
```

E com isso, temos o teste e o laborátorio da Azure ML finalizado. Gostei bastante sobre a forma que a plataforma apresenta todos os recursos, principalmente sobre a análise de métricas, no qual apresenta de forma bem detalhada sobre cada cálculo e valor gerado.
