FROM tensorflow/tensorflow:1.12.0-gpu-py3
RUN pip install --proxy http://10.128.0.100:8080 --upgrade pip
RUN pip3 install --proxy http://10.128.0.100:8080 --user \
    Cython \
    matplotlib \
    Keras

WORKDIR  /home
CMD ["jupyter", "notebook", "--allow-root", "--notebook-dir=/home/", "--ip=0.0.0.0", "--port=8888", "--no-browser"]
