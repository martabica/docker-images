FROM satijalab/seurat:5.4.0

# Install HDF5 system libraries
RUN apt-get update && apt-get install -y \
    libhdf5-dev \
    libhdf5-103-1 \
    libhdf5-hl-100 \
    && rm -rf /var/lib/apt/lists/*

# Reinstall hdf5r so it links correctly
RUN R -e "install.packages('hdf5r', repos='https://cloud.r-project.org')"
