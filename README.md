# Seazone Challenge: Project Overview 

<p align="center">
  <a href="https://www.linkedin.com/in/r%C3%B4mulo-carneiro-00106414a/" re="nofollow">
    <img alt="Romulo Carneiro" src="https://img.shields.io/badge/Romulo-141F4F?style=flat&logo=linkedin&labelColor=141F4F" style="max-width:100%;">
  </a>
  <a href="https://www.repostatus.org/">
    <img alt="Project Status: WIP" src="https://img.shields.io/badge/repo status-WIP-141F4F">
  </a>
  <img alt="Repository Size" src="https://img.shields.io/github/repo-size/carneiroRomulo/SeazoneChallenge?color=141F4F">
  <img alt="License" src="https://img.shields.io/badge/license-MIT-141F4F">
</p>

---

## Descrição

Este projeto foi criado com o proposito de solucionar um desafio proposto pela [Seazone](https://www.seazone.com.br/) como parte do processo seletivo para o programa de estágio em Ciência de Dados.

---

## Objetivos

* Ordene os bairros em ordem crescente de número de listings.
* Ordene os bairros em ordem crescente de faturamento médio dos listings.
* Existem correlações entre as características de um anúncio e seu faturamento? Quais? Explique.
* Qual a antecedência média das reservas? Esse número é maior ou menor para finais de semana?
* Onde possível, embasar a análise com gráficos.

---

## Dados

### priceav.csv (Contains occupancy data and ad price)
* airbnb_listing_id: Identificador de um anúncio.
* price_string: : Preço ofertado.
* occupied: Booleano de ocupação. 0 significa livre e 1 ocupado.
* date: Data a ser alugada.
* booked_on: Data quando “date” foi alugado. Null caso ainda esteja disponível.

### details.csv (Contains characteristics of each ad)
* airbnb_listing_id: Identificador de um anúncio.
* suburb: Bairro do listing.
* star_rating: Nota 1-5 do anúncio.
* is_superhost: Booleano que indica se é superhost ou não.
* number_of_bedrooms: Quantidade de quartos do anúncio.
* number_of_reviews : Quantidade de reviews do anúncio.
* ad_name: Título do anúncio.
* number_of_bathrooms: Quantidade de banheiros do anúncio.
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
