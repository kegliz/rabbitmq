#install krew
https://krew.sigs.k8s.io/docs/user-guide/setup/install/
# unstall rabbitmq plagin
k krew install rabbitmq
# check it
k rabbitmq help
# install rabbitmq kubernetes cluster operator
k rabbitmq install-cluster-operator
# install rabbitmq Messaging Topology Operator
https://github.com/rabbitmq/messaging-topology-operator/#quickstart

k apply -f user.yaml
k apply -f permissions.yaml
...

k rabbitmq secrets keglingpet-rabbitmq

username: RABBITMQ_USERNAME
password: RABBITMQ_PASSWORD


k get secrets keglingpet-rabbitmq-default-user -o jsonpath='{.data.username}'| base64
--decode
k get secrets keglingpet-rabbitmq-default-user -o jsonpath='{.data.password}'| base64
--decode

k get rabbitmqclusters.rabbitmq.com keglingpet-rabbitmq -o json | grep -A 10 serviceReference

k delete rabbitmqcluster keglingpet-rabbitmq

k rabbitmq manage keglingpet-rabbitmq

k run perf-test --image=pivotalrabbitmq/perf-test -- --uri "amqp://RABBITMQ_USERNAME:RABBITMQ_PASSWORD@keglingpet-rabbitmq"

k logs -f perf-test
k delete pod perf-test
