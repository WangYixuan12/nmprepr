# Learning Obstacle Representations for Neural Motion Planning

Robin Strudel, Ricardo Garcia, Justin Carpentier, Jean-Paul Laumond, Ivan Laptev, Cordelia Schmid\
CoRL 2020

![](images/overview.png)

- [Project Page](https://www.di.ens.fr/willow/research/nmp_repr/)
- [Paper](https://arxiv.org/abs/2008.11174)



### Table of Content

- [Setup](#setup)
- [Training](#training)
- [Run](#run)
- [Logging](#logging)
- [Cite](#cite)


## Setup

Download the code
```
git clone https://github.com/rstrudel/nmprepr
cd nmprepr
```

To create a new conda environment containing dependencies
```
conda env create -f environment.yml
conda activate nmprepr
```

To update a conda environment with dependencies
```
conda env update -f environment.yml
```

## Train

### Maze

To train a planning policy on maze environments generated by 3x3 grid
```
python -m nmp.train Maze-Simple-v0 maze_baseline --horizon 75 --seed 0
```

For 5x5 grids use `Maze-Medium-v0` and for 7x7 grid use `Maze-Hard-v0`.
<div id="banner">
    <div class="inline-block">
        <img src="images/easy.png" width="100">
    </div>
    <div class="inline-block">
        <img src="images/medium.png" width="100">
    </div>
    <div class="inline-block">
        <img src="images/hard.png" width="100">
    </div>
</div>

### Monitor

You can monitor experiments with
```
tensorboard --logdir=/path/to/experiment
```

## Run

Run a planning policy and visualize it with
```
python -m nmp.run Maze-Simple-v0 --exp-name log_dir/params.pkl --seed 100 --horizon 75
```
       
Evaluate the success rate of a policy on 100 episodes
```
python -m nmp.run Maze-Simple-v0 --exp-name log_dir/params.pkl --seed 100 --horizon 75 --episodes 100
```

## Observation

The maze are represented by a set of edges $(x_1, y_1, x_2, y_2)$ which are passed through PointNet.
The edge set and goals are centered with respect to the agent current position. You can see below on the left an example of an environment and on the right its representation:

<img src="images/maze_repr.png" width="600">

## Logging

By default the checkpointing will be in your home directory. You can change it by defining a `CHECKPOINT` environment variable. Add the following to your `.bashrc` file to change the logging directory.
```
export CHECKPOINT=/path/to/checkpoints
```

## Cite

Please cite our work if you use our code or compare to our approach
```
@inproceedings{strudelnmp2020,
title={Learning Obstacle Representations for Neural Motion Planning},
author={R. {Strudel} and R. {Garcia} and J. {Carpentier} and J.P. {Laumond} and I. {Laptev} and C. {Schmid}},
journal={Proceedings of Conference on Robot Learning (CoRL)},
year={2020}
}
```
