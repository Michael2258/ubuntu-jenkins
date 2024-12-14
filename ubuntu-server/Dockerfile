FROM ubuntu:latest

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
    
RUN apt-get install -y openssh-server \
    # Creates the directory for SSH daemon runtime files
    && mkdir /var/run/sshd \
    # set username as 'root' and password as 'password', 'chpasswd' will update username and password based on output (root:password)
    # '|' is a pipe, use the output of former command as an input of the latter
    # 'echo': display line of text that are passed as arguments -> it's like passing 'root:password' as usrAndPw in chpasswd(usrAndPw)
    && echo 'root:password' | chpasswd

# '>' will overwrite but '>>' won't
# both will append data to the openssh config file: /etc/ssh/sshd_config.d/custom.conf 
RUN echo 'PermitRootLogin yes' > /etc/ssh/sshd_config.d/custom.conf \
    && echo 'PasswordAuthentication yes' >> /etc/ssh/sshd_config.d/custom.conf

# 'CMD' will be executed when the container starts (docker compose up)
# using 'docker run <image> <command> will override CMD instruction'

# start ssh service
# same as sudo /usr/sbin/sshd -D (but without sudo because we used 'usermod' already)
CMD ["/usr/sbin/sshd", "-D"]
