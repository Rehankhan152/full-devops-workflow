FROM ubuntu:22.04

ENV DEBIAN_FRONTEND=noninteractive

RUN apt-get update && \
    apt-get install -y openjdk-17-jdk git curl gnupg2 docker.io ansible sshpass && \
    curl -fsSL https://pkg.jenkins.io/debian-stable/jenkins.io.key | tee \
        /usr/share/keyrings/jenkins-keyring.asc > /dev/null && \
    echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] \
        https://pkg.jenkins.io/debian-stable binary/ | tee \
        /etc/apt/sources.list.d/jenkins.list > /dev/null && \
    apt-get update && apt-get install -y jenkins && \
    usermod -aG docker jenkins

EXPOSE 8080
CMD ["java", "-jar", "/usr/share/jenkins/jenkins.war"]