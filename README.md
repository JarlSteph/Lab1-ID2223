### Our additions
## Jarl Stephansson & Stefan Ivchenko

In the first notebook, we added the rolling features, for 1, 2 and 3 days before a specific day. This was done by shifting our dataframes by 1, 2, and 3 steps.  For all sensors in our region, we insert all our dataframes into the same feature groups - one fg for weather and one for air quality. The city was used as the primary key to distinguish between them. We then upload our full featrue groups to Hopswork. We use objects that we called "Place" objects, to keep track of cities, and their values. We also validated the data, and preprocessed it so the formats were matching between sensors. For all sensors but Hedemora, the historical data downloaded was not the PM25 values - it was the raw particle concentration values. By comparing them, we found a relationship between them, with PM25 often being 4 times the raw concentration. This was an assumption, but without it we would only have been able to do one sensor in our area (Dalarna and Gävleborg).

For the second notebook, we added the same features as in the first one, but it is meant to be automatically run once a day. The second one and the fourth notebook are run each day. We add the rolling features by downloading data from our previous three days from hopswork. When this is done, we upload the daily dataframe, inserting it at the end of our air quality and weather feature groups in Hopswork.

The third notebook is used for training our model. We added one hot encoding for which month a day belongs to, as the air quality seemed to be connected to the seasons. We one hot encoded the months to not imply a ordinal relationship between the months. We trained an XG Boost model on the Hedemora dataset first, as this one was the best quality data of all sensors in our region. We used a grid search and a validation dataset to find the best parameters to use, and then we used those parameters when we trained all other models as well. The MSE was over 130 with the base XG Boost model with the default featuers, and after we added ours and changed the parameters for the XG Boost model, we got it below 55. We trained one model for each city, but only used the grid search and validation set on our Hedemora set.

Finally, we display our results using our fourth notebook. They can be seen in Github pages, with one image per city. This is also run each day together with the second notebook.


**The link for the pages is:** https://jarlsteph.github.io/Lab1-ID2223/


# mlfs-book
O'Reilly book - Building Machine Learning Systems with a feature store: batch, real-time, and LLMs


## ML System Examples


[Dashboards for Example ML Systems](https://featurestorebook.github.io/mlfs-book/)


# Run Air Quality Tutorial

See [tutorial instructions here](https://docs.google.com/document/d/1YXfM1_rpo1-jM-lYyb1HpbV9EJPN6i1u6h2rhdPduNE/edit?usp=sharing)
    
# Create a conda or virtual environment for your project before you install the requirements
    pip install -r requirements.txt


##  Run pipelines with make commands

    make aq-backfill
    make aq-features
    make aq-train
    make aq-inference
    make aq-clean

or 
    make aq-all



## Feldera


mkdir -p /tmp/c.app.hopsworks.ai
ln -s  /tmp/c.app.hopsworks.ai ~/hopsworks
docker run -p 8080:8080 \
  -v ~/hopsworks:/tmp/c.app.hopsworks.ai \
  --tty --rm -it ghcr.io/feldera/pipeline-manager:latest


## Introduction to ML
I wrote a brief introduction to machine learning [here](./introduction_to_supervised_ml.pdf)
