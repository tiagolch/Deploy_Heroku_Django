# Deploy_Heroku_Django
## Procedimento com base no video do [Samuel Gonçalves](https://www.youtube.com/watch?v=8l8xwvRO1_U&ab_channel=SamuelGon%C3%A7alves)


1. Criar projeto no Heroku

2. Instalar heroku-cli
    * sudo snap install --classic heroku [link](https://devcenter.heroku.com/articles/heroku-cli)
    * heroku login
	* git init
	* heroku git:remote -a \<nome-do-projeto\>
  
3. Instalando o Gunicorn para servir a aplicação no Heroku
	* pip install gunicorn
  
4. instalar o django-on-heroku.
	* pip install django-on-heroku
	* Em settings importar
		* import django_on_heroku
	* No Final do arquivo settings colocar
		* django_on_heroku.settings(locals())
  
5. [Desacoplando as variáveis de ambiente](https://pypi.org/project/python-decouple/)
	* Instalar o python-decouple:
		* pip install python-decouple
	* Criar o arquivo .env na raiz do projeto
	* Inserir no arquivo
		* DEBUG=True
		* SECRET_KEY=<chave_sem _aspas>
	* Em Settings fazer o import
		* from decouple import config
	* Na variavel DEBUG substituir True por:
		* DEBUG = config('DEBUG', cast=bool, default=False)
	* Na variavel SECRET_KEY substituir por:
		* SECRET_KEY = config('SECRET_KEY')
  
6. Preparando as dependências para instalar no Heroku
	* pip freeze > requirements.txt
  
7. Determinando qual versão do Python o Heroku vai utilizar
	* Criar arquivo runtime.txt na raiz do projeto e colocar a versão do python suportado pelo Heroku. [verificar aqui](https://devcenter.heroku.com/articles/python-support).
		* exemplo:  python-3.9.7
  
8. Configurando o arquivo Procfile
	* Criar arquivo Procfile na raiz do projeto.
	* inserir no arquivo o seguinte:
		* web: gunicorn \<nomedoprojeto\>.wsgi --log-file -
  
9. Criar .gitignore na raiz do projeto
	* Adicionar no arquivo o seguinte:
		* .idea/
		* db.sqlite3
		* .env
  
10. Fazendo o Deploy no Heroku
	* git add .
	* git commit -am "make it better"
	* git push heroku master
  
11. Executando o migrate e criando um super usuário no Heroku
	* heroku run python manage.py migrate
	* heroku run python manage.py createsuperuser
  
12. Atribuir DEBUG false no heroku (opcional)
	* Em settings > config vars



