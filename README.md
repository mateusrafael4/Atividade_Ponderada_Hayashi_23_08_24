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
