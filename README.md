# py3-tf-gpu-ale

[Singularity](http://singularity.lbl.gov/) recipe that includes Python 3, TensorFlow, and the [Arcade Learning Environment](https://github.com/mgbellemare/Arcade-Learning-Environment) (ALE). You can build this recipe yourself, or pull the image from [Singularity Hub](https://www.singularity-hub.org/collections/627). The image is about 1.2 GB in size and is built on top of an official [TensorFlow](https://www.tensorflow.org/) [Docker](https://www.docker.com/) image.


## Usage

Use this container as the foundation for various ALE experiments in TensorFlow.

Ideally, you would add your setup and experiments to this recipe and build a read-only image to run reproducible experiments. However, since building the image takes a few minutes, and copying it from your local machine to a remote scientific computing system can take minutes or hours, depending on your connection. You can avoid having to upload your image from a local machine by building on [Singularity Hub](https://www.singularity-hub.org/collections/627), but you cannot build directly on a scientific computing system because image building requires root access.

Since it is slow to change the container image, I recommend using a somewhat generic base image and modifying it slightly at runtime with the [`singularity exec`](http://singularity.lbl.gov/docs-exec) command. Since [virtualenv](https://virtualenv.pypa.io/en/stable/) is installed in the container, you can install new Python libraries easily at the beginning of an exec script, like so:

```bash
virtualenv --system-site-packages venv && source venv/bin/activate
pip install <library>
```

On some systems, like [Compute Canada's Cedar](https://docs.computecanada.ca/wiki/Cedar), you may have to include `--trusted-host pypi.python.org` as an argument to `pip`. This should principally be used to install libraries that you are actively developing for your experiments.

You cannot change system packages or settings with an exec script though, unless you are running exec with root access.

If you have pulled the image, `dmorrill10-py3-tf-gpu-ale-master-latest.simg`, from [Singularity Hub](https://www.singularity-hub.org/collections/627), you can run `experiment.sh` with NVIDIA GPU support with

```bash
singularity exec --nv dmorrill10-py3-tf-gpu-ale-master-latest.simg experiment.sh
```

Of course, installing extra packages at runtime makes experiments less reproducible, so after finalizing experiment changes it could be useful to fork this image, add your own setup to the recipe, and add your experiment as the container's [runscript](http://singularity.lbl.gov/docs-run#defining-the-runscript).


## Background on [Singularity](http://singularity.lbl.gov/)

[Singularity](http://singularity.lbl.gov/) is a containerization system for scientific computing. It is similar to the popular [Docker](https://www.docker.com/), if you are familiar with that, except that they target very different use cases. In particular, Docker is difficult to use in scientific computing settings, while Singularity is designed precisely for this setting. You can watch [this talk](https://www.youtube.com/watch?v=DA87Ba2dpNM) by Singularity's creator for more information.


## License

Copyright Dustin Morrill, 2018

[MIT License](LICENSE.md).
