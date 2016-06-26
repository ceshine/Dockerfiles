FROM julia:0.4.6

MAINTAINER CeShine Lee

## Set a default user. Available via runtime flag `--user docker`
## User should also have & own a home directory
RUN useradd docker \
	&& mkdir /home/docker \
	&& chown docker:docker /home/docker \
	&& addgroup docker staff

RUN apt-get update
RUN apt-get install -y build-essential wget

# Cairo
RUN apt-get install -y \
    gettext \
    libpango1.0-dev \
    libpango1.0-0 \
    libgvc6 \
    graphviz \
    libgraphviz-dev \
    && apt-get clean

# Stan
RUN mkdir stan; cd stan; wget https://github.com/stan-dev/cmdstan/releases/download/v2.10.0/cmdstan-2.10.0.tar.gz; \
    tar -xzvf cmdstan-2.10.0.tar.gz; mv cmdstan-2.10.0 /usr/share/cmdstan; \
    (cd /usr/share/cmdstan && make build -j4); \
    rm -rf /usr/share/cmdstan/stan-2.10.0

USER docker

RUN julia -e 'Pkg.add("Stan"); Pkg.add("DataFrames"); Pkg.add("IJulia"); Pkg.add("XGBoost")'
RUN julia -e 'Pkg.build("Stan"); Pkg.build("DataFrames"); Pkg.build("IJulia"); Pkg.build("XGBoost")'

ENV CMDSTAN_HOME /usr/share/cmdstan
ENV PATH $PATH:/usr/share/cmdstan/bin:/home/docker/.julia/v0.4/Conda/deps/usr/bin/
