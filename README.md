# Tensorflow-serving-universal
Docker build files for making tensorflow-model-server-universal and enabling REST API

As it turned out our Kubernetes cluster in test needed tensorflow-model-server-universal as it failed with tensorflow-model-server.

The [Tensorflow serving toturial for Kubernetes]("https://www.tensorflow.org/tfx/serving/serving_kubernetes")  used a prebuild Docker image, and i could not find any prebuild imaged for -universal

To build the tensorflow-model-server-universal run:

```console
$ docker build -t serving_universal -f create_universal/Dockerfile
```
The image is now created and you can copy the resnet model into the image manually

```console
$ docker run -d --name serving_base serving_universal:latest
$ docker cp /tmp/resnet serving_base:/resnet
$ docker commit --change 'CMD ["--port=8500","--rest_api_port=80", "--model_name=resnet", "--model_base_path=/resnet"]' serving_base $USER/resnet_serving
```

For continuous deploy the model copy can also be automated in a Dockerfile
```console
$ docker build -t $USER/resnet_serving -f package_model/Dockerfile.
```
The image can now be run locally, or comitted to a repository for deploy
and you can continue the toturial from [Start the server]("https://www.tensorflow.org/tfx/serving/serving_kubernetes#start_the_server")