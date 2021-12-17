FROM jamesdbloom/docker-java8-maven as maven_builder
ENV JAVA_HOME=/usr/lib/jvm/java-8-openjdk-amd64/jre
RUN mkdir -p /app
WORKDIR /app/
RUN git clone https://github.com/ankur-katiyar/log4j-vunerable-server.git   && javac /app/log4j-vunerable-server/Log4jpoc.java
WORKDIR /app/log4j-vunerable-server/
CMD ["sh", "-c", "python -m SimpleHTTPServer 8080"]

