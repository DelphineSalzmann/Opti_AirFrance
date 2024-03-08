# Opti_AirFrance

Optimizing passenger seating for group cohesion, aircraft balance, and special needs is crucial for both customer satisfaction and operational efficiency. 

## Contents
- [Overview of the data](#Overview of the data)
- [Static model](#Static model)

## Overview of the data

For all the dates entered, we have datasets that contain the following data structure:

**Data Structure:**

| Column           | Description                                   |
|------------------|-----------------------------------------------|
| Numéro du groupe | Group number associated with passengers      |
| Femmes           | Number of women in the group                  |
| Hommes           | Number of men in the group                    |
| WCHR             | Number of passengers using wheelchairs        |
| TransitTime      | Transit time for each passenger in the group  |

## Static model

We can see that the problem of allocating passengers on an airplane requires a binary variable \(S_{ij}\), which associates each passenger \(i\) with a seat \(j\):

\[
S_{ij} = 
\begin{cases} 
1 & \text{if Passenger \(i\) is in seat \(j\)} \\ 
0 & \text{otherwise} 
\end{cases} 
\]

To meet the restriction of having a maximum of one passenger per seat:

\[
\sum_{i=1}^{n_p} S_{ij} \leq 1 ~~\forall j \in [1, n_s]
\]

where \(n_p\) is the number of passengers and \(n_s\) the number of seats.

To meet the restriction that every passenger has one and only one seat:

\[
\sum_{j=1}^{n_s} S_{ij} = 1 ~~\forall i \in [1, n_p]
\]