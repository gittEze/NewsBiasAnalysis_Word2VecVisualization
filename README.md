# Análisis de Sesgos en Noticias con Word2Vec  

En este colab se realizó un **análisis de sesgos en el lenguaje** utilizando el modelo **Word2Vec**.  
El objetivo fue explorar **cómo ciertas palabras relacionadas con género, edad, clase social, ocupación, etc.** Se agrupan en el espacio graficado, tomando como base un conjunto de noticias.  

---

## 📊 Descripción del Dataset  

Se trabajó con un dataset compuesto por **1217 noticias**, cada una con su **URL**, **la noticia en si** y el **tipo**.  
Estos textos provienen de fuentes periodísticas diversas y reflejan distintos contextos sociales y económicos. 

---

## Preprocesamiento

El texto fue transformado a minúsculas y tokenizado para facilitar el entrenamiento del modelo.
Cada noticia se dividió en palabras mediante la siguiente instrucción:

```python
sentences = [frase.lower().split() for frase in corpus]
```
---

## Entrenamiento del Modelo Word2Vec

El modelo fue entrenado usando los siguientes parámetros:

```python
model = Word2Vec(
    sentences,
    vector_size=50,
    window=3,
    min_count=1,
    workers=4,
    sg=1
)
```

---

## Visualización

Para analizar las relaciones entre palabras y posibles sesgos en el lenguaje, se seleccionaron los siguientes términos:

`mujer, hombre, extranjero, refugiado, joven, adulto, niño, rico, pobre, trabajador, empresario`

Se aplicó PCA (Análisis de Componentes Principales) y visualizar las relaciones en un gráfico:

<img width="741" height="548" alt="image" src="https://github.com/user-attachments/assets/353ebf6d-9c38-4413-ab0f-1e3212d287fa" />

## Análisis realizado

El modelo Word2Vec agrupa palabras según los contextos en los que suelen aparecer juntas dentro de las noticias. Cada punto representa una palabra, y las que están más cerca entre sí son las que el modelo considera que tienen un significado o un uso similar, se puede ver que las palabras “hombre”, “empresario” y “rico” aparecen cerca una de otra. Esto sugiere que, en las noticias, estos deben usarse en contextos parecidos, lo que puede reflejar un sesgo de género y económico, donde se relaciona a los hombres con el éxito o el poder. En cambio, la palabra “mujer” está bastante separada de ese grupo, lo que indica que aparece en contextos distintos, alejada de la economía o los negocios empresariales. También se puede ver como “extranjero” y “trabajador” están un poco cerca, lo que puede indicar un sesgo hacia la migración laboral, ya que muchas veces los medios asocian a los inmigrantes principalmente con el trabajo. A su vez, “refugiado” y “adulto” aparecen cerca también, lo que podría indicar que las noticias suelen hablar de los refugiados como personas adultas y tebiendo en cuenta que la palabra "pobre" esta relativamente cerca también, puede ser que estos tambien sufran de probreza.
