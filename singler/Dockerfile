FROM satijalab/seurat:5.4.0

# Avoid interactive prompts
ENV DEBIAN_FRONTEND=noninteractive

# Fix cache location (critical for celldex)
ENV XDG_CACHE_HOME=/tmp/.cache
RUN mkdir -p /tmp/.cache

# Install HDF5 system libraries
RUN apt-get update && apt-get install -y \
    libhdf5-dev \
    libhdf5-103-1 \
    libhdf5-hl-100 \
    && rm -rf /var/lib/apt/lists/*

# Reinstall hdf5r so it links correctly
RUN R -e "install.packages('hdf5r', repos='https://cloud.r-project.org')"

# Install Bioconductor + SingleR + celldex
RUN R -e "install.packages('BiocManager', repos='https://cloud.r-project.org')" && \
    R -e "BiocManager::install(c('SingleR','celldex'), ask=FALSE, update=FALSE)"
