# Are Larger Cities More Segregated?

This project asks whether people from different social groups live further apart from each other in large French cities than in small ones. It uses the 2021 French census from INSEE and measures segregation in 638 urban areas (aires d'attraction des villes) across France.

## Method

Segregation is measured with the Duncan dissimilarity index, which goes from 0 (both groups are spread the same way across the municipalities of a city) to 1 (the two groups never live in the same municipality). It can be read as the share of one group that would have to move for both groups to be evenly distributed.

The index is computed for two pairs of groups: managers versus manual workers (occupation), and people with a master's degree or more versus people with no diploma (education). It is then regressed on the log of each city's population, with HC1 robust standard errors:

```
D = β0 + β1 · log(population) + β2 · log(number of municipalities) + ε
```

## Main findings

In a simple regression, larger cities do look more segregated: doubling a city's population is associated with a Duncan index about 0.008 points higher for occupation and 0.013 points higher for education, and both effects are statistically significant.

This relationship reverses once the number of municipalities in the city is controlled for. Larger cities are divided into many more municipalities, and a city split into more units mechanically shows more measured segregation. Holding the number of units constant, the population coefficient becomes negative for occupation (β1 = −0.026, p < 0.01) and close to zero for education. The result holds when the sample is restricted to cities with at least 10 municipalities.

So the apparent link between city size and segregation is largely driven by how finely each city is divided, a classic measurement problem known as the modifiable areal unit problem.

## Running the code

Open `Are_larger_cities_segregated.ipynb` and run all cells. The notebook downloads the three INSEE files it needs into an `inputs/` folder on the first run, and saves the figures and tables into `outputs/`. No API key is needed.

The notebook uses pandas, numpy, matplotlib, statsmodels, openpyxl and geopandas.

## Data sources

All data comes from [INSEE](https://www.insee.fr): the 2021 census employment and labour force base, the 2020 urban area definitions (AAV2020, 2024 geography), and the urban area boundary maps.

Project by Hana Fatteh.
