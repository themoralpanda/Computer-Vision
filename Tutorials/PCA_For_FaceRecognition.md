Date: 19th Nov 2017
*************************
Title: PCA for Face Recognition
***************************
Keywords: PCA, Principal Component Analysis, Dimensionality Reduction, Face Recoginition.
*********************************************************************************************
Note: This is not a short set of steps for Face detection. This is just for Face recognition. That is, How to find if a New face, is a part of the database or not.

1. Assume the training set has 100 face images each of size N*N pixels. eg 100*100 images.
2. The images are converted in to a <b> 1D Vector </b> of size N^2 * 1
3. After converting images in the training set into 1D vectors, the average image vector is found. ( Average of 100 face image 1D vectors )
4. Then Each image 1D vector is subtracted from the Mean vector to remove any common features in the images. So as to just retain only the unique features in the images. Simply ( X - Img(i) ) is perfomed on each vectors. 
5. These resultant vectors are put up as a columns of a final big matrix called A. ( i.e Each image is a column in this final matrix). Therefore the dimensions of this image pool matrix is ( N^2  *  M) where M is the total number of images in the training set each of which is a N^^2* 1 matrix.
6. Then the Covariance matrix is to be formed. <b> Cov() = A*A' </b>. But this will result in N^2 * N^2 Cov matrix. Which is a 10000*10000 matrix, a huge one. So Instead we will find an alternative computation to avoid this big of dimensions. Simply, we will compute the Covariance matrix as <b> Cov() = A' * A </b>.
7. This computaion will result in M * M matrix. In our case, it is 100*100 matrix instead of ( 10000*10000) matrix. 8. Then we need to select K vectors from this reduced Eigen space and project it to the original image space. Reducing the vector space to 100*100 is easy to pick K vectors than in the original image space. 
9. After selecting K Vectors from the Eigen space, we need to project the K vectors to the image space and get the K vectors in the Image space. This can be efficiently done thanks to Linear algebra. We can compute V = A*K  Since K's dimension is M*1 and A's dimension is N^2 * M , Doing this V = A*K  will result in a Eigen vector of dimension N^2 * M 
10. Thus we have K vectors in the original image space that represent all the images in the training set effectively. 
11. Now how can we map the Eigen vector in to a image in the training set? It is done by using the formula ( Image = Mean_Vector + ( weighted sum of Eigen Vectors) ) i.e Image = Mean + (w0 * E0 + w1* E1 +....wk* Ek) 
12. The weight vector is nothing but the percentage of the contribution by each eigen vector to the original image in the tranining set. i.e  w0 percent of E0 and w1 percent of E1 all the way to wk percent of Ek, contributes to the original Image. 
13. The reason why we are adding Mean vector to the formula, is because initially we subtracted the values from the mean vector.
14. The last step in training is to collect the Weight vectors for each image in the training data set. It will be a 1D vector of length K. This is stored in the database. 

**********************************************************************************************************
So far we have just used PCA for training the Recognizer. We have just used the images from the training set. Now what happens if a new image is to be recognized by our Recognizer? The steps go as follows. 

1. The Given image of size N*N is converted into the 1D vector like in the training, and then normalized using mean vector. 
2. Then the normalized input vector is projected in to the Eigen Space and weight vector is obtained for this image. 
3. Then the distance between this weight vector to the other weight vector is computed. This distance is then compared with a predefined trheshold and if the distance is less than the threshold, it is considered as Face and if its not, its considered as Non Face.

For much clearer tutorial and beautiful Video, visit the following tutorial @Youtube by @Mahvish Nasir in the following URL. 
<a href="https://www.youtube.com/watch?v=SaEmG4wcFfg">https://www.youtube.com/watch?v=SaEmG4wcFfg</a>


