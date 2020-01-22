### Getting Started 

sudo nvidia-docker run -it --rm -v /tmp/projects/tensor:/projects/tensor nvcr.io/nvidia/tensorflow:18.03-py3


nvidia-docker run -it --rm -v /srv/docker-vault/tensor:/docker-vault/tensor nvcr.io/nvidia/tensorflow:18.04-py3


```
$ python
>>> import tensorflow as tf
>>> hello = tf.constant('Hello, TensorFlow!')
>>> sess = tf.Session()
>>> sess.run(hello)
Hello, TensorFlow!
>>> a = tf.constant(10)
>>> b = tf.constant(32)
>>> sess.run(a+b)
42
```

$ docker run -d \
--name TensorFlow \
--mount source=tensorflow,target=/app \
nvcr.io/nvidia/tensorflow:18.04-py3 --> run tensorflow and create a volume 