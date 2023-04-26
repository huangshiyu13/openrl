<div align="center">
    <a href="https://openrl-docs.readthedocs.io/zh/latest/index.html"><img width="450px" height="auto" src="./docs/images/openrl_text.png"></a>
</div>

---
[![PyPI](https://img.shields.io/pypi/v/openrl)](https://pypi.org/project/openrl/)
![PyPI - Python Version](https://img.shields.io/pypi/pyversions/openrl)
[![Anaconda-Server Badge](https://anaconda.org/openrl/openrl/badges/version.svg)](https://anaconda.org/openrl/openrl)
[![Anaconda-Server Badge](https://anaconda.org/openrl/openrl/badges/latest_release_date.svg)](https://anaconda.org/openrl/openrl)
[![Anaconda-Server Badge](https://anaconda.org/openrl/openrl/badges/downloads.svg)](https://anaconda.org/openrl/openrl)
[![Code style: black](https://img.shields.io/badge/code%20style-black-000000.svg)](https://github.com/psf/black)


[![Hits-of-Code](https://hitsofcode.com/github/OpenRL-Lab/openrl?branch=main)](https://hitsofcode.com/github/OpenRL-Lab/openrl/view?branch=main)
[![codecov](https://codecov.io/gh/OpenRL-Lab/openrl_release/branch/main/graph/badge.svg?token=4FMEYMR83U)](https://codecov.io/gh/OpenRL-Lab/openrl_release)

[![Documentation Status](https://readthedocs.org/projects/openrl-docs/badge/?version=latest)](https://openrl-docs.readthedocs.io/zh/latest/?badge=latest)
[![Read the Docs](https://img.shields.io/readthedocs/openrl-docs-zh?label=%E4%B8%AD%E6%96%87%E6%96%87%E6%A1%A3)](https://openrl-docs.readthedocs.io/zh/latest/)

![GitHub Org's stars](https://img.shields.io/github/stars/OpenRL)
[![GitHub stars](https://img.shields.io/github/stars/OpenRL-Lab/openrl)](https://github.com/opendilab/OpenRL/stargazers)
[![GitHub forks](https://img.shields.io/github/forks/OpenRL-Lab/openrl)](https://github.com/OpenRL-Lab/openrl/network)
![GitHub commit activity](https://img.shields.io/github/commit-activity/m/OpenRL-Lab/openrl)
[![GitHub issues](https://img.shields.io/github/issues/OpenRL-Lab/openrl)](https://github.com/OpenRL-Lab/openrl/issues)
[![GitHub pulls](https://img.shields.io/github/issues-pr/OpenRL-Lab/openrl)](https://github.com/OpenRL-Lab/openrl/pulls)
[![Contributors](https://img.shields.io/github/contributors/OpenRL-Lab/openrl)](https://github.com/OpenRL-Lab/openrl/graphs/contributors)
[![GitHub license](https://img.shields.io/github/license/OpenRL-Lab/openrl)](https://github.com/OpenRL-Lab/openrl/blob/master/LICENSE)

OpenRL-v0.0.3 is updated on April 21, 2023 

## Welcome to OpenRL

[中文介绍](./README.md) | [Documentation](https://openrl-docs.readthedocs.io/en/latest/) | [中文文档](https://openrl-docs.readthedocs.io/zh/latest/)

OpenRL is an open-source general reinforcement learning research framework that supports training for various tasks 
such as single-agent, multi-agent, and natural language. 
Developed based on PyTorch, the goal of OpenRL is to provide a simple-to-use, flexible, efficient and sustainable platform for the reinforcement learning research community.

Currently, the features supported by OpenRL include:

- A simple-to-use universal interface that supports training for both single-agent and multi-agent

- Reinforcement learning training support for natural language tasks (such as dialogue)

- Importing models and datasets from [Hugging Face](https://huggingface.co/)

- Support for models such as LSTM, GRU, Transformer etc.

- Multiple training acceleration methods including automatic mixed precision training and data collecting wth half precision policy network

- User-defined training models, reward models, training data and environment support

- Support for [gymnasium](https://gymnasium.farama.org/) environments

- Dictionary observation space support

- Popular visualization tools such as [wandb](https://wandb.ai/),  [tensorboardX](https://tensorboardx.readthedocs.io/en/latest/index.html) are supported

- Serial or parallel environment training while ensuring consistent results in both modes

- Chinese and English documentation

- Provides unit testing and code coverage testing

- Compliant with Black Code Style guidelines and type checking

This framework has undergone multiple iterations by the [OpenRL-Lab](https://github.com/OpenRL-Lab) team which has applied it in academic research. 
It has now become a mature reinforcement learning framework.

OpenRL-Lab will continue to maintain and update OpenRL, and we welcome everyone to join our [open-source community](./docs/CONTRIBUTING_en.md) 
to contribute towards the development of reinforcement learning.

For more information about OpenRL, please refer to the [documentation](https://openrl-docs.readthedocs.io/en/latest/).

## Outline

- [Welcome to OpenRL](#welcome-to-openrl)
- [Outline](#outline)
- [Installation](#installation)
- [Quick Start](#quick-start)
- [Gallery](#gallery)
- [Projects Using OpenRL](#projects-using-openrl)
- [Feedback and Contribution](#feedback-and-contribution)
- [Maintainers](#maintainers)
- [Supporters](#supporters)
  - [&#8627; Stargazers](#-stargazers)
  - [&#8627; Forkers](#-forkers)
- [Citing OpenRL](#citing-openrl)
- [License](#license)

## Installation

Users can directly install OpenRL via pip:

```bash
pip install openrl
```

If users are using Anaconda or Miniconda, they can also install OpenRL via conda:

```bash
conda install -c openrl openrl
```

Users can also install OpenRL from source code:

```bash
git clone https://github.com/OpenRL-Lab/openrl && cd openrl
pip install -e .
```

After installation, users can check the version of OpenRL through command line:

```bash
openrl --version
```

## Quick Start

OpenRL provides a simple and easy-to-use interface for beginners in reinforcement learning. 
Below is an example of using the PPO algorithm to train the `CartPole` environment:
```python
# train_ppo.py
from openrl.envs.common import make
from openrl.modules.common import PPONet as Net
from openrl.runners.common import PPOAgent as Agent
env = make("CartPole-v1", env_num=9) # Create an environment and set the environment parallelism to 9.
net = Net(env) # Create neural network.
agent = Agent(net) # Initialize the agent.
agent.train(total_time_steps=20000) # Start training and set the total number of steps to 20,000 for the running environment.
```
Training an agent using OpenRL only requires four simple steps: 
**Create Environment** => **Initialize Model** => **Initialize Agent** => **Start Training**!

For a well-trained agent, users can also easily test the agent:
```python
# train_ppo.py
from openrl.envs.common import make
from openrl.modules.common import PPONet as Net
from openrl.runners.common import PPOAgent as Agent
agent = Agent(Net(make("CartPole-v1", env_num=9))) # Initialize trainer.
agent.train(total_time_steps=20000)
# Create an environment for test, set the parallelism of the environment to 9, and set the rendering mode to group_human.
env = make("CartPole-v1", env_num=9, render_mode="group_human")
agent.set_env(env) # The agent requires an interactive environment.
obs, info = env.reset() # Initialize the environment to obtain initial observations and environmental information.
while True:
    action, _ = agent.act(obs) # The agent predicts the next action based on environmental observations.
    # The environment takes one step according to the action, obtains the next observation, reward, whether it ends and environmental information.
    obs, r, done, info = env.step(action)
    if any(done): break
env.close() # Close test environment
```
Executing the above code on a regular laptop only takes a few seconds 
to complete the training. Below shows the visualization of the agent:

<div align="center">
  <img src="./docs/images/train_ppo_cartpole.gif"></a>
</div>


**Tips:** Users can also quickly train the `CartPole` environment by executing a command line in the terminal.
```bash
openrl --mode train --env CartPole-v1
```

For training tasks such as multi-agent and natural language processing, OpenRL also provides a similarly simple and easy-to-use interface.

For information on how to perform multi-agent training, set hyperparameters for training, load training configurations, use wandb, save GIF animations, etc., please refer to:
- [Multi-Agent Training Example](https://openrl-docs.readthedocs.io/en/latest/quick_start/multi_agent_RL.html)

For information on natural language task training, loading models/datasets on Hugging Face, customizing training models/reward models, etc., please refer to:
- [Dialogue Task Training Example](https://openrl-docs.readthedocs.io/en/latest/quick_start/train_nlp.html)

For more information about OpenRL, please refer to the [documentation](https://openrl-docs.readthedocs.io/en/latest/).

## Gallery

In order to facilitate users' familiarity with the framework, we provide more examples and demos of using OpenRL in [Gallery](./Gallery.md). 
Users are also welcome to contribute their own training examples and demos to the Gallery.

## Projects Using OpenRL

We have listed research projects that use OpenRL in the [OpenRL Project](./Project.md). 
If you are using OpenRL in your research project, you are also welcome to join this list.

## Feedback and Contribution
- If you have any questions or find bugs, you can check or ask in the [Issues](https://github.com/OpenRL-Lab/openrl/issues).
- Join the QQ group: [OpenRL Official Communication Group](./docs/images/qq.png)
<div align="center">
<a href="./docs/images/qq.png"><img width="250px" height="auto" src="./docs/images/qq.png"></a>
</div>

- Join the [slack](https://join.slack.com/t/openrlhq/shared_invite/zt-1tqwpvthd-Eeh0IxQ~DIaGqYXoW2IUQg) group to discuss OpenRL usage and development with us.
- Send an E-mail to: [huangshiyu@4paradigm.com](huangshiyu@4paradigm.com)
- Join the [GitHub Discussion](https://github.com/orgs/OpenRL-Lab/discussions).

The OpenRL framework is still under continuous development and documentation. 
We welcome you to join us in making this project better:
- How to contribute code: Read the [Contributors' Guide](./docs/CONTRIBUTING_en.md)
- [OpenRL Roadmap](https://github.com/OpenRL-Lab/openrl/issues/2)

## Maintainers

At present, OpenRL is maintained by the following maintainers:
- [Shiyu Huang](https://huangshiyu13.github.io/)([@huangshiyu13](https://github.com/huangshiyu13))
- Wenze Chen([@Chen001117](https://github.com/Chen001117))

Welcome more contributors to join our maintenance team (send an E-mail to [huangshiyu@4paradigm.com](huangshiyu@4paradigm.com) 
to apply for joining the OpenRL team).

## Supporters

### &#8627; Stargazers

[![Stargazers repo roster for @OpenRL-Lab/openrl](https://reporoster.com/stars/OpenRL-Lab/openrl)](https://github.com/OpenRL-Lab/openrl/stargazers)

### &#8627; Forkers

[![Forkers repo roster for @OpenRL-Lab/openrl](https://reporoster.com/forks/OpenRL-Lab/openrl)](https://github.com/OpenRL-Lab/openrl/network/members)

## Citing OpenRL

If our work has been helpful to you, please feel free to cite us:
```latex
@misc{openrl2023,
    title={OpenRL},
    author={OpenRL Contributors},
    publisher = {GitHub},
    howpublished = {\url{https://github.com/OpenRL-Lab/openrl}},
    year={2023},
}
```

## Star History

[![Star History Chart](https://api.star-history.com/svg?repos=OpenRL-Lab/openrl&type=Date)](https://star-history.com/#OpenRL-Lab/openrl&Date)

## License
OpenRL under the Apache 2.0 license.