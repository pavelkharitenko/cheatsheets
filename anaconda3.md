list environment:
```
conda info --envs
```

create environment:
```
conda create -n myenv python=3.8
```

create from environment.yml:
```
conda env create -f environment.yml 
```

activate environment:
```
conda activate myenv
```

deactivate environment:
```
conda deactivate myenv
```

delete environment:
```
conda env remove --name myenv
```

remove caches and unused packages:
```
conda clean
```
