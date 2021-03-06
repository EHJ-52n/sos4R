################################################################################
# Copyright (C) 2019 by 52 North                                               #
# Initiative for Geospatial Open Source Software GmbH                          #
#                                                                              #
# Contact: Andreas Wytzisk                                                     #
# 52 North Initiative for Geospatial Open Source Software GmbH                 #
# Martin-Luther-King-Weg 24                                                    #
# 48155 Muenster, Germany                                                      #
# info@52north.org                                                             #
#                                                                              #
# This program is free software; you can redistribute and/or modify it under   #
# the terms of the GNU General Public License version 2 as published by the    #
# Free Software Foundation.                                                    #
#                                                                              #
# This program is distributed WITHOUT ANY WARRANTY; even without the implied   #
# WARRANTY OF MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE. See the GNU #
# General Public License for more details.                                     #
#                                                                              #
# You should have received a copy of the GNU General Public License along with #
# this program (see gpl-2.0.txt). If not, write to the Free Software           #
# Foundation, Inc., 59 Temple Place - Suite 330, Boston, MA 02111-1307, USA or #
# visit the Free Software Foundation web page, http://www.fsf.org.             #
#                                                                              #
# Author: Jürrens, Eike Hinderk (e.h.juerrens@52north.org)                     #
# Created: 2019-02-27                                                          #
# Project: sos4R - visit the project web page,                                 #
#      http://52north.org/communities/sensorweb/clients/sos4R/                 #
################################################################################
#                                                                              #
# Build image  : docker pull rocker/geospatial:latest && \                     #
#                docker build -t sos4r-rstudio-dev:$(date +%Y-%m-%d) .         #
#                                                                              #
# Run container: docker run --name=sos4r-dev --env PASSWORD=sos \              #
#                --publish 8787:8787 \                                         #
#                --volume $(pwd):/home/rstudio/sos4R \                         #
#                -d sos4r-rstudio-dev:$(date +%Y-%m-%d)                        #
#                                                                              #
# Start rstudio: chromium-browser --app=http://localhost:8787/                 #
#                                                                              #
# Clean-Up     : docker stop sos4r-dev; \                                      #
#                docker rm sos4r-dev; \                                        #
#                docker images | grep sos4r-rstudio-dev | awk '{print $3}' \   #
#                | xargs docker rmi                                            #
#                                                                              #
################################################################################
FROM rocker/geospatial:latest
MAINTAINER "Jürrens, Eike Hinderk" e.h.juerrens@52north.org

RUN install2.r --error --skipinstalled \
        dplyr \
        parsedate \
        uuid \
        httr \
        methods \
        sp \
        stringr \
        xml2 \
        devtools \
        kableExtra \
        skimr \
        webmockr && \
    rm -rf /tmp/downloaded_packages && \
    rm -rf /tmp/repos_*.rds && \
    rm -rf /var/lib/apt/lists/*


# Build:
# docker build --tag sos4r:dev .
# Run (in package base directory):
# docker run -it --rm --volume $(pwd):/home/rstudio/sos4R --publish 8787:8787 -e PASSWORD=sos sos4r:dev
# Run without network to ensure check works without network on CRAN (cannot use RStudio over port then!):
# docker run -it --rm --volume $(pwd):/home/rstudio/sos4R -e PASSWORD=sos --network none sos4r:dev /bin/bash
## Then:
## R CMD build --no-build-vignettes sos4R
## R CMD check --as-cran --no-manual --no-vignettes sos4R_<full tar.gz file name>
