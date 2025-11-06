---
title: "Ejemplo de tablero con Flexdashboard"
date: "2025-11-03"
description: "Un ejemplo de cómo integrar un dashboard dentro de tu sitio creado con blogdown."
tags: ["flexdashboard", "visualización", "R"]
---

En esta entrada mostramos cómo crear un tablero interactivo con **Flexdashboard**.

El siguiente botón te llevará al tablero completo, donde podrás explorar las gráficas generadas en R.

[Ver el dashboard interactivo →](/dashboard/riesgo_default.html)

---


``` r
# Código utilizado para generar el dashboard:
rmarkdown::render("content/posts/02-flexdashboard/02-flexdashboard.Rmd",
                  output_dir = "static/dashboard")

library(flexdashboard)
library(ggplot2)
library(dplyr)
library(gapminder)

Column {data-width=650}
-----------------------------------------------------------------------

### PIB per cápita por continente

data <- gapminder %>% filter(year == 2007)

ggplot(data, aes(continent, gdpPercap, fill = continent)) +
  geom_col() +
  theme_minimal() +
  labs(
    title = "PIB per cápita por continente (2007)",
    x = "Continente", y = "PIB per cápita"
  )

Column
-----------------------------------------------------------------------

### Esperanza de vida

ggplot(data, aes(continent, lifeExp, fill = continent)) +
  geom_boxplot() +
  theme_minimal() +
  labs(
    title = "Esperanza de vida por continente (2007)",
    x = "Continente", y = "Años"
  )
```
