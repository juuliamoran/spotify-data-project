# Spotify Recommender

Els sistemes de recomanació han esdevingut una eina fonamental en les plataformes digitals actuals, ja que proporcionen una experiència personalitzada als usuaris suggerint contingut que s’ajusta als seus interessos. En el cas de serveis que ofereixen música, aquests sistemes permeten als usuaris descobrir cançons, artistes o una nova diversitat de sons que podrien ser del seu interès.

Hi ha diversos enfocaments utilitzats per desenvolupar sistemes de recomanació, i en aquest treball hem explorat tres d'ells: 
- **Els basats en contingut (Content-Based):** es fonamenten en les característiques del contingut per generar recomanacions. En aquest cas, hem implementat diverses funcions que utilitzen diferents enfocaments per recomanar cançons, basant-nos en aspectes com l'artista, el títol de la cançó o la similitud sonora.

- **El filtratge col·laboratiu (Collaborative Filtering):** aquest és un mètode per fer prediccions automàtiques (filtering) sobre els interessos d'un usuari mitjançant l'ús de preferències o informació de gust recopilada d'un o més usuaris (collaborative).

- **Els enfocaments basats en gràfics (Graph-Based):** representen les relacions entre cançons i usuaris com un graf, on les connexions es basen en co-aparicions d'usuaris, generant embeddings amb Node2Vec per capturar aquestes relacions.

**L’objectiu** d’aquest treball és explorar i comparar aquestes tècniques de recomanació utilitzant un conjunt de dades proporcionat per la Spotify Web API. Pretenem analitzar les diferències entre els enfocaments esmentats, tot identificant els seus avantatges i limitacions en la personalització de recomanacions musicals.

---

## Dataset
Per obtenir les dades necessàries per a la creació del sistema de recomanació, vam utilitzar la Spotify Web API. Aquesta API permet consultar informació detallada sobre diferents atributs musicals, incloent-hi els noms de les cançons, els artistes, els gèneres musicals, la popularitat, la durada, el tempo, la valència, entre d'altres. Vam obtenir un token d'accés que ens va permetre descarregar informació relacionada amb les cançons de les nostres playlists per a la creació del nostre conjunt de dades.
A continuació una mostra de les 5 primeres files del dataset:
| id | song_name                                           | artist_name       | popularity | release_date | genres                      | danceability | energy  | valence | tempo   | loudness | duration_ms | key | mode |
|----|----------------------------------------------------|-------------------|------------|--------------|----------------------------|--------------|---------|---------|---------|----------|-------------|-----|------|
| 0  | 34xTFwjPQ1dC6uJmleno7x Godspeed                    | Frank Ocean       | 78         | 2016-08-20   | lgbtq+ hip hop, neo soul   | 0.399        | 0.0969  | 0.0758  | 109.540 | -12.578  | 177922      | 6   | 1    |
| 1  | 3YJJjQPAbDT7mGpX3WtQ9A Good Days                   | SZA               | 73         | 2020-12-25   | pop, r&b, rap              | 0.436        | 0.6550  | 0.4120  | 121.002 | -8.370   | 279204      | 1   | 0    |
| 2  | 2UJsKjM595pEyWUcd8JEIR Fight For You - From the... | H.E.R.            | 43         | 2021-02-04   | r&b, rap                   | 0.695        | 0.6890  | 0.3920  | 95.013  | -8.176   | 270710      | 2   | 1    |
| 3  | 0KS2h61pHQ4WmOwruD7uxD Damage                      | H.E.R.            | 55         | 2020-10-21   | r&b, rap                   | 0.646        | 0.6960  | 0.1800  | 81.336  | -6.505   | 223415      | 1   | 1    |
| 4  | 2I88NEWpKrAPZuapXNV5G6 Belong to You (feat. 6LACK) | Sabrina Claudio   | 55         | 2017-10-05   | alternative r&b, r&b       | 0.605        | 0.5530  | 0.6200  | 152.076 | -10.845  | 185617      | 10  | 0    |

Els atributs que conté són:
- **id**: l'identificador únic de la cançó
- **song_name**: nom de la cançó
- **artist_name**: nom de l'artista de la cançó
- **genres**: múltiples gèneres musicals associats a la cançó
- **release_date**: data de publicació de la cançó
- **popularity**: nivell de popularitat que va de 0 a 100
- **danceability**: mesura de la facilitat de ball de la cançó i va de 0 a 1
- **energy**: nivell d'energia, pren valors de 0 a 1
- **valence**: mesura de la positivitat o vivacitat general de la cançó, pren valors que van de 0 per cançons tristes a 1 per cançons alegres
- **tempo**: tempo en BPM
- **loudness**: nivell de volum en dB
- **duration_ms**: duració de la cançó en mil·lisegons
- **key**: tonalitat, pren valors entre 0, que correspon a Do i 11 que correspon a Si
- **mode**: on 1 és escala major i 0 és menor

---

Aquest repositori conté els següents fitxers:
- `spotify.ipynb`: una jupyter notebook que conté el codi d'aquest treball
- `spotify_multiple_playlists_datasets_no_duplicates.csv`: aquest arxiu csv conté el dataset principal del treball (primer usuari)
- `spotify_adrian_dataset.csv`: aquest arxiu csv conté les cançons i característiques del segon usuari
- `total_dataset.csv`: aquest arxiu csv és el total de 13 usuaris creats a partir de la divisió i solapació dels dos arxius anteriors combinats
- `README.md`: aquest mateix arxiu el qual conté la informació principal

### Autores:
- Mara Montero
- Júlia Morán