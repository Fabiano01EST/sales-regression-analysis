# Sales Regression Analysis

Projeto de portfólio de regressão linear múltipla para prever vendas a partir de renda média e investimento em publicidade.

---

## Objetivo

Construir e validar um modelo estatístico capaz de explicar e prever o volume de vendas com base em duas variáveis independentes: renda média do cliente e investimento em publicidade.

---

## Etapas do projeto

### 1. Exploração dos dados
- Pairplot para visualizar distribuições e relações entre variáveis
- Boxplots para identificar possíveis outliers
- Matriz de correlação de Pearson

**Principais achados:**
- Renda média e publicidade têm baixa correlação entre si (0.10), indicando independência entre os preditores
- Ambas se correlacionam com vendas (0.51 e 0.45, respectivamente, com p < 0.001)

### 2. Modelagem

Regressão linear múltipla (OLS) com dois preditores.

```
Vendas = -100.81 + 0.089 × Renda + 2.98 × Publicidade
```

| Métrica | Valor |
|---|---|
| R² | 0.43 |
| R² ajustado | 0.42 |
| p-valor (F-statistic) | < 0.001 |

### 3. Generalização

O modelo foi testado em dados separados (holdout), obtendo R² = 0.44 — ligeiramente superior ao treino, indicando boa capacidade de generalização sem overfitting.

### 4. Validação dos pressupostos

| Pressuposto | Teste | Resultado |
|---|---|---|
| Normalidade dos resíduos | Shapiro-Wilk | p = 0.93 ✅ |
| Homocedasticidade | Breusch-Pagan | p = 0.28 ✅ |
| Linearidade | — | p = 0.31 ✅ |
| Independência dos erros | Durbin-Watson | 1.85 ✅ |
| Multicolinearidade | VIF | Próximo de 1 ✅ |

### 5. Diagnóstico visual

Análise dos 4 gráficos clássicos de resíduos: Residual vs. Fitted, Q-Q plot, Scale-Location e Residuals vs. Leverage.

### 6. Observações influentes

Utilizei a Distância de Cook (limiar 4/n) para identificar observações com impacto desproporcional no modelo. As observações 9, 14, 54, 71, 74, 155, 162 e 167 ultrapassaram o limiar e foram investigadas.

Após a retirada, comparei AIC, BIC, erros padrão e R² entre os dois modelos, e todas as métricas apresentaram melhora.

| Métrica | Modelo completo | Sem influentes |
|---|---|---|
| AIC | 2330 | 2205 |
| BIC | 2340 | 2215 |
| R² | 0.426 | 0.432 |

Os coeficientes se mantiveram estáveis, indicando que as observações adicionavam ruído sem distorcer a direção das estimativas. O modelo sem as influentes foi mantido como versão final.

### 7. Interpretação dos coeficientes

- **Renda média:** a cada R$1 a mais na renda média do cliente, as vendas aumentam ~0,09 unidade, mantendo o investimento em publicidade constante.
- **Investimento em publicidade:** a cada R$1.000 a mais investido em publicidade, as vendas sobem ~2,98 unidades, mantendo a renda constante.

---

## Tecnologias utilizadas

- Python
- Pandas / NumPy
- Statsmodels
- Matplotlib / Seaborn

---

## Tags

`DataScience` `Python` `RegressaoLinear` `Estatistica` `MachineLearning` `AnaliseDeDados` `EstatisticaAplicada` `CienciadeDados`
