---
title: Tutorial – Saiba mais sobre Django no Visual Studio, etapa 5
description: Um passo a passo dos conceitos básicos do Django no contexto dos projetos do Visual Studio, especificamente os recursos de autenticação fornecidos pelos modelos Projeto Web do Django.
ms.date: 11/19/2018
ms.prod: visual-studio-dev15
ms.technology: vs-python
ms.topic: tutorial
author: kraigb
ms.author: kraigb
manager: douge
ms.workload:
- python
- data-science
ms.openlocfilehash: cb195e971612124ace53d8eb33b5c3563cd19a12
ms.sourcegitcommit: f61ad0e8babec8810295f039e67629f4bdebeef0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/19/2018
ms.locfileid: "52001224"
---
# <a name="step-5-authenticate-users-in-django"></a>Etapa 5: Autenticar usuários no Django

**Etapa anterior: [Usar o modelo Projeto Web completo do Django](learn-django-in-visual-studio-step-04-full-django-project-template.md)**

Como a autenticação é uma necessidade comum dos aplicativos Web, o modelo "Projeto Web do Django" inclui um fluxo de autenticação básico. (O modelo "Pesquisa Projeto Web do Django" abordado na etapa 6 deste tutorial também inclui o mesmo fluxo.) Ao usar um dos modelos de projeto do Django, o Visual Studio inclui todos os módulos necessários para a autenticação em *settings.py* do projeto do Django.

Nesta etapa, você aprenderá:

> [!div class="checklist"]
> - Como usar o fluxo de autenticação fornecido em modelos do Visual Studio (etapa 5 – 1)

## <a name="step-5-1-use-the-authentication-flow"></a>Etapa 5-1: Usar o fluxo de autenticação

As etapas a seguir acionam o fluxo de autenticação e descrevem as partes envolvidas do projeto:

1. Se você ainda não seguiu as instruções do arquivo *readme.html* na raiz do projeto para criar uma conta de superusuário (administrador), faça isso agora.

1. Execute o aplicativo no Visual Studio usando **Depurar** > **Iniciar Depuração** (**F5**). Quando o aplicativo aparecer no navegador, observe que a opção **Login** aparecerá no canto superior direito da barra de navegação.

    ![Controle de logon na página do aplicativo do Projeto Web do Django](media/django/step05-login-control.png)

1. Abra *templates/app/layout.html* e observe que o elemento `<div class="navbar ...>` contém a marcação `{% include app/loginpartial.html %}`. A marca `{% include %}` instrui o sistema de modelos do Django a efetuar pull do conteúdo do arquivo incluído neste momento no modelo que o contém.

1. Abra *templates/app/loginpartial.html* e observe como ele usa a marcação condicional `{% if user.is_authenticated %}` juntamente com uma marcação `{% else %}` para renderizar diferentes elementos da interface do usuário, dependendo se o usuário realizou a autenticação:

    ```html
    {% if user.is_authenticated %}
    <form id="logoutForm" action="/logout" method="post" class="navbar-right">
        {% csrf_token %}
        <ul class="nav navbar-nav navbar-right">
            <li><span class="navbar-brand">Hello {{ user.username }}!</span></li>
            <li><a href="javascript:document.getElementById('logoutForm').submit()">Log off</a></li>
        </ul>
    </form>

    {% else %}

    <ul class="nav navbar-nav navbar-right">
        <li><a href="{% url 'login' %}">Log in</a></li>
    </ul>

    {% endif %}
    ```

1. Como nenhum usuário é autenticado quando você inicia o aplicativo pela primeira vez, esse código de modelo renderiza apenas o link "Fazer logon" para o caminho relativo "logon". Conforme especificado em *urls.py* (mostrado na seção anterior), essa rota é mapeada para a exibição `django.contrib.auth.views.login`. Essa exibição recebe os seguintes dados:

    ```python
    {
        'template_name': 'app/login.html',
        'authentication_form': app.forms.BootstrapAuthenticationForm,
        'extra_context':
        {
            'title': 'Log in',
            'year': datetime.now().year,
        }
    }
    ```

    Aqui, `template_name` identifica o modelo da página de logon, nesse caso, *templates/app/login.html*. A propriedade `extra_context` é adicionada aos dados de contexto padrão fornecidos para o modelo. Por fim, `authentication_form` especifica uma classe de formulário a ser usada com o logon; no modelo, ele é exibido como o objeto `form`. O valor padrão é `AuthenticationForm` (de `django.contrib.auth.views`). Em vez disso, o modelo de projeto do Visual Studio usa o formulário definido no arquivo *forms.py* do aplicativo:

    ```python
    from django import forms
    from django.contrib.auth.forms import AuthenticationForm
    from django.utils.translation import ugettext_lazy as _

    class BootstrapAuthenticationForm(AuthenticationForm):
        """Authentication form which uses boostrap CSS."""
        username = forms.CharField(max_length=254,
                                   widget=forms.TextInput({
                                       'class': 'form-control',
                                       'placeholder': 'User name'}))
        password = forms.CharField(label=_("Password"),
                                   widget=forms.PasswordInput({
                                       'class': 'form-control',
                                       'placeholder':'Password'}))
    ```

    Como você pode ver, essa classe de formulário deriva de `AuthenticationForm` e, especificamente, substitui os campos de nome de usuário e senha para adicionar texto de espaço reservado. O modelo do Visual Studio inclui esse código explícito considerando que você possa querer personalizar o formulário, por exemplo, adicionando uma validação de força de senha.

1. Quando você navega para a página de logon, o aplicativo renderiza o modelo *login.html*. As variáveis `{{ form.username }}` e `{{ form.password }}` renderizam os formulários `CharField` de `BootstrapAuthenticationForm`. Há também uma seção interna para mostrar erros de validação e um elemento predefinido para efetuar logons em redes sociais, se você optar por adicionar esses serviços.

    ```html
    {% extends "app/layout.html" %}

    {% block content %}

    <h2>{{ title }}</h2>
    <div class="row">
        <div class="col-md-8">
            <section id="loginForm">
                <form action="." method="post" class="form-horizontal">
                    {% csrf_token %}
                    <h4>Use a local account to log in.</h4>
                    <hr />
                    <div class="form-group">
                        <label for="id_username" class="col-md-2 control-label">User name</label>
                        <div class="col-md-10">
                            {{ form.username }}
                        </div>
                    </div>
                    <div class="form-group">
                        <label for="id_password" class="col-md-2 control-label">Password</label>
                        <div class="col-md-10">
                            {{ form.password }}
                        </div>
                    </div>
                    <div class="form-group">
                        <div class="col-md-offset-2 col-md-10">
                            <input type="hidden" name="next" value="/" />
                            <input type="submit" value="Log in" class="btn btn-default" />
                        </div>
                    </div>
                    {% if form.errors %}
                    <p class="validation-summary-errors">Please enter a correct user name and password.</p>
                    {% endif %}
                </form>
            </section>
        </div>
        <div class="col-md-4">
            <section id="socialLoginForm"></section>
        </div>
    </div>

    {% endblock %}
    ```

1. Quando você envia o formulário, o Django tenta autenticar suas credenciais (como as credenciais do superusuário). Se a autenticação falhar, você permanecerá na página atual, mas `form.errors` será definido como true. Se a autenticação for bem-sucedida, o Django navegará para a URL relativa no campo "avançar", `<input type="hidden" name="next" value="/" />`, que, nesse caso, é a página inicial (`/`).

1. Agora, quando a home page for novamente renderizada, a propriedade `user.is_authenticated` será verdadeira quando o modelo *loginpartial.html* for renderizado. Como resultado, você verá uma mensagem **Olá, (nome de usuário)** e **Fazer logoff**. Você pode usar `user.is_authenticated` em outras partes do aplicativo para verificar a autenticação.

    ![Mensagem de Olá e controle de logon na página do aplicativo do Projeto Web do Django](media/django/step05-logoff-control.png)

1. Para verificar se o usuário autenticado está autorizado a acessar recursos específicos, você precisa recuperar as permissões específicas do usuário do banco de dados. Para obter mais informações, confira [Using the Django authentication system](https://docs.djangoproject.com/en/2.0/topics/auth/default/#permissions-and-authorization) (Usando o sistema de autenticação do Django) (documentos do Django).

1. O superusuário ou o administrador, em particular, está autorizado a acessar as interfaces de administrador internas do Django usando as URLs relativas "/admin/" e "/admin/doc/". Para habilitar essas interfaces, faça o seguinte:

    1. Instale o pacote Python docutils em seu ambiente. Uma boa maneira de fazer isso é adicionar "docutils" ao arquivo *requirements.txt* e, em seguida, no **Gerenciador de Soluções**, expandir o projeto, expandir o nó **Ambientes do Python** e, em seguida, clicar com o botão direito do mouse no ambiente que você está usando e selecionar **Instalar do requirements.txt**.

    1. Abra o projeto do Django *urls.py* e remova os comentários padrão das seguintes entradas:

        ```python
        from django.conf.urls import include
        from django.contrib import admin
        admin.autodiscover()

        # ...
        urlpatterns = [
            # ...
            url(r'^admin/doc/', include('django.contrib.admindocs.urls')),
            url(r'^admin/', include(admin.site.urls)),
        ]
        ```

    1. No arquivo *settings.py* do projeto do Django, navegue até a coleção `INSTALLED_APPS` e adicione `'django.contrib.admindocs'`.

    1. Quando você reiniciar o aplicativo, navegue até "/admin/" e "/admin/doc/" e execute tarefas, como criar contas de usuário adicionais.

        ![Interface de administrador do Django](media/django/step05-administrator-interface.png)

1. A parte final do fluxo de autenticação é fazer logoff. Como você pode ver em *loginpartial.html*, o link **Fazer logoff** apenas faz um POST para a URL relativa "/login", que é manipulada pela exibição interna `django.contrib.auth.views.logout`. Essa exibição não exibe nenhuma interface do usuário e apenas navega para a home page (conforme mostrado em *urls.py* para o padrão "^logout$"). Se você quiser exibir uma página de logoff, primeiro altere o padrão da URL conforme mostrado a seguir para adicionar uma propriedade "template_name" e remover a propriedade "next_page":

    ```python
    url(r'^logout$',
        django.contrib.auth.views.logout,
        {
            'template_name': 'app/loggedoff.html',
            # 'next_page': '/',
        },
        name='logout')
    ```

    Em seguida, crie *templates/app/loggedoff.html* com o seguinte conteúdo (mínimo):

    ```html
    {% extends "app/layout.html" %}
    {% block content %}
    <h3>You have been logged off</h3>
    {% endblock %}
    ```

    O resultado se parece com o seguinte:

    ![Página de logoff adicionada](media/django/step05-logged-off-page.png)

1. Quando terminar, interrompa o servidor e, mais uma vez, confirme suas alterações no controle do código-fonte.

### <a name="question-what-is-the-purpose-of-the--csrftoken--tag-that-appears-in-the-form-elements"></a>Pergunta: Qual é a finalidade da marcação {% csrf_token %} exibida nos elementos \<form\>?

Resposta: A marcação `{% csrf_token %}` inclui a [proteção interna contra solicitações intersites forjadas (csrf)](https://docs.djangoproject.com/en/2.0/ref/csrf/) do Django (documentos do Django). Normalmente, essa marca é adicionada a qualquer elemento que envolva métodos de solicitação POST, PUT ou DELETE, como um formulário. Em seguida, a função de renderização de modelo (`render`) insere a proteção necessária.

## <a name="next-steps"></a>Próximas etapas

> [!div class="nextstepaction"]
> [Usar o modelo Pesquisas Projeto Web do Django](learn-django-in-visual-studio-step-06-polls-django-web-project-template.md)

## <a name="go-deeper"></a>Aprofunde-se um pouco mais

- [Autenticação de usuário no Django](https://docs.djangoproject.com/en/2.0/topics/auth/) (docs.djangoproject.com)
- Código-fonte do tutorial no GitHub: [Microsoft/python-sample-vs-learning-django](https://github.com/Microsoft/python-sample-vs-learning-django)
