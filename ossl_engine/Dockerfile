FROM rocker/shiny:4.1.1
# Install system requirements for index.R as needed
RUN apt-get update && apt-get install -y \
    --no-install-recommends \
    git-core \
    libssl-dev \
    libcurl4-gnutls-dev \
    curl \
    libsodium-dev \
    libxml2-dev \
    libicu-dev \
    libudunits2-dev libgdal-dev libgeos-dev libproj-dev \
    libnode-dev libjq-dev \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*
ENV _R_SHLIB_STRIP_=true
RUN install2.r --error --skipinstalled \
    mongolite \
    jsonify \
    shiny \
    shinydashboard \
    leaflet \
    tidyverse \
    sf \
    RColorBrewer \
    data.table \
    plotly
RUN install2.r --error --skipinstalled \
    remotes \
    devtools \
    systemfonts \
    triebeard
RUN install2.r --error --skipinstalled \
    DT \
    shinythemes \
    shinyjqui \
    shinyWidgets \
    shinyjs \
    shinycssloaders \
    jsonlite \
    geojsonio \
    ggplot2 \
    kableExtra \
    shinyBS \
    s2 \
    magrittr
RUN install2.r --error --skipinstalled \
    leaflet.extras \
    leafgl \
    shinybusy
# Have to install an archived package https://www.listendata.com/2015/05/r-install-archived-package.html
RUN R -e 'install.packages("https://cran.r-project.org/src/contrib/Archive/rgdal/rgdal_1.6-7.tar.gz", type="source", repos=NULL)'
RUN R -e 'install.packages("https://cran.r-project.org/src/contrib/Archive/plotKML/plotKML_0.8-3.tar.gz", type="source", repos=NULL)'
RUN R -e "require(devtools); install_version('plotKML', version = '0.8-3', repos = 'http://cran.us.r-project.org')"
RUN install2.r --error --skipinstalled \
    yaml \
    pls \
    randomForest \
    tidyr \
    auth0 \
    readxl \
    xgboost \
    Cubist \
    terra \
    sp \
    httr \
    prospectr \
    fastDummies \
    cowplot \
    matrixStats \
    mlr \
    parallelMap \
    rworldmap
RUN R -e 'install.packages(c("openair", "yardstick"))'

ENV AUTH0_USER=makalii-metrics.us
ENV AUTH0_KEY=rSZpW65tm15AiW2a0IqCRKQa4gsjUmEQ
ENV AUTH0_SECRET=??? # GET FROM AUTH0

COPY ./app/ /srv/shiny-server/
# RUN chmod 757 -R /srv/shiny-server/data/
USER shiny
EXPOSE 3838

# run app on container start
CMD ["R", "-e", "source('/srv/shiny-server/app.R')"]
# CMD ["/usr/bin/shiny-server"]
# CMD ["tail","-f","/dev/null"]
