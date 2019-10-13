# Miniconda 3

This is a Docker image based on `debian:buster-slim` with updated Miniconda 3 and `conda-forge` channel activated in `strict` mode.

`tini` is defined as an entrypoint.

This image is designed to be used in production, so I try to keep its size minimal.

## Example usage

Here is an example Dockerfile based on this image:

```Dockerfile
FROM olegtarasov/miniconda3

WORKDIR /usr/app

COPY . .

RUN conda env create -n my_env -f environment.yml && \
    conda clean --all -y

CMD ["/bin/bash", "-c", "eval \"$(conda shell.bash hook)\" && conda activate my_env && python my_script.py"]
``` 

This dockerfile assumes that you have an exported environment definition in `environment.yml` and your script in `my_script.py`. This template creates a new environment based on your specification and cleans after itself. On startup it uses a trick with `eval "$(conda shell.bash hook)"` to activate the environment and run your script.