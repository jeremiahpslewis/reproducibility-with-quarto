
FROM jupyter/datascience-notebook:notebook-6.4.10

USER root

# ** [Optional] Uncomment this section to install additional packages. **
RUN apt-get update && export DEBIAN_FRONTEND=noninteractive \
    && wget https://github.com/quarto-dev/quarto-cli/releases/download/v0.9.301/quarto-0.9.301-linux-amd64.deb \
    && dpkg -i quarto-0.9.301-linux-amd64.deb \
    && rm quarto-0.9.301-linux-amd64.deb

COPY Project.toml Manifest.toml requirements.txt ./ 

RUN pip install --quiet --no-cache-dir -r requirements.txt && \
    fix-permissions "${CONDA_DIR}" && \
    fix-permissions "/home/${NB_USER}"

RUN julia -e 'using Pkg; Pkg.activate("."); Pkg.instantiate();'

USER ${NB_UID}
