# Dicas de Python/Django - Grupo de estudo
## Preparando o ambiente para desenvolvimento
> ***Ocorrência:*** A cada nova instalação do Sistema Operacional.

### Instalação do PIP (Python Index Package):
```shell
#Linux/Mac OSx:
sudo easy_install pip

#Distribuições Linux derivados do Debian - Ex.: Ubuntu:
sudo apt-get install python-pip
```

### Instalação do Virtualenv (Ferramenta gestora de ambientes Python virtualizados isolados):
```shell
#Linux/Mac OSx:
pip install virtualenv

#Distribuições Linux derivados do Debian - Ex.: Ubuntu:
sudo apt-get install python-virtualenv
```
### Instalação do GIT (Habilitar o Sistema Operacional para trabalhar com controle de versão GIT)
```shell
#Mac OS/x:
http://sourceforge.net/projects/git-osx-installer/

#Distribuições Linux derivados do Debian - Ex.: Ubuntu:
sudo apt-get install git
```

## Criação de um projeto exemplo:
> Passo a passo com principais atividades necessárias para iniciar um projeto.

> ***Objetivo:*** Projeto Django rodando localmente, versionado com Git e distribuído na plataforma Github

```shell
#Criando o diretorio que conterá os recursos necessários para execução, desenvolvimento e distribuição do projeto
mkdir exemplo

#Acessando o diretório principal
cd exemplo

#Criando uma virtualenv com Python 3 (ambiente isolado) - Ambiente localizado no diretório venv
virtualenv -p python3 venv

#Ativando a virtualenv
source venv/bin/activate

#Instalando o Django 1.10 no ambiente isolado por meio do PIP
pip install Django==1.10

#Criando o arquivo de requirements do projeto
pip freeze > requirements.txt

#Iniciando um projeto Django
django_admin.py startproject projeto .

#Configurando a linguagem e data/hora do projeto. Edite o arquivo: projeto/settings.py
LANGUAGE_CODE = 'pt-br'

TIME_ZONE = 'America/Sao_Paulo'

#Rodar a migração para criação das tabelas básicas do Django no Banco de dados
python manage.py migrate

#Criação de uma aplicação chamada core
python manage.py startapp core

#Criacao da view responsável pela exibição da home/index na app core
#edite o arquivo core/views.py adicione a seguinte função:
def home(request):
    return render('core/home.html')

#crie o home.html em core/templates/core/home.html

#crie o arquivo urls.py em: core/urls.py Ele é responsável pela identificação da view responsável para cada URL pertencente a app core
touch core/urls.py

#edite o arquivo core/urls.py com o seguinte conteúdo:
from django.conf.urls import url
from .views import home

urlpatterns = [
    url(r'^$', home, name='home')
]

#instale a app core no projeto editando o arquivo projeto/settings.py adicionando na lista INSTALLED_APPS como no exemplo:
INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
    'core',
]

#habilite o gerenciador de URLs do projeto para trabalhar com as URLs da app core, para isto, edite o arquivo projeto/urls.py importando o urls do core, veja o exemplo:
from django.conf.urls import url, include
from django.contrib import admin

urlpatterns = [
    url(r'^admin/', admin.site.urls),
    url(r'', include('core.urls'))
]

#neste ponto a sua home já pode ser exibida no navegador

#rodando o servidor web de desenvolvimento
python manage.py runserver

#acessando via navegador
http://localhost:8000
```
