FROM ubuntu:16.04
# Locale Settings
RUN apt-get clean && apt-get update && apt-get install locales && locale-gen en_US.UTF-8

# required packages for erlang development
RUN apt-get update && apt-get install -y autoconf gcc g++ build-essential make ncurses-dev curl software-properties-common
RUN apt-get install -y --no-install-recommends apt-transport-https

# Install Microsoft ODBC driver and tools
RUN curl https://packages.microsoft.com/keys/microsoft.asc | apt-key add - \
&& curl https://packages.microsoft.com/config/ubuntu/16.04/prod.list > /etc/apt/sources.list.d/mssql-release.list \
&& apt-get update && ACCEPT_EULA=Y apt-get install -y msodbcsql && ACCEPT_EULA=Y apt-get install -y mssql-tools
ENV PATH="$PATH:/opt/mssql-tools/bin"
RUN apt-get install -y unixodbc-dev

# Install Java.
RUN echo oracle-java8-installer shared/accepted-oracle-license-v1-1 select true | debconf-set-selections
RUN add-apt-repository -y ppa:webupd8team/java
RUN apt-get update
RUN apt-get install -y oracle-java8-installer
RUN rm -rf /var/lib/apt/lists/*
RUN rm -rf /var/cache/oracle-jdk8-installer

# Define commonly used JAVA_HOME variable
ENV JAVA_HOME /usr/lib/jvm/java-8-oracle

CMD ["bash"]
