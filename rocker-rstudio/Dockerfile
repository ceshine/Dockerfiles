FROM rocker/rstudio:latest

# Install system packages
RUN apt-get -o Acquire::Check-Valid-Until=false update && \
    apt-get install -y --no-install-recommends git zlib1g-dev libxml2-dev && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

RUN Rscript -e "install.packages('devtools')"
RUN Rscript -e "install.packages('packrat')"
RUN Rscript -e "install.packages('remotes')"
