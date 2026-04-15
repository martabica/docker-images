FROM satijalab/seurat:5.4.0

ENV DEBIAN_FRONTEND=noninteractive

# Install system deps
RUN apt-get update && apt-get install -y \
    libhdf5-dev \
    libhdf5-103-1 \
    libhdf5-hl-100 \
    && rm -rf /var/lib/apt/lists/*

# Fix hdf5r
RUN R -e "install.packages('hdf5r', repos='https://cloud.r-project.org')"

# Install Bioconductor + SingleR ONLY (no celldex needed anymore)
RUN R -e "install.packages('BiocManager', repos='https://cloud.r-project.org')" && \
    R -e "BiocManager::install('SingleR', ask=FALSE, update=FALSE)"

# Copy pre-downloaded reference into image
COPY hpca_part1.rds /opt/reference/hpca_part1.rds
COPY hpca_part2.rds /opt/reference/hpca_part2.rds
