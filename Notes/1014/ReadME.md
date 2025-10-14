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
