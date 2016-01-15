FROM registry:2

# Add the custom configuration file we made
ADD ./config.yml /docker-registry/config/config.yml

# Set the configuration file to config.yml
env DOCKER_REGISTRY_CONFIG /docker-registry/config/config.yml

# Make sure we use the prod configuration settings
env SETTINGS_FLAVOR s3
env SEARCH_BACKEND=sqlalchemy

RUN apt-get install -y ca-certificates librados2 apache2-utils
