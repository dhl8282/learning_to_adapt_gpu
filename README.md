# Learning to Adapt in Dynamic, Real-World Environment through Meta-Reinforcement Learning

Implementation of [Learning to Adapt in Dynamic, Real-World Environment through Meta-Reinforcement Learning](https://arxiv.org/abs/1803.11347).
The code is written in Python 3 and builds on Tensorflow. The environments require the Mujoco131 physics engine.

## Getting Started
### A. Docker-gpu
Install Docker-nvidia
1. Set repo\
curl -s -L https://nvidia.github.io/nvidia-docker/gpgkey | \
  sudo apt-key add -
distribution=$(. /etc/os-release;echo $ID$VERSION_ID)
curl -s -L https://nvidia.github.io/nvidia-docker/$distribution/nvidia-docker.list | \
  sudo tee /etc/apt/sources.list.d/nvidia-docker.list
sudo apt-get update

2. Install docker-gpu\
sudo apt-get install nvidia-docker2
sudo pkill -SIGHUP dockerd

3. Build Docker Image\
docker image build -t adapt_gpu:1.0 docker/.

4. Test gpu use\
docker run --runtime=nvidia --rm adapt_gpu:1.0 nvidia-smi

------------updated 2020.03.09

## Usage
The run scripts are located in the folder ``` run_scripts```.
In order to run experiments with GrBAL, run the following command:

```python run_scripts/run_grbal.py ```

If instead, you want to run ReBAL:

``` python run_scripts/run_rebal.py ```

We have also implement a non-adaptive model-based method that uses random shooting or cross-entropy for planning. You
can run this baseline by executing the command:

``` python run_scripts/run_mb_mpc.py ```


When running experiments, the data will be stored in ``` data/$EXPERIMENT_NAME ```. You can visualize the learning process
by using the visualization kit:

``` python viskit/frontend.py data/$EXPERIMENT_NAME ```

In order to visualize and test a learned policy run:

``` python experiment_utils/sim_policy data/$EXPERIMENT_NAME```

## Acknowledgements
This repository is partly based on [Duan et al., 2016](https://arxiv.org/abs/1611.02779).
