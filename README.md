# Run anaconda locally using Docker
- Anaconda is a bundle of 
	- Python distribution
	- Jupyter notebokk
	- Essential Python libraries
- Installing Anaconda locally or directly on your computer (Laptop/Desktop) can at times become complicated to maintain
- Running it as a docker helps easily run it locally and also makes switch different versions of Anacond, destruction of the env easy
- You can mount and share the Data files/folders to docker container and run it

### How to use this
- Clone this repository to a local folder
- You may chose to fork this repository for your personal changes and preferences, into your personal git acount
- Regardless of you fork or clone, below steps can be same or similar
	1. Clone the repo from its remote
	Eg: `git clone git@github.com:rajiff/conda_local_docker.git` 
	2. Traverse to the just cloned repository folder, now you have code required to run conda in your local environment, make sure your current working directory is the root folder of the repository
	Eg: `cd conda_local_docker`
	3. docker-compose up -d
	4. Above will start the anaconda in a docker container, upon successful starting, we can access http://localhost:8888 to access the jupyter notebook
	5. To access the jupyter notebook, you need the token, which is logged by the continer. You can access the log of container for token using command `docker-compose logs | grep -i token`, note the URL, token from this command, which you will need for accessing python env from jupyter notebook

### Running without docker-compose
- if you chose not to use docker-compose and want to run the anaconda directly you can try this 

```unix
docker run -i -t -p 8888:8888 \
	-v $PWD/data:/opt/data -v $PWD/notebooks:/opt/notebooks \
	continuumio/anaconda3 /bin/bash -c "\
    conda install jupyter -y --quiet && \
    mkdir -p /opt/notebooks && \
    jupyter notebook \
    --notebook-dir=/opt/notebooks --ip='*' --port=8888 \
    --no-browser --allow-root"
```