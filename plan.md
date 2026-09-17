# Planejamento — Trabalho MLP

## 1. Proposta e validação do dataset

- **Dataset:** Vehicle Sales and Market Trends Dataset.
- **Fonte:** <https://www.kaggle.com/datasets/syedanwarafridi/vehicle-sales-data>.
- **Problema:** regressão supervisionada.
- **Variável-alvo:** `sellingprice` — preço efetivo de venda do veículo, em dólares.
- **Dimensão esperada:** aproximadamente 558.837 instâncias, 15 atributos preditores e 1 alvo.
- **Objetivo:** estimar o preço de venda de um veículo a partir de suas características, estado de conservação e informações de mercado.

> Antes de prosseguir com os experimentos, submeter esta proposta para validação da professora, conforme o enunciado.

## 2. Organização do projeto e reprodutibilidade

```text
data/
  raw/                 # arquivo original baixado do Kaggle (não alterar)
  processed/           # dados derivados; gerados pelo notebook/script
notebooks/
  01_exploracao_e_mlp.ipynb
plan.md
```

- O arquivo original será armazenado em `data/raw/` e não será incluído em um eventual repositório Git.
- A origem, o link e a data do download serão registrados no notebook.
- Fixar uma semente aleatória única em todas as divisões e experimentos para permitir reprodução.

## 3. Análise exploratória e pré-processamento

1. Carregar `car_prices.csv`, inspecionar tipos, duplicatas e valores ausentes.
2. Examinar `sellingprice`: estatísticas descritivas, histograma, dispersão e valores extremos.
3. Remover `vin`, pois é um identificador praticamente único e não generaliza.
4. Converter `saledate` em atributos úteis (ano, mês, dia da semana), se a qualidade do campo permitir.
5. Tratar dados ausentes: imputação numérica e categórica dentro do pipeline.
6. Para variáveis categóricas, aplicar One-Hot Encoding, agrupando categorias raras quando necessário.
7. Para variáveis numéricas, aplicar `StandardScaler` dentro do pipeline.
8. Investigar `mmr`: ele só será mantido se representar informação disponível antes da venda; seu impacto será discutido como possível fonte de previsão excessivamente fácil.
9. Avaliar a assimetria de `sellingprice`. Se apropriado, treinar com `log1p(sellingprice)` e converter as previsões para dólares na avaliação.

## 4. Separação e avaliação

- Reservar **20%** das observações para teste antes de qualquer ajuste de hiperparâmetros.
- Usar uma divisão estratificada por faixas de preço (quantis), quando viável.
- Executar validação cruzada `KFold` com 3 ou 5 folds **somente** no conjunto de treinamento.
- Métrica principal de seleção: **MAE** (erro médio absoluto), por ser interpretável em dólares.
- Métricas finais adicionais: **RMSE** e **R²**.

## 5. MLP e busca de hiperparâmetros

- Construir uma MLP de regressão com saída linear e `EarlyStopping`.
- Aplicar **Random Search** com validação cruzada e orçamento de **25 configurações**.
- Aplicar **TPE com Optuna** usando exatamente o mesmo espaço de busca, mesma validação, métrica e orçamento de **25 trials**.

Espaço inicial de busca:

| Hiperparâmetro | Valores/faixa inicial |
| --- | --- |
| Camadas ocultas | 1 a 3 |
| Neurônios por camada | 32, 64, 128, 256 |
| Ativação | `relu`, `tanh` |
| Learning rate | log-uniforme entre 1e-4 e 1e-2 |
| Batch size | 32, 64, 128 |
| Otimizador | `adam`, `rmsprop` |
| Paciência do early stopping | 8, 12, 16, 20 |

## 6. Comparação e análise de sensibilidade

- Registrar os principais resultados de cada estratégia de busca em tabelas.
- Exibir a evolução dos trials e a importância estimada dos hiperparâmetros pelo TPE.
- Comparar Random Search e TPE pelo melhor MAE de validação e estabilidade dos resultados.
- Cada integrante investigará um hiperparâmetro diferente, fixando a melhor configuração e testando ao menos cinco valores.
- Avaliar uma única vez no conjunto de teste, após definir a configuração final.

## 7. Entregáveis

- Notebook com análise, preparação, MLP, buscas, comparação, sensibilidades e teste final.
- Slides focados em contexto, decisões, gráficos e conclusões — não em código.
- Declaração inicial de uso de IA generativa, se aplicável, com ferramenta, finalidade, extensão e validação humana.
