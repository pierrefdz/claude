
## Environments

If needed, look at conda environments via `ls /home/$USER/miniconda3/envs/`

## Running code on the cluster

The login node have CPUs, so for low resource jobs you can run them directly on the login node without `srun`. But for GPU jobs you must use `srun` to get a GPU node.

To get some interactive access to a GPU node on the cluster:
```
srun --account=avseal --nodes=1 --gpus-per-node=1 --cpus-per-gpu=24 --mem-per-cpu=8G --qos=h200_avseal_high --time=10:00:00 --job-name=dev_llmwm --pty 
```
Just replace `--gpus-per-node=1` with the number of GPUs you want (up to 8). 
This will allocate a node with the specified resources and give you a shell prompt on that node.

In this case:
1. do the `srun` first and *wait* for it to be allocated. Do not run `srun ... python ...` directly.
You need to check every 30s if you have been allocated. If you haven't been allocated after 5 minutes, use qos=h200_dev instead of qos=h200_avseal_high.
2. activate the good environment with `conda env ...`.
3. run the python commands.

