# HTCondor Tutorial

- Submit your first job
```
condor_submit torch_matmul_docker.sub
```

- check the state of your job in the condor queue
```
condor_q
```

- analyze how many machines can run your job or if there are problems
```
condor_q -analyze
condor_q -better
```

- overview of machines in cluster
```
condor_status
```

- submit an interactive job
```
condor_submit -i torch_matmul_docker_interactive.sub
```

Feel free to change the parameters in the sub files and submit the jobs again. For interactive jobs, you can acquire maximal 1 GPU + 1 CPU. If you use larger values, your job will never get a slot on the interactive machine. 



