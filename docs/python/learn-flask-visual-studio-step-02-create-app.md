---
title: Tutorial – Saiba mais sobre o Flask no Visual Studio, etapa 2
description: Um passo a passo dos conceitos básicos do Flask no contexto dos projetos do Visual Studio, mostrando especificamente as etapas para criar um aplicativo e usar modos de exibição e modelos.
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
ms.openlocfilehash: 92b34ed0abbef18473ab9ccf6b85c236111822f9
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49812605"
---
# <a name="step-2-create-a-flask-app-with-views-and-page-templates"></a>Etapa 2: Criar um aplicativo Flask com exibições e modelos de página

**Etapa anterior: [Criar uma solução e um projeto do Visual Studio](learn-flask-visual-studio-step-01-project-solution.md)**

Na etapa 1 deste tutorial, você tem um aplicativo Flask com uma página e todo o código em um único arquivo. Para permitir o desenvolvimento futuro, é melhor refatorar o código e criar uma estrutura para modelos de página. Em particular, separe o código para exibições do aplicativo de outros aspectos como o código de inicialização.

Nesta etapa, você aprenderá a:

> [!div class="checklist"]
> - Refatorar o código do aplicativo para separar exibições do código de inicialização (etapa 2-1)
> - Renderizar uma exibição usando um modelo de página (etapa 2-2)

## <a name="step-2-1-refactor-the-project-to-support-further-development"></a>Etapa 2-1: Refatorar o projeto para dar suporte ao desenvolvimento adicional

No código criado pelo modelo "Projeto Web em Branco do Flask", você tem um único arquivo *app.py* que contém o código de inicialização junto com uma única exibição. Para permitir o desenvolvimento adicional de um aplicativo com várias exibições e modelos, é melhor separar essas preocupações.

1. Na pasta do seu projeto, crie uma pasta de aplicativo chamada `HelloFlask` (clique com o botão direito do mouse no projeto em **Gerenciador de Soluções** e selecione **Adicionar** > **Nova Pasta**.)

2. Na pasta *HelloFlask*, crie um arquivo chamado *\_\_init\_\_.py* com o seguinte conteúdo que cria a instância `Flask` e carrega as exibições do aplicativo (criadas na próxima etapa):

    ```python
    from flask import Flask
    app = Flask(__name__)

    import HelloFlask.views
    ```

3. Na pasta *HelloFlask*, crie um arquivo chamado *views.py* com o conteúdo a seguir. O nome *views.py* é importante, porque você usou `import HelloFlask.views` dentro de *\_\_init\_\_.py*; você verá um erro em tempo de execução se os nomes não corresponderem.

    ```python
    from flask import Flask
    from HelloFlask import app

    @app.route('/')
    @app.route('/home')
    def home():
        return "Hello Flask!"
    ```

    Além de renomear a função e a rota como `home`, esse código contém o código de renderização da página de *app.py* e importa o objeto `app` declarado em *\_\_init\_\_.py*.

4. Crie uma subpasta em *HelloFlask* chamada *templates*, que permanecerá vazia por enquanto.

5. Na pasta raiz do projeto, renomeie *app.py* como *runserver.py* e faça o conteúdo corresponder ao seguinte código:

    ```python
    import os
    from HelloFlask import app    # Imports the code from HelloFlask/__init__.py

    if __name__ == '__main__':
        HOST = os.environ.get('SERVER_HOST', 'localhost')

        try:
            PORT = int(os.environ.get('SERVER_PORT', '5555'))
        except ValueError:
            PORT = 5555

        app.run(HOST, PORT)
    ```
6. A estrutura do seu projeto deve ser semelhante à da imagem a seguir:

    ![Estrutura do projeto após a refatoração do código](media/flask/step02-project-structure.png)

7. Selecione **Depurar** > **Iniciar Depuração** (**F5**) ou use o botão **Servidor Web** na barra de ferramentas (o navegador exibido poderá variar) para iniciar o aplicativo e abrir um navegador. Experimente as rotas de URL / e /home.

8. Também é possível definir pontos de interrupção em várias partes do código e reiniciar o aplicativo para seguir a sequência de inicialização. Por exemplo, defina um ponto de interrupção nas primeiras linhas de *runserver.py* e *HelloFlask\_* init_*.py* e na linha `return "Hello Flask!"` de *views.py*. Em seguida, reinicie o aplicativo (**Depurar** > **Reiniciar**, **Ctrl**+**F5** ou o botão de barra de ferramentas mostrado abaixo) e execute o código em etapas (**F10**) ou execute-o em cada ponto de interrupção usando **F5**.

    ![Botão de reinicialização na barra de ferramentas de depuração no Visual Studio](media/debugging-restart-toolbar-button.png)

9. Interrompa o aplicativo ao terminar.

### <a name="commit-to-source-control"></a>Confirmar o controle do código-fonte

Como você já fez alterações no seu código e as testou com êxito, agora é o momento ideal para revisar e confirmar as alterações ao controle do código-fonte. As etapas posteriores deste tutorial indicam os momentos apropriados para fazer a confirmação no controle do código-fonte novamente e direcionam você mais uma vez para esta seção.

1. Selecione o botão de alterações na parte inferior do Visual Studio (circulado abaixo), que encaminha para o **Team Explorer**.

    ![Botão de alterações de controle do código-fonte na barra de status do Visual Studio](media/flask/step02-source-control-changes-button.png)

1. No **Team Explorer**, digite uma mensagem de confirmação como "Refatorar código" e selecione **Confirmar Tudo**. Quando a confirmação for concluída, será exibida a mensagem **Confirmar \<hash> criada localmente. Sincronize para compartilhar as alterações com o servidor.** Se você quiser enviar alterações por push para o repositório remoto, selecione **Sincronizar**, depois selecione **Push** em **Confirmações de Saída**. Também é possível acumular várias confirmações locais antes de enviar para o repositório remoto.

    ![Enviar confirmações por push para repositório remoto no Team Explorer](media/flask/step02-source-control-push-to-remote.png)

### <a name="question-how-frequently-should-one-commit-to-source-control"></a>Pergunta: Com que frequência é necessário fazer a confirmação no controle do código-fonte?

Resposta: A confirmação de alterações no controle do código-fonte cria um registro no log de alterações e um ponto em que é possível reverter o repositório, se necessário. Cada confirmação também pode ser examinada para suas alterações específicas. Como as confirmações no GIT não são caras, é melhor realizar confirmações frequentes do que acumular um grande número de alterações em uma única confirmação. Obviamente, não é necessário confirmar cada pequena alteração em arquivos individuais. Normalmente, você realiza uma confirmação ao adicionar uma funcionalidade, alterando uma estrutura como você fez nesta etapa, ou realizar alguma refatoração do código. Verifique também com outras pessoas da sua equipe para a granularidade de confirmações que funcionam melhor para todos.

A frequência de confirmação e a frequência de envio de confirmações por push a um repositório remoto são duas preocupações diferentes. Você pode acumular várias confirmações no seu repositório local antes de enviá-las por push para o repositório remoto. Novamente, a frequência de confirmação depende de como sua equipe deseja gerenciar o repositório.

## <a name="step-2-2-use-a-template-to-render-a-page"></a>Etapa 2-2: Usar um modelo para renderizar uma página

A função `home` que você tem até agora em *views.py* não gera nada além de uma resposta HTTP de texto sem formatação para a página. No entanto, a maioria das páginas da Web reais respondem com páginas HTML avançadas que incorporam dados dinâmicos com frequência. Na verdade, a principal razão para definir uma exibição usando uma função é gerar esse conteúdo dinamicamente.

Como o valor retornado para a exibição é apenas uma cadeia de caracteres, é possível criar qualquer HTML que desejar dentro de uma cadeia de caracteres, usando conteúdo dinâmico. No entanto, como é melhor separar a marcação dos dados, é muito melhor inserir a marcação em um modelo e manter os dados no código.

1. Para iniciantes, edite *views.py* para que ela contenha o seguinte código que usa HTML embutido para a página com algum conteúdo dinâmico:

    ```python
    from datetime import datetime
    from flask import render_template
    from HelloFlask import app

    @app.route('/')
    @app.route('/home')
    def home():
        now = datetime.now()
        formatted_now = now.strftime("%A, %d %B, %Y at %X")

        html_content = "<html><head><title>Hello Flask</title></head><body>"
        html_content += "<strong>Hello Flask!</strong> on " + formatted_now
        html_content += "</body></html>"

        return html_content
    ```

1. Execute o aplicativo e atualize a página poucas vezes para ver que a data/hora está atualizada. Interrompa o aplicativo ao terminar.

1. Para converter a renderização da página para usar um modelo, crie um arquivo chamado *index.html* na pasta *templates* com o seguinte conteúdo, em que `{{ content }}` é um espaço reservado ou um token de substituição (também chamado de uma *variável de modelo*) para o qual você fornece um valor no código:

    ```html
    <html>
        <head><title>Hello Flask</title></head>

        <body>
            {{ content }}
        </body>
    </html>
    ```

1. Modifique a função `home` para usar `render_template` para carregar o modelo e fornecer um valor para "conteúdo", que é feito usando um argumento nomeado correspondente ao nome do espaço reservado. O Flask procura automaticamente os modelos na pasta *templates*; portanto o caminho para o modelo é relativo a essa pasta:

    ```python
    def home():
        now = datetime.now()
        formatted_now = now.strftime("%A, %d %B, %Y at %X")

        return render_template(
            "index.html",
            content = "<strong>Hello, Flask!</strong> on " + formatted_now)
    ```

1. Execute o aplicativo para ver os resultados e observe que o HTML embutido no valor `content` não é renderizado *como* HTML, porque o mecanismo de modelagem (Jinja) ignora automaticamente o conteúdo HTML. O escape automático impede vulnerabilidades acidentais em ataques de injeção: os desenvolvedores geralmente coletam a entrada de uma página e a usam como um valor em outra por meio de um espaço reservado de modelo. O escape também funciona como um lembrete de que é melhor novamente manter o HTML fora do código.

    Da mesma forma, examine *templates\index.html* para conter espaços reservados distintos em cada parte dos dados dentro da marcação:

    ```html
    <html>
        <head>
            <title>{{ title }}</title>
        </head>
        <body>
            <strong>{{ message }}</strong>{{ content }}
        </body>
    </html>
    ```

    Em seguida, atualize a função `home` para fornecer valores para todos os espaços reservados:

    ```python
    def home():
        now = datetime.now()
        formatted_now = now.strftime("%A, %d %B, %Y at %X")

        return render_template(
            "index.html",
            title = "Hello Flask",
            message = "Hello, Flask!",
            content = " on " + formatted_now)
    ```

1. Execute o aplicativo novamente para ver a saída renderizada corretamente.

    ![Aplicativo em execução usando o modelo](media/flask/step02-result.png)

1. Confirme suas alterações no controle do código-fonte e atualize seu repositório remoto, se desejado, conforme descrito em [etapa 2-1](#commit-to-source-control).

### <a name="question-do-page-templates-have-to-be-in-a-separate-file"></a>Pergunta: Os modelos de página precisam ficar em um arquivo separado?

Resposta: Embora os modelos geralmente sejam mantidos em arquivos HTML separados, também é possível usar um modelo embutido. No entanto, é recomendável usar um arquivo separado para manter uma distinção clara entre marcação e código.

### <a name="question-must-templates-use-the-html-file-extension"></a>Pergunta: Os modelos precisam usar a extensão de arquivo .html?

Resposta: A extensão *.html* dos arquivos de modelo de página é totalmente opcional, porque você sempre identifica o caminho relativo exato para o arquivo no primeiro argumento para a função `render_template`. No entanto, o Visual Studio (e outros editores) costuma fornecer funcionalidades como preenchimento de código e coloração de sintaxe com arquivos *.html*, o que supera o fato de os modelos de página não serem estritamente HTML.

De fato, quando você está trabalhando com um projeto do Flask, o Visual Studio detecta automaticamente quando o arquivo HTML que você está editando é, na verdade, um modelo do Flask e fornece algumas funcionalidades de preenchimento automático. Por exemplo, quando você começa a digitar um comentário no modelo de página do Flask, `{#`, o Visual Studio fornece automaticamente os caracteres de fechamento `#}`. Os comandos **Comentar Seleção** e **Remover Marca de Comentário da Seleção** (no menu **Editar** > **Avançado** e na barra de ferramentas) também usam comentários de modelo em vez de comentários em HTML.

### <a name="question-when-i-run-the-project-i-see-an-error-that-the-template-cannot-be-found-whats-wrong"></a>Pergunta: Quando executo o projeto, é exibido um erro indicando que não é possível encontrar o modelo. Qual é o problema?

Resposta: Se forem exibidos erros indicando que o modelo não pode ser encontrado, verifique se você adicionou o aplicativo a *settings.py* do projeto do Flask na lista `INSTALLED_APPS`. Sem essa entrada, o Flask não saberá o que procurar na pasta *templates* do aplicativo.

### <a name="question-can-templates-be-organized-into-further-subfolders"></a>Pergunta: Os modelos podem ser organizados em subpastas adicionais?

Resposta: Sim. É possível usar subpastas e, em seguida, referir-se ao caminho relativo em *templates* nas chamadas a `render_template`. Isso é uma ótima maneira de criar efetivamente namespaces para os modelos.

## <a name="next-steps"></a>Próximas etapas

> [!div class="nextstepaction"]
> [Fornecer arquivos estáticos, adicionar páginas e usar a herança do modelo](learn-flask-visual-studio-step-03-serve-static-files-add-pages.md)

## <a name="go-deeper"></a>Aprofunde-se um pouco mais

- [Início rápido do Flask – Renderizando modelos](http://flask.pocoo.org/docs/1.0/quickstart/#rendering-templates) (flask.pocoo.org)
- Código-fonte do tutorial no GitHub: [Microsoft/python-sample-vs-learning-flask](https://github.com/Microsoft/python-sample-vs-learning-flask)
