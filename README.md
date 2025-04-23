# Passo a passo - aplicação Django

---

- Python inclui um banco de dados leve chamado SQLite então você não precisará configurar um banco de dados agora.
- https://www.hashtagtreinamentos.com/projeto-em-django-python?gad_source=1&gbraid=0AAAAADLlh88OkPZfB3cvgf1IP9wMRMKE2&gclid=Cj0KCQjwqv2_BhC0ARIsAFb5Ac9J2SYefFMQvqYlCcR_85bRWejHSEix8uEFngmNIFsxEk840LrQ45UaAhMdEALw_wcB
- https://docs.djangoproject.com/en/5.2/intro/tutorial01/

### Passo a passo:

---

1. Ambiente Virtual
2. Instalar o Framework Django
3. Criar o projeto Django
4. Criar o App
5. Configurar o settings
6. Configurar a Url’s(App)
7. Criar template
8. Configurar o settings com o template
9. Criar pastas static e media
10. Configurar o settings
11. Configurar um super user
12. Rodar as migrações
13. **criar uma modal

# Configurar o ambiente virtual

---

1. Criar o ambiente virtual pelo terminal
    
    ```python
    python -m venv venv
    ```
    

2. Entrar no ambiente virtual
    
    ```python
    venv\Scripts\activate.ps1
    ```
    

# **Instalando Django**

---

1. No vscode, dentro da pasta do projeto com django, executar o comando
    
    ```python
    pip install Django
    ```
    

2. Conferir se todo o procedimento foi feito corretamente executando:
    
    ```python
    django-admin
    ```
        

# **Iniciar um Projeto no Django**

---

1. Executar o comando para iniciar um projeto
    
    ```python
    django-admin startproject teste01
    ```
    

        

2. Abrir a pasta `teste01` no terminal do projeto, executando o comando:
    
    ```python
    cd teste01
    ```
    

3. Executar o **runserver:**
    
    ```python
    python manage.py runserver
    ```
    
        
    
    Esse comando é o que colocará nosso site no ar. Depois de executarmos a primeira vez o nosso projeto em Django, também surgirá o banco de dados (**db.sqlite3**) dentro da pasta dele.
    

        

  

### **Estrutura do Projeto**

---

Vamos revisar a estrutura do nosso projeto. Assim que criarmos nosso projeto, teremos o arquivo **`manage.py`** e a pasta com o mesmo nome do projeto, além dos demais arquivos.

Dentro dessa pasta, teremos o arquivo **`__init__.py`**, que estará vazio. Esse arquivo indica para o Python que essa pasta **`teste01`** faz parte de um módulo Python.

Os arquivos **`asgi.py`** e **`wsgi.py`** são os arquivos de configuração que, quando colocarmos o site em um servidor, o servidor saberá como lidar com esse projeto. Utilizaremos esses arquivos apenas no momento de fazer o **deploy** do projeto.

No arquivo **`urls.py`**, é onde definiremos os links, os endereços das páginas do nosso site. Já o **`settings.py`** é onde iremos de fato configurar o projeto. É dentro desse arquivo que definiremos as configurações e as informações essenciais para o nosso site funcionar corretamente.


    

# **Aplicativos(APP) dentro do Projeto**

---

1. Assim, em todo projeto Django, após criar o projeto, você irá acessar a página do projeto e dentro dela executar:
    
    ```python
    python manage.py startapp polls #no exemplo é chamado de polls
    ```
    
        

### **Arquivos dentro dos Aplicativos**

---

Em cada aplicativo criado, também teremos alguns arquivos que serão gerados automaticamente. Entre eles, um arquivo **`__init__.py`** que também iniciará vazio e indicará que a pasta **loja** é um aplicativo do nosso projeto.

A pasta **`migrations`** será responsável por gerenciar e registrar as modificações no banco de dados.

O **`admin.py`** será onde você configurará o que será exibido na tela de administração do site, ou seja, o que o usuário que é administrador do site visualizará ao acessá-lo.

No **`apps.py`**, você irá configurar e registrar os aplicativos referentes à aplicação **`nomedoaplicativo`**. Por padrão, o Django já irá criar o app referente à sua aplicação, e costumamos deixar apenas um app por aplicação mesmo.

O arquivo **`tests.py`**, como o próprio nome sugere, serve para que você execute os testes da sua aplicação.

Por fim, temos dois arquivos muito importantes: o **`models.py`** e o **`views.py`**. Esses arquivos são os que você mais utilizará e modificará.

No **`models.py`**, é onde você definirá as informações que serão registradas no seu sistema e no seu banco de dados. O **`views.py`** é onde definirá a lógica por trás do seu site, ou seja, onde você definirá as funções ou classes que serão executadas quando o usuário acessar um link específico do seu site.

    

# Começando uma homepage

---

1. Dentro da pasta `views` do `polls`, adicionar esse código:
    
    ```python
    from django.http import HttpResponse
    
    def index(request):
        return HttpResponse("Hello, world. You're at the polls index.")
    ```
    

2. Na pasta `polls`, criar o arquivo `urls.py`
    
    Dentro do arquivo, adicionar esse código:
    
    ```python
    from django.urls import path # trazer a função de url
    
    from . import views # trazer tudo que tiver em views
    
    urlpatterns = [
        path("", views.index, name="index"),
    ]
    ```
    

3. No arquivo `urls.py` da pasta `teste01` , adicionar esse código:
    
    ```python
    from django.contrib import admin
    from django.urls import include, path
    
    urlpatterns = [
        path("", include("polls.urls")),
        path("admin/", admin.site.urls),
    ]
    ```
    

4. Dentro do arquivo `settings.py` modifique a parte de “INSTALLED_APPS” com o nome do aplicativo criado:
    
    ```python
    INSTALLED_APPS = [
        'django.contrib.admin',
        'django.contrib.auth',
        'django.contrib.contenttypes',
        'django.contrib.sessions',
        'django.contrib.messages',
        'django.contrib.staticfiles',
        'polls' #nome do app que eu criei
    ]
    ```
    

# Criar e configurar um template

---

1. Criar a pasta templates e a index dentro do APP
        

2. Mudar as `settings.py` na parte de templates
    
    ```python
    TEMPLATES = [
        {
            'BACKEND': 'django.template.backends.django.DjangoTemplates',
            'DIRS': [os.path.join(BASE_DIR, 'templates')],  # Corrigido aqui
            'APP_DIRS': True,
            'OPTIONS': {
                'context_processors': [
                    'django.template.context_processors.request',
                    'django.contrib.auth.context_processors.auth',
                    'django.contrib.messages.context_processors.messages',
                ],
            },
        },
    ]
    ```
    

3. Em views, dentro do pools(APP), retornar a página criada, no caso o index
    
    ```python
    from django.http import HttpResponse
    from django.shortcuts import render
    
    def index(request):
        return render(request, "index.html")
    ```
    

4. Em `urls` dentro de `teste01`, adicione a urlpatterns no código. O código completo ficara assim:
    
    ```python
    from django.contrib import admin
    from django.urls import include, path
    from django.conf import settings
    from django.conf.urls.static import static
    
    urlpatterns = [
        path("", include("polls.urls")),
        path("admin/", admin.site.urls),
    ]
    
    if settings.DEBUG:
        urlpatterns += static(settings.MEDIA_URL, document_root=settings.MEDIA_ROOT)
        urlpatterns += static(settings.STATIC_URL, document_root=settings.STATIC_ROOT)
    ```
    

# Pastas static e media

---

1. Na pasta raiz do projeto, nesse caso, TESTE01, criar as pastas `static` e `media` .
    - Pastas:
        
        ![image.png](attachment:421233ac-bc1b-45e2-b4f0-050f1fd32393:image.png)
        

2. No `settings.py` configurar ele com as pastas novas. Adicione isso ao arquivo.
    
    ```python
    # começo do codigo
    import os
    
    # fim do codigo
    # Arquivos estáticos (CSS, JS, imagens)
    STATIC_URL = '/static/'
    STATICFILES_DIRS = [os.path.join(BASE_DIR, 'static')]
    STATIC_ROOT = os.path.join(BASE_DIR, 'staticfiles')  # para produção
    
    # Arquivos de mídia (uploads)
    MEDIA_URL = '/media/'
    MEDIA_ROOT = os.path.join(BASE_DIR, 'media')
    ```
    

3. Modificar a pasta de `urls.py` da pasta do projeto (`teste01`), 
    
    ```python
    # importar
    from django.conf import settings
    from django.conf.urls.static import static
    
    urlpatterns = [
        # continuar com as urls aqui
    ]
    
    if settings.DEBUG:
        urlpatterns += static(settings.MEDIA_URL, document_root=settings.MEDIA_ROOT)
        urlpatterns += static(settings.STATIC_URL, document_root=settings.STATIC_ROOT)
    ```
    

# Configurar um super user

---

1. Para criar um super user, rodar o comando no terminal:
    
    ```python
    python manage.py createsuperuser
    ```
    

2. Para aplicar as migrações do Django e do app:
    
    ```python
    python manage.py makemigrations
    
    python manage.py migrate
    ```
    

3. No navegador, adicionar a rota `/admin/` do lado na url e fazer o login do super user
