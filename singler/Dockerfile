FROM satijalab/seurat:5.4.0

ENV DEBIAN_FRONTEND=noninteractive

# Use a proper cache location
ENV XDG_CACHE_HOME=/cache

# Create cache dir with open permissions
RUN mkdir -p /cache && chmod -R 777 /cache

# Install HDF5 system libraries
RUN apt-get update && apt-get install -y \
    libhdf5-dev \
    libhdf5-103-1 \
    libhdf5-hl-100 \
    && rm -rf /var/lib/apt/lists/*

# Fix hdf5r
RUN R -e "install.packages('hdf5r', repos='https://cloud.r-project.org')"

# Install Bioconductor + packages
RUN R -e "install.packages('BiocManager', repos='https://cloud.r-project.org')" && \
    R -e "BiocManager::install(c('SingleR','celldex'), ask=FALSE, update=FALSE)"

# Pre-create cache structure safely
RUN R -e "dir.create('/cache/gypsum', recursive=TRUE, showWarnings=FALSE)"
