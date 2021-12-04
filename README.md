# Ephemeral Self Hosted Github Actions on Raspberry Pi 4

This is a quick prototype of self hosting a Github runner, and registering dynamically at run time using the Github API.

Based on [here](https://testdriven.io/blog/github-actions-docker/).

## Steps:

1. Ensure you have an Organization on Github.
2. Create a Personal Access Token with repo, workflow, admin:org privileges. 
3. Build the Docker image locally:

    docker build --tag runner-image .

4. 