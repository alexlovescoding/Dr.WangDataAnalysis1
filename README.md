# Dr.WangDataAnalysis1
The idea of detecting web attacks through machine learning is not a brand new topic, but an area that still needs better development and research. This project analyzed 822,226 log records from a software company's user login page in a 5-hour range. After pre-processing the dataset, the algorithm detected some records being potential attacks and calculated the likelihood based on suspicious behaviors. 

The project first processes the data into Pandas data frame and omits all the features of the record that are not interested in detecting the attacks. Next, the data is compressed from 822,226 data to around 44,514 by combining the records that have the same sources and destination IP addresses in the same UNIX time. The higher rate the compression is, the more duplicate responses there are in the dataset. This significantly improved the efficiency of the process. Then, unsupervised machine learning is applied to give the detection of the dataset using K-means clustering. The three clusters each represent not-suspicious, suspicious, and gray area. 

Training/testing the data into 0.66/0.33 to analyze the likelihood of each response's abnormal behaviors, and use the previous result as a supervisor for accuracy. The gray area is again using k-mean clustering to separate into 2 clusters, labeled as "more suspicious" and "less suspicious". The "more suspicious" are added into the suspicious_activity dataset. Doing so ensures the machine does not miss any responses that get filtered out from the analysis but still remain an abnormal behavior. The likelihood of the suspicious is calculated based on the percentage over the maximum response in 1 second.

The initial approach of this problem was to use k-mean clustering based on how much time it took to process the response. However, this is not significant due to the delay from each server and the unknown source of the dataset being analyzed. After researching the definition of abnormal behaviors in reality, most of the features are filtered out because they do not have much impact in analyzing attacks. An attack for a general log-in page is defined as multiple visits, responses, callbacks in a short period of time. Thus, pre-processing the data by combining each duplicate response in the same second helps determine the responses' number of visits that stands out.

The 3-2 double-clustering technique helps the machine narrows down the suspicious activities. If k-means clustering is applied only once with 2 clusters, the uncertain groups of the dataset's log records would possibly wrong the result. Therefore, creating a gray area in the middle of two certainties helps to detect the potential attacks that could be missed.

The result is saved into result.csv and all detected attacks are saved in suspicious_activity.csv

References:

<li>Gong, X., Zhou, Y., Bi, Y., He, M., Sheng, S., Qiu, H., He, R., & Lu, J. (2019, October 3). Estimating web attack detection via model uncertainty from inaccurate annotation. IEEE Xplore. https://ieeexplore.ieee.org/abstract/document/8854029. 
?? ?? 
<br>This article illustrated the potential attacks in log records that are not successfully recorded, which are label as "unknown". This project is aware of the situation from this article. All the unknown log flow records have no source and destination IP address, therefore are all filtered out before creating the Panda dataframe to avoid it reducing the accuracy of the result.</li><br>
<li>Tian, Z., Luo, C., Qiu, J., Du, X., & Guizani, M. (2019, August 30). A distributed deep learning system for web attack detection on edge devices. IEEE Xplore. https://ieeexplore.ieee.org/document/8821336. 

<br>In this article, the author developed a machine learning model using deep learning to detect web attacks by analyzing its URLs. The result has high accuracy. The approach of machine learning was inspired into this project in which the author created a system that solves challenges in the paradigm of the Edge of Things.</li><br>
<li>G??ron, A. (2019). Hands-On Machine Learning with Scikit-Learn, Keras, and TensorFlow, 2nd Edition. O'Reilly Media, Inc.
<br>
?? ?? 
The idea of using K-means clustering, sklearn, data split, training, and testing machine learning algorithms to apply to this project is inspired by this book. </li><br>
<li>Torrano-Gimenez, C., Franke, K., Alvarez, G., & Nguyen, H. T. (2012, August 29). Combining expert knowledge with automatic feature extraction for reliable web attack detection. https://onlinelibrary.wiley.com/doi/epdf/10.1002/sec.603. 
<br>
?? ?? 
This article discussed the feature construction and feature selection of web attack detection. This project applied the idea of omitting the features that are not interested in attack detection. </li><br>
<li>Betarte, G., Pardo, ??., &amp; Mart??nez, R. (2019, January 17). Web application attacks detection using machine learning techniques. IEEE Xplore. https://ieeexplore.ieee.org/document/8614199. 
<br>


</li><br>
<li>Abdulraheem, M., &amp; Ibraheem, N. (2019). A DETAILED ANALYSIS OF NEW INTRUSION DETECTION DATASET. http://www.jatit.org/volumes/Vol97No17/4Vol97No17.pdf</li><br>
<li>https://github.com/p-neumann/User-Behavior-Analysis-and-Prediction</li>
