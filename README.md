# Seazone Challenge: Project Overview 

<p align="center">
  <a href="https://www.linkedin.com/in/r%C3%B4mulo-carneiro-00106414a/" re="nofollow">
    <img alt="Romulo Carneiro" src="https://img.shields.io/badge/Romulo-141F4F?style=flat&logo=linkedin&labelColor=141F4F" style="max-width:100%;">
  </a>
  <a href="https://www.repostatus.org/">
    <img alt="Project Status: Active" src="https://img.shields.io/badge/repo status-Active-141F4F">
  </a>
  <img alt="Repository Size" src="https://img.shields.io/github/repo-size/carneiroRomulo/SeazoneChallenge?color=141F4F">
  <img alt="License" src="https://img.shields.io/badge/license-MIT-141F4F">
</p>

---

## Descrição

Este projeto foi criado com o proposito de solucionar um desafio proposto pela [Seazone](https://www.seazone.com.br/) como parte do processo seletivo para o programa de estágio em Ciência de Dados.

---

## Sumário
* [Dados](#dados)
* [Objetivos](#objetivos)
  * [1. Data Cleaning](#1-Data-Cleaning)
  * [2. Ordene os bairros em ordem crescente de número de listings](#2-Ordene-os-bairros-em-ordem-crescente-de-número-de-listings)
  * [3. Ordene os bairros em ordem crescente de faturamento médio dos listings](#3-Ordene-os-bairros-em-ordem-crescente-de-faturamento-médio-dos-listings)
  * [4. Existem correlações entre as características de um anúncio e seu faturamento? Quais? Explique](#4-Existem-correlações-entre-as-características-de-um-anúncio-e-seu-faturamento-Quais-Explique)
  * [5. Qual a antecedência média das reservas? Esse número é maior ou menor para finais de semana?](#5-Qual-a-antecedência-média-das-reservas-Esse-número-é-maior-ou-menor-para-finais-de-semana)
* [Objetivos Extras](#objetivos-extras)
* [Tecnologias](#tecnologias)

---
## Dados

### priceav.csv (Contém dados de ocupação e preço do anúncio)
* airbnb_listing_id: Identificador de um anúncio.
* price_string: : Preço ofertado.
* occupied: Booleano de ocupação. 0 significa livre e 1 ocupado.
* date: Data a ser alugada.
* booked_on: Data quando “date” foi alugado. Null caso ainda esteja disponível.

```python
raw_priceav_df = pd.read_csv('https://raw.githubusercontent.com/carneiroRomulo/SeazoneChallenge/main/datasets/priceav.csv')
raw_priceav_df.head()
```
       Unnamed: 0   Unnamed: 0.1   airbnb_listing_id booked_on date           date   price_string  occupied
    0           0           2148            40201349          blank     2020-11-15          250.0         0
    1           1           2159            40201349          blank     2020-11-26          250.0         0
    2           2           2160            40201349          blank     2020-11-27          250.0         0
    3           3           2173            40201349          blank     2020-12-10          250.0         0
    4           4           2226            40201349          blank     2021-02-01          250.0         0

### details.csv (Contém características de cada anúncio)
* airbnb_listing_id: Identificador de um anúncio.
* suburb: Bairro do listing.
* star_rating: Nota 1-5 do anúncio.
* is_superhost: Booleano que indica se é superhost ou não.
* number_of_bedrooms: Quantidade de quartos do anúncio.
* number_of_reviews : Quantidade de reviews do anúncio.
* ad_name: Título do anúncio.
* number_of_bathrooms: Quantidade de banheiros do anúncio.
```python
raw_details_df = pd.read_csv('https://raw.githubusercontent.com/carneiroRomulo/SeazoneChallenge/main/datasets/details.csv')
raw_details_df.head()
```
           Unnamed: 0    airbnb_listing_id        suburb                                            ad_name  number_of_bedrooms   number_of_bathrooms star_rating  is_superhost  number_of_reviews
      0             0             31389869        Jurerê                        Lindo Apartamento em Jurerê                 2.0                   2.0         5.0         False               15.0
      1             1             40010667  Canasvieiras                       Residencial Arruda, 1 quarto                 1.0                   1.0         NaN         False                0.0
      2             2             38905997      Ingleses  Apartamento NOVO Completo - Moderno e Sofisticado                 1.0                   1.0         4.5          True               13.0
      3             3             22343656      Ingleses                    06- Apartamento 02 habitaciones                 2.0                   1.0         5.0          True               28.0
      4             4             18328184  Canasvieiras     Apto 2 quartos em Canasvieiras, Florianopolis!                 2.0                   1.0         5.0          True               35.0

---

## Objetivos
### 1. Data Cleaning

A principio foi realizado uma análise inicial nos datasets para visualizar toda sua estrutura e a tipagem das features. Foram removidas aquelas features desnecessárias para análise que não diziam nada sobre o problema, bem como, o conteúdo daquelas features que possuiam quantidade substancial de missing values e foram substituidos os valores da feature `star_rating` - já que possui um grande número de missing values - por sua mediana, além de formatar a data na feature `booked_on`, excluindo o horário, já que era insignificante para a análise

### 2. Ordene os bairros em ordem crescente de número de listings
```python
df3_details = df3_details.groupby('suburb', as_index=False).airbnb_listing_id.count()
df3_details.sort_values(['airbnb_listing_id'], inplace=True)
```
                    suburb    airbnb_listing_id
    1               Centro                  238
    4   Lagoa da Conceição                  258
    3               Jurerê                  498
    0         Canasvieiras                 1125
    2             Ingleses                 2281
    
`listings_per_location`    

![alt_text](https://github.com/carneiroRomulo/SeazoneChallenge/blob/main/graphs/listings_per_location.png)
    
### 3. Ordene os bairros em ordem crescente de faturamento médio dos listings

Primeiro foi feita a seleção daqueles listings que apenas continham o booleano de `occupied` verdadeiro. Logo em seguida, o dataset que contem as caracteristicas dos listings foi combinado com o que contém os preços e datas nas quais eles foram reservados

```python
df3_price = df2_price.get(df2_price['occupied']==1)
df_merged = pd.merge(df2_details, df3_price, how='inner')
df_merged.rename(columns={'price_string':'billing'}, inplace=True)
```
            airbnb_listing_id    suburb                                   ad_name  number_of_bedrooms   number_of_bathrooms star_rating  is_superhost  number_of_reviews   booked_on        date  billing occupied
         0           31389869    Jurerê               Lindo Apartamento em Jurerê                 2.0                   2.0         5.0         False               15.0  2020-12-04  2020-12-04    270.0         1
         1           31389869    Jurerê               Lindo Apartamento em Jurerê                 2.0                   2.0         5.0         False               15.0  2020-12-04  2020-12-05    270.0         1
         2           31389869    Jurerê               Lindo Apartamento em Jurerê                 2.0                   2.0         5.0         False               15.0  2020-12-04  2020-12-06    270.0         1
         3           31389869    Jurerê               Lindo Apartamento em Jurerê                 2.0                   2.0         5.0         False               15.0  2020-12-04  2020-12-07    270.0         1
         4           31389869    Jurerê               Lindo Apartamento em Jurerê                 2.0                   2.0         5.0         False               15.0  2020-12-04  2020-12-08    270.0         1
       ...                ...       ...                                       ...                 ...                   ...         ...           ...                ...         ...         ...      ...       ...
    130927           40277915  Ingleses   2 dormitório a 100 metros do mar (202B)                 2.0                   2.0         5.0         False                0.0  2021-02-28  2021-03-26    150.0         1
    130928           40277915  Ingleses   2 dormitório a 100 metros do mar (202B)                 2.0                   2.0         5.0         False                0.0  2021-02-28  2021-03-27    150.0         1
    130929           40277915  Ingleses   2 dormitório a 100 metros do mar (202B)                 2.0                   2.0         5.0         False                0.0  2021-02-28  2021-03-28    150.0         1
    130930           40277915  Ingleses   2 dormitório a 100 metros do mar (202B)                 2.0                   2.0         5.0         False                0.0  2021-02-28  2021-03-29    150.0         1
    130931           40277915  Ingleses   2 dormitório a 100 metros do mar (202B)                 2.0                   2.0         5.0         False                0.0  2021-02-28  2021-03-30    150.0         1
    
    130932 rows × 12 columns

Ordena os bairros em ordem crescente de faturamento médio dos listings
```python
df2_merged = df_merged.groupby('suburb', as_index=False).billing.mean().round(2)
df2_merged.sort_values(['billing'], inplace=True)
```
                    suburb  billing
    1               Centro   219.70
    4   Lagoa da Conceição   243.83
    0         Canasvieiras   294.30
    2             Ingleses   350.27
    3               Jurerê   414.28
    
`billing_per_location`

![alt_text](https://github.com/carneiroRomulo/SeazoneChallenge/blob/main/graphs/billing_per_location.png)

### 4. Existem correlações entre as características de um anúncio e seu faturamento? Quais? Explique
Para se comparar todas as features, primeiro deve-se transforar a coluna `suburb` com a função OneHotEncoder do sklearn, isso porque a feature está como variável categórica, não sendo possível que a máquina consiga a identificar propriamente e depois transformar a saída em dataframe de forma que possa ser realizado o merge com o restante das features
```python
from sklearn.preprocessing import OneHotEncoder
encoder = OneHotEncoder()
X = encoder.fit_transform(df_merged.suburb.values.reshape(-1,1)).toarray()

suburb_encoded = pd.DataFrame(X, columns = ['Jurerê', 'Canasvieiras', 'Ingleses', 'Lagoa da Conceição', 'Centro'])

df_analysis = df_merged.join(suburb_encoded, lsuffix='_caller', rsuffix='_other')
df_analysis = df_analysis.drop(columns=['suburb', 'ad_name', 'booked_on', 'date', 'occupied'])
```

Agora, para checar se há correlação entre os dados uma boa métrica para se utilizar é o `coeficiente de relação de Pearson`, com a ajuda da biblioteca seaborn para representar o resultado em um `gráfico de heatmap`.

```python
import matplotlib.pyplot as plt
import seaborn as sns

plt.figure(figsize=(10, 7))
sns.heatmap(df_analysis.corr(),
            annot = True,
            vmin=0,
            fmt = '.2f',
            cmap='Reds')
plt.title('Correlação entre variáveis do dataset')
plt.show()
```
`correlation_between_data_heatmap`

![alt text](https://github.com/carneiroRomulo/SeazoneChallenge/blob/main/graphs/correlation_between_data_heatmap.png)

**CONCLUSÃO:** Através do gráfico de heatmap é perceptível que há sim uma correlação entre algumas das features e o faturamento. Pode-se observar que: `number_of_bedrooms`, `number_of_bathrooms` tem uma forte correlação entre si e com o faturamento, e a feature `star_rating`, junto dos bairros: `Ingleses` e `Lagoa da Conceição` apesar de possuirem uma correlação mais fraca com o faturamento, ela também é considerável.
Pode-se absorver também dessa análise que ao alugar através de um anúncio no airbnb, as pessoas costumam procurar por um número de quartos e banheiros equivalente, o que pode estar relacionado com um maior aluguel de suites e geralmente localizados no bairro Ingleses já que este possui forte correlação com esses cômodos.

### 5. Qual a antecedência média das reservas? Esse número é maior ou menor para finais de semana?

Primeiro deve-se extrair a diferença em dias das features `booked_on` e `date` e para se obter a antecedência média das reservas, deve-se fazer uma análise para saber se há presença de outliers que não irão comprometer no cálculo
```python
df4_price['advance_booking'] = (df3_price['date'] - df3_price['booked_on']).dt.days
df4_price['advance_booking'].sort_values()
```
    12           0
    85443        0
    85444        0
    85446        0
    85450        0
               ... 
    120661     369
    120662     370
    76559     7622
    302698    7644
    238097    7644
    
    Name: advance_booking, Length: 140508, dtype: int64
    
Ordenando os valores em ordem crescente já é visível que há uma descrepância grande entre os últimos dados, denunciando outliers. Para removê-los foi escolhido como paramêtro valores menores que 36, através da análise em um gráfico boxplot até que não houvesse mais outliers plotados

`advance_booking_boxplot_comparison`

![alt_text](https://github.com/carneiroRomulo/SeazoneChallenge/blob/main/graphs/advance_booking_boxplot_comparison.png)

Logo podemos observar que a média da antecêdencia das reservas foi: 8.19 dias
```python
df5_price['advance_booking'].mean()
```
    8.193997537043657
Para se obter a média da antecêdencia das reservas por dia, agrupa-se os dados de acordo com a feature `days`
```python
df6_price = df5_price.groupby('days', as_index=False).advance_booking.mean().round(2)
df6_price = df6_price.sort_values(['days'])
```
       days  advance_booking
    0     0             8.11
    1     1             7.66
    2     2             7.97
    3     3             8.25
    4     4             8.37
    5     5             8.35
    6     6             8.58
    
`average_advance_booking_per_day`

![alt_text](https://github.com/carneiroRomulo/SeazoneChallenge/blob/main/graphs/average_advance_booking_per_day.png)

**CONCLUSÃO:** Desconsiderando os outliers, houve uma antecedência média de 8.19 dias nas reservas e esse número foi maior no final de semana

---

## Objetivos Extras

### Para quando na semana e mês houve maior número de reservas
Primeiro deve-se extrair da feature `date` o mês correspondente as datas alugadas
```python
df7_price = df5_price.copy()
df7_price['months'] = df7_price['date'].dt.month_name()
df7_price['months'].unique()
```
    array(['January', 'February', 'March', 'December', 'November'], dtype=object)

Posteriormente agrupar em dataframes separados a frequência que uma data é alugada e criar duas listas que serão usadas para plotar no gráfico
```python
df_days = df7_price.groupby('days', as_index=False).days.count()
df_months = df7_price.groupby('months', as_index=False).months.count()

days = ['Monday','Tuesday','Wednesday','Thursday','Friday','Saturday','Sunday']
months = ['Jan','Feb','Mar','Nov','Dec']
```

`frequency_rental`

![alt_text](https://github.com/carneiroRomulo/SeazoneChallenge/blob/main/graphs/frequency_rental.png)

**CONCLUSÃO:** Como pode ser visualizado nos gráficos a cima, os alugueis dos imoveis anunciados estão focados nos finais de semana e no primeiro trimestre do ano, correspondente ao verão

---

## Tecnologias

* Python
* Jupyter
* Numpy
* Pandas
* Matplot
* Seaborn
* Sklearn

---

## License

This project is under the [MIT](./LICENSE) license.

---

<p align="center">Made with ❤️ by Rômulo Carneiro<p/>
