# Crea el artefacto .war usando mvn install a través de la imágen JDK
FROM openjdk:11 AS BUILD_IMAGE
RUN apt update && apt install maven -y
# Para comodidad se clona el codigo ya que deberia traerse el artefacto desde Nexus
RUN git clone https://github.com/devopshydclub/vprofile-project.git
RUN cd vprofile-project && git checkout docker && mvn install

# Copia el artefacto .war y lo ejecuta en la imagen del servidor web Tomcat
FROM tomcat:9-jre11

RUN rm -rf /usr/local/tomcat/webapps/*

COPY --from=BUILD_IMAGE vprofile-project/target/vprofile-v2.war /usr/local/tomcat/webapps/ROOT.war

EXPOSE 8080
CMD ["catalina.sh", "run"]
