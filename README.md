# fission-python-3.11-torch-cpu

Instructions and Dockerfiles on how to build a custom environment with pytorch (cpu only) included on Fission, originally meant to use in UniMelb Cluster and Cloud Computing (COMP90024)

## Why?

1. Because we need to use `sentence_transformers` in our project.
2. Default Fission Python Environment is built upon alpine, where `pytorch` doesn't support musl.
3. The kube template in MRC doesn't allow us to create a large fission package as it will run out it's ephemeral storage limit.

## How to?

> [!NOTE]
> Change the image tag if you want.

### Make sure of the following

1. Make sure you have Docker installed and running
2. Make sure you have totally read and understand [Official Fission Python Environment](https://github.com/fission/environments/tree/master/python)

### Build the builder

```bash
cd builder && docker build -t anzupop/fission-python-builder-3.11-bookworm-slim .
```

### Build the environment

> [!NOTE]  
> You should check the `requirements*.txt` and `Dockerfile*` to see what is included in this environment and MAKE CHANGES if needed. i.e. if you doesn't need `sentence_transformers` and `elasticsearch`, you can remove it from `requirements_sentence_transformer.txt` and `Dockerfile_sentence_transformer`.

```bash
cd environment && docker build -t anzupop/fission-python-env-3.11-bookworm-slim . && docker build -t anzupop/fission-python-env-3.11-bookworm-slim:sentence_transformers -f Dockerfile_sentence_transformer .
```

## Todos

1. environment: Make Dockerfile_sentence_transformer reuse image produced by Dockerfile