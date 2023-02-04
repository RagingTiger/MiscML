# MiscML
Repository of `Jupyter Notebooks` for exploring miscellaneous *tips*, *tricks*,
*examples*, and *experiments* related to machine learning.

## Docker
Below we discuss how to run the `Jupyter Notebooks` using **Docker**:

### Development
To run the notebooks locally, and persist changes made to the notebooks, first
`git clone` the repo:
```
git clone https://github.com/RagingTiger/MiscML.git
```
Then `cd MiscML` and run the following:
```
docker run -d \
           --rm \
           --name misc_ml \
           -e JUPYTER_ENABLE_LAB=yes \
           -p 8888 \
           -v $PWD:/home/jovyan \
           jupyter/scipy-notebook:lab-3.5.0 && \
sleep 5 && \
  docker logs misc_ml 2>&1 | grep "http://127.0.0.1" | tail -n 1 | \
    awk '{print $2}' | sed "s/:8888/:$(docker port misc_ml | \
    grep ':::' | awk '{print $3'} | sed 's/::://g')/g"
```
Click the link (should look similar to:
http://127.0.0.1:RANDOM_PORT/lab?token=LONG_ALPHANUMERIC_STRING) which will
`automatically` log you in and allow you to start running the *notebooks*.
