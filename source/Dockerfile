FROM jenkins/jenkins:lts

LABEL Author='Maciej Rachuna'
LABEL Application='Jenkins Master'
LABEL Version='${jenkins_include_version}'
LABEL JenkinsJob='${jenkins_include_jenkinsJob}'

# install plugins
COPY source/plugins/plugins.txt /usr/share/jenkins/ref/plugins.txt
RUN /usr/local/bin/install-plugins.sh < /usr/share/jenkins/ref/plugins.txt

# Add user
USER root
RUN echo "jenkins:x:$(id -g):" >> /etc/groups
RUN echo "jenkins:x:30001:$(id -g):Jenkins:$JENKINS_HOME:/bin/false" >> /etc/passwd
USER 30001

# update the username and password
ENV JENKINS_USER='${jenkins_include_admin_username}'
ENV JENKINS_PASS='${jenkins_include_admin_password}'

# allows to skip Jenkins setup wizard
ENV JAVA_OPTS -Djenkins.install.runSetupWizard=false

# Jenkins runs all grovy files from init.groovy.d dir
# use this for creating default admin user
COPY source/scripts/default-user.groovy /usr/share/jenkins/ref/init.groovy.d/
