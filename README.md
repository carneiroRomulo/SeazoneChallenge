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

## Description

This project was created with the objective of solve a challenge proposed by [Seazone](https://www.seazone.com.br/) as part of a selection process for an internship program in Data Science.

---

## Goals

* Sort neighborhoods in ascending order of number of listings.
* Sort the neighborhoods in ascending order of average listing earnings.
* Is there any correlation between the characteristics of an ad and its billing? That are? Explain.
* What is the average advance of reservations? Is this number higher or lower for weekends?
* Support the analysis with graphs.

---

## Data

### priceav.csv (Contém dados de ocupação e preço de anúncios)
* airbnb_listing_id: Identificador de um anúncio.
* price_string: Preço ofertado.
* occupied: Booleano de ocupação. 0 significa livre e 1 ocupado.
* date: Data a ser alugada.
* booked_on: Data quando “date” foi alugado. Null caso ainda esteja available.

### details.csv (Contém características de cada anúncio)
* airbnb_listing_id: dentificador de um anúncio
* suburb: Bairro do listing
* star_rating: Nota 1-5 do anúncio
* is_superhost: Booleano que indica se é superhost ou não.
* number_of_bedrooms: Quantidade de quartos do anúncio.
* number_of_reviews : Quantidade de reviews do anúncio.
* ad_name: Título do anúncio.
* number_of_bathrooms: Número de banheiros do anúncio.
---

## Technologies

* Python
* Jupyter
* Numpy
* Pandas

---

## License

This project is under the license [MIT](./LICENSE) .

---

<p align="center">Made with ❤️ by Rômulo Carneiro<p/>
