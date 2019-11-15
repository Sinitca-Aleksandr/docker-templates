FROM tensorflow/tensorflow:latest-gpu-py3

ARG http_proxy
ARG https_proxy
ARG no_proxy
ARG socks_proxy

ENV TERM=xterm \
    http_proxy=${http_proxy}   \
    https_proxy=${https_proxy} \
    no_proxy=${no_proxy} \
    socks_proxy=${socks_proxy}

RUN apt-get update && yes | apt-get upgrade -y
RUN apt-get update && apt-get install -y \
    git \
    python-pip
RUN apt-get update && apt-get install -y \
    protobuf-compiler \
    python-pil \
    python-lxml \
    python-tk \
    libsm6 \
    && rm -rf /var/lib/apt/lists/*

RUN pip install --upgrade pip
RUN pip install --user \
    Cython \
    contextlib2 \
    matplotlib \
    pillow \
    lxml
RUN pip3 install --user \
    Cython \
    contextlib2 \
    matplotlib \
    pillow \
    lxml \
    Keras

RUN pip3 install jupyter

# Install models/recearch
WORKDIR  /home/tensorflow/
RUN git clone https://github.com/tensorflow/models.git

RUN ln -sf python3 /usr/bin/python
# Install cocoapi
WORKDIR  /home
RUN git clone https://github.com/cocodataset/cocoapi.git
WORKDIR  /home/cocoapi/PythonAPI
RUN make
RUN cp -r pycocotools /home/tensorflow/models/research/
WORKDIR  /home/tensorflow/models/research/

RUN curl https://github.com/google/protobuf/releases/download/v3.0.0/protoc-3.0.0-linux-x86_64.zip -L -o protobuf.zip
RUN unzip protobuf.zip
RUN ./bin/protoc object_detection/protos/*.proto --python_out=.

ENV PYTHONPATH "/home/tensorflow/models/research:/home/tensorflow/models/research/slim"
WORKDIR  /home
RUN rm -r cocoapi

CMD ["jupyter", "notebook", "--allow-root", "--notebook-dir=/home/", "--ip=0.0.0.0", "--port=8888", "--no-browser"]
