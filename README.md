# Leds Zeppelin
##Passo a Passo da integração com Travis/Sonar/Slack/Taiga
###Adicionar arquivo _.travis.yml_
Primeiro passo é criar o arquivo _.travis.yml_ dentro do repositorio do git.
Em seguida editar esse arquivo para conter as seguintes informações:<br>
<hr>

language: python
python:
  - "3.4"
  
before_install:
  - wget http://repo1.maven.org/maven2/org/codehaus/sonar/runner/sonar-runner-dist/2.4/sonar-runner-dist-2.4.zip
  - unzip sonar-runner-dist-2.4.zip

branches:
  only:
    - master

install:
  - pip install -r requirements.txt
  
script: 
  - nosetests

after_script:
 - ./sonar-runner-2.4/bin/sonar-runner

<hr>

##Travis CI
Logar no [Travis](https://travis-ci.org/) com a conta do LEDS para criar a conexão do repositorio git com o Travis.
Ir em LEDS/Accounts e ativar seu repositório.
Em seguida clicar na engrenagem de configurações e habilitar a opção _Build only if .travis.yml is present_.
Para testar a conexão clique em _Build History_ sobre o icone da opção acima e de algum git push no seu diretorio.

##Sonar

