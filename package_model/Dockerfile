FROM serving_universal:latest

WORKDIR /tmp/resnet
COPY . /resnet

ENTRYPOINT ["tensorflow_model_server"]

CMD ["--port=8500","--rest_api_port=80", "--model_name=resnet", "--model_base_path=/resnet"]