Instalação
==========

Antes de mais nada, como iremos trabalhar em ambiente linux precisamos instalar/atualizar alguns pacotes.
::
  aptitude update && aptitude upgrade


Depois digite o proximo comando:
::

  sudo aptitude install build-essential libssl-dev libxml2-dev libxslt1-dev libbz2-dev zlib1g-dev python-setuptools python-dev python-virtualenv libjpeg62-dev libreadline-gplv2-dev python-imaging wv poppler-utils git -y



Em ambiente de desenvolvimento
------------------------------
	

Clone o *buildout*:
::

    cd ~
    git clone https://github.com/:plonegovbr/portal.buildout.git portal.buildout


    Acesse o diretório portal.buildout


Execute o Virtualenv
--------------------

Por questões de conflito com o Python utilizado pelo sistema operacional, verifique a versão
::

  virtualenv --version


Verifique a versão do Ubuntu para seguir no proximo passo, por exemplo   
Na distribuição LTS do Ubuntu for 12.04 execute o virtualenv da seguinte forma:
::

  cd $HOME/portal.buildout
  virtualenv --setuptools py27
  source py27/bin/activate

Se for maior ou igual a 1.10, o comando virtualenv não necessita do parâmetro *--setuptools* como indicado acima:
::

  cd $HOME/portal.buildout
  virtualenv py27
  source py27/bin/activate

Criando arquivo Buildout
------------------------

É necessário criar um arquivo de configuração chamado **buildout.cfg** onde ele estende de um outro arquivo **development.cfg** para definir variáveis deste ambiente
  
Conteúdo do Buildout inicialmente é este logo abaixo:
::

    [buildout]
    extends =
        development.cfg

    [remotes]
    plonegovbr = https://github.com/plonegovbr
    collective = https://github.com/collective
    plone = https://github.com/plone
    simplesconsultoria = https://github.com/simplesconsultoria


.. note:: Como iremos usar o portal padrao como template no arquivo buildout.cfg precisamos adicionar uma egg brasil.gov.temas]


O arquivo **buildout.cfg** ficará assim:
::

    [buildout]
    extends =
        development.cfg

    [remotes]
    plonegovbr = https://github.com/plonegovbr
    collective = https://github.com/collective
    plone = https://github.com/plone
    simplesconsultoria = https://github.com/simplesconsultoria

    eggs=
        brasil.gov.temas

E por fim executa-se o *buildout* 
::

  python bootstrap.py


Em seguida:
::

  ./bin/buildout



Iniciando em modo serviço (daemon)
------------------------------------

Para subir o portal digite os seguintes comandos
::

  cd ~/portal.buildout
  ./bin/instance start


Acesse: localhost:8080/


Para parar o serviço
::

  ./bin/instance stop


