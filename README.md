# Challenge Motiva/CCR — Sprint I
### Monitoramento Inteligente de Vegetação em Rodovias
**FIAP — 2º ano Ciência da Computação | Data Science and Analytics**

---

## Sobre o Projeto

Solução de Data Science desenvolvida para a Motiva/CCR com foco no monitoramento automatizado de vegetação ao longo do **Rodoanel Mário Covas (SP-021 Oeste)**, cobrindo do KM 0 ao KM 29+300.

O objetivo é prever quais trechos atingirão nível crítico de vegetação (h > 30 cm) antes do próximo ciclo de inspeção, permitindo priorizar as equipes de roçada de forma proativa.

---

## Problema

Atualmente, o monitoramento depende de inspeções manuais periódicas registradas em planilhas. O modelo proposto aprende com o histórico de níveis por trecho e área para antecipar situações de risco — reduzindo custos operacionais e aumentando a segurança da rodovia.

## Formulação Data Science

```
f(X) → y
```

| Componente | Descrição |
|---|---|
| **X (features)** | Tipo de área, posição (KM), nível anterior (T1), flag interna/externa, intervalo em dias |
| **y (target)** | Nível em T2 — multiclasse {1, 2, 3} ou binário {crítico / não-crítico} |
| **Tarefa** | Classificação supervisionada |
| **Modelo base** | Random Forest com `class_weight='balanced'` |

---

## Dataset

- **Fonte:** Motiva/CCR — dados reais de levantamento de campo
- **Rodovia:** SP-021 — Rodoanel Mário Covas Oeste
- **Levantamentos:** 13/03/2026 e 20/03/2026
- **Áreas monitoradas:** 8 canteiros (Lateral Ext./Int., Central Ext./Int., Marginal Ext./Int., Dispositivo Ext./Int.)
- **Trechos:** 60 pontos de KM por área

---

## Estrutura do Repositório

```
Sprint-Data/
├── RA-RET-ROÇ-LIMP-2026-03-13.xlsx   # Levantamento 13/03/2026
├── RA-RET-ROÇ-LIMP-2026-03-20.xlsx   # Levantamento 20/03/2026
├── Challenge_Motiva_Sprint1_EDA.ipynb # Notebook com EDA e pré-processamento
├── Documento_Solucao_Motiva_Sprint1.docx  # Documento técnico (2 páginas)
└── README.md
```

---

## Como Executar

O notebook baixa os dados automaticamente do GitHub — nenhum arquivo externo necessário.

```bash
pip install pandas numpy matplotlib seaborn scikit-learn openpyxl requests
jupyter notebook Challenge_Motiva_Sprint1_EDA.ipynb
```

Ou abra direto no **Google Colab** clicando no badge abaixo:

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/Luisin07/Sprint-Data/blob/main/Challenge_Motiva_Sprint1_EDA.ipynb)

---

## Conteúdo do Notebook

1. Carregamento automático dos dados via GitHub
2. Parsing das planilhas no formato Unifilar da Motiva/CCR
3. Análise Exploratória (EDA) — distribuição de níveis, evolução entre datas, mapa por KM
4. Matriz de transição T1 → T2
5. Análise de qualidade dos dados
6. Pré-processamento e feature engineering
7. Teste inicial com Random Forest

---

## Métricas de Sucesso

| Métrica | Justificativa |
|---|---|
| **Recall (Classe Crítica)** | Métrica primária — minimizar falsos negativos |
| **F1-Score macro** | Equilíbrio entre precisão e recall com classes desbalanceadas |
| **AUC-ROC** | Separabilidade do modelo independente do threshold |
| **Precision@K** | Relevância para priorização de equipes de manutenção |

---

*Challenge Sprint I — Entrega: 22/05/2026*
