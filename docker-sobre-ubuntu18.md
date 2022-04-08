### Instalacion de Docker sobre Ubuntu 18.04
Actualizar repositorio APT e instalar dependencias
```
sudo apt-get update && \
sudo apt-get install \
    apt-transport-https \
    ca-certificates \
    curl \
    gnupg-agent \
    software-properties-common
```

Claves GPG
```
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
```

Verificamos clave
```
sudo apt-key fingerprint 0EBFCD88
```

Agregar repositorio estable
```
sudo add-apt-repository \
   "deb [arch=amd64] https://download.docker.com/linux/ubuntu \
   $(lsb_release -cs) \
   stable"
```

Instalar motor de docker
```
sudo apt-get update | sudo apt-get install docker-ce docker-ce-cli containerd.io
```

Docker como Usuario
```
sudo groupadd docker && sudo usermod -aG docker $USER newgrp docker
```

##### Instalacion de docker-compose
Para instalar docker-compose en linux. Verificar version y reemplazar por 1.27.4 en el siguiente comando.
```
sudo curl -L "https://github.com/docker/compose/releases/download/1.27.4/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose && sudo chmod +x /usr/local/bin/docker-compose
```
