## Installation

Install the conda environment by typing the following command:
``conda env create -f spec.yml``

Then, based on your setup, run the ``census-data-collector.ipynb`` notebook under the environment named ``census-data``. For instance, if you are using vs-code, you can do it by specifying the kernel as ``census-data`` before running the cells in the notebook. 

The data will be collected under the folder ``data/`` created by means of running the notebook. This notebook retrieves one year estimates, one year supplementary estimates and five year estimates of census community survey tables regarding the household income for the counties in the US for several years (ranging from 2011 to 2021). The retrieved tables are purified by only keeping relevant columns which are ``Name``, ``Geo_id``, and number of households belonging to several income ranges (e.g. ``0 - 9999`` or ``100000 - 149000``). These income ranges are going to be used to approximate the median household income of metro areas specified by the Google Trends. 