<h1>TP DATAMINING</h1>

> Fichier notebook :
> [TP_DATAMINING.ipynb](TP_DATAMINING.ipynb)

<h2>1. Problématiques</h2>

> A ce stade les données ne sont pas facilement exploitable.
> En effet, il y a beaucoup trop de données, et il faut donc élabober différentes analyses qui permerttront d'avoir un rendu graphique facilitant l'interprétation de celles-ci.
> Néanmoins, les problématiques que nous pouvons mettre en avant, sont de savoir par exemple si il y'a une corrélation entre le prix et le carat, le prix et la qualité, et le prix et la clarté des diamants.

<h2>2. Analyse univariée</h2>

<h3>Étape 1 : Import des librairies et chargement du fichier csv (dataset)</h3>

```python
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns
df = pd.read_csv('/home/ubuntu/Documents/DATAMINING/diamonds.csv')
```

<h3>Étape 2 : Vérification si le fichier csv est bien chargé</h3>

```python
df.shape
(53940, 10)
```

> La commande df.shape permet de connaître le nombre de lignes et de colonnes : Ici nous avons 53 940 lignes et 10 colonnes
    
    
<h3>Étape 3 : Affichage d'un tableau permettant d'avoir le total des diamants en fonction de la qualité (cut)</h3>

```python
freq_table = df.groupby(['cut']).size().reset_index(name='Total').rename(columns={'cut': 'Qualité'})
freq_table
```

<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Qualité</th>
      <th>Total</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Fair</td>
      <td>1610</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Good</td>
      <td>4906</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Ideal</td>
      <td>21551</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Premium</td>
      <td>13791</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Very Good</td>
      <td>12082</td>
    </tr>
  </tbody>
</table>
</div>

<h3>Étape 4 : Création des différents  graphiques pertinents</h3>

<h4>Cut / Price</h4>

```python
sns.barplot(x='cut', y='price', data=df)
```
![png](cut.png)

<h4>Cara / Price</h4>

```python
sns.boxplot(x='carat', y='price', data=df)
```
![png](output_8_1.png)

<h4>Clarity / Price</h4>

```python
sns.barplot(x='clarity', y='price', data=df)
```
![png](clarity.png)

<h2>2.a Description des diamants</h2>

Le tableau faisant référence à la quantité en fonction de la qualité des diamants, nous montre que nous avons beaucoup plus de diamants de bonnes qualités par rapport aux qualités les plus basses.
De plus au niveaux des prix, nous pouvons remarquer une corrélation entre la taille du carat et son prix.
Néanmoins, on remarque que la qualité et la clarté ne sont pas les caractéristiques qui impactent les prix d'une manière significative, contrairement aux carats.

<h2>2.b Anomalies</h2>

Les anomalies remarquées sont la non corrélation entre le prix et la qualité, et le prix et la clarté. 
Il serait donc plus judicieux de se baser sur le nombre de carats pour déterminer et prévoir les prix.

<h2>3. Analyse bivariée / tri variée</h3>

<h3>Création de graphiques pertinents</h3>

<h4>Carat / Price / Color</h4>

```python
sns.lmplot(x='price', y='carat', hue='color', fit_reg=False, data=df)
```
![color_bivarie](color_bivarie.png)

<h4>Génération des coefficients de corrélation</h4>

```python
df.corr()
```

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>carat</th>
      <th>depth</th>
      <th>table</th>
      <th>price</th>
      <th>x</th>
      <th>y</th>
      <th>z</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>carat</th>
      <td>1.000000</td>
      <td>0.028224</td>
      <td>0.181618</td>
      <td>0.921591</td>
      <td>0.975094</td>
      <td>0.951722</td>
      <td>0.953387</td>
    </tr>
    <tr>
      <th>depth</th>
      <td>0.028224</td>
      <td>1.000000</td>
      <td>-0.295779</td>
      <td>-0.010647</td>
      <td>-0.025289</td>
      <td>-0.029341</td>
      <td>0.094924</td>
    </tr>
    <tr>
      <th>table</th>
      <td>0.181618</td>
      <td>-0.295779</td>
      <td>1.000000</td>
      <td>0.127134</td>
      <td>0.195344</td>
      <td>0.183760</td>
      <td>0.150929</td>
    </tr>
    <tr>
      <th>price</th>
      <td>0.921591</td>
      <td>-0.010647</td>
      <td>0.127134</td>
      <td>1.000000</td>
      <td>0.884435</td>
      <td>0.865421</td>
      <td>0.861249</td>
    </tr>
    <tr>
      <th>x</th>
      <td>0.975094</td>
      <td>-0.025289</td>
      <td>0.195344</td>
      <td>0.884435</td>
      <td>1.000000</td>
      <td>0.974701</td>
      <td>0.970772</td>
    </tr>
    <tr>
      <th>y</th>
      <td>0.951722</td>
      <td>-0.029341</td>
      <td>0.183760</td>
      <td>0.865421</td>
      <td>0.974701</td>
      <td>1.000000</td>
      <td>0.952006</td>
    </tr>
    <tr>
      <th>z</th>
      <td>0.953387</td>
      <td>0.094924</td>
      <td>0.150929</td>
      <td>0.861249</td>
      <td>0.970772</td>
      <td>0.952006</td>
      <td>1.000000</td>
    </tr>
  </tbody>
</table>

<h2>3.a Critères qui influencent le prix</h3>

Le critère qui influence le prix est la taille du carat, comme le démontre le tableau relatant les coefficients de corrélation, où l'on peut voir un coefficient de corrélation entre le prix et le carat de 0.921591.

<h2>3.b Corrélation entre le prix et la couleur</h3>

Lorsque l'on analyse le dernier graphique, on remarque que la couleur ayant la meilleure qualité 'D' n'est pas la plus onéreuse. Cela peut s'expliquer par le fait que la majorité des diamants ayant cette qualité n'ont pas les plus gros carats. De plus, ces diamants sont les plus rares à trouver, et donc moins nombreux dans le dataset.




