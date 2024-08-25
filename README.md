# Atividade_Ponderada_Hayashi_23_08_24
Repositório criado para a atividade em grupo em sala correspondente a aula do professor Victor Hayashi no dia 23/08/2024

**Alunos participantes:** André Lessa, Arthur Reis, Jonas Sales, Luiz Junior, Luiz Granville, Mateus Rafael e Vinicius Souza.


## Construção da atividade
Para resolver a atividade, o grupo separou em 2 notebooks, correspondendo à parte A e à parte B.

### Parte A
O notebook da parte A corresponde a extração de features e preparação dos dados, construção da rede neural usando Keras, configuração do TensorBoard, treinamento e avaliação do modelo.

#### Modelo
Para a construção do modelo de rede neural, o grupo usou o Sequential e os seguintes atributos:
- **Embedding:** responsável por definir o tamanho do vocabulário de palavras únicas no dataframe, configurado com o vocabulário + 1, que pode ser um token de padding ou desconhecido como entrada; dimensionalidade de cada palavra representada por um vetor de 128 dimensões como saída; e comprimento máximo das sequências de palavras em cada amostra.
- **Primeira camada (LSTM):** camada com 64 unidades LSTM, ou seja, 64 células de memória e retorno da sequencia completa de saída ao invés de receber apenas a última saída, ponto necessário para alimentar a próxima camada LSTM;
- **Dropout:** especifica que 0.5 é a probabilidade de cada neurônio ser "desligado" durante o treinamento, abordagem usada para prevenir overfitting;
- **Segunda camada (LSTM):** camada com 64 unidades LSTM, ou seja, 64 células de memória, porém com o retorno da sequência não especificado (False), o que retorna apenas a última saída da sequência;
- **Primeira camada Densa:** camada com 32 neurônios totalmente conectada e função de ativação ReLU, introduzindo não-linearidade no modelo;
- **Segunda camada Densa:** o número de neurônios nesta camada é igual ao número de classes únicas e a função de ativação Softmax produz a probabilidade de cada classe, garantindo que a soma das probabilidades seja 1.

A compilação do modelo usa otimizador Adam, função de perda 'sparse_categorical_crossentropy' e métrica de acurácia.


#### Treinamento
O treinamento do modelo é feito com 10 épocas e analisa acurácia e perda para treino e para validação do aprendizado da rede neural, onde o melhor resultado foi de 27.33% de acurácia de treino na epoca 6 de 10 e estabilizada em 20,79% na acurácia de validação.


#### Métricas
As métricas pedidas na atividade foram: Acurácia, Precisão, Recall e F1-Score e os resultados obtidos no modelo foram:
- Accuracy: 0.2079, ou 20,79%
- Precision: 0.0514, ou 5,14%
- Recall: 0.2079, ou 20,79%
- F1-Score: 0.0824, ou 8,24%


### Parte B
O notebook da parte B corresponde a aplicação de Word2Vec e visualização através do Embedding Projector

#### Pré-processamento
Antes de configurar e treinar o modelo, o grupo fez um pré-processamento do dataset, separando as colunas de pergunta e intenção e transformando em LabelEncoder. Após este processo, o dataset foi dividido em 2, sendo 80% dele para treinamento e os outros 20% para testes.

#### Treinamento do Modelo

**Entrada**
*sentences*: lista de sentenças de texto;
*model*: modelo Word2Vec treinado;
*embedding_size*: dimensão dos vetores de embedding configurado com tamanho 100.

**Processamento**
Dentro da função desta finalidade, foi criada uma variável que recebe uma lista vazia, a qual será usada para armazenar os outputs do modelo treinado, o qual itera da seguinte forma:
- um loop que percorre cada sentença na lista de sentenças de texto e divide a sentença em palavras;
- para cada palavra na lista de palavras, é feita uma verificação para se a palavra está no vocabulário do modelo e obtém o seu vetor de embedding. Caso não esteja, utiliza um vetor de zeros com a dimensão embedding_size;
- calcula a média dos vetores de embedding das palavras na sentença. Caso o vetor não tenha palavras no vocabulário, a média é um vetor de zeros;
- adiciona um vetor de embeddings na lista vecs.

**Saída**
Um array NumPy qye contém os vetores de embedding de todas as sentenças.


**Treinamento do Modelo Word2Vec**
Para o treinamento do modelo, foram utilizadas as seguintes configurações:
- **embedding_size:** para definir que a dimensão dos vetores deve ser igual a 100;
- **word2vec_model:** para treinar um modelo Word2Vec usando as sentenças em X_train;
- **sentences:** para dividir cada linha em X_train em palavras para formar as sentenças de treinamento;
- **vector_size:** para definir a dimensão dos vetores de embedding, tal qual o embedding_size;
- **window:** para definir o tamanho da janela de contexto para o treinamento do modelo Word2Vec;
- **min_count:** para definir o número mínimo de ocorrências de cada palavra a ser incluída no vocabulário;
- **workers:** para definir o número de threads para o treinamento.

**Transformação das Sentenças em Vetores**
Estruturada em duas linhas para realizar a transformação das sentenças em vetores usando o modelo Word2Vec treinado e a função *send_to_vec* para X_train e para X_test


#### Treinamento do Classificador
Nesta etapa, foi feita uma função softmax para o treinamento do classificador de regressão logística com o modelo Word2Vec. Para isso, foi feito:
- **Normalização dos dados com Softmax**
- **Definição dos base learners**
- **Definição do meta learner**
- **Definição do StackingClassifier**
- **Pipeline para treinar o StackingClassifier**
- **Treinamento do modelo Stacking** e
- **Avaliação do modelo com as métricas de avaliação: precision, recall, f1-score e support**

#### Visualização do Word2Vec com PCA
Para visualizar a distribuição dos vetores, foi feito um gráfico de dispersão para entender como ficou distribuída a dimensionalidade dos vetores.
