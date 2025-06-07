# Artist Collaboration Network Analysis: Understanding Music Industry Partnerships

**Author**: Harsh Malik
**Date**: `r Sys.Date()`
**Output Format**: HTML with floating TOC, numbered sections

---

## Project Overview

This project explores collaboration patterns among music artists by constructing and analyzing a **network graph** using Spotify Charts data. Each artist is represented as a node, and edges connect artists who have worked together on a track. This method transforms collaboration data into a social network, revealing insights about influence, popularity, and group dynamics in the music industry.

---

## Objectives

* Build a network graph of artist collaborations using Spotify Charts data.
* Identify the most connected, influential, and strategically positioned artists using:

  * Degree Centrality
  * Betweenness Centrality
  * Eigenvector Centrality
* Discover community structures of artists who frequently collaborate with each other.
* Visualize the overall network and sub-networks of top artists.
* Provide statistical summaries, visual insights, and network metrics to better understand collaborative behavior in the modern music industry.

---

## Data Description

**Dataset**: `Charts.csv`
**Source**: Spotify Global Charts
**Structure**:

* `track_name`: Name of the song
* `artists`: Semi-colon separated list of artists for each track
* `track_id`: Unique identifier for each track

**Network Construction**:

* **Nodes (Artists)**: Individual musicians listed on Spotify tracks
* **Edges**: Presence of two or more artists on the same song (i.e., co-appearance)
* **Edge Weights**: Number of collaborations between each pair

---

## Tools and Libraries

The analysis is written in R Markdown and uses the following packages:

```r
library(tidyverse)
library(igraph)
library(ggraph)
library(knitr)
library(kableExtra)
library(RColorBrewer)
library(gridExtra)
library(corrplot)
```

---

## Analysis Workflow

### 1. Data Cleaning and Preprocessing

* Remove rows with missing artist or track data
* Parse artist strings into lists
* Generate edge lists using artist pair combinations from each track

### 2. Network Construction

* Build undirected graph from edge list
* Compute summary statistics: node count, edge count, average degree, and density

### 3. Network Visualization

* Visualize full network using `ggraph` (limited to top 50 most connected artists for clarity)
* Nodes sized by degree (collaborations), colored by community
* Edge thickness scaled by weight

### 4. Degree Distribution

* Visual and log-log distribution plots to analyze the structure
* Indicates presence of "superstar" artists and many with few collaborations (power law behavior)

### 5. Centrality Measures

* **Degree Centrality**: Most connected artists
* **Betweenness Centrality**: Artists acting as bridges across communities
* **Eigenvector Centrality**: Influential artists connected to other influential artists

### 6. Community Detection

* Use the Louvain algorithm to detect groups
* Report modularity score and top communities by size
* Display sample artists from each top community

### 7. Centrality Correlation

* Analyze relationships between centrality measures using correlation matrices and visualizations

---

## Key Insights

* Collaboration is uneven: Most artists collaborate with a few others, while a few are extremely well connected.
* Communities exist: Artists tend to cluster, often due to genre, language, or industry affiliations.
* Bridge artists matter: Some artists serve as important connectors between different communities.
* Influence is not only about quantity: Eigenvector centrality shows that connecting with influential artists increases status.

---

## Results Summary

| Metric                    | Value                    |
| ------------------------- | ------------------------ |
| Number of Artists         | `r vcount(g)`            |
| Number of Collaborations  | `r ecount(g)`            |
| Most Collaborative Artist | `r most_central_degree`  |
| Top Bridge Artist         | `r most_central_between` |
| Most Influential Artist   | `r most_central_eigen`   |
| Communities Detected      | `r num_communities`      |
| Largest Community Size    | `r max(comm_sizes)`      |

---

## Applications

This project can support:

* Music Producers: Identifying influential artists for collaborations
* Record Labels: Understanding cross-genre potential and partnership opportunities
* Researchers: Studying patterns in collaborative creativity
* Emerging Artists: Identifying potential collaborators and entry points into the industry

---

## How to Run This Project

1. Place `Charts.csv` in your working directory.
2. Open the R Markdown file and knit to HTML.
3. Install all required R packages listed above using `install.packages()`.

---

Let me know if you’d like this version exported to PDF, embedded into a GitHub site, or adjusted for class submission.
