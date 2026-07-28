---
schema_version: "1.0.0"
document_id: "34b91ee3af48e0f4667a03cb6708dd6b3501244916dd6026eaf09d7f34c8a54e"
company_key: "yc-pipekit"
company: "Pipekit"
source_id: "yc-pipekit-rss-36462c6998f9"
canonical_url: "https://homepage.pipekit.io/blog/how-to-run-argo-workflows-codebase-locally"
published_at: "2024-01-24T15:17:49+00:00"
first_seen_at: "2026-07-25T19:08:09.004424+00:00"
fetched_at: "2026-07-28T22:26:17.179631+00:00"
content_hash: "sha256:0df9f9ec223dafcb0da1eb2d7016c1f65a1cc78a5b61cda0ac2215958dacf458"
---

# How to Run the Argo Workflows Codebase Locally

In this tutorial, you'll learn how to run the[Argo Workflows codebase](https://pipekit.io/blog/top-10-argo-workflows-examples) locally, including the API and UI, using the[minikube](https://minikube.sigs.k8s.io/docs/) distribution of Kubernetes. We'll install each dependency step-by-step, with instructions for Windows, macOS, and Ubuntu-Linux.


If you're new to developing on Argo Workflows, this is a perfect place to start. If you need help with a particular dependency, or want to run Argo Workflows with minikube right away, scroll down to find the relevant section.


## What is Argo Workflows?


Argo Workflows is an open source workflow engine for orchestration of jobs (workflows) on Kubernetes. What Argo Workflows allows you to do is to define a set of tasks and its dependencies as a directed acyclic graph (DAG). Argo Workflows is commonly used for ETL and CI workloads on Kubernetes.


## How to run Argo Workflows


Let's get started on running Argo Workflows locally. For the Ubuntu steps, we will be working with a fresh Ubuntu 20.04 LTS installation.


Alternatively, if you would like to get Argo Workflows up and running in the cloud, I have provided some[Terraform scripts here](https://github.com/isubasinghe/pipekit) to get it running on AWS.


## Requirements


- Docker
- Minikube
- protoc
- node
- npm
- Yarn
- jq
- Go 1.17


### Installing Docker


The Docker website[provides](https://docs.docker.com/get-docker/) a comprehensive guide into installing Docker. I have provided the steps for macOS, Windows and Ubuntu below, this should still provide help when installing Docker on other distributions.


#### Windows


Installing Docker Desktop on windows is quite simple:


1. Download the Docker Desktop Installed from[Docker Hub](https://hub.docker.com/editions/community/docker-ce-desktop-windows/) .
2. Double click on the {% c-line %}Docker Desktop Installer.exe{% c-line-end %} file that you just downloaded.
3. When the installation finishes, open up PowerShell and check if your installation was successful by running {% c-line %}docker version{% c-line-end %}.


#### macOS


Installing Docker Desktop on macOS is just as simple as on windows:


1. Download dmg file from[here](https://docs.docker.com/desktop/mac/install/) depending on your chip, either Intel or Apple silicon.
2. Double click on the dmg to open the installer, from here you simply need to drag and drop the Docker icon into the Applications folder.
3. Search for Docker in launchpad and click to launch Docker.


#### Ubuntu


##### Uninstall old versions


If you already have an old version of Docker, you may first uninstall that. This can be fairly easily achieved through running:


```text


```


Note that this will not remove images, containers, volumes and networks which are installed at {% c-line %}/var/lib/docker{% c-line-end %}. If you would like to remove these first, you may run:


```text


```


{% cta-1 %}


##### Install using the repository


First let's install the utilities we need to add the Docker repository by running the two commands below:


```text


```


Now we can add Docker's official GPG key by:


```text


```


And now we can setup the **stable** repository:


```text


```


After this process, the latest Docker binaries should be available for download following an update, you can use the below commands to install Docker:


```text


```


Verify Docker has been installed correctly by running {% c-line %}docker ps{% c-line-end %} you should see output like this:


Expected Docker output when installed correctly.


‍


In the case you get a permission error, you need to add setup Docker to run without root privileges.


To do this, you must follow the steps below:


1. Create the {% c-line %}docker{% c-line-end %} group:


```text


```


1. Add your user to the {% c-line %}docker{% c-line-end %} group:


```text


```


1. Run the following command to activate the changes to groups:


```text


```


### Installing Minikube


As with Docker, the k8s website[provides](https://minikube.sigs.k8s.io/docs/start/) a more comprehensive guide to installing minikube on various architectures, so we will cover the installation of a minikube on x86-64 only.


#### Windows


To install the latest minikube stable: Download the latest release by running the following PowerShell command:


```text


```


After this we also need to add {% c-line %}minikube{% c-line-end %} to our PATH, this can be achieved through running:


```text


```


#### macOS


```text


```


#### Ubuntu


The process is quite straightforward, simply run the command below:


```text


```


### Installing protoc


Your distribution may have protobuf already installed, but I would not recommend using this installation. When I first attempted running Argo Workflows on my Fedora installation, protobuf on the system was missing the entirety of the include folder. You may find the installation instructions[here](http://google.github.io/proto-lens/installing-protoc.html) , but it is fairly simple.


#### Windows


Unfortunately the protobuf website does not provide instructions for installing protobuf on Windows but it is farily simple because binaries are provided on the github[repository](https://github.com/protocolbuffers/protobuf/releases/) . Simply download these and extract them to a directory (such as {% c-line %}C:\\Program Files\\protobuf{% c-line-end %}) and add the {% c-line %}bin{% c-line-end %} and {% c-line %}include{% c-line-end %} directories to the PATH variable.


#### macOS


The steps are given below for macOS but note that this is not for the latest Apple Silicon but x86-64. Binaries have not been released for Apple Silicon at the time of writing this. Here are the steps:


```text


```


#### Ubuntu


The steps are given below for Ubuntu: First install {% c-line %}zip{% c-line-end %} and {% c-line %}unzip{% c-line-end %}:


```text


```


Now we may install protobuf through:


```text


```


Try running {% c-line %}protoc{% c-line-end %} now, if you get a permission error, simply run {% c-line %}sudo chmod +x $(which protoc){% c-line-end %}. You can of course view the permissions by navigating to {% c-line %}/usr/local{% c-line-end %} and running {% c-line %}ls -lah{% c-line-end %}.


### Installing Yarn, Npm and Node


#### Windows


Through the nodejs[website](https://nodejs.org/en/download/) you may download the latest installer, here is the link for[node v16.13.1](https://nodejs.org/dist/v16.13.1/node-v16.13.1-x86.msi) .


1. Once you have downloaded the installer, simply double click on it.
2. The system may ask you if you want to run the software, you should click on run. This should launch the Setup Wizard, make sure the installer adds the binary folder to the PATH variable.
3. Verify the installation by running {% c-line %}node{% c-line-end %} on a command prompt.


#### macOS & Ubuntu


I would recommend installing {% c-line %}npm{% c-line-end %} and {% c-line %}node{% c-line-end %} via[nvm](https://github.com/nvm-sh/nvm) . The install process is quite simply, just run:


curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.0/install.sh | bash


You should of course run {% c-line %}source ~/.bashrc{% c-line-end %}or {% c-line %}source /.zshrc{% c-line-end %} after this and verify the installation by running {% c-line %}nvm{% c-line-end %}.


Following this, you can install node by {% c-line %}nvm install node{% c-line-end %}. To install yarn, you may simply run {% c-line %}npm install -g yarn{% c-line-end %} after this step.


### Installing jq


{% c-line %}jq{% c-line-end %} is the one item in this list that I would recommend installing through your system itself (apt/dnf/yum), you may get a slightly outdated version, but it shouldn't matter as much as the other tools.


#### Windows


The steps on Windows are a bit more complex.


1. Download a windows executable from[here](https://github.com/stedolan/jq/releases) .
2. Rename your exe which at the time of writing had this format {% c-line %}jq-win(32|64).exe{% c-line-end %} to just {% c-line %}jq.exe{% c-line-end %}.
3. Then move the executable to {% c-line %}C:\\Program Files\\jq\\{% c-line-end %}, the executable should now be located at {% c-line %}C:\\Program Files\\jq\\jq.exe{% c-line-end %}.
4. Add this folder to the PATH variable.


#### macOS


On macOS simply run:


```text


```


#### Ubuntu


On Ubuntu, simply run:


```text


```


### Installing Go


#### Windows


The installer for go provided in the Golang[website](https://go.dev/doc/install) is likely the easiest way to install go on Windows. This is once again the standard msi installer we have encountered previously.


1. Simply download the installer from the[website](https://go.dev/doc/install) .
2. Double click on the installer and follow the prompts to install Go
3. Verify your installation by opening up a command prompt and typing {% c-line %}go version{% c-line-end %}.


#### macOS


Brew typically contains the latest release of golang and we should have an easier installtion method by using {% c-line %}brew{% c-line-end %}, simply run the commands below to get Go on macOS through brew:


```text


```


#### Ubuntu


As with nearly previous steps, refer to the[official website](https://go.dev/doc/install) for a comprehensive guide but I will now cover how I installed go 1.17.5 on my Ubuntu installation.


1. Download the binaries A link for the binaries is provided in the website above but here it is anyway:[https://go.dev/dl/go1.17.5.linux-amd64.tar.gz](https://go.dev/dl/go1.17.5.linux-amd64.tar.gz) . This can be performed on the command line by running the below command:


```text


```


You should be able to run {% c-line %}ls{% c-line-end %} to verify that the download was successful.


1. Extract the archive This can be done by running the following command:


```text


```


1. Add /usr/local/go/bin to the PATH environment variable. Open up your ~/.bashrc or ~/.zshrc file and add the /usr/local/go/bin path to it. This is quite simply done in bash by adding the following line: {% c-line %}export PATH=$PATH:/usr/local/go/bin{% c-line-end %}.
2. Verify installation of Go. If you are still in the same shell, it is likely that your PATH variable has not been updated. To apply the changes without leaving the shell run {% c-line %}source ~/.bashrc{% c-line-end %} or {% c-line %}source ~/.zshrc{% c-line-end %} or similar depending on your shell. You should be able to verify the existance of Golang by running {% c-line %}go version{% c-line-end %}.
3. Set the GOPATH. First make a directory called {% c-line %}go{% c-line-end %} in your home directory. This is achieved through:


```text


```


If your GOPATH is not set, you need to define it. this is quite simple. Just open up the {% c-line %}~/.bashrc{% c-line-end %} or {% c-line %}~/.zshrc{% c-line-end %} file and add {% c-line %}export GOPATH=/home/$USER/go{% c-line-end %}. Verify the that the path was correctly set by running {% c-line %}go env{% c-line-end %}.


### Other important notes


Please make sure the following is appended to your /etc/hosts file:


```text


```


## Cloning the Argo Workflows repository


Before we clone Argo Workflows, let's make sure that our GOPATH is set by running {% c-line %}echo $GOPATH{% c-line-end %}. Now we need to clone the argo-workflows repo into exactly the correct directory. This is critical to ensure everything works as expected. This directory is {% c-line %}$GOPATH/src/github.com/argoproj/argo-workflows{% c-line-end %}, you may need to mkdir some folders in order to have this structure, feel free to do so and then navigate to {% c-line %}$GOPATH/src/github.com/argoproj{% c-line-end %}. From here we may clone the project by running:


```text


```


## Running minikube


In order to start minikube we can run:


```text


```


You may also view the status of minikube by running:


```text


```


Of course, had you installed {% c-line %}kubectl{% c-line-end %}, you would also be able to view information about the cluster.


{% related-articles %}


### Setting up Docker for minikube


Since minikube runs in a VM, the Docker images you build locally are not accessible to the Docker deamon in minikube. You need to build your images on the Docker deamon in minikube. You can do this by pointing the Docker host to minikube. This can be achieved by:


```text


```


## Run Argo Workflows locally


Nice work, now we are finally at a stage where we can run the Argo Workflows project. You may need to install {% c-line %}make{% c-line-end %} but this is straightforward to install through your systems package manager.


### Run the Argo Workflows API only


To run only the api, you can run the following command:


```text


```


### Running the Argo Workflows API and UI


To run and use the Argo Workflows UI you may run the following command:


```text


```


## Conclusion


Congratulations on running Argo Workflows locally with minikube! You're now ready to develop on the project.


If you haven't already, make sure to check out the[Argo Workflows contributor guidelines](https://argoproj.github.io/argo-workflows/CONTRIBUTING/) and watch the[contributor workshop recording](https://www.youtube.com/watch?v=zZv0lNCDG9w) on YouTube.


And make sure to run the following before committing code:


```text


```
