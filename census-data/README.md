## Installation

Install the conda environment by typing the following command:
``conda env create -f spec.yml``

Then, based on your setup, run the ``census-data-collector.ipynb`` notebook under the environment named ``census-data``. For instance, if you are using vs-code, you can do it by specifying the kernel as ``census-data`` before running the cells in the notebook. 

The data will be collected under the folder ``data/`` created by means of running the notebook. This notebook retrieves data for various years (from 2011 to 2021 (skipping 2020)) from various geographical hierarchies (state, county, place, metropolitan areas). Each table consists of the following columns:
``|Name|``, ``|Geo_id|``, ``|Estimate, Households, Median income (dollars)|``, ``|Margin of Error, Households, Median income (dollars)|``, ``|Estimate, Households, Mean income (dollars)|`` and ``|Margin of Error, Households, Mean income (dollars)|``.