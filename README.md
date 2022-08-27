# Atividade Docker

## **Instruções:**

1. Linux Subir 1(um) servidor Oracle Linux do zero (sem
interface gráfica).
2. Instalar 1 imagem Oracle Linux last stable
version, para execução de atividades;
3. Ajustar a rede da máquina virtual para um cidr
/24, sob o protocolo IPv4, utilizando um range
classe A;
4. Deixar a rede virtual em modo NAT para acesso
à internet;
5. Ajustar LVMs para as partições em separado:
/home, /var, /tmp; (durante a instalação);
6. Configurar hostname;
7. Ajustar DNS com o nome
elklabmonitoriacontainer;
8. Configurar IP fixo;
9. Configurar SSH;
10. Bloquear o acesso SSH para root;
11. Criar um filesystem /var/lib/docker com 10GB em
EXT4 para as imagens do docker;
12. Criar um projeto de versionamento;
Subir um Docker;
13. Instalar uma imagem da aplicação ELK via
Docker.

## **Restrições:**

1. Proibido acesso à console após ajustar o IP Fixo;
2. Proibido logar como root;
3. Proibido executar e rodar o Docker como root
mode;
4. Criar um usuário com o nome diferente do DNS
sugerido.

## Documentação detalhada:

### Downloads:

Obter instalador ***VirtualBox*** em: [https://www.virtualbox.org/wiki/Downloads](https://www.virtualbox.org/wiki/Downloads)

Obter imagem ***Oracle Linux*** em: [https://yum.oracle.com/oracle-linux-isos.html](https://yum.oracle.com/oracle-linux-isos.html)

### Especificações da máquina virtual:

**Processador:**

![Processador](https://user-images.githubusercontent.com/108694840/185004332-d900af95-34ef-4124-ab02-34c2e4143dd2.png)

**Memória Ram:**

![Ram](https://user-images.githubusercontent.com/108694840/185004585-ecbca7a7-ab0a-4e32-97f7-644427b6fb56.png)

**Rede:**

![Rede](https://user-images.githubusercontent.com/108694840/185004683-2ec5dc27-7359-4ce6-8ccd-5393b4d65dae.png)

**Imagem:**

![Imagem](https://user-images.githubusercontent.com/108694840/185004898-3627d1b4-ac3c-4cc6-a960-7a2d3395124d.png)

### Configuração da Imagem:

**Seleção de software:**

![Captura de tela 2022-08-26 213336](https://user-images.githubusercontent.com/108694840/187008945-563b3866-d162-477d-9277-d0f60477794a.png)

**Particionamento dos diretórios:**

![Captura de tela 2022-08-26 215450](https://user-images.githubusercontent.com/108694840/187008884-23bec01d-af38-4516-b86e-6d12f4c4081d.png)

### Instalação e configuração do GitHub:

Comando de instalação do Git

```
$ sudo dnf install git-all
```

Comandos para criação do repositório de arquivos do Git

```
$ mkdir git-repository
```

```
$ cd git-repository
```

```
$ git init
```

Criação de vínculo com repositório remoto

```
$ git remote add origin https://github.com/Ryan-Amaro/Atividade-Docker.git
```

Comando para exibir o status da conexão com o repositório remoto

```
$ git status ip route
```

### Armazenamento de usuário e senha do GitHub

```
$ git config credential.helper store
```

```
$ git config --global credential.helper store
```

### Preparação e envio de arquivos para o repositório remoto do GitHub:

Prepara o arquivo para ser enviado ao repositório remoto

```
$ git add nome-do-arquivo
```

> Adiciona uma descrição ao commit.

```
$ git commit -m "digite-uma-mensagem"
```

> Substitua pela descrição do commit.

Criação do branch

```
$ git branch -M "main"
```

Envio do arquivo

```
$ git push -u origin main
```

### Configuração de rede:

Comando para exibir IP

```
$ hostname -I
```

Comando para alterar configurações da placa de rede

```
$ nmtui
```

```
= IPV4 CONFIGURATION <Manual>
ADDRESSES: 10.0.2.15/8
  GATEWAY: 10.0.2.2
      DNS: 8.8.8.8
           8.8.4.4

= IPV6 CONFIGURATION <Disabled>
```

![Captura_de_tela_2022-08-16_153007](https://user-images.githubusercontent.com/108694840/185005443-7da190ad-946f-47f6-9358-bcbaf32f9986.png)

Execute o comando para alterar o arquivo de configuração da placa de rede

```
$ sudo nano /etc/sysconfig/network-scripts/ifcfg-enp0s3
```

Inclua o seguinte parâmetro para definir a rede como classe A

```
NETMASK=255.0.0.0
```

![Captura_de_tela_2022-08-16_153956](https://user-images.githubusercontent.com/108694840/185005494-2cba4d5e-dda4-48eb-93d4-b3bf0683220b.png)

Alteração do hostname

```
$ sudo nano /etc/hostname
```

```
atividade-docker.localdomain
```

Configuração adicional

```
$ sudo nano /etc/sysconfig/network
```

```
NETWORKING=yes
HOSTNAME=atividade-docker
GATEWAY=10.0.2.2
```

![Captura_de_tela_2022-08-16_154555](https://user-images.githubusercontent.com/108694840/185005550-4819cfb1-9b7f-45f1-94a9-354fb6af159f.png)

```
$ sudo nano /etc/hosts
```

```
127.0.0.1   elklabmonitoriacontainer
10.0.2.15   atividade-docker
```

![Captura_de_tela_2022-08-16_104620](https://user-images.githubusercontent.com/108694840/185005614-0d2d708d-89c0-40d0-952c-6dd604691456.png)

Visualização do arquivo que armazena os endereços de servidores DNS

```
$ cat /etc/resolv.conf
```

![Captura_de_tela_2022-08-16_124648](https://user-images.githubusercontent.com/108694840/185005670-7df79052-32d9-4610-8d77-2df8ff200ba7.png)

Aplicação das configurações ao serviço de rede

```
$ sudo systemctl restart NetworkManager.service
```

```
$ sudo systemctl status NetworkManager.service
```

### Instalação e configuração do serviço SSH no Linux:

Comando para instalar o serviço SSH

```
$ sudo dnf install openssh-server
```

Ativação e status do serviço

```
$ sudo systemctl start sshd
```

```
$ sudo systemctl status sshd
```

Configurando serviço para inicializar com o sistema

```
$ sudo systemctl enable sshd
```

Modificação de arquivo para bloquear acesso via ssh

```
$ sudo nano /etc/ssh/sshd_config
```

```
PermitRootLogin no
```

![Captura_de_tela_2022-08-15_004631](https://user-images.githubusercontent.com/108694840/185005760-5aba7ebb-be21-4c04-8df7-aff91b83a8a8.png)

Aplicando alterações

```
$ sudo systemctl restart sshd
```

```
$ sudo systemctl status sshd
```

### Configurando acesso SSH no VirtualBox:

Na tela do VirtualBox selecione a máquina virtual e acesse o seguinte caminho **Configurações > Rede > Avançado > Redirecionamento de Portas**, e crie uma nova regra

![Captura_de_tela_2022-08-16_104129](https://user-images.githubusercontent.com/108694840/185005885-10bd09c7-edf4-42cc-9e44-6fcb323938e5.png)

### Configurando acesso SSH no Windows:

Execute o bloco de notas como administrador, e vá em **Arquivo > Abrir > C:\Windows\System32\drivers\etc** e altere a opção **Documentos de texto** para **Todos os arquivos**

![Captura_de_tela_2022-08-15_012010](https://user-images.githubusercontent.com/108694840/185005933-4b7c0935-d48f-4cb1-a1f9-b325f0e66e09.png)

Acrescente a seguinte linha ao arquivo e depois salve

```
127.0.0.1   elklabmonitoriacontainer
```

![Captura_de_tela_2022-08-15_151475](https://user-images.githubusercontent.com/108694840/185005997-f9918698-2d02-4daa-b1c5-53e38d75335e.png)

### Acessando servidor via SSH pelo Windows:

Abra o prompt de comando do Windows e digite o seguinte comando

```
ssh admin@127.0.0.1 -p 2222
```

ou

```
ssh admin@elklabmonitoriacontainer -p 2222
```

![Captura_de_tela_2022-08-15_163004](https://user-images.githubusercontent.com/108694840/185006049-ebf28a56-22b7-49db-bd4f-2bba7b1830ed.png)

### Instalação e configuração do Docker:

Comando para instalação do Docker

```
$ sudo dnf install dnf-plugins-core
```

```
$ sudo dnf config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo
```

```
$ sudo dnf install docker-ce docker-ce-cli containerd.io
```

Ativação do serviço Docker

```
$ sudo systemctl start docker
```

Configurando o serviço Docker para iniciar com o sistema

```
$ sudo systemctl enable docker
```

Reiniciando sistema para aplicar e testar alterações

```
$ shutdown -r now
```

```
$ systemctl status docker
```

Teste de criação de container

```
$ sudo docker run hello-world
```

Definindo usuário do sistema como superusuário no Docker

```
$ sudo groupadd docker
```

```
$ sudo usermod -aG docker admin
```

> Nome do usuário “**admin**”.
> 

```
$ newgrp docker
```

### Instalação e configuração da imagem ELK:

Comando para baixar imagem ELK

```
$ docker pull sebp/elk
```

Exibição das imagens armazenadas

```
$ docker images
```

![Captura_de_tela_2022-08-16_162693](https://user-images.githubusercontent.com/108694840/185006251-8c63c5e3-8c02-474f-9b9d-d7caaae5a6ac.png)

Criando um container ELK que inicia com o sistema

```
$ docker run -d --restart unless-stopped -p 5601:5601 -p 9200:9200 -p 5044:5044 -it 48c088a6f82c
```

> ID da imagem do container **48c088a6f82c**.

Exibir containers ativos

```
$ docker ps
```

Renomeando container

```
$ docker rename 443d73f1677b elk
```

> ID do container **443d73f1677b**.

> Novo nome “**elk**”.

![Captura_de_tela_2022-08-16_163707](https://user-images.githubusercontent.com/108694840/185006362-a4d5617c-4aa8-4b2d-94ca-1ba05e03d8b7.png)
