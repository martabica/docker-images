FROM satijalab/seurat:5.4.0

# Avoid interactive prompts
ENV DEBIAN_FRONTEND=noninteractive

# Fix cache location (critical for celldex)
ENV XDG_CACHE_HOME=/tmp/.cache

# Create full cache structure
RUN mkdir -p /tmp/.cache/gypsum/status/celldex/hpca && \
    mkdir -p /tmp/.cache/gypsum/files && \
    chmod -R 777 /tmp/.cache

# Install system dependencies (HDF5)
RUN apt-get update && apt-get install -y \
    libhdf5-dev \
    libhdf5-103-1 \
    libhdf5-hl-100 \
    && rm -rf /var/lib/apt/lists/*

# Install R packages
RUN R -e "install.packages(c('hdf5r','clustree','BiocManager'), repos='https://cloud.r-project.org')"

# Install Bioconductor packages
RUN R -e "BiocManager::install(c('SingleR','celldex'), ask=FALSE, update=FALSE)"

# Pre-download celldex reference to avoid runtime issues
RUN R -e "dir.create('/tmp/.cache/gypsum/status/celldex/hpca', recursive=TRUE, showWarnings=FALSE); \
          library(celldex); \
          ref <- celldex::HumanPrimaryCellAtlasData(); \
          print('celldex reference cached successfully')"
