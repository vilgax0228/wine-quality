## Introdução

```R
> wine_data <- read.csv("winequality-red.csv", sep=";")
> head(wine_data)
```

```R
ggplot(wine_data, aes(x = quality)) +
  geom_bar() +
  labs(title = "Distribuição de Qualidade do Vinho", x = "Qualidade", y = "Quantidade")
```

![Rplot07](https://github.com/user-attachments/assets/9e60dc75-f3fd-47b9-8637-5aa8417c05b8)

Para identificar outliers, podemos usar o método baseado no intervalo interquartil (IQR). Outliers são definidos como valores que estão fora do intervalo definido pelos quartis 1 (Q1) e 3 (Q3), com uma distância maior do que 1,5 vezes o IQR.

```R
Q1 <- quantile(wine_data$quality, 0.25)  # Primeiro quartil (25%)
Q3 <- quantile(wine_data$quality, 0.75)  # Terceiro quartil (75%)
IQR <- Q3 - Q1  # Intervalo interquartil

lower_limit <- Q1 - 1.5 * IQR
upper_limit <- Q3 + 1.5 * IQR

outliers = wine_data$quality[wine_data$quality < lower_limit | wine_data$quality > upper_limit]
outliers
[1] 8 8 8 8 8 3 8 8 8 3 8 3 8 3 3 8 8 8 8 8 3 3 8 8 3 3 3 8
```

