---
title: Criar uma instalação baseada em rede
description: Saiba como criar um ponto de instalação de rede para implantar o Visual Studio em uma empresa.
ms.date: 04/06/2021
ms.custom: seodec18
ms.topic: conceptual
helpviewer_keywords:
- '{{PLACEHOLDER}}'
- '{{PLACEHOLDER}}'
ms.assetid: 4CABFD20-962E-482C-8A76-E4012052F701
author: j-martens
ms.author: jmartens
manager: jmartens
ms.workload:
- multiple
ms.prod: visual-studio-windows
ms.technology: vs-installation
ms.openlocfilehash: 080c4450cfcdca28386811865229af75303beb6a
ms.sourcegitcommit: 5fb4a67a8208707e79dc09601e8db70b16ba7192
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2021
ms.locfileid: "112307525"
---
# <a name="create-a-network-installation-of-visual-studio"></a>Criar uma instalação de rede do Visual Studio

Às vezes, um administrador corporativo deseja criar um ponto de instalação de rede que contém Visual Studio arquivos que podem ser implantados em estações de trabalho cliente. Isso é para facilitar cenários em que os máquinas cliente podem ter permissões limitadas ou acesso limitado à Internet ou quando as equipes internas quiserem fazer testes de compatibilidade antes que sua organização padronizar em uma versão específica do modelo de ferramentas do desenvolvedor. Criamos um Visual Studio para que um administrador possa criar um layout de rede que basicamente está criando um _cache_ de arquivos localizado em um compartilhamento de rede estático interno que inclui todos os arquivos Visual Studio para instalação inicial e todas as atualizações futuras do produto.

 > [!NOTE]
 >  - Se você tiver várias edições do Visual Studio em uso em sua empresa (por exemplo, Visual Studio 2019 Professional e Visual Studio 2019 Enterprise), deverá criar um compartilhamento de instalação de rede separado para cada edição.
 >  - Recomendamos que você decida como deseja que os clientes recebam atualizações de produto _antes_ de fazer a instalação inicial do cliente.  Isso torna mais fácil garantir que suas opções de configuração sejam definidas corretamente. Suas opções incluem fazer com que os clientes recebam atualizações do local de layout de rede ou da Internet. 
 >  - O layout Visual Studio instalação original e todas as atualizações subsequentes do produto devem estar localizados no mesmo diretório de rede para garantir que a funcionalidade de reparo e desinstalação funcione corretamente.

## <a name="download-the-visual-studio-bootstrapper"></a>Baixar o bootstrapper do Visual Studio

Baixe um arquivo bootstrapper para a edição Visual Studio você deseja. Escolha Salvar **e,** em seguida, escolha **Abrir pasta**.

::: moniker range="vs-2017"

Para obter o bootstrapper mais recente do Visual Studio 2017 versão 15.9, acesse [Visual Studio](https://visualstudio.microsoft.com/vs/older-downloads/) página de versões anteriores e baixe um dos seguintes arquivos de bootstrapper:

| Edition                                      | Nome de arquivo            |
|----------------------------------------------|---------------------|
| Visual Studio 2017 Enterprise versão 15.9   | vs_enterprise.exe   |
| Visual Studio 2017 Professional versão 15.9 | vs_professional.exe |
| Visual Studio 2017 Build Tools versão 15.9  | vs_buildtools.exe   |

Outros bootstrappers com suporte incluem vs_feedbackclient.exe, vs_teamexplorer.exe, vs_testagent.exe, vs_testcontroller.exe e vs_testprofessional.exe.

::: moniker-end

::: moniker range="vs-2019"

Comece baixando o bootstrapper do Visual Studio 2019 na página [de downloads](https://visualstudio.microsoft.com/downloads) do Visual Studio ou na página [Versões do Visual Studio 2019](/visualstudio/releases/2019/history#installing-an-earlier-release) para sua versão e edição escolhidas do Visual Studio.  Seu executável de instalação ou para ser mais específico, um arquivo bootstrapper corresponderá ou será semelhante &mdash; &mdash; a um dos seguintes:

| Edition                    | Baixar                                                                                                                                                                                                                           |
|----------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Visual Studio Enterprise   | [vs_enterprise.exe](https://visualstudio.microsoft.com/thank-you-downloading-visual-studio/?sku=enterprise&rel=16&utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=network+install&utm_content=download+vs2019)     |
| Visual Studio Professional | [vs_professional.exe](https://visualstudio.microsoft.com/thank-you-downloading-visual-studio/?sku=professional&rel=16&utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=network+install&utm_content=download+vs2019) |
| Ferramentas de Build do Visual Studio  | [vs_buildtools.exe](https://visualstudio.microsoft.com/thank-you-downloading-visual-studio/?sku=buildtools&rel=16&utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=offline+install&utm_content=download+vs2019)     |

Outros bootstrappers com suporte [ incluemvs_teamexplorer.exe](https://download.visualstudio.microsoft.com/download/pr/f6473c9f-a5f6-4249-af28-c2fd14b6a0fb/4026077127d25d33789f3882998266946608d8ada378b6ed7c8fff8c07f3dde2/vs_TeamExplorer.exe), [vs_testagent.exe](https://download.visualstudio.microsoft.com/download/pr/f6473c9f-a5f6-4249-af28-c2fd14b6a0fb/1383bf8bcda3d0e986a2e42c14114aaea8a7b085d31aa0623c9f70b2bad130e4/vs_TestAgent.exe)e [vs_testcontroller.exe](https://download.visualstudio.microsoft.com/download/pr/f6473c9f-a5f6-4249-af28-c2fd14b6a0fb/54dcf24b76e7cd9fb8be0ac518a9dfba6daf18fe9b2aa1543411b1cda8820918/vs_TestController.exe).

::: moniker-end

::: moniker range=">=vs-2022"

>![!TIP]
> As versões Visual Studio 2022 ainda não estão disponíveis, os bootstrappers abaixo são para a versão prévia do Visual Studio 2022.
Comece baixando o bootstrapper Visual Studio 2022 da [página Visual Studio downloads](https://aka.ms/vs2022preview).

| Edition                    | Baixar                                                                             |
|----------------------------|--------------------------------------------------------------------------------------|
| Visual Studio Enterprise   | [vs_enterprise.exe](https://aka.ms/vs/17/preview/bootstrapper/vs_enterprise.exe)     |
| Visual Studio Professional | [vs_professional.exe](https://aka.ms/vs/17/preview/bootstrapper/vs_professional.exe) |

::: moniker-end

::: moniker range="vs-2017"

>[!TIP]
>Se você baixou anteriormente um arquivo bootstrapper e deseja verificar qual é a versão, veja como. No Windows, abra Explorador de Arquivos, clique com o botão direito do  mouse no arquivo bootstrapper, escolha **Propriedades,** escolha a guia Detalhes e, em seguida, veja o Número de **versão do** produto. Para corresponder esse número a uma versão do Visual Studio, consulte Visual Studio de build e [datas de lançamento.](visual-studio-build-numbers-and-release-dates.md)

::: moniker-end

::: moniker range="vs-2019"

>[!TIP]
>Se você baixou anteriormente um arquivo bootstrapper e deseja verificar qual é a versão, veja como. No Windows, abra Explorador de Arquivos, clique com o botão direito do  mouse no arquivo bootstrapper, escolha **Propriedades,** escolha a guia Detalhes e, em seguida, veja o Número de **versão do** produto. Para corresponder esse número a uma versão do Visual Studio, [consulte Visual Studio 2019.](/visualstudio/releases/2019/history)

::: moniker-end

::: moniker range=">=vs-2022"

>[!TIP]
>Se você baixou anteriormente um arquivo bootstrapper e deseja verificar qual é a versão, veja como. No Windows, abra Explorador de Arquivos, clique com o botão direito do  mouse no arquivo bootstrapper, escolha **Propriedades,** escolha a guia Detalhes e, em seguida, veja o Número de **versão do** produto. Para corresponder esse número a uma versão do Visual Studio, [consulte Visual Studio 2022.](/visualstudio/releases/2022/history)

::: moniker-end

## <a name="create-an-offline-installation-folder"></a>Criar uma pasta de instalação offline

Você deve ter uma conexão com a Internet para concluir esta etapa.

Abra um prompt de comando, navegue até o diretório no qual você baixou o bootstrapper e use os parâmetros do bootstrapper conforme definido na página Usar [parâmetros](../install/use-command-line-parameters-to-install-visual-studio.md) de linha de comando para instalar o Visual Studio para criar e manter o cache de instalação de rede. Exemplos comuns de criação de layouts iniciais são ilustrados abaixo e em [Exemplos](../install/command-line-parameter-examples.md)de parâmetro de linha de comando para Visual Studio instalação do .  

   > [!IMPORTANT]
   > Um layout inicial completo para uma única localidade de idioma requer cerca de 35 GB de espaço em disco para Visual Studio Community e 42 GB para Visual Studio Enterprise. Localidades [de idioma adicionais](use-command-line-parameters-to-install-visual-studio.md#list-of-language-locales) exigem cerca de meio GB cada. Confira a [seção Personalizar o layout de](#customize-the-network-layout) rede para obter mais informações. Fique atento de que as atualizações de layout subsequentes também devem ser armazenadas nesse mesmo local de rede, portanto, espere que o conteúdo do diretório do local de layout de rede possa ficar muito grande ao longo do tempo.  

- Para criar um layout inicial de Visual Studio Enterprise com todos os idiomas e todos os recursos, execute:

  ```vs_enterprise.exe --layout c:\VSLayout```

- Para criar um layout inicial de Visual Studio Professional com todos os idiomas e todos os recursos, execute:

  ```vs_professional.exe --layout c:\VSLayout```

## <a name="modify-the-responsejson-file"></a>Modificar o arquivo response.json

Você pode modificar o `response.json` arquivo para definir valores padrão que são usados quando a instalação é executado.  Por exemplo, você pode configurar o arquivo para selecionar um conjunto específico de cargas de `response.json` trabalho que devem ser selecionadas automaticamente. Você também pode configurar o `response.json` para especificar se o cliente só deve receber arquivos atualizados do local de layout de rede. Para obter mais informações, [consulte Automatizar Visual Studio instalação com um arquivo de resposta](../install/automated-installation-with-response-file.md). 

Se você tiver um problema com o bootstrapper Visual Studio ao emparelhá-lo com um arquivo, consulte Solucionar problemas de erros relacionados à rede ao instalar ou usar Visual Studio página para obter `response.json` mais informações. [](../install/troubleshooting-network-related-errors-in-visual-studio.md#error-failed-to-parse-id-from-parent-process)

## <a name="copy-the-layout-to-a-network-share"></a>Copiar o layout para um compartilhamento de rede

Hospede o layout em um compartilhamento de rede para que ele possa ser executado nos máquinas cliente.

O exemplo a seguir usa [`xcopy`](/windows-server/administration/windows-commands/xcopy/) . Você também pode usar [`robocopy`](/windows-server/administration/windows-commands/robocopy/) , se desejar.

::: moniker range="vs-2017"

Exemplo:

```shell
xcopy /e c:\VSLayout \\server\products\VS2017
```

::: moniker-end

::: moniker range="vs-2019"

```shell
xcopy /e c:\VSLayout \\server\products\VS2019
```

::: moniker-end

::: moniker range=">=vs-2022"

```shell
xcopy /e c:\VSLayout \\server\products\VS2022
```

::: moniker-end

> [!IMPORTANT]
> Para evitar um erro, verifique se o caminho de instalação completo tem menos do que 80 caracteres.

## <a name="customize-the-network-layout"></a>Personalizar o layout de rede

Há várias opções que você pode usar para personalizar o layout de rede. Você pode criar um layout parcial que contém apenas um conjunto específico de [localidades de idiomas](use-command-line-parameters-to-install-visual-studio.md#list-of-language-locales), [cargas de trabalho, componentes e suas dependências recomendadas ou opcionais](workload-and-component-ids.md). Isso pode ser útil se você sabe que só vai implantar um subconjunto de cargas de trabalho em estações de trabalho cliente. Parâmetros de linha de comando típicos para personalizar o layout incluem:

* `--add` para especificar [IDs de componente ou carga de trabalho](workload-and-component-ids.md). <br>Se `--add` for usado, somente as cargas de trabalho e os componentes especificados com `--add` serão baixados.  Se `--add` não for usado, todas as cargas de trabalho e todos os componentes serão baixados.
* `--includeRecommended` para incluir todos os componentes recomendados para as IDs de carga de trabalho especificadas
* `--includeOptional` para incluir todos os componentes recomendados e opcionais para as IDs de carga de trabalho especificadas.
* `--lang`para especificar [localidades de idioma.](use-command-line-parameters-to-install-visual-studio.md#list-of-language-locales)

Aqui estão alguns exemplos de como criar um layout personalizado parcial.

* Para baixar todas as cargas de trabalho e todos os componentes para um único idioma, execute:

    ```shell
    vs_enterprise.exe --layout C:\VSLayout --lang en-US
    ```

* Para baixar todas as cargas de trabalho e todos os componentes para vários idiomas, execute:

    ```shell
    vs_enterprise.exe --layout C:\VSLayout --lang en-US de-DE ja-JP
    ```

* Para baixar uma carga de trabalho para todos os idiomas, execute:

    ```shell
    vs_enterprise.exe --layout C:\VSLayout --add Microsoft.VisualStudio.Workload.Azure --includeRecommended
    ```

* Para baixar duas cargas de trabalho e um componente opcional para três idiomas, execute:

    ```shell
    vs_enterprise.exe --layout C:\VSLayout --add Microsoft.VisualStudio.Workload.Azure --add Microsoft.VisualStudio.Workload.ManagedDesktop --add Component.GitHub.VisualStudio --includeRecommended --lang en-US de-DE ja-JP
    ```

* Para baixar duas cargas de trabalho e todos os seus componentes recomendados:

    ```shell
    vs_enterprise.exe --layout C:\VSLayout --add Microsoft.VisualStudio.Workload.Azure --add Microsoft.VisualStudio.Workload.ManagedDesktop --add Component.GitHub.VisualStudio --includeRecommended
    ```

* Para baixar duas cargas de trabalho e todos os seus componentes opcionais e recomendados, execute:

    ```shell
    vs_enterprise.exe --layout C:\VSLayout --add Microsoft.VisualStudio.Workload.Azure --add Microsoft.VisualStudio.Workload.ManagedDesktop --add Component.GitHub.VisualStudio --includeOptional
    ```

### <a name="save-your-layout-options"></a>Salvar suas opções de layout

Quando você executa um comando de layout, as opções que você especifica são salvas (por exemplo, as cargas de trabalho e os idiomas). Comandos de layout subsequentes incluirão todas as opções anteriores.  Aqui está um exemplo de um layout com uma carga de trabalho apenas para inglês:

```shell
vs_enterprise.exe --layout c:\VSLayout --add Microsoft.VisualStudio.Workload.ManagedDesktop --lang en-US
```

Quando você quer atualizar o layout para uma versão mais recente, não é necessário especificar nenhum parâmetro de linha de comando adicional. As configurações anteriores são salvas e usadas por quaisquer comandos de layout subsequentes nesta pasta de layout.  O comando seguinte atualizará o layout parcial existente.

```shell
vs_enterprise.exe --layout c:\VSLayout
```

Você pode consultar aqui um exemplo de como adicionar uma carga de trabalho adicional. Nesse caso, vamos adicionar a carga de trabalho do Azure e um idioma traduzido.  Agora, tanto a Área de Trabalho Gerenciada quanto o Azure são incluídos neste layout.  Os recursos de idioma para inglês e alemão estão incluídos para todas essas cargas de trabalho. O layout é atualizado para a versão mais recente disponível.

```shell
vs_enterprise.exe --layout c:\VSLayout --add Microsoft.VisualStudio.Workload.Azure --lang de-DE
```

Se você deseja atualizar um layout existente para um layout completo, use a opção --all, conforme mostrado no exemplo a seguir.

```shell
vs_enterprise.exe --layout c:\VSLayout --all
```

## <a name="deploy-from-a-network-installation"></a>Implantação por meio de uma instalação de rede

Os administradores podem implantar o Visual Studio em estações de trabalho cliente como parte de um script de instalação. Ou, os usuários que têm direitos de administrador podem executar a instalação diretamente do compartilhamento para instalar o Visual Studio em seu computador.

* Os usuários podem fazer a instalação executando o seguinte comando: <br>

    ```shell
    \\server\products\VS\vs_enterprise.exe
    ```

* Os administradores podem fazer a instalação em um modo autônomo executando o seguinte comando:

    ```shell
    \\server\products\VS\vs_enterprise.exe --quiet --wait --norestart
    ```

> [!IMPORTANT]
> Para evitar um erro, verifique se o caminho de instalação completo tem menos do que 80 caracteres.

> [!TIP]
> Quando executada como parte de um arquivo em lotes, a opção `--wait` garante que o processo `vs_enterprise.exe` aguarde até que a instalação seja concluída antes de ela retornar um código de saída.
>
> Isso é útil se um administrador corporativo deseja executar ações adicionais em uma instalação concluída (por exemplo, para [aplicar uma chave do produto (Product Key) a uma instalação bem-sucedida](automatically-apply-product-keys-when-deploying-visual-studio.md)), mas precisa aguardar a conclusão da instalação para obter o código de retorno dessa instalação.
>
> Se você não usar `--wait`, o processo `vs_enterprise.exe` será encerrado antes que a instalação seja concluída e retornará um código de saída impreciso, que não representará o estado da operação de instalação.
>

::: moniker range=">=vs-2019"
> [!IMPORTANT]
> Para instalações offline, se você receber uma mensagem de erro informando "Um produto que corresponde aos parâmetros a seguir não pode ser encontrado", certifique-se de que você está usando a opção com a versão `--noweb` 16.3.5 ou posterior.
>
::: moniker-end

Quando você instala com base em um layout, o conteúdo instalado é adquirido do layout. No entanto, se você selecionar um componente que não está no layout, ele será adquirido da Internet.  Se você quiser impedir que a instalação do Visual Studio baixe qualquer conteúdo que está ausente em seu layout, use a opção `--noWeb`. Se `--noWeb` for usado e o layout não tiver qualquer conteúdo selecionado a ser instalado, a configuração falhará.

> [!TIP]
> Se você quiser instalar de uma fonte offline em um computador não conectado à Internet, especifique as opções `--noWeb` `--noUpdateInstaller` e . O primeiro impede o download de cargas de trabalho atualizadas, componentes e assim por diante. O último impede que o instalador se atualiza da Web.

> [!IMPORTANT]
> A opção não impede Visual Studio configuração em um computador conectado à `--noWeb` Internet para verificar se há atualizações. Para saber mais, confira a página [Controlar atualizações para implantações do Visual Studio baseadas em rede](controlling-updates-to-visual-studio-deployments.md).

### <a name="error-codes"></a>Códigos do Erro

Se você tiver usado o parâmetro `--wait`, dependendo do resultado da operação, a variável de ambiente `%ERRORLEVEL%` será definida como um dos seguintes valores:

[!INCLUDE[install-error-codes-md](includes/install-error-codes-md.md)]

## <a name="update-a-network-install-layout"></a>Atualizar um layout de instalação de rede

Quando atualizações de produto se tornam disponíveis, pode-se [atualizar o layout de instalação de rede](update-a-network-installation-of-visual-studio.md) para incorporar pacotes atualizados.

## <a name="how-to-create-a-layout-for-a-previous-visual-studio-release"></a>Como criar um layout para uma versão anterior do Visual Studio

Primeiro, você precisa entender que há dois tipos de bootstrappers do Visual Studio – um que pode ser caracterizado pelas palavras "latest", "current", "evergreen" e "tip" e outro que significa essencialmente "versão fixa". Ambos os tipos de arquivos bootstrapper têm exatamente o mesmo nome e a melhor maneira de distinguir o tipo é prestar atenção ao local em que você o recebeu. Os bootstrappers Visual Studio disponíveis na página [de downloads](https://visualstudio.microsoft.com/downloads) do Visual Studio são considerados bootstrappers Visual Studio evergreen e sempre instalam (ou atualizam) a versão mais recente disponível no canal no momento em que o bootstrapper é executado. Os bootstrappers do Visual Studio disponíveis na página Versões do [Visual Studio 2019](/visualstudio/releases/2019/history) [Visual Studio 2022](/visualstudio/releases/2022/history)  ou inseridos dentro da atualização de administrador no Catálogo do Microsoft Update instalam uma versão fixa específica do produto.

Portanto, se você baixar um bootstrapper Visual Studio evergreen hoje e o executar daqui a seis meses, ele instalará a versão Visual Studio atual no momento em que o bootstrapper for executado. Ele foi projetado para sempre instalar os bits mais recentes e mantê-lo atualizado.

Se você baixar um bootstrapper de link fixo ou se executar uma atualização de administrador baixada do Catálogo da Microsoft, ele sempre instalará uma versão específica do produto, independentemente de quando ele foi executado.

Por fim, você pode criar um layout de rede usando qualquer um desses bootstrappers e a versão que será criada no layout depende do bootstrapper que você está usando, por exemplo, ele será uma versão fixa ou atual. Em seguida, você pode atualizar o layout de rede usando qualquer bootstrapper posterior ou também pode usar o pacote de atualização do administrador do Microsoft Update Catalog. Independentemente de como você atualiza o layout, o layout atualizado resultante será um cache de pacote que contém uma versão específica do produto e, em seguida, ele se comportará como um bootstrapper de link fixo. Portanto, sempre que o cliente for instalado do layout, o cliente instalará a versão específica do Visual Studio existente no layout (embora uma versão mais recente possa existir online).

### <a name="how-to-get-support-for-your-offline-installer"></a>Como obter suporte para o instalador offline

Caso tenha um problema com a instalação offline, gostaríamos de saber a respeito. A melhor maneira de fazer isso é usando a ferramenta [Relatar um Problema](../ide/how-to-report-a-problem-with-visual-studio.md). Ao usar essa ferramenta, é possível enviar-nos a telemetria e os logs necessários para nos ajudar a diagnosticar e corrigir o problema.

Também oferecemos uma opção de suporte por meio de [**chat de instalação**](https://visualstudio.microsoft.com/vs/support/#talktous) (somente em inglês) para problemas relacionados à instalação.

Também temos outras opções de suporte disponíveis. Para obter uma lista, confira nossa página de [comentários](../ide/feedback-options.md).

## <a name="see-also"></a>Confira também

- [Guia do administrador do Visual Studio](visual-studio-administrator-guide.md)
- [Atualizar uma instalação em rede do Visual Studio](update-a-network-installation-of-visual-studio.md)
- [Solucionar problemas de erros relacionados à rede ao instalar ou usar Visual Studio](troubleshooting-network-related-errors-in-visual-studio.md)
- [Atualizações de controle para implantações do Visual Studio com base em rede](controlling-updates-to-visual-studio-deployments.md)
- [Visual Studio ciclo de vida e manutenção do produto](/visualstudio/releases/2019/servicing/)
- [Atualizar o Visual Studio enquanto estiver em uma linha de base de manutenção](update-servicing-baseline.md)
- [Usar parâmetros de linha de comando para instalar o Visual Studio](use-command-line-parameters-to-install-visual-studio.md)
- [IDs de carga de trabalho e de componente do Visual Studio](workload-and-component-ids.md)
- [Instalar os certificados necessários para instalação offline do Visual Studio](install-certificates-for-visual-studio-offline.md)
