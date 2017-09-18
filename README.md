GOAI (Mapd + pygdf) + additional data science GPU based packages 
==========

A docker image for [MapD](https://www.mapd.com/) and [pygdf](http://gpuopenanalytics.com/) and some usefull additional GPU based data science tools, like gpu version of [XGBoost](https://github.com/dmlc/xgboost/tree/master/plugin/updater_gpu).

The Image is based on [MapD-pygdf](https://hub.docker.com/r/aghorbani/mapd-pygdf/) image, and inherits its *run* command.

## Pull the image from Docker Repository

```
docker pull aghorbani/goai
```

## Building the image

```
docker build --rm -t aghorbani/goai .
```

## Running the image

```
nvidia-docker run -it --rm \
    -p 8888:8888 \
    -p 9092:9092 \
    aghorbani/goai [--load-data] [--jupyter-args=<arguments for jupyter>]
```

* `--load-data`: will lead to load the sample [data](https://raw.githubusercontent.com/a-ghorbani/docker-mapd-pygdf/master/scripts/churn.txt) into database.
* `--jupyter-args`: specify arguments you want to pass to `jupyter notebook`.

When all running fine, you can reach 
* *Jupyter notebook* via http://localhost:8888 and 
* *MapD Immerse* via http://localhost:9092 

## Running the image - mount host directory

Many time it is desirable to have data directories to be on the host volume.
With the following command you can mount host directories for database data and jupyter notebook.

```
nvidia-docker run -it --rm \
    -p 8888:8888 \
    -p 9092:9092 \
    -v /PATH/TO/LOCAL/NB-DIR/:/home/appuser/notebooks/mein/ \
    -v /PATH/TO/LOCAL/DATA-DIR/:/opt/mapd/data/ \
    aghorbani/goai [--load-data] [--jupyter-args=<arguments for jupyter>]
```


