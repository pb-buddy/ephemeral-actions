# Ephemeral Self Hosted Github Actions on Raspberry Pi 4

This is a quick prototype of self hosting a Github runner, and registering dynamically at run time using the Github API.

Based on [here](https://testdriven.io/blog/github-actions-docker/).

## Steps:

- Ensure you have an Organization on Github.
- Install Docker on your Raspberry Pi using [the convenience script](https://docs.docker.com/engine/install/debian/#install-using-the-convenience-script).
- Create a Personal Access Token with `repo`, `workflow`, `admin:org` privileges. 
- Clone the repo, add your Personal Access Token to a .env file with form ACCESS_TOKEN=YOUR_TOKEN_HERE
- Build the Docker image locally:

```console
$ docker build --tag runner-image .
```

- Add your ACCESS_TOKEN to the environment with:

```console
$ export $(cat .env | xargs)
```

- Run the actions-runner within the container with:

```console
$ docker run \
  --detach \
  --env ORGANIZATION=YOUR_ORG_NAME \
  --env ACCESS_TOKEN=$ACCESS_TOKEN \
  --name runner \
  runner-image
```

- Check it's running with:

```
$ docker logs runner -f
```