FROM satijalab/seurat:5.4.0

ENV DEBIAN_FRONTEND=noninteractive

# Stable cache location
ENV XDG_CACHE_HOME=/cache

# Create FULL gypsum directory tree + open permissions
RUN mkdir -p /cache/gypsum/status/celldex/hpca && \
    mkdir -p /cache/gypsum/files && \
    chmod -R 777 /cache

# Install system deps
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

# Force-create deeper lock path at build time (this is the missing fix)
RUN R -e "dir.create('/cache/gypsum/status/celldex/hpca/2024-02-26', recursive=TRUE, showWarnings=FALSE)"
