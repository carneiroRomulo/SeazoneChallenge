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

### priceav.csv (Contains occupancy data and ad price)
* airbnb_listing_id: Ad identifier.
* price_string: Price offered.
* occupied: Occupation Boolean. 0 means free and 1 means rented.
* date: Date to be rented.
* booked_on: Date when “date” was rented. Null if still available.

### details.csv (Contains characteristics of each ad)
* airbnb_listing_id: Ad identifier.
* suburb: Listing neighborhood.
* star_rating: Note 1-5 of the ad.
* is_superhost: Boolean indicating whether it is a superhost or not.
* number_of_bedrooms: Number of rooms in the ad.
* number_of_reviews : Number of ad reviews.
* ad_name: Ad title.
* number_of_bathrooms: Number of bathrooms in the ad.
---

## Technologies

* Python
* Jupyter
* Numpy
* Pandas
* Matplot

---

## License

This project is under the [MIT](./LICENSE) license.

---

<p align="center">Made with ❤️ by Rômulo Carneiro<p/>
