# 📊 Análise de Dados UOL Noticias com NER 

aplicacao do modelo "monilouise/ner_news_portuguese" para identificar e extrair entidades do tipo Organização (ORG) em notícias da seção "Mercado" da Folha UOL, no período de janeiro a março de 2015, e apresentar um ranking das organizações mais citadas.

## 🛠️ Metodologia

- 📚 Transformers da Hugging Face (monilouise/ner_news_portuguese)

- 🐍 Python e Pandas para processamento

- 📊 Matplotlib e Seaborn para visualizações

- ☁️ Google Colab para edicao do codigo


## 📦Coleta de Dados

1. O dataset foi obtido no Kaggle
   ```bash
    https://www.kaggle.com/datasets/marlesson/news-of-the-site-folhauol

2. Filtragem de Dados
   O dataset foi filtrado para:
 - Categoria: mercado
- Período: 1º de janeiro a 31 de março de 2015
   ```bash
  df_mercado = df[
    (df['category'].str.lower().str.strip() == 'mercado') &
    (df['date'] >= '2015-01-01') &
    (df['date'] < '2015-04-01')
  ].copy()


 4. Modelo de NER Utilizado
    - Nome: monilouise/ner_pt_br
   ```bash
ner_pipe = pipeline(
    "ner",
    model="monilouise/ner_news_portuguese",
    tokenizer="monilouise/ner_news_portuguese",
    trust_remote_code=True,
    revision="main",
   aggregation_strategy="simple",
model_kwargs={"use_safetensors": True}

)

```

4. Extração das Organizações
   ```bash
    from tqdm import tqdm

    orgs = []

    for texto in tqdm(mercado_df['text'].dropna()):  
        if isinstance(texto, str) and texto.strip():
            ents = ner_pipe(texto)
            for ent in ents:
                if ent['entity_group'] == 'ORG':
                    nome = limpar(ent['word'])
                    if nome:
                        orgs.append(nome)


## 📈 Visualização dos Resultados
![image](https://github.com/user-attachments/assets/1ee3757e-0e2b-4d08-b0fa-81b157caab99)

---

<div align="center">

✨ Desenvolvido por **Cristina Andrade** 

Engenheira da Computação - CREA 2024107872

Aplicação de Análise de Dados com NER 



</div>
