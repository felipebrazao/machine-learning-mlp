# Roteiro da apresentação

Tempo sugerido: **10 a 12 minutos**, cerca de 40 a 55 segundos por slide de conteúdo.

## 1. Capa

Apresentar o problema, o uso de uma MLP para regressão e a comparação entre Random Search e TPE.

## 2. Equipe, escopo e uso de IA

Apresentar os integrantes e declarar o uso do Codex. Ressaltar que a equipe executou os experimentos, conferiu os resultados e assumiu a responsabilidade pela interpretação.

## 3. Problema e conjunto de dados

Explicar que o alvo é o preço efetivo de venda, em dólares. Destacar o tamanho da base e a variedade de atributos de veículo, condição e mercado.

## 4. Pipeline experimental

Explicar que 20% dos dados foram isolados antes dos ajustes. A seleção ocorreu por validação cruzada no treino, evitando usar o teste para escolher hiperparâmetros.

## 5. MLP e espaço de busca

Mostrar que foi usada uma rede densa adequada à regressão, com saída linear. Explicar brevemente os hiperparâmetros avaliados e que as duas estratégias receberam o mesmo orçamento.

## 6. Random Search versus TPE

Destacar que Random Search venceu no melhor resultado isolado por aproximadamente 4,2%. O TPE, porém, foi mais consistente ao longo das 25 tentativas.

## 7. Andrey — learning rate

Explicar que taxas próximas de 1e-4 funcionaram melhor. Taxas altas pioraram fortemente o erro, tornando este o hiperparâmetro de maior impacto.

## 8. Felipe Gabriel — batch size

Mostrar que o efeito não foi monotônico e que o lote 128 obteve o melhor equilíbrio entre erro e estabilidade.

## 9. Felipe Vieira — neurônios

Explicar que redes estreitas perderam desempenho. Com 256 neurônios ocorreu o menor erro; aumentar para 512 não justificou o custo adicional.

## 10. Gabriel — paciência

Explicar que todos os valores tiveram o mesmo MAE porque o treinamento atingiu o limite de épocas antes de a paciência atuar. O valor 4 seria suficiente nessa configuração.

## 11. Ablação de MMR

Explicar que MMR é uma referência de mercado muito forte. A MLP melhora essa referência, mas retirar o atributo aumenta o MAE em 83,1%. Ressaltar que ele só deve ser usado se estiver disponível antes da venda.

## 12. Teste reservado

Apresentar as três métricas finais. Comentar que as curvas indicam leve overfitting tardio, controlado pelo Early Stopping, sem evidência forte de underfitting.

## 13. Síntese crítica

Retomar as respostas exigidas: estratégia vencedora, hiperparâmetro mais importante, comportamento de generalização e influência de MMR. Citar as limitações.

## 14. Conclusão

Encerrar com o resultado final e reforçar que desempenho alto deve ser interpretado junto com a disponibilidade real dos atributos.
