# We are basing our builder image on openshift base-centos7 image
# FROM openshift/base-centos7
FROM harisekhon/centos-java

# Inform users who's the maintainer of this builder image
MAINTAINER Flavio Roncat <flavioroncat@gmail.com>

# Inform about software versions being used inside the builder
#ENV LIGHTTPD_VERSION=1.4.35

# Set labels used in OpenShift to describe the builder images
LABEL io.k8s.description="Platform for serving static HTML files" \
      io.k8s.display-name="Hello Docker Springboot" \
      io.openshift.expose-services="8080:http" \
      io.openshift.tags="builder,java,springboot"

# Install the required software, namely Lighttpd and
#RUN yum install -y epel-release && yum install -y lighttpd && yum clean all -y

# Defines the location of the S2I
# Although this is defined in openshift/base-centos7 image it's repeated here
# to make it clear why the following COPY operation is happening
LABEL io.openshift.s2i.scripts-url=image:///usr/local/s2i

# Prepare package and adding source
#WORKDIR /package
#ADD target/sample-rest-spring-boot-0.1.0.jar /package/sample-rest-spring-boot-0.1.0.jar

#EXPOSE 8080
#CMD ["java", "-jar", "/package/sample-rest-spring-boot-0.1.0.jar"]


# Copy the S2I scripts from ./.s2i/bin/ to /usr/local/s2i when making the builder image
 COPY ./s2i/bin/ /usr/local/s2i

# Copy the lighttpd configuration file
# COPY ./etc/ /opt/app-root/etc

# Drop the root user and make the content of /opt/app-root owned by user 1001
#RUN chown -R 1001:1001 /opt/app-root

# Set the default user for the image, the user itself was created in the base image
USER 1001

# Specify the ports the final image will expose
EXPOSE 8080

# Set the default CMD to print the usage of the image, if somebody does docker run
CMD ["usage"]
