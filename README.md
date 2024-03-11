# Opti_AirFrance

Optimizing passenger seating for group cohesion, aircraft balance, and special needs is crucial for both customer satisfaction and operational efficiency. 

## Contents
- [Overview of the Data](#overview-of-the-data)
- [Static Model](#static-model)

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

We can see that the problem of allocating passengers on an airplane requires a binary variable $S_{ij}$, which associates each passenger i with a seat j:


$$S_{ij} = 
\begin{cases} 
1 & \text{if Passenger i is in seat j} \\ 
0 & \text{otherwise} 
\end{cases}$$ 


To meet the restriction of having a maximum of one passenger per seat:


$$\sum_{i=1}^{n_p} S_{ij} \leq 1 ~~\forall j \in [1, n_s]$$


where $n_p$ is the number of passengers and $n_s$ the number of seats.

To meet the restriction that every passenger has one and only one seat:


$$\sum_{j=1}^{n_s} S_{ij} = 1 ~~\forall i \in [1, n_p]$$

It is important that the plane has a balanced weight distribution around its center of mass

$$x_g = \sum_{i=1}^{np} \sum_{j=1}^{n_s} \frac{(j\mod 7)S_{i,j}w_i}{\left(\sum\limits_{i=1}^{n_p} w_i\right)}$$

$$3 < x_g < 7$$

$$y_g = \sum_{i=1}^{np} \sum_{j=1}^{n_s} \frac{(j\mod 21)S_{i,j}w_i}{\left(\sum\limits_{i=1}^{n_p} w_i\right)}$$

$$13 < y_g < 17$$

With $x_g$ and $y_g$ the barycenters on x and y respectively.

Objective Functions

$$f = \sum_{k=1}^{n_t} \sum_{j=1}^{n_s} S_{k,j} \times \frac{1}{T_k} \times q$$

where: 


- ** $$f$$ **: Represents the objective function.
- ** $$n_t$$ **: Denotes the total number of transit passengers.
- ** $$T_k$$ **: Stands for the connection time of transit passenger \( k \).
- ** $$q$$ **: A parameter representing the weight associated with the seat's position in the aircraft.
