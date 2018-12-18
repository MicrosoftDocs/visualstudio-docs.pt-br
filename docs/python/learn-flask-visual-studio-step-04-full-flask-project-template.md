---
title: Tutorial – Saiba mais sobre o Flask no Visual Studio, etapa 4
description: Um passo a passo das noções básicas do Flask no contexto dos projetos do Visual Studio, especificamente as funcionalidades fornecidas pelos modelos Projeto Web do Flask e Projeto Web do Flask/Jade.
ms.date: 09/04/2018
ms.prod: visual-studio-dev15
ms.technology: vs-python
ms.topic: tutorial
author: kraigb
ms.author: kraigb
manager: douge
ms.workload:
- python
- data-science
ms.openlocfilehash: 6e9171b7f44a51380fd086798b4ab9c50fa98729
ms.sourcegitcommit: 6944ceb7193d410a2a913ecee6f40c6e87e8a54b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/05/2018
ms.locfileid: "43775952"
---
# <a name="step-4-use-the-full-flask-web-project-template"></a>Etapa 4: Usar o modelo Projeto Web do Flask completo

**Etapa anterior: [Fornecer arquivos estáticos, adicionar páginas e usar a herança do modelo](learn-flask-visual-studio-step-03-serve-static-files-add-pages.md)**

Agora que você explorou as noções básicas do Flask ao compilar um aplicativo com o modelo "Projeto de Aplicativo em Branco do Flask" no Visual Studio, é possível compreender facilmente o aplicativo mais completo produzido pelo modelo "Projeto Web do Flask".

Nesta etapa, agora você poderá:

> [!div class="checklist"]
> - Criar um aplicativo Web do Flask mais completo usando o modelo "Projeto Web do Flask" e examinar a estrutura do projeto (etapa 4-1)
> - Entender os modos de exibição e os modelos de página criados pelo modelo de projeto, que consistem em três páginas que são herdadas a partir de um modelo de página de base e que emprega bibliotecas JavaScript estáticas como jQuery e Bootstrap (etapa 4-2)
> - Entender o roteamento de URL fornecido pelo modelo (etapa 4-3)

Este artigo aplica-se também ao modelo "Projeto Web do Flask/Jade", que produz um aplicativo idêntico ao do "Projeto Web do Flask" usando o mecanismo de modelagem do Jade, em vez do Jinja. Detalhes adicionais são incluídos ao fim deste artigo.

## <a name="step-4-1-create-a-project-from-the-template"></a>Etapa 4-1: Criar um projeto com base no modelo

1. No Visual Studio, acesse **Gerenciador de Soluções**, clique com o botão direito do mouse na solução **LearningFlask** criada anteriormente neste tutorial e selecione **Adicionar** > **Novo Projeto**. (Como alternativa, se você quiser usar uma nova solução, selecione **Arquivo** > **Novo** > **Projeto**).

1. Na caixa de diálogo Novo Projeto, pesquise e selecione o modelo **Projeto Web do Flask**, nomeie o projeto "FlaskWeb" e selecione **OK**.

1. Como o modelo novamente inclui um arquivo *requirements.txt*, o Visual Studio solicita o local em que essas dependências serão instaladas. Escolha a opção **Instalar em um ambiente virtual** e, na caixa de diálogo **Adicionar Ambiente Virtual**, selecione **Criar** para aceitar os padrões.

1. Depois que o Visual Studio concluir a configuração do ambiente virtual, defina o projeto **FlaskWeb** para ser o padrão para a solução do Visual Studio clicando com o botão direito do mouse nesse projeto em **Gerenciador de Soluções** e selecionando **Definir como Projeto de Inicialização**. O projeto de inicialização, mostrado em negrito, é o que é executado quando você inicia o depurador.

    ![Gerenciador de Soluções mostrando o projeto FlaskWeb como o projeto de inicialização](media/flask/step04-second-project-in-solution-set-as-startup-project.png)

1. Selecione **Depurar** > **Iniciar Depuração** (**F5**) ou use o botão **Servidor Web** na barra de ferramentas para executar o servidor:

    ![Executar o botão da barra de ferramentas do servidor Web no Visual Studio](media/flask/run-web-server-toolbar-button.png)

1. O aplicativo criado pelo modelo tem três páginas, Página inicial, Sobre e Contato, que você navega usando a barra de navegação. Levar um minuto ou dois para examinar as diferentes partes do aplicativo. Para autenticar com o aplicativo por meio do comando **Login**, use as credenciais de superusuário criadas anteriormente.

    ![Exibição completa do navegador do aplicativo Projeto Web do Flask](media/flask/step04-full-app-desktop-view.png)

1. O aplicativo criado pelo modelo "Projeto Web do Flask" usa Bootstrap para layout responsivo que acomoda fatores de forma móveis. Para ver essa capacidade de resposta, redimensione o navegador para uma exibição específica para que o conteúdo seja renderizado verticalmente e a barra de navegação se transforme em um ícone de menu:

    ![Exibição (estreita) móvel do aplicativo Projeto Web do Flask](media/flask/step04-full-app-mobile-view.png)

1. Você pode deixar o aplicativo em execução para as seções a seguir.

    Caso deseje interromper o aplicativo e [confirmar as alterações no controle do código-fonte](learn-flask-visual-studio-step-02-create-app.md#commit-to-source-control), primeiro abra a página **Alterações** no **Team Explorer**, clique com o botão direito do mouse na pasta do ambiente virtual (provavelmente **env**) e selecione **Ignorar estes itens locais**.

### <a name="examine-what-the-template-creates"></a>Examine o que o modelo cria

O modelo "Projeto Web do Flask" cria a estrutura abaixo. O conteúdo é muito semelhante ao que você criou nas etapas anteriores. A diferença é que o modelo "Projeto Web do Flask" contém mais estrutura na pasta *static*, porque ela inclui jQuery e Bootstrap para obter um design responsivo. O modelo também adiciona uma página Contato. Em geral, se você seguiu as etapas anteriores deste tutorial, você já deve conhecer tudo com base no modelo.

- Arquivos na raiz do projeto:
  - *runserver.py*, um script para executar o aplicativo em um servidor de desenvolvimento.
  - *requirements.txt* contendo uma dependência do Flask 0.x.
- A pasta *FlaskWeb* contém todos os arquivos de aplicativo:
  - *\_\_init.py\_\_* marca o código do aplicativo como um módulo do Python, cria o objeto do Flask e importa as exibições do aplicativo.
  - *views.py* contém o código para renderizar páginas.
  - A pasta *static* contém subpastas chamadas *content* (arquivos CSS), *fonts* (arquivos de fonte) e *scripts* (arquivos JavaScript).
  - A pasta *templates* contém um modelo base *layout.html* juntamente com *about.html*, *contact.html* e *index.html*, para páginas específicas que estendem *layout.html*.

### <a name="question-is-it-possible-to-share-a-virtual-environment-between-visual-studio-projects"></a>Pergunta: É possível compartilhar um ambiente virtual entre projetos do Visual Studio?

Resposta: Sim, mas faça isso sabendo que diferentes projetos provavelmente usam pacotes diferentes ao longo do tempo e, portanto, um ambiente virtual compartilhado deve conter todos os pacotes para todos os projetos que o usam.

No entanto, para usar um ambiente virtual existente, faça o seguinte:

1. Quando for solicitado a instalar dependências no Visual Studio, selecione a opção **Eu os instalarei por conta própria** opção.
1. No **Gerenciador de Soluções**, clique com o botão direito do mouse no nó **Ambientes do Python** e escolha **Adicionar Ambiente Virtual Existente**.
1. Navegue até e selecione a pasta que contém o ambiente virtual e selecione **OK**.

## <a name="step-4-2-understand-the-views-and-page-templates-created-by-the-project-template"></a>Etapa 4-2: Entender os modos de exibição e os modelos de página criados pelo modelo de projeto

Quando você executa o projeto, observe que o aplicativo contém três modos de exibição: Página inicial, Sobre e Contato. O código dessas exibições é encontrado na pasta *FlaskWeb/views.py*. Cada função de exibição simplesmente chama `flask.render_template` com o caminho para um modelo e uma lista de variáveis de argumentos para os valores darem ao modelo. Por exemplo, a página Sobre é tratada pela função `about` (cujo decorador fornece o roteamento de URL):

```python
@app.route('/about')
def about():
    """Renders the about page."""
    return render_template(
        'about.html',
        title='About',
        year=datetime.now().year,
        message='Your application description page.'
    )
```

As funções `home` e `contact` são quase idênticas, com decoradores semelhantes e argumentos ligeiramente diferentes.

Os modelos estão localizados na pasta *templates* do aplicativo. O modelo base, *layout.html*, é o mais abrangente. Ele se refere a todos os arquivos estáticos necessários (JavaScript e CSS), define um bloco nomeado "conteúdo" que outras páginas substituem e fornece outro bloco chamado "scripts". Os seguintes trechos anotados de *layout.html* mostram essas áreas específicas:

```html
<!DOCTYPE html>
<html>
<head>
    <meta charset="utf-8" />

    <!-- Define a viewport for Bootstrap's responsive rendering -->
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>{{ title }} - My Flask Application</title>

    <link rel="stylesheet" type="text/css" href="/static/content/bootstrap.min.css" />
    <link rel="stylesheet" type="text/css" href="/static/content/site.css" />
    <script src="/static/scripts/modernizr-2.6.2.js"></script>
</head>

<body>
    <!-- Navbar omitted -->

    <div class="container body-content">
        <!-- "content" block that pages are expected to override -->
        {% block content %}{% endblock %}
        <hr />
        <footer>
            <p>&copy; {{ year }} - My Flask Application</p>
        </footer>
    </div>

    <!-- Additional scripts; use the "scripts" block to add page-specific scripts.  -->
    <script src="/static/scripts/jquery-1.10.2.js"></script>
    <script src="/static/scripts/bootstrap.js"></script>
    <script src="/static/scripts/respond.js"></script>
    {% block scripts %}{% endblock %}

</body>
</html>
```

Cada um dos modelos de página individual, *about.html*, *contact.html* e *index.html*, estende o modelo base *layout.html*. *about.html* é o mais simples e mostra as marcações `{% extends %}` e `{% block content %}`:

```html
{% extends "app/layout.html" %}

{% block content %}

<h2>{{ title }}.</h2>
<h3>{{ message }}</h3>

<p>Use this area to provide additional information.</p>

{% endblock %}
```

*index.html* e *contact.html* usam a mesma estrutura e fornecem mais conteúdo no bloco "conteúdo".

## <a name="the-flaskjade-web-project-template"></a>O modelo Projeto Web do Flask/Jade

Conforme observado no início deste artigo, o Visual Studio fornece um modelo "Projeto Web do Flask/Jade", que cria um aplicativo visualmente idêntico ao produzido pelo "Projeto Web do Flask". A principal diferença é que ele usa o mecanismo de modelagem Jade, que é uma extensão do Jinja que implementa os mesmos conceitos com uma linguagem mais sucinta. Especificamente, o Jade usa palavras-chave em vez de marcas entre delimitadores {% %}, por exemplo, e permite que você se refira a elementos HTML e estilos CSS usando palavras-chave.

Para habilitar o Jade, o modelo de projeto inclui primeiro o pacote pyjade em *requirements.txt*. 

O arquivo *\_\_init\_\_.py* do aplicativo contém uma linha para

```python
app.jinja_env.add_extension('pyjade.ext.jinja.PyJadeExtension')
```
Na pasta *templates*, são exibidos arquivos *.jade* em vez de modelos *.html*, e as exibições em *views.py* referenciam esses arquivos em suas chamadas a `flask.render_template`. Caso contrário, o código de modos de exibição é o mesmo.

Abrindo um dos arquivos *.jade*, você pode ver a expressão mais sucinta de um modelo. Por exemplo, este é o conteúdo de *templates/layout.jade*, conforme criado pelo modelo "Projeto Web do Flask/Jade":

```jade
doctype html
html
  head
    meta(charset='utf-8')
    meta(name='viewport', content='width=device-width, initial-scale=1.0')
    title #{title} - My Flask/Jade Application
    link(rel='stylesheet', type='text/css', href='/static/content/bootstrap.min.css')
    link(rel='stylesheet', type='text/css', href='/static/content/site.css')
    script(src='/static/scripts/modernizr-2.6.2.js')
  body
    .navbar.navbar-inverse.navbar-fixed-top
      .container
        .navbar-header
          button.navbar-toggle(type='button', data-toggle='collapse', data-target='.navbar-collapse')
            span.icon-bar
            span.icon-bar
            span.icon-bar
          a.navbar-brand(href='/') Application name
        .navbar-collapse.collapse
          ul.nav.navbar-nav
            li
              a(href='/') Home
            li
              a(href='/about') About
            li
              a(href='/contact') Contact
    .container.body-content
      block content
      hr
      footer
        p &copy; #{year} - My Flask/Jade Application

    script(src='/static/scripts/jquery-1.10.2.js')
    script(src='/static/scripts/bootstrap.js')
    script(src='/static/scripts/respond.js')

    block scripts
```

E este é o conteúdo de *templates/about.jade*, mostrando o uso de `#{ <name>}` para espaços reservados:

```jade
extends layout

block content
  h2 #{title}.
  h3 #{message}
  p Use this area to provide additional information.
```

Fique à vontade para fazer experimentos com sintaxes do Jinja e do Jade para ver qual funciona melhor para você.

## <a name="next-steps"></a>Próximas etapas

> [!div class="nextstepaction"]
> [O modelo Pesquisa Projeto Web de Flask](learn-flask-visual-studio-step-05-polls-flask-web-project-template.md)

## <a name="go-deeper"></a>Aprofunde-se um pouco mais

- [Como gravar seu primeiro aplicativo do Flask, parte 4 – Modos de exibição genéricos e de formulários](https://docs.djangoproject.com/en/2.0/intro/tutorial04/) (docs.djangoproject.com)
- [Jade no GitHib (Documentação)](https://github.com/liuliqiang/pyjade) (github.com)
- Código-fonte do tutorial no GitHub: [Microsoft/python-sample-vs-learning-flask](https://github.com/Microsoft/python-sample-vs-learning-flask)
