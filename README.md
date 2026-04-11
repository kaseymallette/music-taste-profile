# music-taste-profile
Analyzing my Spotify music library using k-means clustering and nearest neighbors to map audio features and generate playlists. 

## Introduction

I wanted to understand my own music taste algorithmically — not through Spotify's black-box recommendations, but by clustering my library on audio features I could inspect and interpret.

**The dataset:** I started with four genre playlists (rock, pop, rap/R&B, 2010s alternative) of 250 songs each, plus my liked songs (~2,000 tracks). After deduplication and intersection, the working library contained **2,309 songs**.

**The features:** Spotify's audio descriptors plus metadata:

`BPM` · `Valence` · `Dance` · `Energy` · `Acoustic` · `Loud (Db)` · `Speech` · `Live` · `Time Signature` · `Album Year` · `Popularity`

## Methods

**Two approaches:**

1. **Nearest neighbors** — given a seed song, find similar tracks by audio feature distance. This answers: *"I like this song, what else sounds like it?"*

2. **K-means partitioning** — split a large playlist into smaller clusters using silhouette-optimized k. This answers: *"How does my library naturally group, and can I turn those groups into playlists?"*

| Notebook | Approach | Purpose |
|----------|----------|---------|
| `01_exploratory_analysis` | — | Artist/decade/popularity distributions, feature selection, correlation matrix, PCA |
| `02_knn_playlist_generator` | Nearest neighbors | Seed song retrieval and playlist generation |
| `03_partition_generator` | K-means partitioning | Automated playlist splitting with silhouette-optimized k selection |

## Results

### Library composition

The library contained **1,046 unique artists** across 2,309 songs.

| Playlist | Unique Artists |
|----------|----------------|
| Liked Songs | 618 |
| Rap/R&B | 182 |
| Alternative | 152 |
| Rock | 144 |
| Pop | 141 |

**Top 5 artists by song count:**

| Artist | Songs |
|--------|-------|
| Eminem | 20 |
| The Neighbourhood | 20 |
| Matt Maeson | 20 |
| Florence + The Machine | 20 |
| Maroon 5 | 18 |

![Distribution of Song Count by Artist by Playlist](images/song_count_by_artist.png)

*Figure 1: Artist frequency follows a long-tail distribution across all playlists — most artists contribute only 1–2 songs, with a small number contributing 10+.*

## Discussion 