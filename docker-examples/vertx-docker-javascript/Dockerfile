###
# vert.x docker example using a JavaScript verticle
# To build:
#  docker build -t sample/vertx-javascript .
# To run:
#   docker run -t -i -p 8080:8080 sample/vertx-javascript
###

# Extend vert.x image                       <1>
FROM vertx/vertx3

# Set the name of the verticle to deploy    <2>
ENV VERTICLE_NAME hello-verticle.js

# Set the location of the verticles         <3>
ENV VERTICLE_HOME /usr/verticles
ENV HAWKULAR_APM_VERSION 0.9.0.Final

ADD https://github.com/hawkular/hawkular-apm/releases/download/$HAWKULAR_APM_VERSION/hawkular-apm-agent.jar hawkular-apm-agent.jar

ENV JAVA_OPTS -javaagent:/hawkular-apm-agent.jar
EXPOSE 8080

# Copy your verticle to the container       <4>
COPY $VERTICLE_NAME $VERTICLE_HOME/

# Launch the verticle                       <5>
WORKDIR $VERTICLE_HOME
ENTRYPOINT ["sh", "-c"]
CMD ["exec vertx run $VERTICLE_NAME -cp $VERTICLE_HOME/*"]
