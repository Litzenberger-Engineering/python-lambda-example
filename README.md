# setup

- cd into python directory `cd python/`
- run setup script to create env and install dependencies locally `sh setup.sh`
- the local dependencies are actually not needed, because the code is run in a docker container that has the same dependencies
- the local installation has convenience reasons because only then you can jump into the packages, have linting, autoformat etc.
- local dependency installation can be skipped once python docker development is fully supported by Visual Studio Code
- if you want to debug in docker container, check: https://vinta.ws/code/remotely-debug-a-python-app-inside-a-docker-container-in-visual-studio-code.html
- activate the environment with `source env/bin/activate` if it didnt happen automatically (you might need to restart VS Code to make linting + autoformat working)

# development

- first, run `docker-compose up postgres`
- then start django with `docker-compose up python`
- we need to follow the order, otherwise the command in the python service will fail and therefore the django server not start
- access http://127.0.0.1:8000/ or http://0.0.0.0:8000/ - you should see a django screenpython

# deployment

- go to python directory `cd python/`
- activate env `source env/bin/activate`
- follow zappa setup instructions on https://github.com/Miserlou/Zappa#installation-and-configuration
- configure zappa_settings.json `cp zappa_settings_example.json > zappa_settings.json`
- run `zappa deploy dev` for initial deployment, run `zappa update dev` for updates
- todo: reuse current dockerfile for building a deployment container
- todo: do deployments from inside the container
- todo: probably add a deployment command that can be passed to deployment container

# how to make postgres & lambda work together

- configure security groups and inbound & outbound rules accordingly
- e.g. if you want to access the database only from within a VPC, you need to add the IPv4 CIDR of the VPC as Inbound Rule
- you can find the IPv4 CIDRs e.g. for eu-central-1 e.g. here: https://eu-central-1.console.aws.amazon.com/vpc/home?region=eu-central-1#vpcs:sort=VpcId
