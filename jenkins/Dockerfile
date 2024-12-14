FROM jenkins/jenkins:lts

# Ensure the commands are run as root
USER root

# 'RUN' will be executed during the image build process

# -y -> automatically answer 'yes'
RUN apt-get update && apt-get install -y \
    sudo \
    curl \
    gnupg \
    lsb-release \
    # install get-docker.sh
    && curl -fsSL https://get.docker.com -o get-docker.sh \
    # run get-docker.sh
    && sh get-docker.sh \
    # after that, remove this to keep the Docker image clean and has smaller size
    && rm get-docker.sh \
    # allow to run Docker commands without 'sudo'
    # -a -> append user to specified group without removing them from other groups they already joined
    # -G -> list of group user should be added to
    && usermod -aG docker root \
    && apt-get clean

USER jenkins