# Homework 1

The instructions to setup your copy of the project can be found on the course
web site: https://dslab2018.github.io/labs/week4/.

Open the notebook to find all the questions for this assignment.
There are 4 sections totalling to 60 points.
You can also find a version on gitlab: https://git-dslab.epfl.ch/dslab2018/homework1/blob/master/Assignment_DataScience_Lab_week4.ipynb.

Edit the notebook and Dockerfile to complete the assignment.
Commit and push regularly your changes to gitlab.
The content of your repository at the time of the deadline will be used for
grading your work.
In other words, if you push changes past the deadline, these will NOT be
taken into account.

To open the notebook with jupyter, you can type the following command in
your shell.
```bash
jupyter notebook \
  --NotebookApp.default_url=/notebooks/Assignment_DataScience_Lab_week4.ipynb
```

## Using Docker

To create the Docker image from the Dockerfile type:
```bash
docker build -t co2notebook .
```
This instructs docker to build an image using:
- The current directory as the context from the last argument `.`
- The `Dockerfile` as the recipe to create the image.
  This is a convention from Docker.
- `co2notebook` as the resulting image tag.
  Tags are used by Docker to designate images.

To run this image, you can type:
```bash
docker run --init --rm -it -p 8888:8888 co2notebook
```
Using Docker, the notebook will not open itself, but you can
look at the output of the command to open it.
You should see something similar to:
```
[C 19:35:11.113 NotebookApp]

    Copy/paste this URL into your browser when you connect for the first time,
    to login with a token:
        http://0.0.0.0:8888/?token=0ed084c62aa100da287f45819cb376d0685b7f48699c734b
```
You can simply open the corresponding link or copy/paste it to access
the notebook.
Note: the token `0ed0...` will not be the same.

Explanation for the options:
- `--init` use `tini` as a process reaper. Read more: <https://docs.docker.com/engine/reference/run/#specify-an-init-process>
- `--rm` do not keep the container after it is terminated
- `-it` Assign a terminal (TTY) and run in interactive mode.
  This is essentially to allow to stop jupyter using `SIGINT`
  (by pressing `CTRL-C`)
- `-p 8888:8888` bind port 8888 on localhost to port 8888 in the container.
  We cannot connect to jupyter otherwise.
- `co2notebook` designates the image to be run.
  Here we use the tag we assigned earlier during the build.
