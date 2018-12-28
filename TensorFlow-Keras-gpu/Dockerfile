FROM tensorflow/tensorflow:1.12.0-gpu-py3

ARG http_proxy
ARG https_proxy
ARG no_proxy
ARG socks_proxy

ENV TERM=xterm \
    http_proxy=${http_proxy}   \
    https_proxy=${https_proxy} \
    no_proxy=${no_proxy} \
    socks_proxy=${socks_proxy}

RUN pip install  --upgrade pip
RUN pip3 install --user \
    Cython \
    matplotlib \
    Keras

WORKDIR  /home
CMD ["jupyter", "notebook", "--allow-root", "--notebook-dir=/home/", "--ip=0.0.0.0", "--port=8888", "--no-browser"]
