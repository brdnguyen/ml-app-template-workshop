# ml-app-template-workshop

An ML project template for CD4ML Workshop in Melbourne, Australia.
Credit: it is based closely on the TW Singapore's team at https://github.com/ThoughtWorksInc/ml-app-template

For infrastructure-related stuff (e.g. provisioning of CI server, deployments, etc.), please refer to https://github.com/ThoughtWorksInc/ml-cd-starter-kit.

# Getting started

1. Fork repository: https://github.com/ThoughtWorksInc/ml-app-template-workshop
2. Clone repository: `git clone https://github.com/YOUR_USERNAME/ml-app-template`
3. Install Docker ([Mac](https://docs.docker.com/docker-for-mac/install/), [Linux](https://docs.docker.com/install/linux/docker-ce/ubuntu/))
4. Start Docker host (Docker Desktop) on your desktop
5. Build Docker images and start containers:

```shell
# build docker image [Mac/Linux users]
# Workshop's note: walk through content of Dockerfile before running this command.
docker-compose build

# start docker container [Mac/Linux users]
docker-compose up

```

At this point, you should see 2 running containers, which expose 2 http endpoints via ports 5000 (MLFlow) and 8080 (Flask app for making). visit:

http://localhost:5000  (this is where MLFlow is hosted)
http://localhost:8080  (This is where the main Flask app is )


<br/>
You are ready to roll! Here are some common commands that you can run in your dev workflow. Run these in the container.


```shell
# View list of running containers
docker ps


# Log into the main app container
docker exec -it <container-id> /bin/bash


# add some color to your terminal
source bin/color_my_terminal.sh
```


## Task 1: Run tests, and fix failing tests

In your container (`ml-app-template-workshop`), run:
```
nosetests
```

To fix this failing test, in your code editor, edit

`test_model_metrics.py, line 16`

Follow the instruction around the TODO comment. Once you fix the tests, run test again with `nosetests`


## Task 2: Train and version model with MLFlow

In your container, run:

```
python src/train.py
```

In your web browser (on local laptop), visit http://localhost:5000 and you shoud see MLFlow begin to capture the change.

## Task 3: Let's change the "Model"

Let's keep the training data the same, but change the model logic, and see the change versioned by MLFlow.

In `src\train.py`, look for "TODO for Task 3" change it to:
```
N_ESTIMATORS = 100
```

then, run:

```
python src/train.py
```

See the change in MLFlow UI (localhost:5000)

## Task 4: Make a change to the training data, and version that with MLFlow

Go to `src/train.py`, find "TODO for Task 4", and make the change (uncomment the code) as in the suggestion.

Run
```
    python src/train.py
```

Then check Mlflow again (localhost:5000 to see the change reflected)



# Consume the model

It is not the focus of this workshop, but we'll walk you through the bit to make live prediction (from an API), from the model we have trained.

## make requests to your app
1. In your browser, visit http://localhost:8080 to verify the end point is ready.
2. Open another terminal and run:
```
bin/predict.sh http://localhost:8080
```
