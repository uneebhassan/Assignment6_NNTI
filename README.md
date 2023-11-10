# Getting Started

More information on using the cluster can be found at [the SIC wiki](https://wiki.cs.uni-saarland.de/en/HPC/faq) and [in this tutorial])(https://kingsx.cs.uni-saarland.de/index.php/s/ssmj33dxmgGsAYd)

## Connecting to the cluster

### Standard SSH Connection
To initiate a connection with the cluster, execute the following SSH command, substituting `<username>` with your specific username:

```bash
ssh <username>@conduit.cs.uni-saarland.de
```

Upon execution, enter your assigned password when prompted to complete the login process.

### Utilizing SSH Keys for easier access

#### Step 1: Generating an SSH Key
To avoid entering your password on each login, consider setting up SSH keys. Start by generating a new SSH key. Note these commands should be run on your local machine not the cluster.
```bash
ssh-keygen -t rsa -b 4096 -f .ssh/sic_cluster
```

#### Step 2: Transferring the Public Key to the Cluster
Next, transfer the newly created public key to the cluster to enable key-based authentication:

```bash
ssh-copy-id -i ~/.ssh/sic_cluster.pub <username>@conduit.cs.uni-saarland.de
```

Post completion, you should be able to log in using `ssh <username>@conduit.cs.uni-saarland.de` without entering the password each time.

#### Simplifying the SSH Command
To further simplify the SSH connection process, you can add an entry to your `~/.ssh/config` file:

```bash
Host sic_cluster
    HostName conduit.cs.uni-saarland.de
    User <username>
```
Replace `<username>` with your specific username (`neuronet_teamxyz`). With this configuration, you can connect to the cluster by simply executing `ssh sic_cluster`.

## Installation of Miniconda

### Step 1: Install Miniconda
To initiate the setup, begin by installing Miniconda. Execute the following command:

```bash
condor_submit setup.sub
```

This command installs Miniconda in the directory `~/miniconda3` and includes all the packages listed in `environment.yml`. Should you require additional packages, you can easily incorporate them by adding them to the `environment.yml` file and re-executing the setup job.

### Step 2: Configuring the System Path
To integrate `conda` into your system path, append the following line to your `~/.bashrc` file:

```bash
export PATH=$HOME/miniconda3/bin:$PATH
```

Afterwards, activate the changes by sourcing the `~/.bashrc` file:

```bash
source ~/.bashrc
```

### Step 3: Submitting Scripts to the Cluster
With Miniconda configured, you can now submit scripts to the cluster. For instance, to submit the `torch_matmul_docker.py` script, use the following command:

```bash
condor_submit run.sub
```

This process triggers `conda_run.sh`, which in turn selects the Conda environment as specified in the `environment.yml` file, and subsequently executes the script defined in `run.sh`. To modify the Python script being executed, simply edit the last line in the `run.sh` file.

## Monitoring Job Execution and Logs

### Accessing Job Logs
Upon the successful execution of a job, its log files are stored within the `logs/` directory. To review the output of a specific job, utilize the following command, replacing `<job_id>` with the actual ID of the job:

```bash
less logs/run.<job_id>.0.out
```

### Real-time Monitoring of Ongoing Processes
For real-time monitoring of a process that is currently in execution, the following command can be used, again substituting `<job_id>` with the correct job ID:

```bash
tail -f logs/run.<job_id>.0.out
```
