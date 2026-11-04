🎵 Neo4j Music Graph Analytics: Recomendação e Análise de Músicas do Spotify

Este repositório contém o projeto prático de modelagem e análise de dados em grafos utilizando o **Neo4j** e dados de faixas do **Spotify**, desenvolvido como requisito para o módulo de Bancos de Dados NoSQL da **DIO**.

---

## 📌 Contexto do Problema e Justificativa para Grafos

Em plataformas de streaming de música como o Spotify, o ecossistema de dados é altamente interconectado: **Artistas** lançam **Músicas**, que pertencem a **Álbuns** e são classificadas em **Gêneros**.

### Por que utilizar Grafos em vez de um Banco Relacional (SQL)?
1. **Performance em Consultas Complexas:** Em um banco relacional (SQL), responder a perguntas como *"Quais músicas recomendadas pertencem aos mesmos gêneros de uma faixa X?"* exige múltiplos `JOINs` entre tabelas de associação, tornando a consulta lenta à medida que a base cresce.
2. **Conexões de Primeira Classe:** No Neo4j, relacionamentos são armazenados como ponteiros diretos entre nós. Navegar de uma música para o seu gênero ou artista é instantâneo (complexidade $O(1)$ por travessia).
3. **Facilidade para Recomendação:** Grafos permitem implementar algoritmos de filtragem colaborativa e caminhamento mais curto de forma nativa e intuitiva.

---

## 📐 Modelo do Grafo (Modelagem)

A estrutura do banco de dados foi modelada com base nas seguintes entidades e relacionamentos:

* **Nós (Labels):**
  * `Track`: Representa a faixa musical (Propriedades: `trackId`, `trackName`, `popularity`).
  * `Artist`: Representa o artista ou banda (Propriedades: `artistName`).
  * `Album`: Representa o álbum (Propriedades: `albumName`).
  * `Genre`: Representa o gênero musical (Propriedades: `genreName`).
* **Relacionamentos:**
  * `(:Track)-[:PERFORMED_BY]->(:Artist)`
  * `(:Track)-[:BELONGS_TO]->(:Album)`
  * `(:Track)-[:HAS_GENRE]->(:Genre)`

### Visualização do Esquema (`CALL db.schema.visualization()`)
O esquema da base de dados gerado nativamente no Neo4j pode ser visualizado abaixo:

<img width="1123" height="742" alt="image" src="https://github.com/user-attachments/assets/7dab5501-6dcb-4a87-b797-c29288506f47" />


---

## 🛠️ Dataset e Script de Importação

* **Base de Dados:** Dataset público extraído do Kaggle (*Spotify Tracks Dataset*), contendo métricas de popularidade, gêneros e identificadores das músicas.
* **Amostra:** Disponível na pasta `/data` deste repositório para reprodução do projeto.
* **Perguntas:**
  **Quais são as 10 músicas mais populares do gênero 'chill'?**
    <img width="1155" height="844" alt="image" src="https://github.com/user-attachments/assets/e70d52e2-f4b4-470b-81d5-bfb1ab2cca1a" />

  **Todas as musicas com o gênero 'chill'**
    <img width="1154" height="796" alt="image" src="https://github.com/user-attachments/assets/c23f2e07-145d-47d8-9724-e6e4ca56793a" />

