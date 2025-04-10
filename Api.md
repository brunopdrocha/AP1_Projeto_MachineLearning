# 📡 API REST – Previsão de CGPA e Classificação de Depressão

Esta API foi desenvolvida em R utilizando o pacote **plumber**, com base em dois modelos de Machine Learning aplicados ao dataset "Student Depression Dataset". A API fornece dois endpoints para previsão de nota (`CGPA`) e classificação de depressão.

---

## ⚙️ Tecnologias Utilizadas

- Linguagem R
- Bibliotecas: `plumber`, `Metrics`
- Modelos treinados com `glm()` e `lm()`
- Modelos exportados com `saveRDS()`

---

## 📌 Endpoints da API

### 🔷 `/predicao`

**Objetivo:** Prever o CGPA com base no nível de pressão acadêmica (`Academic.Pressure`).

**Parâmetro:**
- `Academic.Pressure`: valor numérico contínuo (ex: 1.5, 2.8)

**Resposta:**

```json
{
  "cgpa_previsto": 6.41,
  "probabilidade_normalizada": 0.641,
  "input": {
    "Academic.Pressure": 2.5
  }
}
```

---

### 🔷 `/classificacao`

**Objetivo:**  
Classificar a presença de depressão com base no grupo de sono (`Sleep_Group`), utilizando um modelo de regressão logística.

**Parâmetro:**

- `Sleep_Group`: valor numérico de 1 a 5, representando a duração do sono do indivíduo:

  ```
  1 = "Others"  
  2 = "More than 8 hours"  
  3 = "5-6 hours"  
  4 = "7-8 hours"  
  5 = "Less than 5 hours"
  ```

**Exemplo de chamada:**

```bash
GET /classificacao?Sleep_Group=4
```

**Resposta:**

```json
{
  "probabilidade": 0.712,
  "classe_prevista": 1,
  "dados_utilizados": {
    "Sleep_Group": 4
  },
  "classificacao": "Com indícios de depressão"
}
```

**Legenda da `classe_prevista`:**

- `0` = Sem indícios de depressão  
- `1` = Com indícios de depressão
