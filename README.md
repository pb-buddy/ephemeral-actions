# Ephemeral Self Hosted Github Actions on Raspberry Pi 4

This is a quick prototype of self hosting a Github runner, and registering dynamically at run time using the Github API.

Based on [here](https://testdriven.io/blog/github-actions-docker/).

## Steps:

1. Ensure you have an Organization on Github.
2. Create a Personal Access Token with repo, workflow, admin:org privileges. 
3. Clone the repo, add your Personal Access Token to a .env file with form ACCESS_TOKEN=YOUR_TOKEN_HERE
4. Build the Docker image locally:

```console
$ docker build --tag runner-image .
```

4. Add your ACCESS_TOKEN to the environment with:

```console
$ export $(cat .env | xargs)
```

5. Run the actions-runner within the container with:

```console
$ docker run \
  --detach \
  --env ORGANIZATION=YOUR_ORG_NAME \
  --env ACCESS_TOKEN=$ACCESS_TOKEN \
  --name runner \
  runner-image
```

6. Check it's running with:

```
$ docker logs runner -f
```