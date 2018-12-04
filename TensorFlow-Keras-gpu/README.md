# TensorFlow-Keras-IRTK

Build command as

~~~sh
docker build . -t digiratory/keras-image
~~~

This is nvidia-docker image. For running use command same

~~~sh
docker run --runtime=nvidia -it -p 8888:8888 digiratory/keras-image
~~~
