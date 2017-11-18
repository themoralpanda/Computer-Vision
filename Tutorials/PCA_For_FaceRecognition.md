Date: 19th Nov 2017
Title: PCA for Face Recognition
Keywords: PCA, Principal Component Analysis, Dimensionality Reduction, Face Recoginition.

Note: This is not a short set of steps for Face detection. This is just for Face recognition. That is, How to find if a New face, is a part of the database or not.

1. Assume the training set has 100 face images each of size N*N pixels. eg 100*100 images.
2. The images are converted in to a <b> 1D Vector </b> of size N^2 * 1
3. After converting images in the training set into 1D vectors, the average image vector is found. ( Average of 100 face image 1D vectors )
4. Then Each image 1D vector is subtracted from the Mean vector to remove any common features in the images. So as to just retain only the unique features in the images. Simply ( X - Img(i) ) is perfomed on each vectors. 
5. These resultant vectors are put up as a columns of a final big matrix called A. ( i.e Each image is a column in this final matrix). Therefore the dimensions of this image pool matrix is ( N^2  *  M) where M is the total number of images in the training set each of which is a N^^2* 1 matrix.
6. Then the Covariance matrix is to be formed. <b> Cov() = A*A' </b>. But this will result in N^2 * N^2 Cov matrix. Which is a 10000*10000 matrix, a huge one. So Instead we will find an alternative computation to avoid this big of dimensions. Simply, we will compute the Covariance matrix as <b> Cov() = A' * A </b>.
7. This computaion will result in M * M matrix. In our case, it is 100*100 matrix instead of ( 10000*10000) matrix. 