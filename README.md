# Análise de Dados Ambientais com Python

Este projeto realiza a leitura, tratamento e análise de dados ambientais utilizando Python, Pandas e Matplotlib.

Os dados analisados incluem:

- Temperatura em °C
- Nível do rio em metros
- Índice NDVI

Além disso, o programa gera gráficos para visualização da evolução dos dados ao longo do tempo.

---

# Bibliotecas Utilizadas

O projeto utiliza as seguintes bibliotecas:

- pandas
- matplotlib

## Instalação das bibliotecas

Caso as bibliotecas não estejam instaladas no computador, utilize:

```bash
pip install pandas matplotlib
```

---

# Estrutura Esperada do Arquivo CSV

O arquivo `dados_projeto.csv` deve estar na mesma pasta do código.

Exemplo:

```csv
Data;Temperatura_c;Nivel_rio_m;NDVI
01/01/2025;32.5;4.2;0.65
02/01/2025;33.1;4.3;0.67
03/01/2025;34.0;4.1;0.70
```

---

# Explicação do Código

## Importação das bibliotecas

```python
import pandas as pd
import matplotlib.pyplot as plt
```

- `pandas` é utilizado para manipulação e análise dos dados.
- `matplotlib.pyplot` é utilizado para criação dos gráficos.

---

## Leitura do arquivo CSV

```python
df = pd.read_csv("dados_projeto.csv", sep=";")
```

O programa lê o arquivo CSV utilizando `;` como separador das colunas.

---

## Tratamento dos dados

### Conversão da coluna Data

```python
df["Data"] = pd.to_datetime(df["Data"], format="%d/%m/%Y")
```

Converte a coluna `Data` para o formato de data do Python.

---

### Verificação de valores ausentes

```python
print(df.isnull().sum())
```

Mostra quantos valores vazios existem em cada coluna.

---

### Remoção de valores ausentes

```python
df = df.dropna()
```

Remove linhas que possuem dados faltando.

---

## Organização dos dados

```python
df = df.sort_values(by="Data")
```

Organiza os dados em ordem cronológica.

---

## Cálculo das médias

```python
media_temperatura = df["Temperatura_c"].mean()
media_nivel_rio_m = df["Nivel_rio_m"].mean()
media_ndvi = df["NDVI"].mean()
```

Calcula:

- Média da temperatura
- Média do nível do rio
- Média do NDVI

---

# Geração dos Gráficos

O programa gera três gráficos:

1. Evolução da temperatura
2. Evolução do nível do rio
3. Evolução do NDVI

Todos os gráficos possuem:

- Linha principal dos dados
- Linha horizontal mostrando a média
- Título
- Legenda
- Grade
- Rotação das datas para melhor visualização

---

# Código Completo

```python
import pandas as pd
import matplotlib.pyplot as plt

df = pd.read_csv("dados_projeto.csv", sep=";")

# Tratando dados

df["Data"] = pd.to_datetime(df["Data"], format="%d/%m/%Y")

print("\n====== VALORES AUSENTES =====")
print(df.isnull().sum())

df = df.dropna()

# Organizando data

df = df.sort_values(by="Data")

# Estrutura básica

media_temperatura = df["Temperatura_c"].mean()
media_nivel_rio_m = df["Nivel_rio_m"].mean()
media_ndvi = df["NDVI"].mean()

# Gráfico temperatura

plt.figure(figsize=(12,6))

plt.plot(
    df["Data"],
    df["Temperatura_c"],
    marker="o"
)

plt.axhline(
    media_temperatura,
    linestyle="--",
    label=f"Média: {media_temperatura:.2f}C"
)

plt.title("Evolução da temperatura ao decorrer do tempo")
plt.xlabel("Data")
plt.ylabel("Temperatura C")
plt.grid(True)
plt.legend()

plt.xticks(rotation=45)
plt.tight_layout()
plt.show()

# Gráfico nível do rio

plt.figure(figsize=(12,6))

plt.plot(
    df["Data"],
    df["Nivel_rio_m"],
    marker="o"
)

plt.axhline(
    media_nivel_rio_m,
    linestyle="--",
    label=f"Média: {media_nivel_rio_m:.2f}M"
)

plt.title("Nível do rio ao decorrer do tempo")
plt.xlabel("Data")
plt.ylabel("Nivel do rio (M)")
plt.grid(True)
plt.legend()

plt.xticks(rotation=45)
plt.tight_layout()
plt.show()

# Gráfico NDVI ao decorrer do tempo

plt.figure(figsize=(12,6))

plt.plot(
    df["Data"],
    df["NDVI"],
    marker="o"
)

plt.axhline(
    media_ndvi,
    linestyle="--",
    label=f"Média: {media_ndvi:.2f}"
)

plt.title("Evolução do NDVI ao decorrer do tempo")
plt.xlabel("Data")
plt.ylabel("NDVI")
plt.grid(True)
plt.legend()

plt.xticks(rotation=45)
plt.tight_layout()
plt.show()
```

---

# Resultado Esperado

Ao executar o programa, serão exibidos:

- Quantidade de valores ausentes
- Dados organizados por data
- Três gráficos mostrando a evolução dos indicadores ambientais

---

# Tecnologias Utilizadas

- Python
- Pandas
- Matplotlib
