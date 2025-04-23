# Como configurar o ambiente de trabalho

# Configurar o ambiente virtual

---

- Rodar `python -m venv venv` para criar um ambiente virtual.
- Ativar o ambiente virtual: `venv\Scripts\activate.ps1`
- Instalar o Flask com: `pip install flask`

# Criação de pastas

---

- Criar uma pasta para o projeto.
- Dentro dela, criar a pasta `static` para armazenar arquivos estáticos (CSS, JS, IMG).
- Criar a pasta `templates` para armazenar arquivos HTML.

# **Criar o arquivo app.py**

---

- Importar Flask.
- Criar a aplicação Flask.
- Definir as rotas.
- Configurar o servidor para rodar.

```python
from flask import Flask, render_template

app = Flask(__name__)

@app.route("/")
def homepage():
    context = {}
    return render_template("homepage.html", context=context)

@app.route("/add_produto")
def add_produto():
    context = {}
    return render_template("add_produto.html", context=context)

@app.route("/del_produto")
def del_produto():
    context = {}
    return render_template("del_produto.html", context=context)

@app.route("/up_produto")
def up_produto():
    context = {}
    return render_template("up_produto.html", context=context)

if __name__ == "__main__":
    app.run(debug=True, host="0.0.0.0")
```

# **Criar templates**

---

- Criar `templates/index.html` e outras páginas necessárias.
- Usar `<link rel="stylesheet" type="text/css" href="{{url_for('static', filename='css/style_nav.css')}}">` e `<link rel="stylesheet" type="text/css " href="{{url_for('static', filename='css/style_footer.css')}}">` para carregar CSS da nav e do footer no `index.html`.
- Cada rota tem seu arquivo html:
    
    ![image.png](attachment:86382653-6a0a-494a-9440-7268985c6db7:image.png)
    

# Criar static

---

- Criar `static/style.css` para estilização.
- Criar os arquivos `js` e `img`
    
    ![image.png](attachment:13bdc7be-c664-441f-afa1-3ac13069dd48:image.png)
    
- Dentro de `css` criar cada arquivo para cada html:
    
    ![image.png](attachment:ffd8870e-58b1-4a0d-94d1-73a96d930a83:image.png)
    

# Rodar o servidor e testar

---

- Executar `python app.py`.
- Acessar `http://127.0.0.1:5000/` no navegador.
