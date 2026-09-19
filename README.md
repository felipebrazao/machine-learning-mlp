# Regressão de preços de veículos com MLP

Projeto da disciplina de Inteligência Computacional/Machine Learning. O objetivo é estimar o preço final de venda de veículos (`sellingprice`) com uma rede neural MLP, comparando Random Search e TPE na escolha dos hiperparâmetros.

## Estrutura

```text
notebooks/
  01_exploracao_e_mlp.ipynb   # análise e experimento completo
  figuras/                     # gráficos utilizados pelo notebook
plan.md                        # planejamento metodológico
requirements.txt               # dependências reproduzíveis
```

## Dataset

Foi utilizado o [Vehicle Sales and Market Trends Dataset](https://www.kaggle.com/datasets/syedanwarafridi/vehicle-sales-data), com 558.837 registros e 16 colunas.

O arquivo não é versionado. Depois do download, coloque-o em:

```text
data/raw/car_prices.csv
```

## Ambiente

No Windows PowerShell:

```powershell
python -m venv .venv
.\.venv\Scripts\Activate.ps1
python -m pip install -r requirements.txt
```

Abra `notebooks/01_exploracao_e_mlp.ipynb` usando o kernel do ambiente virtual. A execução das duas buscas completas envolve 25 configurações × 3 folds para cada estratégia e pode levar bastante tempo em CPU.

## Resultados principais

- Melhor busca: Random Search.
- MAE médio de validação: US$ 1.027,26.
- Avaliação final no holdout: MAE de US$ 1.065,15, RMSE de US$ 1.652,57 e R² de 0,9710.
- Hiperparâmetro de maior impacto: taxa de aprendizado.
- A variável `mmr` exerce forte influência: removê-la elevou o MAE de validação para US$ 1.880,53 na ablação com configuração fixa.

O notebook contém a declaração de uso de IA generativa, as análises individuais de sensibilidade, a discussão de overfitting/underfitting e as limitações do experimento.
