# Use the official Python image from the Docker Hub
FROM python:3.12

# Install system dependencies
RUN apt-get update && apt-get install -y \
    git \
    && rm -rf /var/lib/apt/lists/*

# Set the working directory
WORKDIR /workspace

# Install Qiskit and other dependencies
RUN pip install qiskit qiskit-aer matplotlib numpy pylatexenc jupyter

# Set up Jupyter kernel for VS Code
RUN python -m ipykernel install --user --name=qiskit-dev --display-name "Python (Qiskit Dev)"

# Switch to a non-root user
ARG USERNAME=vscode
ARG USER_UID=1000
ARG USER_GID=$USER_UID

RUN groupadd --gid $USER_GID $USERNAME \
    && useradd --uid $USER_UID --gid $USER_GID -m $USERNAME \
    && apt-get update \
    && apt-get install -y sudo \
    && echo $USERNAME ALL=\(root\) NOPASSWD:ALL > /etc/sudoers.d/$USERNAME \
    && chmod 0440 /etc/sudoers.d/$USERNAME

USER $USERNAME