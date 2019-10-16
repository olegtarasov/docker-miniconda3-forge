![](https://github.com/olegtarasov/docker-miniconda3-forge/workflows/Docker%20Image%20CI/badge.svg)
![](https://img.shields.io/microbadger/layers/olegtarasov/miniconda3-forge)
![](https://img.shields.io/microbadger/image-size/olegtarasov/miniconda3-forge)

# Miniconda 3

This is a Docker image based on `debian:buster-slim` with updated Miniconda 3 and `conda-forge` channel activated in `strict` mode.

`tini` is defined as an entrypoint.

This image is designed to be used in production, so I try to keep its size minimal.

## Example usage

Here is an example Dockerfile based on this image:

```Dockerfile
FROM olegtarasov/miniconda3-forge

WORKDIR /usr/app

COPY environment.yml .

RUN conda env create -n test -f environment.yml && \
    conda clean --all -y

COPY . .

CMD ["/bin/bash", "-l", "-c", "conda activate test && python test.py"]
``` 

This dockerfile assumes that you have an exported environment definition in `environment.yml` and your script in `test.py`. This template creates a new environment based on your specification and cleans after itself. On startup it activates the environment and runs your script.