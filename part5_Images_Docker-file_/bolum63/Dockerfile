FROM nginx:latest
LABEL maintainer="awsdevopshasan @swhsnblknc"
ENV KULLANICI="Hasan"
ARG RENK
RUN apt-get update && apt-get -y install curl htop wget
WORKDIR /gecici
ADD https://wordpress.org/latest.tar.gz .
WORKDIR /usr/share/nginx/html
COPY html/${RENK} .
HEALTHCHECK --interval=30s --timeout=30s --start-period=5s --retries=3 CMD curl -f https://localhost/ || exit 1
CMD ["./script.sh"]
