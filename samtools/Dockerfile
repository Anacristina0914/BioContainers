FROM ubuntu
MAINTAINER ana_gonzalez <ana.cristina.gonzales.sanchez@ki.se>
LABEL software="samtools command line" \ 
	base_image="ubuntu:latest" \ 
	container="samtools" \
	about.summary="Samtools docker container" \ 
	software.version="1.15.1" \
	version="1"
    
RUN apt-get update && \
	apt-get install -y samtools && \
	apt-get clean && \
	apt-get purge && \
	rm -rf /var/lib/apt/lists/* /tmp/*
