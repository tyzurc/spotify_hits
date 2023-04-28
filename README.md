# Predicción de éxitos musicales usando Spotify

| Notebook | Presentación |
| :-: | :-: |
| [spotify_hits](spotify_hits.ipynb) | [presentacion_ds]() |

## Contexto

¿Se puede predecir cuando una canción será un éxito? ¿Qué características tendría que tener una canción para que lo sea?

Para contestar estas interrogantes, se creó un dataset con información acerca de canciones "hit" o "flop" (fracaso, en español) y sus características, mediante el uso de las API de Billboard y Spotify.

### Contenido del dataset

- **track**: Nombre de la pista.

- **artist**: Nombre del artista.

- **uri**: Identificador de la pista.

- **danceability**: "Bailabilidad". Describe qué tan adecuada es una pista para bailar en función de una combinación de elementos musicales que incluyen tempo, estabilidad del ritmo, fuerza del ritmo y regularidad general. Un valor de 0,0 es menos bailable y 1,0 es más bailable.
  
- **energy**: La energía es una medida de 0,0 a 1,0 y representa una medida perceptiva de intensidad y actividad. Por lo general, las pistas enérgicas se sienten rápidas, fuertes y ruidosas. Por ejemplo, el death metal tiene mucha energía, mientras que un preludio de Bach tiene una puntuación baja en la escala. Las características perceptivas que contribuyen a este atributo incluyen el rango dinámico, el volumen percibido, el timbre, la tasa de inicio y la entropía general.

- **key**: La tonalidad general estimada de la pista. Los números enteros se asignan a tonos utilizando la notación de clase de tono estándar. P.ej. 0 = C, 1 = C#/Db, 2 = D, y así sucesivamente. Si no se detectó ninguna tonalidad, el valor es -1.

- **loudness**: La sonoridad general de una canción en decibeles (dB). Los valores de sonoridad se promedian en toda la pista y son útiles para comparar la sonoridad relativa de las pistas. La sonoridad es la cualidad de un sonido que es el principal correlato psicológico de la fuerza física (amplitud). Los valores típicos oscilan entre -60 y 0 db.

- **mode**: Modo indica la modalidad (mayor o menor) de una pista, el tipo de escala de la que se deriva su contenido melódico. Mayor está representado por 1 y menor es 0.

- **speechiness**: Speechiness detecta la presencia de palabras habladas en una pista. Cuanto más parecida a la voz sea la grabación (por ejemplo, programa de entrevistas, audiolibro, poesía), más cerca de 1,0 será el valor del atributo. Los valores superiores a 0,66 describen pistas que probablemente estén formadas en su totalidad por palabras habladas. Los valores entre 0,33 y 0,66 describen pistas que pueden contener tanto música como voz, ya sea en secciones o en capas, incluidos casos como la música rap. Los valores por debajo de 0,33 probablemente representen música y otras pistas que no sean de voz.

- **acousticness**: Una medida de confianza de 0,0 a 1,0 de si la pista es acústica. 1.0 representa una alta confianza en que la pista es acústica.

- **instrumentalness**: Predice si una pista no contiene voces. Los sonidos “Ooh” y “aah” se tratan como instrumentales en este contexto. Las pistas de rap o de palabras habladas son claramente "vocales". Cuanto más cerca esté el valor de instrumentalidad de 1,0, mayor será la probabilidad de que la pista no contenga contenido vocal. Los valores superiores a 0,5 pretenden representar pistas instrumentales, pero la confianza es mayor a medida que el valor se acerca a 1,0.

- **liveness**: Detecta la presencia de una audiencia en la grabación. Los valores de liveness más altos representan una mayor probabilidad de que la pista se interprete en vivo. Un valor superior a 0,8 proporciona una gran probabilidad de que la pista sea en vivo.
  
- **valence**: Una medida de 0,0 a 1,0 que describe la positividad musical transmitida por una pista. Las pistas con una valencia alta suenan más positivas (p. ej., felices, alegres, eufóricas), mientras que las pistas con una valencia baja suenan más negativas (p. ej., tristes, deprimidas, enfadadas).

- **tempo**: El tempo general estimado de una pista en pulsaciones por minuto (BPM). En terminología musical, el tempo es la velocidad o ritmo de una pieza dada y se deriva directamente de la duración promedio del tiempo.
  
- **duration_ms**: La duración de la pista en milisegundos.

- **time_signature**: Una estimación general del compás de una pista. El compás (medidor) es una convención de notación para especificar cuántos tiempos hay en cada compás (o compás).

- **chorus_hit**: Esta es la mejor estimación de cuándo comenzaría el coro para la pista. Es la marca de tiempo del inicio de la tercera sección de la pista. Esta función se extrajo de los datos recibidos por la API para el análisis de audio de esa pista en particular.

- **sections**: El número de secciones que tiene la pista en particular. Esta función se extrajo de los datos recibidos por la API para el análisis de audio de esa pista en particular.

- **target**: La variable destino para la pista. Puede ser '0' o '1'. '1' implica que esta canción ha aparecido en la lista semanal (emitida por Billboards) de pistas Hot-100 en esa década al menos una vez y, por lo tanto, es un 'éxito'. '0' implica que la pista es un 'flop' o 'fracaso'.

#### Criterio para que una canción sea un 'flop' o fracaso

- La pista no debe aparecer en la lista 'hit' de la década.
- El artista de la pista no debe aparecer en la lista de 'hits' de la década.
- La pista debe pertenecer a un género que podría considerarse no convencional.
- El género de la pista no debe tener una canción en la lista de 'hits'.
- La pista debe tener 'US' como uno de sus mercados.
