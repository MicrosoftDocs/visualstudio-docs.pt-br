---
title: Configurar aplicativos Web do Python para o IIS
description: Como configurar aplicativos Web do Python para execução com os Serviços de Informações da Internet de uma máquina virtual do Windows.
ms.date: 12/06/2018
ms.topic: how-to
author: JoshuaPartlow
ms.author: joshuapa
manager: jillfra
ms.custom: seodec18
ms.workload:
- python
- data-science
- azure
ms.openlocfilehash: 3c756f3d9a89294ecce054650037be3f7b26c291
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85540927"
---
# <a name="configure-python-web-apps-for-iis"></a>Configurar aplicativos Web do Python para o IIS

Ao usar IIS (Serviços de Informações da Internet) como um servidor Web em um computador Windows (incluindo [máquinas virtuais do Windows no Azure](/azure/architecture/reference-architectures/n-tier/windows-vm), os aplicativos do Python devem incluir configurações específicas nos arquivos *web.config*, de forma que o IIS possa processar corretamente o código do Python. O próprio computador também deve ter o Python instalado, juntamente com quaisquer pacotes que o aplicativo Web exija.

> [!Note]
> Este artigo continha anteriormente diretrizes para configurar o Python no Serviço de Aplicativo do Azure no Windows. As extensões do Python e os hosts de Windows usados nesse cenário foram preteridos em favor do Serviço de Aplicativo do Azure no Linux. Para saber mais, confira [Publicar aplicativos do Python no Serviço de Aplicativo do Azure (Linux)](publishing-python-web-applications-to-azure-from-visual-studio.md). No entanto, o artigo anterior ainda está disponível em [Gerenciar o Serviço de Aplicativo no Windows com as extensões do Python](managing-python-on-azure-app-service.md).

## <a name="install-python-on-windows"></a>Instalar o Python no Windows

Para executar um aplicativo Web, primeiro instale a versão necessária do Python diretamente no computador host do Windows, conforme descrito em [Instalar interpretadores do Python](installing-python-interpreters.md).

Registre o local do interpretador do `python.exe` para etapas posteriores. Para sua conveniência, você pode adicionar esse local à variável de ambiente PATH.

## <a name="install-packages"></a>Instalar Pacotes

Ao usar um host dedicado, você pode usar o ambiente global do Python para executar o aplicativo, em vez de um ambiente virtual. Da mesma forma, você pode instalar todos os requisitos do aplicativo no ambiente global simplesmente executando `pip install -r requirements.txt` em um prompt de comando.

## <a name="set-webconfig-to-point-to-the-python-interpreter"></a>Configurar o web.config para apontar para o interpretador do Python

O arquivo *web.config* do aplicativo instrui o servidor Web do IIS (7 ou posterior) em execução no Windows sobre como ele deve tratar as solicitações do Python por meio de HttpPlatform (recomendado) ou FastCGI. As versões do Visual Studio 2015 e anterior fazem essas modificações automaticamente. Ao usar o Visual Studio 2017 e posterior, você deve modificar *web.config* manualmente.

### <a name="configure-the-httpplatform-handler"></a>Configurar o manipulador HttpPlatform

O módulo HttpPlatform passa conexões de soquete diretamente para um processo de Python autônomo. Essa passagem permite que você execute qualquer servidor Web que desejar, mas requer um script de inicialização que executa um servidor Web local. Você especifica o script no `<httpPlatform>`elemento do *web.config*, em que o atributo `processPath` aponta para o interpretador do Python da extensão de site e o atributo `arguments` aponta para seu script e os argumentos que você quiser fornecer:

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
  <system.webServer>
    <handlers>
      <add name="PythonHandler" path="*" verb="*" modules="httpPlatformHandler" resourceType="Unspecified"/>
    </handlers>
    <httpPlatform processPath="c:\python36-32\python.exe"
                  arguments="c:\home\site\wwwroot\runserver.py --port %HTTP_PLATFORM_PORT%"
                  stdoutLogEnabled="true"
                  stdoutLogFile="c:\home\LogFiles\python.log"
                  startupTimeLimit="60"
                  processesPerApplication="16">
      <environmentVariables>
        <environmentVariable name="SERVER_PORT" value="%HTTP_PLATFORM_PORT%" />
      </environmentVariables>
    </httpPlatform>
  </system.webServer>
</configuration>
```

A variável de ambiente `HTTP_PLATFORM_PORT` mostrada aqui contém a porta que o servidor local deve escutar para as conexões do localhost. Este exemplo também mostra como criar outra variável de ambiente, se desejado, nesse caso `SERVER_PORT`.

### <a name="configure-the-fastcgi-handler"></a>Configurar o manipulador do FastCGI

O FastCGI é uma interface que funciona no nível da solicitação. O IIS recebe conexões de entrada e encaminha cada solicitação para um aplicativo WSGI em execução em um ou mais processos Python persistentes.

Para usá-lo, primeiro instale e configure o pacote wfastcgi, conforme descrito em [pypi.org/project/wfastcgi/](https://pypi.io/project/wfastcgi).

Em seguida, modifique o arquivo *web.config* do aplicativo para incluir os caminhos completos para *python.exe* e *wfastcgi.py* na chave `PythonHandler`. As etapas a seguir pressupõem que o Python esteja instalado em *c:\python36-32* e que o código do aplicativo esteja em *c:\home\site\wwwroot*. Faça ajustes de maneira adequada para seus caminhos:

1. Modifique a entrada `PythonHandler` em *web.config* para que o caminho corresponda à localização de instalação do Python (confira [Referência de configuração do IIS](https://www.iis.net/configreference) (iis.net) para obter detalhes exatos).

    ```xml
    <system.webServer>
      <handlers>
        <add name="PythonHandler" path="*" verb="*" modules="FastCgiModule"
            scriptProcessor="c:\python36-32\python.exe|c:\python36-32\wfastcgi.py"
            resourceType="Unspecified" requireAccess="Script"/>
      </handlers>
    </system.webServer>
    ```

1. Na `<appSettings>` seção de *web.config*, adicione chaves para `WSGI_HANDLER` , `WSGI_LOG` (opcional) e `PYTHONPATH` :

    ```xml
    <appSettings>
      <add key="PYTHONPATH" value="c:\home\site\wwwroot"/>
      <!-- The handler here is specific to Bottle; see the next section. -->
      <add key="WSGI_HANDLER" value="app.wsgi_app()"/>
      <add key="WSGI_LOG" value="c:\home\LogFiles\wfastcgi.log"/>
    </appSettings>
    ```

    Esses valores `<appSettings>` estão disponíveis para seu aplicativo como variáveis de ambiente:

    - O valor de `PYTHONPATH` pode ser estendido livremente, mas deve incluir a raiz do seu aplicativo.
    - `WSGI_HANDLER` deve apontar para um aplicativo WSGI importável do seu aplicativo.
    - `WSGI_LOG` é opcional, mas recomendado para depuração do seu aplicativo.

1. Defina a entrada `WSGI_HANDLER` em *web.config* de acordo com a estrutura que você está usando:

    - **Bottle**: verifique se há parênteses depois de `app.wsgi_app`, conforme mostrado abaixo. Isso é necessário porque esse objeto é uma função (consulte *app.py*) em vez de uma variável:

        ```xml
        <!-- Bottle apps only -->
        <add key="WSGI_HANDLER" value="app.wsgi_app()"/>
        ```

    - **Flask**: altere o valor de `WSGI_HANDLER` para `<project_name>.app`, em que `<project_name>` corresponde ao nome do seu projeto. Você pode localizar o identificador exato examinando a instrução `from <project_name> import app` no *runserver.py*. Por exemplo, se o projeto fosse denominado "FlaskAzurePublishExample", a entrada seria semelhante ao seguinte:

        ```xml
        <!-- Flask apps only: change the project name to match your app -->
        <add key="WSGI_HANDLER" value="flask_iis_example.app"/>
        ```

    - **Django**: duas alterações são necessárias no *web.config* para projetos Django. Primeiro, altere o valor de `WSGI_HANDLER` para `django.core.wsgi.get_wsgi_application()` (o objeto está no arquivo *wsgi.py*):

        ```xml
        <!-- Django apps only -->
        <add key="WSGI_HANDLER" value="django.core.wsgi.get_wsgi_application()"/>
        ```

        Em seguida, adicione a seguinte entrada abaixo da do `WSGI_HANDLER`, substituindo `DjangoAzurePublishExample` pelo nome do seu projeto:

        ```xml
        <add key="DJANGO_SETTINGS_MODULE" value="django_iis_example.settings" />
        ```

1. **Somente aplicativos do Django**: no arquivo *settings.py* do projeto do Django, adicione o domínio de URL do site ou o endereço IP para `ALLOWED_HOSTS`, conforme mostrado abaixo, substituindo '1.2.3.4' por endereço IP ou URL, claro:

    ```python
    # Change the URL or IP address to your specific site
    ALLOWED_HOSTS = ['1.2.3.4']
    ```

    A falha ao adicionar a URL à matriz resulta no erro **DisallowedHost/cabeçalho de HTTP_HOST inválido: ' \<site URL\> '. Talvez seja necessário adicionar ' \<site URL\> ' a ALLOWED_HOSTS.**

    Observe que, quando a matriz estiver vazia, o Django permitirá automaticamente 'localhost' e '127.0.0.1', mas adicionar sua URL de produção removerá essas funcionalidades. Por esse motivo, talvez você queira manter cópias do *settings.py* de desenvolvimento e de produção separadas ou usar variáveis de ambiente para controlar os valores de tempo de execução.

## <a name="deploy-to-iis-or-a-windows-vm"></a>Implantar em IIS ou em uma VM do Windows

Com o arquivo *web.config* correto no projeto, você pode publicar no computador que executa o IIS usando o comando **Publish** no menu de contexto do projeto no **Gerenciador de Soluções** e selecionando a opção **IIS, FTP etc.**. Nesse caso, o Visual Studio simplesmente copia os arquivos do projeto para o servidor. Você é responsável por toda a configuração do lado do servidor.
