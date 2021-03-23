---
title: Tutorial Aprenda a usar o Django no Visual Studio, etapa 5, autenticação
titleSuffix: ''
description: Um passo a passo dos conceitos básicos do Django no contexto dos projetos do Visual Studio, especificamente os recursos de autenticação fornecidos pelos modelos Projeto Web do Django.
ms.date: 11/19/2018
ms.topic: tutorial
author: JoshuaPartlow
ms.author: joshuapa
manager: jmartens
ms.custom: seodec18
ms.workload:
- python
- data-science
ms.openlocfilehash: 3f589aed953a852cb57570988d914f77b2fa10b2
ms.sourcegitcommit: f1dff6c4532c43b0444aa12ea57e90bb7dba6fba
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/23/2021
ms.locfileid: "104806011"
---
# <a name="step-5-authenticate-users-in-django"></a>Etapa 5: Autenticar usuários no Django

**Etapa anterior: [Usar o modelo Projeto Web completo do Django](learn-django-in-visual-studio-step-04-full-django-project-template.md)**

::: moniker range="vs-2017"
Como a autenticação é uma necessidade comum dos aplicativos Web, o modelo "Projeto Web do Django" inclui um fluxo de autenticação básico. (O modelo "pesquisas do Django Web Project" abordado na etapa 6 deste tutorial também inclui o mesmo fluxo.) Ao usar qualquer um dos modelos de projeto Django, o Visual Studio inclui todos os módulos necessários para autenticação no *Settings.py* do projeto Django.
::: moniker-end

::: moniker range=">=vs-2019"
Como a autenticação é uma necessidade comum dos aplicativos Web, o modelo "Projeto Web do Django" inclui um fluxo de autenticação básico. Ao usar um dos modelos de projeto do Django, o Visual Studio inclui todos os módulos necessários para a autenticação em *settings.py* do projeto do Django.
::: moniker-end

Nesta etapa, você aprenderá:

> [!div class="checklist"]
> - Como usar o fluxo de autenticação fornecido em modelos do Visual Studio (etapa 5 – 1)

## <a name="step-5-1-use-the-authentication-flow"></a>Etapa 5-1: Usar o fluxo de autenticação

As etapas a seguir acionam o fluxo de autenticação e descrevem as partes envolvidas do projeto:

1. Se você ainda não seguiu as instruções do arquivo *readme.html* na raiz do projeto para criar uma conta de superusuário (administrador), faça isso agora.

1. Execute o aplicativo do Visual Studio usando **depurar**  >  **Iniciar Depuração** (**F5**). Quando o aplicativo aparecer no navegador, observe que a opção **Login** aparecerá no canto superior direito da barra de navegação.

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

### <a name="question-what-is-the-purpose-of-the--csrf_token--tag-that-appears-in-the-form-elements"></a>Pergunta: Qual é a finalidade da marca {% csrf_token%} que aparece nos \<form\> elementos?

Resposta: A marcação `{% csrf_token %}` inclui a [proteção interna contra solicitações intersites forjadas (csrf)](https://docs.djangoproject.com/en/2.0/ref/csrf/) do Django (documentos do Django). Normalmente, essa marca é adicionada a qualquer elemento que envolva métodos de solicitação POST, PUT ou DELETE, como um formulário. Em seguida, a função de renderização de modelo (`render`) insere a proteção necessária.

## <a name="next-steps"></a>Próximas etapas

::: moniker range="vs-2017"
- [Usar o modelo Pesquisas Projeto Web do Django](learn-django-in-visual-studio-step-06-polls-django-web-project-template.md)
::: moniker-end

::: moniker range=">=vs-2019"
> [!Note]
> Se você tiver confirmando sua solução do Visual Studio para controle de origem ao longo deste tutorial, agora será um bom momento para fazer outra confirmação. A solução deve corresponder ao código-fonte do tutorial no GitHub: [Microsoft/python-sample-vs-learning-django](https://github.com/Microsoft/python-sample-vs-learning-django).

Agora você explorou todo o inteiro dos modelos "projeto Web Django em branco" e "projeto Web Django" no Visual Studio. Você aprendeu as noções básicas do Django como o uso de modelos e modos de exibição e explorou roteamento, autenticação e uso de modelos de banco de dados. Agora você deverá ser capaz de criar um aplicativo Web por sua conta com os modos de exibição e os modelos de que precisar.

A execução de um aplicativo Web no computador de desenvolvimento é apenas uma etapa para disponibilizar o aplicativo para seus clientes. As próximas etapas podem incluir as seguintes tarefas:

- Implante o aplicativo Web em um servidor de produção, como o Serviço de Aplicativo do Azure. Confira [Publicar no Serviço de Aplicativo do Azure](publishing-python-web-applications-to-azure-from-visual-studio.md).

- Personalizar a página 404 criando um modelo chamado *templates/404.html*. Quando presente, o Django usa esse modelo, em vez de seu padrão. Para saber mais, veja [Modos de exibição de erro](https://docs.djangoproject.com/en/2.0/ref/views/#error-views) na documentação do Django.

- Escreva testes de unidade em *tests.py*; os modelos de projeto do Visual Studio fornecem pontos iniciais para eles e mais informações podem ser encontradas em [Escrevendo seu primeiro aplicativo do Django, parte 5 – teste](https://docs.djangoproject.com/en/2.0/intro/tutorial05/) e [Testando no Django](https://docs.djangoproject.com/en/2.0/topics/testing/) na documentação do Django.

- Altere o aplicativo de SQLite para um repositório de dados de nível de produção como PostgreSQL, MySQL e SQL Server (que pode ser hospedado no Azure). Conforme descrito em [Quando usar o SQLite](https://www.sqlite.org/whentouse.html) (sqlite.org), o SQLite funciona bem para sites de tráfego baixo a médio com menos de 100 mil acessos por dia, mas não é recomendado para volumes maiores. Também é limitado a um único computador, de modo que ele não pode ser usado em qualquer cenário de vários servidores, como balanceamento de carga e replicação geográfica. Para obter informações sobre o suporte do Django para outros bancos de dados, veja [Instalação do banco de dados](https://docs.djangoproject.com/en/2.0/intro/tutorial02/#database-setup). Você também pode usar o [SDK do Azure para Python](/azure/python/) para trabalhar com serviços de armazenamento do Azure como tabelas e blobs.

- Configure um pipeline de integração contínua/implantação contínua em um serviço como o Azure DevOps. Além de trabalhar com o controle do código-fonte (por meio do Azure Repos, do GitHub ou em outro local), você pode configurar um projeto do Azure DevOps para executar automaticamente os testes de unidade como um pré-requisito para o lançamento, bem como configurar o pipeline para implantação em um servidor de preparo para testes adicionais antes de implantar na produção. O Azure DevOps, além disso, integra-se às soluções de monitoramento, como o App Insights e fecha o ciclo de inteiro com ferramentas ágeis de planejamento. Para saber mais, confira [Criar um pipeline de CI/CD para Python com o projeto do Azure DevOps](/azure/devops-project/azure-devops-project-python?view=vsts&preserve-view=true) e também a [documentação geral do Azure DevOps](/azure/devops/?view=vsts&preserve-view=true).
::: moniker-end
## <a name="go-deeper"></a>Aprofunde-se um pouco mais

- [Autenticação de usuário no Django](https://docs.djangoproject.com/en/2.0/topics/auth/) (docs.djangoproject.com)
- Código-fonte do tutorial no GitHub: [Microsoft/python-sample-vs-learning-django](https://github.com/Microsoft/python-sample-vs-learning-django)
