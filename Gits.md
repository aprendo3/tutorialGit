# Tutorial Git Básico
[![Watch the video](https://img.youtube.com/vi/9xo0LoYMSp4/default.jpg)](https://youtu.be/9xo0LoYMSp4)

### Comandos básicos en Bash
```shell
pwd
ls
clear
pwd

# Preparar el directorio para el nuevo Repositorio
mkdir /c/Proyectos/Repo1/
cd /c/Proyectos/Repo1/
```

### Crear/iniciar nuevo Repositorio (Local)

```shell
git init
# crear un documento en el directorio con el contenido "Hola1"
echo "Hola1" >> doc.txt
# ver el contenido del documento en la terminal
cat doc.txt 
# ver el estado del repositorio
git status

# agregar el documento a stage
git add doc.txt

git status

# confirmar todos los cambios que están en stage
git commit

# configurar datos de usuario a nivel de este Repo
git config user.email "you@example.com"
git config user.name "Your Name"

# confirmar todos los cambios que están en stage
git commit

# ver el historial de cambios (commits) del Repo
git log

# verificar que no hay cambios en el espacio de trabajo
git status

# agregar un nuevo documento
echo "Hola2" >> doc.txt
git status

# ver las diferencias (cambios) entre el repositorio y el espacio de trabajo
git diff

# agregar el documento a stage
git add doc.txt 
git status

# confirmar todos los cambios que están en stage, con un mensaje
git commit -m "agrega hola2 en doc.txt"
git log

# agregar más cambios
echo "Hola3" >> doc.txt
echo "Hola1" >> doc2.txt

ls
git status

# agregar cambios a stage
git add doc.txt doc2.txt 
git status

# confirmar todos los cambios que están en stage, con un mensaje
git commit -m "agrega doc2"
git log
```

### Demostración, recupera información perdida
```shell
# un nuevo cambio
git status
git add doc.txt
git commit -m "agrega info importante"
git status

# confirmar que se perdió 
git diff
git status

# recuperar (deshacer los cambios en el espacio de trabajo) la información importante
git restore doc.txt 
git status
git diff

# quitar información importante del repo
git add doc.txt 
git commit -m "perder info importante"
git log

# actualizar el espacio de trabajo a un punto en el repositorio donde se encontraba la información importante (volver en el tiempo)
git checkout b8dec3bac494e52aa726f047b61c5058457bc56c
git log

# restaura el espacio de trabajo al último commit
git checkout main
git status
git log

# agregar un nuevo cambio, recuperando el estado del commit anterior
git revert 4d43e3d6033398ecff6a2eb9628364bbb347b2fd
git log
```

### Subir a un Servidor Remoto
```shell
# agrega info del Repo remoto
git remote add origin https://github.com/aprendoTuto1/miRepo1.git

# mandar los últimos cambios al Repo Remoto
git push -u origin main

# Bajar el Repo Remoto a un nuevo Repo Local
cd ..
git clone https://github.com/aprendoTuto1/miRepo1.git
ls
cd miRepo1/
ls
cat doc.txt 

# borrar el Repo local (Directorio)
cd ..
rm -rf miRepo1
ls

# Bajar el Repo Remoto a un nuevo Repo Local
git clone https://github.com/aprendoTuto1/miRepo1.git
ls
cd miRepo1/
ls
cd ..
rm -rf miRepo1
```

### Configurar SSH para conectarse al Servidor Remoto

```shell
# crear nuevas llaves
ssh-keygen -t ed25519 -C "aprendo.tuto1@"

# ver las llaves creadas
ls /c/Users/Aprendo/.ssh/

# copiar llave publica, para configurar en el Servidor
notepad /c/Users/Aprendo/.ssh/id_ed25519.pub 

# bajar el repo usnado SSH
ls
git clone git@github.com:aprendoTuto1/miRepo1.cd miRepo1/
ls
cat doc.txt 
```

### Actualizar Repo Local y el espacio de trabajo con los últimos cambios en el Repo Remoto
```shell
git pull origin main 
```

### Ramas, crear nuevas ramas, y moverse entre ellas
```shell
# listar ramas del Repo
git branch

# crear nueva rama y listar
git branch rama1
git branch

# ver el historial del Repo con más información
git log --oneline --decorate --all --graph

# cambiar a rama1
git switch rama1
git log --oneline --decorate --all --graph

# agregar un nuevo cambio en rama1
echo "hola2" >> doc2.txt
git add doc2.txt 
git commit -m "agrega doc2.txt"

# configurar a nivel global datos del usuario
git config --global user.email "aprendoTuto1@"
git config --global user.name "aprendoTuto1"

git commit -m "agrega doc2.txt"
git status

# volver a rama main (donde no esta los últimos cambios de rama1)
git switch main

# moverse de nuevo a rma1
git switch rama1
git log --oneline --decorate --all --graph

# volver a main
git switch main
git log --oneline --decorate --all --graph

# ver historial con mucha más información
git log --graph --abbrev-commit --decorate --date=relative --format=format:'%C(bold blue)%h%C(reset) - %C(bold green)(%ar)%C(reset) %C(white)%s%C(reset) %C(dim white)- %an%C(reset)%C(bold yellow)%d%C(reset)' --all

# ver historial con mucha más información (otra alternativa)
git log --graph --abbrev-commit --decorate --format=format:'%C(bold blue)%h%C(reset) - %C(bold cyan)%aD%C(reset) %C(bold green)(%ar)%C(reset)%C(bold yellow)%d%C(reset)%n''          %C(white)%s%C(reset) %C(dim white)- %an%C(reset)' --all
# agregar un nuevo cambio
echo "hola3" >> doc.txt
git add doc.txt 
git commit -m "agregar hola3 en doc.txt"
git log --graph --abbrev-commit --decorate --format=format:'%C(bold blue)%h%C(reset) - %C(bold cyan)%aD%C(reset) %C(bold green)(%ar)%C(reset)%C(bold yellow)%d%C(reset)%n''          %C(white)%s%C(reset) %C(dim white)- %an%C(reset)' --all

# subir cambios al Repo Remoto de la rama main
git push -u origin main
# subir cambios al Repo Remoto de la rama rama1
git push -u origin rama1
```
### Merge y Rebase

```shell
# prepara vistas en tmux
tmux
mkdir ../r1 && cd ../r1
watch -t -n0.5 --color "ls" --color
clear
watch -t -n0.5 --color "git log --graph --abbrev-commit --decorate --format=format:'%C(bold blue)%h%C(reset) - %C(bold green)%s%C(reset)%C(bold yellow)%d%C(reset)%n''          ' --all -12" --color
clear

# inicar repo
git init
git checkout -b main
git config user.name "a" && git config user.email "a@"

# crear un nuevo archivo y hacer un commit de los cambios
echo "hola0" >> zd0.txt && git add . && git commit -m "hola0 a zd0"

# trabajar en una nueva rama
git branch
git branch rama1
git branch
git diff main rama1
git switch rama1
git diff rama1 main
echo "hola1" >> zd1.txt && git add . && git commit -m "hola1 a zd1"
git diff rama1 main
git switch main

# traer los cambios de rama1 a la rama main (Fast-Forward), Juntar ramas
git merge rama1

# trabajar en una nueva rama, sin moverse de la rama main
git branch rama2

# crear cambios en main, que no están en la nueva rama
echo "hola2" >> zd2.txt && git add . && git commit -m "hola2 a zd2"
git diff main rama2

# moverse a rama2 y crear cambios
git switch rama2
echo "hola3" >> zd3.txt && git add . && git commit -m "hola3 a zd3"
git diff rama2 main
git switch main

# traer los cambios de rama2 a la rama main (No Fast-Forward), Juntar ramas, creando un commit de Merge
git merge rama2

# trabajar en una nueva rama
git branch rama3
echo "hola4" >> zd4.txt && git add . && git commit -m "hola4 a zd4"
git switch rama3
echo "hola5" >> zd5.txt && git add . && git commit -m "hola5 a zd5"
git merge main
echo "hola6" >> zd6.txt && git add . && git commit -m "hola6 a zd6"
git switch main
git merge rama3
git branch rama4
echo "hola7" >> xd0.txt && git add . && git commit -m "hola7 a xd0"
git checkout rama4
echo "hola8" >> xd1.txt && git add . && git commit -m "hola8 a xd1"

# estando en rama4, traer lso cambios de main, rescribiendo la base, rescribiendo la historia
git rebase main
git checkout main

# traer los cambios de rama1 a la rama main (Fast-Forward), Juntar ramas
git merge rama4
```

Una ves mas:
```shell
mkdir ../r2 && cd ../r2
git init
git checkout -b main
ls
git config user.name "a" && git config user.email "a@"
echo "hola0" >> zd0.txt && git add . && git commit -m "hola0 a zd0"
git switch -c rama1
echo "hola1" >> zd1.txt && git add . && git commit -m "hola1 a zd1"
git switch main
git merge rama1
git branch rama2
echo "hola2" >> zd2.txt && git add . && git commit -m "hola2 a zd2"
git switch rama2
echo "hola3" >> zd3.txt && git add . && git commit -m "hola3 a zd3"
git switch main
git merge rama2
git branch rama3
echo "hola4" >> zd4.txt && git add . && git commit -m "hola4 a zd4"
git switch rama3
echo "hola5" >> zd5.txt && git add . && git commit -m "hola5 a zd5"
git merge main
echo "hola6" >> zd6.txt && git add . && git commit -m "hola6 a zd6"
git switch main
git merge rama3
git branch rama4
echo "hola7" >> xd0.txt && git add . && git commit -m "hola7 a xd0"
git checkout rama4
echo "hola8" >> xd1.txt && git add . && git commit -m "hola8 a xd1"
git rebase main
git checkout main
git merge rama4
```

### Merge con cambios en el mismo archivo
```shell
mkdir ../r3 && cd ../r3
git init
git checkout -b main
git config user.name "a" && git config user.email "a@"
git config --global merge.ff

# habilitar Merge Fast-Forward
git config --global --add merge.ff true

echo "hola1" >> zd1.txt && git add . && git commit -m "hola1 a zd1"
git commit -am "hola 2 - 7"
checkout -b rama1
git checkout -b rama1
git status
git diff
git commit -am "editRama1"
git switch main
git commit -am "editMain"
git switch rama1
git merge main
git switch main
git merge rama1
git checkout -b rama2
git commit -am "editRama2"
git switch main
git commit -am "editMain"
git switch rama2
git merge main
git status
cat zd1.txt
vim zd1.txt
git commit -a
git switch main
git merge rama2
```

### Ignorar archivos 
```shell
mkdir ../r4 && cd ../r4
git init
git checkout -b main
git config user.name "a" && git config user.email "a@"

# crear archivo donde configurar que archivos no se tomarán en cuenta en este repositorio
touch .gitignore
git status
git commit -am "Inicio"
git status
git add .
git status
git commit -m "Inicio"
git status
touch app.exe
git status
git commit -am "Ignorar .exe"
```

### Resolviendo conflictos
```shell
mkdir ../r5 && cd ../r5
cd ..
ls
git clone git@gitlab.com:aprendo-tuto1/tuto2repo2.git
ls
cd tuto2repo2
git checkout -b main
vim .gitignore
git status
echo "Hello" >> README.md
git status
git add .
git commit -m "Inicio"
git config user.name "aprendoTuto2" && git config user.email "aprendo.tuto2@"
git commit -m "Inicio"
git push -u origin main

# subiendo cambios al Repo Remoto con la opción force
git push -u origin main -f
cd ..
rm -rf tuto2repo2
git clone git@gitlab.com:aprendo-tuto1/tuto2repo2.git
cd tuto2repo2
ls
git switch develop
git status
ls
vim Main.java
vim Main.java
java Main.java
ls
git status
git add . && git commit -m "agrega mensajes en Main.java"
git config user.name "aprendoTuto2" && git config user.email "aprendo.tuto2@"
git add . && git commit -m "agrega mensajes en Main.java"
git push -u origin develop
git checkout -b tarea3
git status
git add . && git commit -m "cambiar por println Main.java"
git push -u origin tarea3
git switch develop
git pull
cat Main.java
git switch tarea3

# actualizar con los últimos cambios y resolver conflictos
git rebase develop
git status
git push -u origin tarea3
git push -u origin tarea3 -f
```
