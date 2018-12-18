---
title: Tutorial – Saiba mais sobre o Flask no Visual Studio, etapa 1
description: Um passo a passo das noções básicas do Flask no contexto de projetos do Visual Studio.
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
ms.openlocfilehash: 9865e8e6faaac7b0c3af28532223ea2d5c9f7c01
ms.sourcegitcommit: 25fc9605ba673afb51a24ce587cf4304b06aa577
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/24/2018
ms.locfileid: "47029060"
---
# <a name="tutorial-get-started-with-the-flask-web-framework-in-visual-studio"></a>Tutorial: Introdução à estrutura da Web do Flask no Visual Studio

O [Flask](http://flask.pocoo.org/) é uma estrutura leve do Python para aplicativos Web que fornece as noções básicas de roteamento de URL e renderização de página.

O Flask é denominado uma "microestrutura", porque não oferece diretamente funcionalidades como validação de formulário, abstração de banco de dados, autenticação e assim por diante. Essas funcionalidades são fornecidas por pacotes especiais do Python chamados *extensões* do Flask. As extensões integram-se perfeitamente ao Flask para serem exibidas como se fizessem parte do próprio Flask. Por exemplo, o Flask não oferece um mecanismo de modelo de página. A modelagem é fornecida por extensões como Jinja e Jade, conforme demonstrado neste tutorial.

Neste tutorial, você aprenderá como:

> [!div class="checklist"]
> - Criar um projeto básico do Flask em um repositório GIT usando o modelo "Projeto Web em Branco do Flask" (etapa 1)
> - Criar um aplicativo do Flask com uma página e renderizar essa página usando um modelo (etapa 2)
> - Fornecer arquivos estáticos, adicionar páginas e usar a herança do modelo (etapa 3)
> - Usar o modelo Projeto Web do Flask para criar um aplicativo com várias páginas e design responsivo (etapa 4)
> - Use o modelo Pesquisa Projeto Web de Flask para criar um aplicativo de votação que usa uma variedade de opções de armazenamento (armazenamento do Azure, MongoDB ou memória).

No decorrer dessas etapas, você criará uma única solução do Visual Studio que contém três projetos separados. Você criará o projeto usando diferentes modelos de projeto do Flask incluídos com o Visual Studio. Se você mantiver os projetos na mesma solução, poderá facilmente alternar entre diferentes arquivos para comparação.

> [!Note]
> Este tutorial é diferente do [Início Rápido do Flask](../ide/quickstart-python.md?toc=/visualstudio/python/toc.json&bc=/visualstudio/python/_breadcrumb/toc.json) no qual você saberá mais sobre o Flask e como usar os diferentes modelos de projeto do Flask que fornecem um ponto de início mais amplo para seus próprios projetos. Por exemplo, os modelos de projeto instalam automaticamente o pacote do Flask ao criar um projeto, em vez de precisar instalar o pacote manualmente, conforme mostrado no Início Rápido.

## <a name="prerequisites"></a>Pré-requisitos

- Visual Studio 2017 no Windows com as seguintes opções:
  - A carga de trabalho **desenvolvimento do Python** (guia **Carga de Trabalho** no instalador). Para obter instruções, confira [Instalar o suporte do Python no Visual Studio](installing-python-support-in-visual-studio.md).
  - **GIT para Windows** e **Extensão GitHub para Visual Studio** na guia **Componentes individuais** em **Code Tools**.

Os modelos de projeto do Flask são incluídos com todas as versões anteriores das Ferramentas Python para Visual Studio, embora os detalhes possam ser diferentes do que foi discutido neste tutorial.

No momento, não há suporte para o desenvolvimento do Python no Visual Studio para Mac. No Mac e no Linux, use a [Extensão Python no Visual Studio Code](https://code.visualstudio.com/docs/python/python-tutorial).

## <a name="step-1-1-create-a-visual-studio-project-and-solution"></a>Etapa 1-1: Criar uma solução e um projeto do Visual Studio

1. No Visual Studio, selecione **Arquivo** > **Novo** > **Projeto**, pesquise "Projeto Web em Branco do Flask" e selecione o modelo **Projeto Web em Branco do Flask**. O modelo também pode ser encontrado em **Python** > **Web** na lista à esquerda.

    ![Nova caixa de diálogo do projeto no Visual Studio para o Projeto Web em Branco do Flask](media/flask/step01-new-blank-project.png)

1. Nos campos, na parte inferior da caixa de diálogo, insira as informações a seguir (conforme mostrado no gráfico anterior) e, em seguida, escolha **OK**:

    - **Nome**: defina o nome do projeto do Visual Studio como **BasicProject**. Esse nome também é usado para o projeto do Flask.
    - **Local**: especifique um local no qual criar o projeto e a solução do Visual Studio.
    - **Nome da solução**: definido como **LearningFlask**, apropriado para a solução como um contêiner para vários projetos neste tutorial.
    - **Criar diretório para a solução**: deixar definido (o padrão).
    - **Criar um novo repositório Git**: escolha essa opção (que é clara por padrão) para que o Visual Studio crie um repositório Git local quando criar a solução. Caso essa opção não seja exibida, execute o instalador do Visual Studio 2017 e adicione o **GIT para Windows** e a **Extensão do GitHub para Visual Studio** à guia **Componentes individuais** em **Ferramentas de código**.

1. Após alguns instantes, o Visual Studio fará uma solicitação em uma caixa de diálogo com a mensagem **Este projeto exige pacotes externos** (mostrado abaixo). Essa caixa de diálogo é exibida porque o modelo inclui um arquivo *requirements.txt* que referencia o último pacote do Flask 1.x. Escolha **Mostrar pacotes necessários** para ver as dependências exatas.

    ![Solicitação dizendo que o projeto requer pacotes externos](media/tutorials-common/step01-requirements-prompt-install-myself.png)

1. Escolha a opção **Eu vou instalá-los sozinho**. Crie o ambiente virtual logo em seguida para garantir que ele será excluído do controle do código-fonte. (O ambiente pode ser sempre criado com base em *requirements.txt*.)

## <a name="step-1-2-examine-the-git-controls-and-publish-to-a-remote-repository"></a>Etapa 1-2: Examinar os controles do Git e publicar em um repositório remoto

Como você marcou a opção **Criar novo repositório Git** na caixa de diálogo **Novo Projeto**, o projeto já ficará confirmado no controle do código-fonte local assim que o processo de criação for concluído. Nesta etapa, familiarize-se com os controles do Git do Visual Studio e a janela do **Team Explorer** onde você trabalha com o controle do código-fonte.

1. Observe os controles do Git no canto inferior da janela principal do Visual Studio. Da esquerda para direita, esses controles mostram confirmações não enviadas, as alterações não confirmadas, o nome do repositório e a ramificação atual:

    ![Controles do Git na janela do Visual Studio](media/flask/step01-git-controls.png)

    > [!Note]
    > Se você não marcar a opção **Criar novo repositório Git** na caixa de diálogo **Novo Projeto**, os controles do Git mostrarão apenas um comando **Adicionar ao controle do código-fonte** que criará um repositório local.
    >
    > ![Se você não tiver criado um repositório, o comando Adicionar ao controle do código-fonte será exibido no Visual Studio](media/tutorials-common/step01-git-add-to-source-control.png)

1. Marque o botão de alterações e o Visual Studio abrirá a janela do **Team Explorer** na página **Alterações**. Como o projeto recém-criado já está automaticamente confirmado no controle do código-fonte, você não verá as alterações pendentes.

    ![Janela do Team Explorer na página Alterações](media/flask/step01-team-explorer-changes.png)

1. Na barra de status do Visual Studio, marque o botão de confirmação não enviada (a seta para cima com um **2**) para abrir a página **Sincronização** no **Team Explorer**. Como você tem apenas um repositório local, a página oferece opções simples para publicar o repositório em diferentes repositórios remotos.

    ![Janela do Team Explorer mostrando opções do repositório Git disponíveis para o controle do código-fonte](media/flask/step01-team-explorer.png)

    Você pode escolher o serviço que desejar para seus próprios projetos. Este tutorial mostra o uso do GitHub, em que o código de exemplo concluído do tutorial é mantido no repositório [Microsoft/python-sample-vs-learning-flask](https://github.com/Microsoft/python-sample-vs-learning-flask).

1. Ao selecionar qualquer um dos controles **Publicar**, o **Team Explorer** solicitará mais informações. Por exemplo, ao publicar o exemplo deste tutorial, o próprio repositório teve que ser criado primeiro, caso em que a opção **Enviar por Push para o Repositório Remoto** foi usada com a URL do repositório.

    ![Janela do Team Explorer para efetuar push para um repositório remoto existente](media/flask/step01-push-to-github.png)

    Se você não tiver um repositório, as opções **Publicar no GitHub** e **Enviar por Push para o Azure DevOps** permitirão criar um repositório diretamente no Visual Studio.

1. Ao trabalhar com este tutorial, adquira o hábito de usar periodicamente os controles no Visual Studio para confirmar e enviar alterações por push. Este tutorial envia-lhe lembretes nos pontos apropriados.

> [!Tip]
> Para navegar rapidamente no **Team Explorer**, selecione o cabeçalho (que indica **Alterações** ou **Efetuar Push** nas imagens acima) para ver um menu pop-up das páginas disponíveis.

### <a name="question-what-are-some-advantages-of-using-source-control-from-the-beginning-of-a-project"></a>Pergunta: Quais são algumas vantagens de usar o controle do código-fonte a partir do início de um projeto?

Resposta: Em primeiro lugar, se você usar o controle do código-fonte desde o início, especialmente se também usar um repositório remoto, terá um backup regular em um local fora do projeto. Em vez de manter um projeto apenas em um sistema de arquivos local, o controle do código-fonte também oferece um histórico de alterações completo e facilita a reversão de um único arquivo ou todo o projeto para um estado anterior. O histórico de alterações ajuda a determinar a causa das regressões (falhas de teste). Além disso, o controle do código-fonte é essencial se várias pessoas estiverem trabalhando em um projeto, pois ele gerencia substituições e fornece a resolução de conflitos. Por fim, o controle do código-fonte, que é basicamente uma forma de automação, deixa você preparado para automatizar o gerenciamento de compilações, testes e versões. Esse recurso realmente representa o primeiro passo no uso de DevOps em um projeto e, como os obstáculos para entrar são muito baixos, realmente não há motivos para não usar o controle do código-fonte desde o início.

Para uma discussão mais aprofundada sobre o controle do código-fonte usado como automação, confira [A origem da verdade: a função dos repositórios no DevOps](https://msdn.microsoft.com/magazine/mt763232), um artigo da MSDN Magazine destinado a aplicativos móveis, mas que também se aplica a aplicativos Web.

### <a name="question-can-i-prevent-visual-studio-from-auto-committing-a-new-project"></a>Pergunta: É possível evitar que o Visual Studio confirme automaticamente um novo projeto?

Resposta: Sim. Para desabilitar a confirmação automática, vá para a página **Configurações** no **Team Explorer**, escolha **Git** > **Configurações Globais**, desmarque o opção rotulada como **Confirmar alterações após mesclagem por padrão** e, em seguida, escolha **Atualizar**.

## <a name="step-1-3-create-the-virtual-environment-and-exclude-it-from-source-control"></a>Etapa 1-3: Criar o ambiente virtual e excluí-lo do controle do código-fonte

Agora que você configurou o controle do código-fonte para o projeto, é possível criar no ambiente virtual os pacotes necessários do Flask que o projeto exige. Você pode usar o **Team Explorer** para excluir a pasta do ambiente do controle do código-fonte.

1. No **Gerenciador de Soluções**, clique com o botão direito do mouse no nó **Ambientes do Python** e escolha **Adicionar Ambiente Virtual**.

    ![Comando Adicionar Ambiente Virtual no Gerenciador de Soluções](media/flask/step01-add-virtual-environment-command.png)

1. Uma caixa de diálogo **Adicionar Ambiente Virtual** é exibida contendo a mensagem **Encontramos um arquivo requirements.txt.** Esta mensagem indica que o Visual Studio usa esse arquivo para configurar o ambiente virtual.

    ![Caixa de diálogo Adicionar Ambiente Virtual com a mensagem requirements.txt](media/tutorials-common/step01-add-virtual-environment-found-requirements.png)

1. Escolha **Criar** para aceitar os padrões. (Se desejar, o nome do ambiente virtual pode ser alterado. Essa ação alterará apenas o nome da subpasta, mas `env` é uma convenção padrão).

1. Caso seja solicitado, concorde com os privilégios de administrador e aguarde alguns minutos enquanto o Visual Studio baixa e instala pacotes, que, para o Flask e para suas dependências, significa expandir cerca de mil arquivos em mais de 100 subpastas. Você pode ver o progresso na janela **Saída** no Visual Studio. Enquanto você aguarda, analise as seções de perguntas a seguir. Também é possível ver uma descrição das dependências do Flask na página [instalação do Flask](http://flask.pocoo.org/docs/1.0/installation/#installation) (flask.pcocoo.org).

1. Nos controles do GIT do Visual Studio (na barra de status), selecione o indicador de alterações (mostrando **99&#42;**) que abre a página **Alterações** no **Team Explorer**.

    A criação do ambiente virtual apresentou centenas de alterações, mas nenhuma delas precisará ser incluída no controle do código-fonte já que você (ou qualquer outra pessoa que venha a clonar o projeto) poderá sempre recriar o ambiente com base em *requirements.txt*.

    Para excluir o ambiente virtual, clique com o botão direito do mouse na pasta **env** e selecione **Ignorar estes itens locais**.

    ![Como ignorar um ambiente virtual em alterações de controle do código-fonte](media/flask/step01-ignore-local-items.png)

1. Depois de excluir o ambiente virtual, as únicas alterações restantes são as referentes ao arquivo de projeto e a *.gitignore*. O arquivo *.gitignore* contém uma entrada adicional para a pasta do ambiente virtual. Você pode clicar duas vezes no arquivo para ver uma comparação.

1. Digite uma mensagem de confirmação, escolha o botão **Confirmar Todos** e, se desejar, envie as confirmações por push para o repositório remoto.

### <a name="question-why-do-i-want-to-create-a-virtual-environment"></a>Pergunta: Por que criar um ambiente virtual?

Resposta: Um ambiente virtual é uma ótima maneira de isolar as dependências exatas do seu aplicativo. Esse isolamento evita conflitos em um ambiente global do Python e auxilia nos testes e na colaboração. Com o tempo, à medida que desenvolver um aplicativo, invariavelmente, você introduzirá muitos pacotes úteis do Python. Mantendo os pacotes em um ambiente virtual específico do projeto, você pode atualizar com facilidade o arquivo *requirements.txt* do projeto que descreve esse ambiente, incluído no controle do código-fonte. Quando o projeto é copiado para outros computadores, incluindo servidores de build, servidores de implantação e outros computadores de desenvolvimento, é fácil recriar o ambiente usando apenas o *requirements.txt* (é por isso que o ambiente não precisa estar no controle do código-fonte). Para obter mais informações, confira [Usar ambientes virtuais](selecting-a-python-environment-for-a-project.md#use-virtual-environments).

### <a name="question-how-do-i-remove-a-virtual-environment-thats-already-committed-to-source-control"></a>Pergunta: Como faço para remover um ambiente virtual que já está confirmado no controle do código-fonte?

Resposta: Primeiro, edite o arquivo *.gitignore* para excluir a pasta: localize a seção ao final com o comentário `# Python Tools for Visual Studio (PTVS)` e adicione uma nova linha à pasta do ambiente virtual, como `/BasicProject/env`. (Como o Visual Studio não mostra o arquivo no **Gerenciador de Soluções**, abra-o diretamente usando o comando de menu **Arquivo** > **Abrir** > **Arquivo**. Abra também o arquivo no **Team Explorer**: na página **Configurações**, selecione **Configurações do Repositório**, vá para a seção **Arquivos Ignorar e de Atributos** e, em seguida, selecione o link **Editar** ao lado de **.gitignore**.)

Em segundo lugar, abra uma janela Comando, navegue para a pasta, como *BasicProject*, que contém a pasta do ambiente virtual, como *env*, e execute `git rm -r env`. Em seguida, confirme essas alterações na linha de comando (`git commit -m 'Remove venv'`) ou confirme na página **Alterações** do **Team Explorer**.

## <a name="step-1-4-examine-the-boilerplate-code"></a>Etapa 1-4: Examinar o código de texto clichê

1. Quando a criação do projeto for concluída, você verá a solução e o projeto no **Gerenciador de Soluções**, em que o projeto contém apenas dois arquivos, *app.py* e *requirements.txt*:

    ![Arquivos de projeto em branco do Flask no Gerenciador de Soluções](media/flask/step01-blank-flask-project-in-solution-explorer.png)

1. Conforme observado anteriormente, o arquivo *requirements.txt* especifica a dependência de pacote do Flask. A presença desse arquivo é que faz com que você seja convidado a criar um ambiente virtual ao desenvolver o projeto pela primeira vez.

1. O único arquivo *app.py* contém três partes. A primeira é uma instrução `import` do Flask, criando uma instância da classe `Flask`, atribuída à variável `app` e, em seguida, atribuindo uma variável `wsgi_app` (útil ao implantar um host da Web, mas não usada no momento):

    ```python
    from flask import Flask
    app = Flask(__name__)

    # Make the WSGI interface available at the top level so wfastcgi can get it.
    wsgi_app = app.wsgi_app
    ```

1. A segunda parte, ao fim do arquivo, é um trecho do código opcional que inicia o servidor de desenvolvimento do Flask com valores de porta e de host específicos extraídos de variáveis de ambiente (padrão para localhost:5555):

    ```python
    if __name__ == '__main__':
        import os
        HOST = os.environ.get('SERVER_HOST', 'localhost')
        try:
            PORT = int(os.environ.get('SERVER_PORT', '5555'))
        except ValueError:
            PORT = 5555
        app.run(HOST, PORT)
    ```

1. A terceira é um breve trecho de código que atribui uma função a uma rota de URL, o que significa que a função oferece o recurso identificado pela URL. Defina rotas usando o decorador `@app.route` do Flask, cujo argumento é a URL relativa da raiz do site. Como é possível ver no código, a função retorna apenas uma cadeia de caracteres de texto, que é suficiente para um navegador renderizar. Nas etapas seguintes, você renderizará páginas mais avançadas com HTML.

    ```python
    @app.route('/')
    def hello():
        """Renders a sample page."""
        return "Hello World!"
    ```

### <a name="question-what-is-the-purpose-of-the-name-argument-to-the-flask-class"></a>Pergunta: Qual é a finalidade do argumento __name__ para a classe do Flask?

Resposta: o argumento é o nome do módulo ou do pacote do aplicativo e informa ao Flask onde procurar modelos, arquivos estáticos e outros recursos que pertencem ao aplicativo. Para aplicativos contidos em um único módulo, `__name__` é sempre o valor adequado. Também é importante para as extensões que precisam de informações de depuração. Para obter mais informações, e outros argumentos, confira a [documentação de classes do Flask](http://flask.pocoo.org/docs/1.0/api/#flask.Flask) (flask.pocoo.org).

### <a name="question-can-a-function-have-more-than-one-route-decorator"></a>Pergunta: Uma função pode ter mais de um decorador de rota?

Resposta: sim, será possível usar quantos decoradores você quiser se a mesma função servir para várias rotas. Por exemplo, para usar a função `hello` para "/" e "/hello", use o seguinte código:

```python
@app.route('/')
@app.route('/hello')
def hello():
    """Renders a sample page."""
    return "Hello World!"
```

<a name="qa-url-variables"></a>

### <a name="question-how-does-flask-work-with-variable-url-routes-and-query-parameters"></a>Pergunta: Como o Flask trabalha com rotas de URL de variável e parâmetros de consulta?

Resposta: em uma rota, marque qualquer variável com `<variable_name>`, e o Flask passará a variável para a função usando um argumento nomeado. A variável pode fazer parte do caminho da URL ou em um parâmetro de consulta. Por exemplo, uma rota no formato de `'/hello/<name>` gera um argumento de cadeia de caracteres chamado `name` para a função e o uso de `?message=<msg>` na rota analisa o valor fornecido para o parâmetro de consulta "message=" e o passa para a função como `msg`:

```python
@app.route('/hello/<name>?message=<msg>')
def hello(name, msg):
    return "Hello " + name + "! Message is " + msg + "."
```

Para alterar o tipo, insira `int`, `float`, `path` à frente da variável (que aceita barras para delinear nomes de pasta) e `uuid`. Para obter detalhes, confira [Regras de variáveis](http://flask.pocoo.org/docs/1.0/quickstart/#variable-rules) na documentação do Flask.

Os parâmetros de consulta também estão disponíveis por meio da propriedade `request.args`, especificamente por meio do método `request.args.get`. Para obter mais informações, confira [O objeto Request](http://flask.pocoo.org/docs/1.0/quickstart/#the-request-object) na documentação do Flask.

### <a name="question-can-visual-studio-generate-a-requirementstxt-file-from-a-virtual-environment-after-i-install-other-packages"></a>Pergunta: O Visual Studio pode gerar um arquivo requirements.txt a partir de um ambiente virtual depois de instalar outros pacotes?

Resposta: Sim. Expanda o nó **Ambientes do Python**, clique com o botão direito do mouse no ambiente virtual e escolha o comando **Gerar requirements.txt**. É recomendável usar esse comando periodicamente conforme você modifica o ambiente e confirma as alterações em *requirements.txt* no controle do código-fonte, juntamente com outras alterações de código que dependem desse ambiente. Se você configurar a integração contínua em um servidor de compilação, deverá gerar o arquivo e confirmar as alterações sempre que modificar o ambiente.

## <a name="step-1-5-run-the-project"></a>Etapa 1-5: Executar o projeto

1. No Visual Studio, selecione **Depurar** > **Iniciar Depuração** (**F5**) ou use o botão **Servidor Web** na barra de ferramentas (o navegador visto pode variar):

    ![Executar o botão da barra de ferramentas do servidor Web no Visual Studio](media/tutorials-common/run-web-server-toolbar-button.png)

1. Qualquer comando atribui um número da porta aleatório à variável de ambiente PORT e, em seguida, executa `python app.py`. O código inicia o aplicativo usando essa porta dentro do servidor de desenvolvimento do Flask. Se o Visual Studio informar **Falha ao iniciar o depurador** com uma mensagem que alerta para a ausência de um arquivo de inicialização, clique com o botão direito do mouse em **app.py** no **Gerenciador de Soluções** e selecione **Definir como Arquivo de Inicialização**.

1. Ao iniciar o servidor, você vê uma janela do console aberta que exibe o log do servidor. O Visual Studio abre automaticamente um navegador para `http://localhost:<port>`, em que você verá a mensagem renderizada pela função `hello`:

    ![Modo de exibição padrão do projeto do Flask](media/flask/step01-first-run-success.png)

1. Quando terminar, interrompa o servidor fechando a janela do console ou usando o comando **Depurar** > **Parar Depuração** no Visual Studio.

### <a name="question-whats-the-difference-between-using-the-debug-menu-commands-and-the-server-commands-on-the-projects-python-submenu"></a>Pergunta: Qual é a diferença entre usar os comandos do menu Depuração e os comandos do servidor no submenu do Python do projeto?

Resposta: Além dos comandos do menu **Depurar** e dos botões da barra de ferramentas, você também pode iniciar o servidor usando os comandos **Python** > **Executar servidor** ou **Python** > **Executar o servidor de depuração** no menu de contexto do projeto. Os dois comandos abrem uma janela de console na qual você vê a URL local (localhost:port) do servidor em execução. Mesmo assim, abra manualmente um navegador usando essa URL já que a execução do servidor de depuração não inicia automaticamente o depurador do Visual Studio. Se desejar, você pode posteriormente anexar um depurador ao processo em execução usando o comando **Depurar** > **Anexar ao Processo**.

## <a name="next-steps"></a>Próximas etapas

Neste ponto, o projeto básico do Flask contém o código de inicialização e o código de página no mesmo arquivo. É melhor separar essas duas questões e também separar o HTML e os dados usando modelos.

> [!div class="nextstepaction"]
> [Criar um aplicativo do Flask com modos de exibição e modelos de página](learn-flask-visual-studio-step-02-create-app.md)

## <a name="go-deeper"></a>Aprofunde-se um pouco mais

- [Início rápido do Flask](http://flask.pocoo.org/docs/1.0/quickstart/) (flask.pocoo.org)
- Código-fonte do tutorial no GitHub: [Microsoft/python-sample-vs-learning-flask](https://github.com/Microsoft/python-sample-vs-learning-flask)
