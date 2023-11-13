## Chapter 2 - Communication Layer

In Chapter 2 of the Kafka Building Blocks course, we explored the following components:

- Kafka / Redpanda records
- Producers
- Consumers
- Consumer Groups

We created a basic producer (see [here][basic-producer]), a producer that provides a record key and event timestamp (see [here][key-producer]), and a simple consumer that can be instantiated multiple times to create a consumer group (see [here][simple-consumer]).

[basic-producer]: /02-communication-layer/producer-examples/basic.py
[key-producer]: /02-communication-layer/producer-examples/basic.py
[simple-consumer]: /02-communication-layer/consumer-examples/consumer.py

The commands we executed are shown below:

```sh
# start the Redpanda cluster
docker-compose up -d

# set an alias for the `rpk` executable
alias rpk="docker exec -ti redpanda-1 rpk"

# inspect the cluster
rpk cluster info

# install python3.11 if doesn't have
python3 --version
sudo apt install python3.11 python3.11-venv

# update alternatives if have multiple python
which python3
sudo update-alternatives --list python3
# use whereis to find python3.11 and etc
sudo update-alternatives --install /usr/bin/python3 python3 /usr/bin/python3.11 1
# update-alternatives for other python version
sudo update-alternatives --config python3

# create and activate a Python virtual environment
python3 -m venv venv
source venv/bin/activate

# update pip
python -m pip install -U pip

# install the needed dependencies
python -m pip install -r requirements.txt

export REDPANDA_BROKERS=["localhost:9092"]

# create the purchases topic
rpk topic create purchases -p 4

# run a basic producer (see producer-examples/basic.py)
python -m producer-examples.basic

# run a producer that groups related records by key, and uses event-time semantics
python -m producer-examples.with_key_and_timestamp

# run one or more consumers
# tab 1
python -m consumer-examples.consumer.py

# tab 2
python -m consumer-examples.consumer.py

# inspect the consumer groups
rpk group list

# get detailed information about the group
rpk group describe my-group
```

Please see the course for more information.
