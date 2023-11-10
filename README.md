# Getting started

## Install miniconda
First we need to install miniconda, to do so run 
```
condor_submit setup.sub
```
This will install miniconda in `~/miniconda3` with all packages that are included in `environment.yml`. To add other packages simply modify the environment file and submit the setup job again.
To add `conda` to the path add `export PATH=$HOME/miniconda3/bin:$PATH` to your `~/.bashrc` file and run `source ~/.bashrc`.

Once you have setup conda you can submit the `torch_matmul_docker.py` script to the cluster by running `condor_submit run.sub`. This will first execute `conda_run.sh`, selecting the correct
environment and then running the script using `run.sh`.
If you want to change the script that is run edit `run.sh`.
