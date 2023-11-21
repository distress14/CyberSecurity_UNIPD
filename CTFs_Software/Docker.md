IT

Per quanto riguarda la settima challenge (e future), è necessario usare Linux, siccome gli script forniti sono "vecchi", e si basano su vecchie versioni linux. 
Dovrebbe funzionare anche su MAC OS, ma alcuni script non funzionano troppo bene con Docker.

-----------------------------------------------------------------------------------
ENG

As for the seventh challenge (and future ones), you need to use Linux, since the scripts provided are "old," and are based on old linux versions. 
It should also work on MAC OS, but some scripts do not work too well with Docker.

-----------------------------------------------------------------------------------
## Installation

#### 1. [Install using the apt repository](https://docs.docker.com/engine/install/ubuntu/#install-using-the-repository)

Before you install Docker Engine for the first time on a new host machine, you need to set up the Docker repository. Afterward, you can install and update Docker from the repository.

Set up Docker's `apt` repository.

```bash
    # Add Docker's official GPG key:
    sudo apt-get update
    sudo apt-get install ca-certificates curl gnupg
    sudo install -m 0755 -d /etc/apt/keyrings
    curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
    sudo chmod a+r /etc/apt/keyrings/docker.gpg
    
    # Add the repository to Apt sources:
    echo \
      "deb [arch="$(dpkg --print-architecture)" signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
      "$(. /etc/os-release && echo "$VERSION_CODENAME")" stable" | \
      sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
    sudo apt-get update
    ```

#### 2. Install the Docker packages.

To install the latest version, run:

```console
$ sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugi
```
 
#### 3. Verify that the Docker Engine installation is successful by running the `hello-world` image.

```console
$ sudo docker run hello-world
```

This command downloads a test image and runs it in a container. When the container runs, it prints a confirmation message and exits.

You have now successfully installed and started Docker Engine.

-----------------------------------------------------------------------------------
## Starting challenges

IT

Come far partire gli esercizi con Docker: 

Una volta dato i permessi alla cartella interessata:
```
chmod -R +rx ./Percoso/File/alla/cartella/interessata/1_ajax_not_soap
```
[Questa operazione va effettuata su OGNI cartella su cui andremo a lavorare]

Dopodiché, entriamo con ```cd /Percoso/File/alla/cartella/interessata/1_ajax_not_soap``` dentro alla cartella di interesse

Eseguiamo la build ```sudo ./docker_build.sh``` 

Un errore comune avviene durante la fase di build. [Riscontrato solamente nel primo esercizio: AjaxNotSoap]

Personalmente, ho risolto eliminando la riga di codice, nel file Dockerfile:
```
RUN apt-get update --fix-missing
```
Così facendo non andrà a controllare ogni volta se ci sono aggiornamenti (anche perché nessuno c'ha messo mani) e il tutto dovrebbe venir eseguito senza troppi problemi

Infine, eseguiamo ```sudo ./docker_run.sh``` ;

Ora possiamo collegarci tramite browser al sito dell'esercizio (in loco)

-----------------------------------------------------------------------------------

ENG

How to start exercises with Docker: 

Once you have given permissions to the relevant folder:
```
chmod -R +rx ./Path/to/the/interested/folder/1_ajax_not_soap
```
[This should be done on EVERY folder we are going to work on]

After that, we go in with ```cd /Path/to/the/interested/folder/1_ajax_not_soap``` inside the folder of interest

We run the build ``sudo ./docker_build.sh``

A common error occurs during the build phase. [Found only in the first exercise: AjaxNotSoap].

Personally, I solved it by deleting the line of code, in the Dockerfile:
```
RUN apt-get update --fix-missing
```
By doing so, it won't go and check every time for updates (also because no one has updated the files) and the whole thing should run without too much trouble

Finally, we run ``sudo ./docker_run.sh`` ;
Now we can connect via browser to the exercise site

