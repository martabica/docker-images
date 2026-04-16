FROM satijalab/seurat:5.4.0

ENV DEBIAN_FRONTEND=noninteractive

# Install system dependencies
RUN apt-get update && apt-get install -y \
    libhdf5-dev \
    libhdf5-103-1 \
    libhdf5-hl-100 \
    && rm -rf /var/lib/apt/lists/*

# Fix hdf5r linkage
RUN R -e "install.packages('hdf5r', repos='https://cloud.r-project.org')"

# Install Bioconductor + SingleR ONLY
RUN R -e "install.packages('BiocManager', repos='https://cloud.r-project.org')" && \
    R -e "BiocManager::install('SingleR', ask=FALSE, update=FALSE)"
