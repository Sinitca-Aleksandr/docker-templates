FROM tensorflow/tensorflow:1.12.0-gpu-py3
RUN apt-get update && yes | apt-get upgrade
RUN apt-get install -y \
    git \
    python-pip \
    protobuf-compiler \
    python-pil \
    python-lxml \
    python-tk \
    libsm6 \
 && rm -rf /var/lib/apt/lists/*

RUN pip install --proxy http://10.128.0.100:8080 --upgrade pip
RUN pip install --proxy http://10.128.0.100:8080 --user \
    Cython \
    contextlib2 \
    jupyter \
    matplotlib \
    pillow \
    lxml
RUN pip3 install --proxy http://10.128.0.100:8080 --user \
    Cython \
    contextlib2 \
    jupyter \
    matplotlib \
    pillow \
    lxml \
    Keras

RUN git config --global http.proxy http://10.128.0.100:8080

# Install models/recearch
WORKDIR  /usr/local/lib/python3.5/dist-packages/tensorflow/
RUN git clone https://github.com/Sinitca-Aleksandr/models.git

RUN ln -sf python3 /usr/bin/python
# Install cocoapi
WORKDIR  /home
RUN git clone https://github.com/cocodataset/cocoapi.git
WORKDIR  /home/cocoapi/PythonAPI
RUN make
RUN cp -r pycocotools /usr/local/lib/python3.5/dist-packages/tensorflow/models/research/
WORKDIR  /usr/local/lib/python3.5/dist-packages/tensorflow/models/research/

RUN apt-get install -y wget

RUN echo "https_proxy = http://10.128.0.100:8080/" >> /etc/wgetrc
RUN echo "http_proxy = http://10.128.0.100:8080/" >> /etc/wgetrc
RUN echo "ftp_proxy = http://10.128.0.100:8080/" >> /etc/wgetrc
RUN echo "use_proxy = on" >> /etc/wgetrc

RUN wget -O protobuf.zip https://github.com/google/protobuf/releases/download/v3.0.0/protoc-3.0.0-linux-x86_64.zip
RUN unzip protobuf.zip
RUN ./bin/protoc object_detection/protos/*.proto --python_out=.

ENV PYTHONPATH "/usr/local/lib/python3.5/dist-packages/tensorflow/models/research:/usr/local/lib/python3.5/dist-packages/tensorflow/models/research/slim"
WORKDIR  /home
RUN rm -r cocoapi

CMD ["jupyter", "notebook", "--allow-root", "--notebook-dir=/tensorflow/models/research/object_detection", "--ip=0.0.0.0", "--port=8888", "--no-browser"]
