---
title: Publicar um aplicativo Python no Serviço de Aplicativo do Azure no Windows
description: Como publicar um aplicativo Web em Python diretamente no Serviço de Aplicativo do Azure no Windows desde o Visual Studio, incluindo o conteúdo necessário para o arquivo web.config.
ms.date: 10/18/2018
ms.prod: visual-studio-dev15
ms.technology: vs-python
ms.topic: conceptual
author: kraigb
ms.author: kraigb
manager: douge
ms.workload:
- python
- data-science
- azure
ms.openlocfilehash: cae15da8b6a59587037171ae982ee77d2cce2861
ms.sourcegitcommit: 551f13774e8bb0eb47cbd973745628a956e866aa
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/19/2018
ms.locfileid: "49459951"
---
# <a name="publishing-to-azure-app-service-on-windows"></a>Como publicar no Serviço de Aplicativo do Azure no Windows

> [!Note]
> Esse conteúdo e os recursos descritos foram preteridos, mas continuam a funcionar. Os desenvolvedores de Python são incentivados a migrarem para o [Serviço de Aplicativo no Linux](publishing-python-web-applications-to-azure-from-visual-studio.md) sempre que possível.

O Visual Studio possibilita publicar um aplicativo Web do Python no Serviço de Aplicativo do Azure no Windows. Publicar no Serviço de Aplicativo do Azure no Windows significa copiar os arquivos necessários para o servidor e a configurar um arquivo `web.config` adequado que instrui ao servidor Web como inicializar o aplicativo.

O processo de publicação difere entre o Visual Studio 2017 e o Visual Studio 2015. Especificamente, o Visual Studio 2015 automatiza algumas etapas, incluindo a criação do `web.config`, mas essa automação limita o controle e flexibilidade a longo prazo. O Visual Studio 2017 requer mais etapas manuais, mas proporciona um controle mais exato sobre o ambiente do Python. As duas opções são descritas aqui.

> [!Note]
> Para obter informações adicionais das alterações entre o Visual Studio 2015 e Visual Studio 2017, consulte a postagem de blog, [Publicar no Azure no Visual Studio 2017](https://blogs.msdn.microsoft.com/pythonengineering/2016/12/12/publish-to-azure-in-vs-2017/).

## <a name="prerequisites"></a>Pré-requisitos

Para este passo a passo, você precisa de um projeto de aplicativo Web com base nas estruturas Bottle, Flask ou Django. Se você ainda não tem um projeto e deseja ver como funciona o processo de publicação, crie um projeto de teste simples da seguinte maneira:

1. No Visual Studio, selecione **Arquivo > Novo > Projeto**, pesquise "Bottle", selecione o **Bottle Web Project**, especifique um nome e um caminho para o projeto e clique em **OK**. (O modelo do Bottle está incluído com a carga de trabalho de desenvolvimento do Python; consulte [Instalação](installing-python-support-in-visual-studio.md)).

1. Siga os prompts para instalar pacotes externos, selecionando **Instalar em um ambiente virtual** bem como o interpretador de base preferencial para o ambiente virtual. Normalmente você combina essa opção com a versão do Python instalada no Serviço de Aplicativo.

1. Teste o projeto localmente, pressionando F5 ou selecionando **Depurar > Iniciar Depuração**.

## <a name="create-an-azure-app-service"></a>Criar um Serviço de Aplicativo do Azure

A publicação no Azure requer um Serviço de Aplicativo de destino. Para essa finalidade, você pode criar um Serviço de Aplicativo usando uma assinatura do Azure ou pode usar um site temporário.

Se você ainda não tem uma assinatura, comece com uma [conta gratuita completa do Azure](https://azure.microsoft.com/free/), que inclui créditos generosos para os serviços do Azure. Além disso, considere inscrever-se no [Visual Studio Dev Essentials](https://azure.microsoft.com/pricing/member-offers/vs-dev-essentials/), que fornece a você um crédito de US$ 25 todo mês durante um ano.

> [!Tip]
> Embora o Azure solicite um cartão de crédito para verificar a sua conta, o cartão não será cobrado. Você também pode definir um [limite de gastos](/azure/billing/billing-spending-limit) igual a seus créditos gratuitos para garantir que não haja encargos adicionais. Além disso, o Azure oferece uma camada gratuita do Plano do Serviço de Aplicativo, que é ideal para aplicativos de teste simples, conforme descrito na próxima seção.

### <a name="using-a-subscription"></a>Usando uma assinatura

Com uma assinatura ativa do Azure, crie um Serviço de Aplicativo com um aplicativo Web vazio da seguinte maneira:

1. Entre no [portal.azure.com](https://portal.azure.com).
1. Selecione **+Novo** e, em seguida, selecione **Web + Celular** seguido por **Aplicativo Web**.
1. Especifique um nome para o aplicativo Web, deixe **Grupo de Recursos** como "Criar Novo" e escolha **Windows** como o sistema operacional.
1. Selecione **Localização/Plano do Serviço de Aplicativo**, selecione **Criar novo** e especifique um nome e local. Em seguida, selecione **Tipo de preço**, role para baixo e selecione o plano **F1 Gratuito**, pressione **Selecionar**, depois **OK** e, em seguida, **Criar**.
1. (Opcional) Quando o Serviço de Aplicativo tiver sido criado, navegue até ele, selecione **Obter perfil de publicação** e salve o arquivo localmente.

### <a name="using-a-temporary-app-service"></a>Usando um Serviço de Aplicativo temporário

Crie um Serviço de Aplicativo temporário sem a necessidade de uma assinatura do Azure da seguinte maneira:

1. Abra o navegador em [try.azurewebsites.net](https://try.azurewebsites.net).
1. Selecione **Aplicativo Web** para o tipo de aplicativo e, em seguida, selecione **Avançar**.
1. Selecione **Site Vazio** e, depois, **Criar**.
1. Entre com um logon social de sua escolha e, após alguns instantes, seu site estará pronto na URL exibida.
1. Selecione **Baixar perfil de publicação** e salve o arquivo `.publishsettings`, que você usará mais tarde.

## <a name="configure-python-on-azure-app-service"></a>Configurar o Python no Serviço de Aplicativo do Azure

Depois que tiver um Serviço de Aplicativo com um aplicativo Web vazio em execução (em sua assinatura ou em um site gratuito), instale a versão do Python à sua escolha, conforme descrito em [Gerenciando Python no Serviço de Aplicativo do Azure](managing-python-on-azure-app-service.md). Para a publicação através do Visual Studio 2017, registre o caminho exato do interpretador do Python instalado com a extensão de site, conforme descrito naquele artigo.

Se desejar, você também pode instalar o pacote `bottle` usando o processo naquelas mesmas instruções, pois o pacote é instalado como parte de outras etapas neste passo a passo.

## <a name="publish-to-app-service---visual-studio-2017"></a>Publicar no Serviço de Aplicativo – Visual Studio 2017

A publicação no Serviço de Aplicativo do Azure através do Visual Studio 2017 copia somente os arquivos do seu projeto para o servidor. Portanto, é necessário criar os arquivos pertinentes para configurar o ambiente de servidor.

1. No **Gerenciador de Soluções** do Visual Studio, clique com botão direito do mouse no projeto e selecione **Adicionar > Novo Item…*. Na caixa de diálogo que é exibida, selecione o modelo "Azure web.config (Fast CGI)" e selecione OK. Isso cria um arquivo `web.config` na raiz do seu projeto.

1. Modifique a entrada `PythonHandler` em `web.config` para que o caminho corresponda à instalação do Python no servidor (consulte [Referência de configuração do IIS](https://www.iis.net/configreference) (iis.net) para obter detalhes exatos). Por exemplo, para o Python 3.6.1 x64, a entrada deve ser semelhante ao seguinte:

    ```xml
    <system.webServer>
      <handlers>
        <add name="PythonHandler" path="*" verb="*" modules="FastCgiModule"
            scriptProcessor="D:\home\Python361x64\python.exe|D:\home\Python361x64\wfastcgi.py"
            resourceType="Unspecified" requireAccess="Script"/>
      </handlers>
    </system.webServer>
    ```

1. Defina a entrada `WSGI_HANDLER` em `web.config` de acordo com a estrutura que você está usando:

    - **Bottle**: adicione parênteses depois de `app.wsgi_app`, conforme mostrado abaixo. Isso é necessário porque esse objeto é uma função (consulte `app.py`) em vez de uma variável:

        ```xml
        <!-- Bottle apps only -->
        <add key="WSGI_HANDLER" value="app.wsgi_app()"/>
        ```

    - **Flask**: altere o valor de `WSGI_HANDLER` para `<project_name>.app`, em que `<project_name>` corresponde ao nome do seu projeto. Você pode localizar o identificador exato examinando a instrução `from <project_name> import app` no `runserver.py`. Por exemplo, se o projeto fosse denominado "FlaskAzurePublishExample", a entrada seria semelhante ao seguinte:

        ```xml
        <!-- Flask apps only: change the project name to match your app -->
        <add key="WSGI_HANDLER" value="FlaskAzurePublishExample.app"/>
        ```

    - **Django**: duas alterações são necessárias no `web.config` para projetos Django. Primeiro, altere o valor de `WSGI_HANDLER` para `django.core.wsgi.get_wsgi_application()` (o objeto está no arquivo `wsgi.py`):

        ```xml
        <!-- Django apps only -->
        <add key="WSGI_HANDLER" value="django.core.wsgi.get_wsgi_application()"/>
        ```

        Em seguida, adicione a seguinte entrada abaixo da do `WSGI_HANDLER`, substituindo `DjangoAzurePublishExample` pelo nome do seu projeto:

        ```xml
        <add key="DJANGO_SETTINGS_MODULE" value="DjangoAzurePublishExample.settings" />
        ```

1. **Somente aplicativos Django**: no arquivo `settings.py` do projeto Django, adicione o domínio de URL do seu site a `ALLOWED_HOSTS` conforme mostrado abaixo, substituindo 'vspython-test-02.azurewebsites.net' por sua URL, é claro:

    ```python
    # Change the URL to your specific site
    ALLOWED_HOSTS = ['vspython-test-02.azurewebsites.net']
    ```

    A falha em adicionar a URL à matriz resultará no erro "DisallowedHost em / Cabeçalho HTTP_HOST inválido: '\<URL do site\>'. Talvez seja necessário adicionar a '\<URL do site\>' ao ALLOWED_HOSTS."

    Observe que, quando a matriz estiver vazia, o Django permitirá automaticamente 'localhost', mas adicionar sua URL de produção removerá essas funcionalidades. Por esse motivo, talvez você queira manter cópias do `settings.py` de desenvolvimento e de produção separadas ou usar variáveis de ambiente para controlar os valores de tempo de execução.

1. No **Gerenciador de Soluções**, expanda a pasta com o mesmo nome que o seu projeto, clique com botão direito do mouse na pasta `static`, selecione **Adicionar > Novo Item...** , selecione o modelo "Arquivos estáticos web.config do Azure" e selecione **OK**. Essa ação cria outro `web.config` na pasta `static`, que desabilita o processamento do Python para essa pasta. Essa configuração envia as solicitações de arquivos estáticos para o servidor Web padrão em vez de usar o aplicativo Python.

1. Salve seu projeto e, em seguida, no **Gerenciador de Soluções** do Visual Studio, clique com o botão direito do mouse e selecione **Publicar**.

    ![Comando Publicar em um menu de contexto do projeto](media/template-web-publish-command.png)

1. Na guia **Publicar** que é exibida, selecione o destino da publicação:

    a. A sua própria assinatura do Azure: selecione **Serviço de Aplicativo do Microsoft Azure** e, em seguida, **Selecionar Existente** e, então, **Publicar**. Uma caixa de diálogo será exibida, na qual você poderá selecionar a assinatura e o serviço de aplicativo apropriados. Se o Serviço de Aplicativo não for exibido, use o perfil de publicação baixado, conforme descrito abaixo, para um Serviço de Aplicativo temporário.

    ![Etapa 1 de publicação no Azure, Visual Studio 2017, assinaturas existentes](media/tutorials-common-publish-1a-2017.png)

    b. Se você estiver usando um Serviço de Aplicativo temporário em try.azurewebsites.net ou se for necessário usar um perfil de publicação, selecione o controle **>** para localizar **Perfil de importação**; selecione essa opção e, em seguida, selecione **Publicar**. Isso solicitará o local do arquivo `.publishsettings` baixado anteriormente.

    ![Etapa 1 de publicação no Azure, Visual Studio 2017, serviço de aplicativo temporário](media/tutorials-common-publish-1b-2017.png)

1. O Visual Studio exibe o status da publicação em uma janela de "Atividade de Publicação na Web" e na janela Publicar. Quando a publicação estiver concluída, o navegador padrão será aberto na URL do site. A URL também será mostrada na janela Publicar.

1. Quando o navegador for aberto, você poderá ver a mensagem "A página não pode ser exibida devido a um erro interno do servidor". Esta mensagem indica que seu ambiente do Python no servidor não está totalmente configurado e, nesse caso, execute as seguintes etapas:

    a. Consulte novamente [Gerenciando Python no Serviço de Aplicativo do Azure](managing-python-on-azure-app-service.md), verificando se você tem uma extensão de site apropriada do Python instalada.

    b. Verifique mais uma vez o caminho para o interpretador do Python em seu arquivo `web.config`. O caminho deve corresponder exatamente ao local de instalação da extensão de site escolhida.

    c. Use o console do Kudu para atualizar todos os pacotes listados no arquivo `requirements.txt` do seu aplicativo: navegue até a mesma pasta do Python que é usada em `web.config`, como `/home/python361x64`, e execute o seguinte comando, conforme descrito na seção [Console do Kudu](managing-python-on-azure-app-service.md#azure-app-service-kudu-console):

    ```command
    python -m pip install --upgrade -r /home/site/wwwroot/requirements.txt
    ```

    Se você encontrar erros de permissão ao executar esse comando, verifique se está executando o comando na sua pasta da extensão de site e *não* na pasta de uma das instalações padrão do Python do Serviço de Aplicativo. Como você não pode modificar esses ambientes padrão, a tentativa de instalar pacotes certamente falhará.

    d. Para obter a saída de erro detalhada, adicione a seguinte linha ao `web.config` dentro do nó `<system.webServer>`, que fornecerá uma saída de erro mais detalhada:

    ```xml
    <httpErrors errorMode="Detailed"></httpErrors>
    ```

    e. Tente reiniciar o Serviço de Aplicativo depois de instalar novos pacotes. Uma reinicialização não é necessária ao alterar o `web.config`, pois o Serviço de Aplicativo executa uma reinicialização automática sempre que o `web.config` é alterado.

    > [!Tip]
    > Se você fizer qualquer alteração no arquivo `requirements.txt` do seu aplicativo, certifique-se de usar novamente o console do Kudu para instalar todos os pacotes que agora estarão listados nesse arquivo.

1. Depois de configurar totalmente o ambiente de servidor, atualize a página no navegador e o aplicativo Web deverá aparecer.

    ![Resultados da publicação de aplicativos Bottle, Flask e Django no Serviço de Aplicativo](media/azure-publish-results.png)

## <a name="publishing-to-app-service---visual-studio-2015"></a>Publicação no Serviço de Aplicativo – Visual Studio 2015

> [!Note]
> Um breve vídeo desse processo pode ser encontrado em [Visual Studio Python Tutorial: Building a Website](https://www.youtube.com/watch?v=FJx5mutt1uk&list=PLReL099Y5nRdLgGAdrb_YeTdEnd23s6Ff&index=6) (Tutorial do Python do Visual Studio: compilando um site) (youtube.com, 3min10s).

1. No **Gerenciador de Soluções**, clique com o botão direito do mouse no projeto e selecione **Publicar**.

1. Na caixa de diálogo **Publicar**, selecione **Serviço de Aplicativo do Microsoft Azure**:

  ![Publicar no Azure etapa 1](media/tutorials-common-publish-1.png)

1. Selecione um destino:

    - Se você tiver uma assinatura do Azure, selecione **Serviço de Aplicativo do Microsoft Azure** como o destino de publicação e, em seguida, na próxima caixa de diálogo, selecione um Serviço de Aplicativo existente ou **Novo** para criar um novo.
    - Se estiver usando um local temporário de try.azurewebsites.net, selecione **Importação** como o destino de publicação, procure o arquivo `.publishsettings` baixado no site e selecione **OK**.

1. Os detalhes do Serviço de Aplicativo são exibidos na guia **Conexão** da caixa de diálogo **Publicar** abaixo.

  ![Publicar no Azure etapa 2](media/tutorials-common-publish-2.png)

1. Selecione **Avançar >**, conforme necessário, para examinar as configurações adicionais.

1. Selecione **Publicar**. Depois que o aplicativo for implantado no Azure, o navegador padrão será aberto nesse site.

Como parte desse processo, o Visual Studio também executa as seguintes etapas:

- Criar um arquivo `web.config` no servidor que contém ponteiros apropriados para a função `wsgi_app` do aplicativo e para o interpretador padrão do Python 3.4 do Serviço de Aplicativo.
- Desligar o processamento de arquivos na pasta `static` do projeto (as regras para isso estão no `web.config`).
- Publicar o ambiente virtual no servidor.
- Adicionar um arquivo `web.debug.config` e as ferramentas de depuração ptvsd para habilitar a depuração remota.

Conforme observado anteriormente, essas etapas automáticas simplificam o processo de publicação, mas tornam o controle do ambiente do Python mais difícil. Por exemplo, o arquivo `web.config` é criado somente no servidor mas não é adicionado ao seu projeto. O processo de publicação também leva mais tempo porque ele copia o ambiente virtual inteiro do seu computador de desenvolvimento em vez de confiar na configuração do servidor.

Eventualmente você talvez queira manter seu próprio arquivo `web.config` e usar o `requirements.txt` para manter os pacotes diretamente no servidor. O uso do `requirements.txt`, em particular, garante que seus ambientes de desenvolvimento e de servidor sejam sempre correspondentes.
