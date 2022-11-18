## Installation

Install the conda environment by typing the following command:
``conda env create -f spec.yml``

Then, based on your setup, run the ``matcher.ipynb`` notebook under the environment named ``census-google_trends-matcher``. For instance, if you are using vs-code, you can do it by specifying the kernel as ``census-google_trends-matcher`` before running the cells in the notebook. 

The generated data will be collected under the folder ``data/`` created by means of running the notebook. By using the estimate data under the folder ``../census-data/data/``, this notebook approximates the median values of the metro areas specified in Google Trends. 

The notebook initially extracts and enlists the metro areas in the US represented by the file ``google_trends-locations.json`` under the resources folder. 

Then, based on the correspondence between counties and these metro areas represented in the file ``trends_metro_counties_crosswalk.csv`` under the resources folder, the notebook finds the counties belonging to a metro area. 

Then, for the counties belonging to that metro area, it populates the household count for income ranges/bins by using the applicable estimate table under the directory ``../census-data/data/`` (favored in the order: one year estimate (2021), one year supplementary estimate (2021) or five years estimate (2020)). For example, it finds the number of households in a metro area with the income in the range ``[10,000$, 15,000$)``, and does this for all the available range information.  

Then, based on the mapping from the income ranges to the household counts obtained for a metro area, the notebook approximates the median income by a clever trial and error algorithm (binary search). 

More specifically, each time, the algorithm tries a median value and approximates the number of households with less income than the tried median value. If there are way too more households than it should be, then it lowers the median value to be tried in the next step. Otherwise, it increases the value. 

To approximate the number of households with less income than the tried median value, it applies the following formula:
Let $med$ be the tried median value, $[l, r)$ represent the income range being considered and $hc$ be the household count with income in that range. Then, the approximated number of households having smaller income than $med$ would be: $max(0, min(1, \frac{med - l}{r - l})) * hc$

Beside the technical details, there are also several hand-fixed data parts.
For instance, some of the state level locations in Google Trends consist only one metro area, which results in not having the metro area information, but only state level location information. This issue is fixed manually by checking the Google Trends website, and learning the metro area associated with the state level location. The followings are the instances:
``Utah`` having ``Salt Lake City UT`` as its only metro area,
``District of Columbia`` having ``Washington DC (Hagerstown MD)`` as its only metro area,
``Rhode Island`` having ``Providence RI-New Bedford MA`` as its only metro area.

Another one is that one county named ``Valdez-Cordova`` does not have a corresponding estimate table collected from the census dataset, even though census assures us that it is always possible to find five years estimate data for any county. Luckily though, by using the [census data finder](https://data.census.gov/cedsci/table?q=S1901&g=0500000US02261&tid=ACSST5Y2019.S1901), a five years estimate table from the year 2019 was retrieved and used. 

Other than these two exceptions, every other county or metro area is processed without any issues. 