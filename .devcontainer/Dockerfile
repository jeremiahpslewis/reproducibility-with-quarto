
FROM jupyter/datascience-notebook:notebook-6.4.10

USER root

RUN apt-get update && export DEBIAN_FRONTEND=noninteractive \
    && wget -O quarto.deb https://github.com/quarto-dev/quarto-cli/releases/download/v0.9.358/quarto-0.9.358-linux-amd64.deb \
    && dpkg -i quarto.deb \
    && rm quarto.deb \
    && apt-get install -y lmodern \
    && apt-get install -y rsync

COPY Project.toml Manifest.toml requirements.txt ./ 
COPY startup_ijulia.jl .julia/config/

RUN pip install --quiet --no-cache-dir -r requirements.txt && \
    fix-permissions "${CONDA_DIR}" && \
    fix-permissions "/home/${NB_USER}"

RUN julia -e 'using Pkg; Pkg.activate("."); Pkg.instantiate();'

CMD quarto render quarto-actions
