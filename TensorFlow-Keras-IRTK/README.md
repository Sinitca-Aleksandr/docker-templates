# TensorFlow-Keras-IRTK

Build command as

~~~sh
docker build . -t digiratory/tf-keras-irtk-image
~~~

This is nvidia-docker image. For running use command same

~~~sh
docker run --runtime=nvidia -it -v /home/user/:/home/ -p 8888:8888 digiratory/tf-keras-irtk-image
~~~
