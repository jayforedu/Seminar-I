# 題目:A study of Efficient GNSS Coordinate Classification Strategies for Epidemic Management
# 講者:陳忠信
# 日期:2025/10/14
# 筆記內容:
## Relate Work:
* PIP
  * These methods cna generally be distinguished by two types: the ray casting and the winding number.
  * It need the edges of a polycon to evaluate a node is inside or iutside of this polygon.
* KNN classification exhibits several remarkable properties.
  * the classification is available in various fields,including data mining algorithms and artifficial intelligence(AI).
  * Containing a number of training data points and a test data point to evaluate the class of the test point.
## Relate Work: Traditional KNN
In the KNN classification, there steps are involved for a test data point as follows:
* Step 1.It evaluates the Euclidean distance between the sample and test point,with a time complexity of O(nTD),where nTD is the dataset size.
* Step 2.It sorts the training dataset based on Euclidean distance with an O(nTD<sup>2</sup>) time complexity.
* Step 3.It use the majority classification rule to predict to class of the test point,with a time complexity of O(k), where K is the number of neighbors in the KNN classification.

## Related Work: One-Area and Cell/Rectangle Based PIP
* Cell Allocation for a target area.
* Techniques:
  * Points in inner cells: unnecessary do evaluation
  * Points in intersected cells: do evaluation
## System Model
### Positioning
<img width="1321" height="397" alt="image" src="https://github.com/user-attachments/assets/781e5b80-ebd0-44c5-883a-41376ee27018" />

1. The data sent from the mobile devices of targets will be stored as unclassified geographic points.
2. The server will individually take out a point from the unclassified points and position which polygon this point is inside.
3. The server will store these geographical points with their classes.
### Classification
<img width="760" height="305" alt="image" src="https://github.com/user-attachments/assets/6445ffbb-1046-45bf-b8b3-6727937cc05c" />

1. The real-time data sent from targets' mobile devices arrive to the server.
2. The server extracts candidate points from the storage of classified targets.
3. The server will classify the targets into their located areas according to the candidate points.
## Proposed Strategy  
* For KNN classification will make statistics on the class g'<sub>pc</sub> of g' using I(－), find the class i with the largest number, and then assign it to g<sub>cc</sub>.
<p align="center">
  <img src="https://latex.codecogs.com/png.latex?\dpi{200}\bg_white\fg_black%20g_{cc}=\underset{i}{\arg}(\max\sum_{g'\in%20NB}I(g'_{pc}=i)))" alt="formula"/>
</p>

* We also contain the weighting KNN
* The Euclidean distance of two points ga and gb is as follow, where (gax,gay) (gbx,gby) is the coordinate value of point gb.
<p align="center">
  <img src="https://latex.codecogs.com/png.latex?\dpi{200}\bg_white\fg_black%20d\left(ga,gb\right)=\sqrt{\left(ga_{x}-gb_{x}\right)^2-\left(ga_{y}-gb_{y}\right)^2}" alt="formula"/>
</p>

* The weighted KNN is
<p align="center">
  <img src="https://latex.codecogs.com/png.latex?\dpi{200}\bg_white\fg_black%20g_{cc}=\underset{i}{\arg}(\max\sum_{g'%5Cin%20NB}I(g'_{pc}=i%5Ctimes%20d(g,g')^{-1}))" alt="formula"/>
</p>

## Proposed Strategy:KNN Classification 
* Algorithm 4 employs the technology of the weighting KNN classification for classifying points into areas.
  * In addition, Step 1 of this algorithm calculates the candidates of k neighbors based on a numerical value r. When necessary, the value of r will be adaptively adjusted until the number of candidates is greater than or equal to k.
  * So, the candidates of k neighbors in Steps 2, 3, and 4 are k or slightly more than k data points, not the total training dataset.
  * In this way, we improve the classification time

## Proposed Strategy: Analysis
* Property 1. Given a point g and a polygon set PA with size m, if point g is inside one of set PA, Algorithm PtPos positions point g in O(m x nmax) time, where nmax is this polygon's largest edge number of this polygon set.
* Property 2. Given a point g and a training dataset T with size ny, algorithm AdaptKNN classifies point g in O(n) time.

## Experiment: Class distributions
The class distributions of Type-1 ans Type-2.Type-1 has 12 classes and Type-2 has 256 classes.
<p align="center">
  <img width="801" height="473" alt="image" src="https://github.com/user-attachments/assets/97eb0889-f5a6-4aa1-b9c4-8b3cb8772911" />
</p>

## Experiment: Classification Time
<p align="center">
  <img width="1152" height="535" alt="image" src="https://github.com/user-attachments/assets/fd86e8f9-446d-4767-891a-fdd945509c1e" />
</p>

## Experiment: Classification Accuracy
<p align="center">
  <img width="1152" height="535" alt="image" src="https://github.com/user-attachments/assets/43c90719-1cee-47dc-8615-c4e1a53fdd71" />
</p>

## Conclusions
* In this paper, we have planned a strategy, including positioning and classification phases, which can be used when epidemic management or other applications need to track the location of some targets or people.
* We hope this research can help epidemic management understand the spread of these pathogens and enable us to make predictions and preparations earlier, significantly as the infection numbers rapidly increase.
