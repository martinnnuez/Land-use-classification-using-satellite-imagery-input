# Land use classification using satellite imagery input

In the first instance I will adjust an unsupervised classification algorithm to characterize the elements that maintain a close relationship. Then I will reclassify these groups based on the land uses of interest helped by Google Earth, Maps and the coverage of land uses in the province of Córdoba as a means of validation of the decisions I make.

From the labels obtained, I will train a predictive algorithm to generate a tool that allows to differentiate the land uses of the province of Córdoba automatically.

## Landsat 8 

Landsat 8 is an American Earth observation satellite launched in 2013. Operated by NASA and the United States Geological Survey (USGS) since 1972.

The Landsat 8 satellite carries two instruments OLI and TIRS, which stand for Operational Land Imager (OLI) and Thermal Infrared Sensor (TIRS). The OLI sensor provides access to nine spectral bands that cover the spectrum from 0.433 μm to 1.390 μm, while TIRS records from 10.30 μm to 12.50 μm.

The satellite completes its 705 km high orbit every 99 minutes, and revisits the same point on the Earth's surface every 16 days with a lag of 8 days with respect to the Landsat 7 satellite, of the same project. Under these conditions the satellite acquires about 650 images daily.

## Work schedule

1. Download / upload Landsat 8 images.

* Download link: 

https://drive.google.com/drive/folders/1NEIEqtID90iXQzqr4Uuie26XRqzABX1q

2. Image preprocessing.

* Upload the image in tif format through the rasterio library.

* Apply a linear enhancement to the image bands

3. Generate a cutout.

* A cut is generated that covers the metropolitan area of ​​the province of Córdoba, Villa Carlos Paz and the San Roque Dam, thus facilitating the work with the image in the area of ​​interest.

4. Pass the pixels of the bands to a DataFrame.

5. Unsupervised classification: K-means clustering with mini batch.

* K-means clustering with mini batch: alternative to the K-means algorithm for clustering massive data. The advantage of this algorithm is that it reduces the computational cost by not using the entire data set in each iteration but a subsample (mini batch) of a fixed size. This strategy reduces the number of distance calculations per iteration and given the number of clusters we are going to split the data into, it is convenient.

6. Assignment of land use labels. Labels:

* Urbano alta compacidad.
* Urbano media compacidad.
* Urbano baja compacidad.
* Monte.
* Pastizales.
* Matorral/Arbustal.
* Cuerpo de Agua.
* Cultivo Extensivo Anual.
* Cultivo Hortícola Multiespecifico.

7. Predictive model adjustment: Xgboost.

* Adjustment of an XGBClassifier with the default parameters. Being in the presence of a multiclass classification, the objective metric is defined as a multi:softprob since it generates a probability of belonging to each of the classes.

8. Optimization of hyperparameters: Bayesian search.

* Search of hyperparameters by Bayesian search.
Bayesian optimization works by constructing a posterior distribution of functions (Gaussian process) that best describes the function you want to optimize. As the number of observations grows, the posterior distribution improves and the algorithm becomes more certain of which regions in the parameter space are worth exploring and which are not.

9. Application of the model to an unknown area.
10. Interpretation results.

