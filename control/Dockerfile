FROM ubuntu:latest

# Install prerequisites
RUN apt-get update && apt-get install -y \
    python3 python3-pip python3-venv sshpass openssh-client \
    vim nano net-tools iputils-ping curl telnet

# Create a virtual environment and install Ansible
RUN python3 -m venv /opt/ansible-venv \
    && /opt/ansible-venv/bin/pip install --upgrade pip \
    && /opt/ansible-venv/bin/pip install ansible

# Set PATH to include the virtual environment
ENV PATH="/opt/ansible-venv/bin:$PATH"

# Set permissions for /control directory
RUN mkdir -p /control && chmod 755 /control

# Enable logging for troubleshooting (logs mapped to external directory)
RUN mkdir -p /var/log/ansible && chmod 777 /var/log/ansible
ENV ANSIBLE_LOG_PATH=/var/log/ansible/ansible.log

# Set the working directory
WORKDIR /control

# Copy configuration and playbook files
COPY ansible.cfg inventory playbook.yml ./


# Add target hosts to known_hosts and test connectivity
RUN mkdir /root/.ssh
# RUN ssh-keyscan -H 192.168.1.11 >> /root/.ssh/known_hosts
# RUN ssh-keyscan -H 192.168.1.12 >> /root/.ssh/known_hosts
# RUN ansible -i /control/inventory all -m ping 
# RUN ansible-playbook -i /control/inventory playbook.yml

# Command to keep the container running
CMD ["tail", "-f", "/dev/null"]
