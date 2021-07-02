<h1><b>Instalar entorno local de Kolibri en Ubuntu 20</b></h1>

<h2><b>Primer paso:</b></h2>

<br>

<p>Abrir una terminal en la raiz y correr los siguientes comandos uno por uno:</p>

<pre style="color: rgb(133, 194, 174);">
<i>
    sudo apt update

    sudo apt-get install git

    sudo apt-get install python3-dev

    sudo apt-get install python3-setuptools python3-pip

    sudo apt-get install virtualenv

    sudo apt-get install curl

    curl -sL https://deb.nodesource.com/setup_12.x | sudo -E bash -

    sudo apt-get install -y nodejs

    sudo npm install -g yarn
</i>
</pre>

<br>
<hr>

<h2><b>Segundo paso: Crear una nueva SSH de GitHub.</b></h2>

<br>

<p>Para crear una nueva SSH, en la terminal corra el siguente comando y siga los pasos que les muestran:</p>
<pre style="color: rgb(133, 194, 174);">
ssh-keygen
</pre>

<p>Una vez creada la SSH, diríjace a la carpeta '.ssh' con el siguente comando:</p>
<pre style="color: rgb(133, 194, 174);">
cd ~/.ssh
</pre>

<p>Cuando esten en el directorio ejecutan en siguiente comando:</p>
<pre style="color: rgb(133, 194, 174);">
cat id_rsa.pub
</pre>
<p>Copian lo que les imprime y con eso crean la SSH en GitHub.</p>

<br>
<hr>

<h2><b>Paso tres:</b></h2>

<p>Ya con la SSH vamos al directorio donde queramos clonar el proyecto y ejecutamos en siguiente comando:</p>

<pre style="color: rgb(133, 194, 174);">
git clone git@github.com:$USERNAME/kolibri.git
</pre>

<p>Reemplazando '$USERNAME' por tu usuario de github y listo.</p>

<br>
<hr>

<h2><b>Paso cuatro: Instalar Git lfs.</b></h2>

<p>Ejecutamos los siguientes comando en la terminal raiz:</p>

<pre style="color: rgb(133, 194, 174);">
curl -s https://packagecloud.io/install/repositories/github/git-lfs/script.deb.sh | sudo bash

sudo apt-get install git-lfs
</pre>

<p>Despues inicializamos Git lfs:</p>

<pre style="color: rgb(133, 194, 174);">
git lfs install
</pre>

<p>Luego nos dirigimos dentro de la carpeta Kolibri y ejecutamos los siguentes comandos.</p>

<pre style="color: rgb(133, 194, 174);">
git remote add upstream git@github.com:learningequality/kolibri.git

git fetch --all

git checkout develop
</pre>

<br>
<hr>

<h2><b>Paso cinco: Instalar pipenv.</b></h2>

<p>Ejecutamos los siguientes comandos en la terminal raiz:</p>

<pre style="color: rgb(133, 194, 174);">
sudo apt update

sudo apt install pipenv
</pre>

<p>Despues creamos un archivo .env en el directorio raiz de kolibri y pegamos lo siguiente dentro del archivo:</p>
<pre>
export KOLIBRI_RUN_MODE="dev"
</pre>

<p>Guardamos los cambios y en la terminal dentro de la directorio kolibri ejecutamos el siguiente comando para arrancar el entorno virtual con pipenv:</p>

<pre style="color: rgb(133, 194, 174);">
pipenv shell
</pre>

<p>
Al virtualizarse se dará cuanta que al inicio de la dirección se agregó algo así: 
<br>
<p style="color: rgb(92, 160, 206)"><b>(kolibri - 'id aleatorio')</b></p>
</p>

<br>
<hr>

<h2><b>Paso seis:</b></h2>

<p>Instalar nvm para las versiones de node, ya que kolibri funciona con las version 10.</p>

<br>

<p>Para instalar nvm ejecutamos el siguiente comando el la terminal raiz:</p>

<pre style="color: rgb(133, 194, 174);">
curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.33.11/install.sh | bash
</pre>

<p>Cerramos la terminal y volvermos a abrirla y ejecutamos el siguinete comando para instalar y usar la version 10.15.3 de node:</p>

<pre style="color: rgb(133, 194, 174);">
nvm install 10.15.3

nvm use 10.15.3
</pre>


<br>
<hr>

<h2><b>Paso siete:</b></h2>

<p>Ya con nuestro entorno virtualizado, avancemos a isntalar las dependencias con los siguientes comandos:</p>

<pre style="color: rgb(133, 194, 174);">
pip install -r requirements.txt --upgrade

pip install -r requirements/dev.txt --upgrade

pip install -e .

yarn install

kolibri manage migrate
</pre>

<h3>Y finalmente arrancamos el servidor.</h3>

<pre style="color: rgb(133, 194, 174);">
yarn run devserver
</pre>











