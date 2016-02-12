# Leds Zeppelin
##Passo a Passo da integração com Travis/Sonar/Slack/Taiga
###Travis CI
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
No arquivo acima uma das informações requer o arquivo _requirements.txt_ esse arquivo é gerado com o comando `pip freeze > requirements.txt` e será salvo dentro da pasta do projeto. De push desse arquivo para a raiz do repositório, ele será exibido na mesma tela do arquivo_.travis.yml_.

Em seguida logar no [Travis](https://travis-ci.org/) com a conta do LEDS para criar a conexão do repositorio git com o Travis.
Ir em LEDS/Accounts e ativar seu repositório.
Em seguida clicar na engrenagem de configurações e habilitar a opção _Build only if .travis.yml is present_.
Para testar a conexão clique em _Build History_ sobre o icone da opção acima e de algum git push no seu diretorio.

###Sonar
Crie o arquivo _sonar-project.properties_ dentro do repositorio do git.
Em seguida, edite esse arquivo para conter as seguintes informações:<br>
<hr>
sonar.projectKey=NOMEDOPROJETO<br>
sonar.projectName=NOMEDOPROJETO<br>
sonar.projectVersion=1.0<br>
sonar.sources=NOME DA PASTA COM O CODIGO<br>
sonar.language=py<br>
sonar.sourceEncoding=UTF-8<br>
sonar.host.url = http://ledszeppellin.sr.ifes.edu.br:9000<br>
sonar.login = leds<br>
sonar.password = ledssonar<br>
<hr>
Onde NOMEDOPROJETO será o nome do repositorio git e NOME DA PASTA COM O CODIGO a pasta onde estarão os arquivos de código do seu repositorio.

Só dar commit e voltar no Travis e ver se tudo deu certo no log.

###Slack
Logar no site do [Slack](https://slack.com/signin) como _leds.slack.com_ e clique continue, em seguida inserir seu login e senha do slack.
Ao logar siga o [link](https://leds.slack.com/apps/manage) e em seguida serão configurados três aplicações: [GitHub](https://leds.slack.com/apps/manage/A0F7YS2SX-github), [TravisCI](https://leds.slack.com/apps/manage/A0F81FP4N-travis-ci) e [Taiga](https://leds.slack.com/apps/manage/A0F7XDUAZ-incoming-webhooks).

Cada um dos links direciona para a página de configuração da respectiva aplicação.

