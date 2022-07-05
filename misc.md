k rabbitmq secrets keglingpet-rabbitmq

username: default_user_3kZQzje4AJofOszBexv
password: hZYw2GjdICQr-aK2NEYs0qIYhQicz2yM


k get secrets keglingpet-rabbitmq-default-user -o jsonpath='{.data.username}'| base64
--decode
k get secrets keglingpet-rabbitmq-default-user -o jsonpath='{.data.password}'| base64
--decode

k get rabbitmqclusters.rabbitmq.com keglingpet-rabbitmq -o json | grep -A 10 serviceReference

k delete rabbitmqcluster keglingpet-rabbitmq

k rabbitmq manage keglingpet-rabbitmq

k run perf-test --image=pivotalrabbitmq/perf-test -- --uri "amqp://default_user_3kZQzje4AJofOszBexv:hZYw2GjdICQr-aK2NEYs0qIYhQicz2yM@keglingpet-rabbitmq"

k logs -f perf-test
k delete pod perf-test
