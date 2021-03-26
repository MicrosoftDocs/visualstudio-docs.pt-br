---
title: Criar uma instalação baseada em rede
description: Saiba como criar um ponto de instalação de rede para implantar o Visual Studio em uma empresa.
ms.date: 08/27/2020
ms.custom: seodec18
ms.topic: conceptual
helpviewer_keywords:
- '{{PLACEHOLDER}}'
- '{{PLACEHOLDER}}'
ms.assetid: 4CABFD20-962E-482C-8A76-E4012052F701
author: ornellaalt
ms.author: ornella
manager: jmartens
ms.workload:
- multiple
ms.prod: visual-studio-windows
ms.technology: vs-installation
ms.openlocfilehash: e76c5346230b6991f238384a4852938dcc540f6c
ms.sourcegitcommit: 00e16b9afe6b22ba0591e4d0d92690544e6d4357
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/26/2021
ms.locfileid: "105616929"
---
# <a name="create-a-network-installation-of-visual-studio"></a>Criar uma instalação de rede do Visual Studio

Normalmente, um administrador corporativo cria um ponto de instalação de rede para implantação em estações de trabalho do cliente. Criamos o Visual Studio para permitir que você armazene em cache os arquivos para a instalação inicial juntamente com todas as atualizações de produto para uma única pasta. (Esse processo também é referido como _criação de um layout_.)

Fizemos isso para que as estações de trabalho cliente pudessem usar o mesmo local de rede para gerenciar sua instalação, mesmo que elas ainda não tivessem sido atualizadas para a atualização de serviço mais recente.

 > [!NOTE]
 > Se você tiver várias edições do Visual Studio em uso em sua empresa (por exemplo, o Visual Studio Professional e o Visual Studio Enteprise), precisará criar um compartilhamento de instalação de rede separado para cada edição.

## <a name="download-the-visual-studio-bootstrapper"></a>Baixar o bootstrapper do Visual Studio

Baixe um arquivo bootstrapper para a edição do Visual Studio que você deseja. Certifique-se de escolher **salvar** e, em seguida, escolha **abrir pasta**.

::: moniker range="vs-2017"

Para obter um bootstrapper para o Visual Studio 2017, consulte a página de download de [versões anteriores do Visual Studio](https://visualstudio.microsoft.com/vs/older-downloads/) para obter detalhes sobre como fazer isso.

Seu executável de instalação &mdash; ou ser mais específico, o arquivo bootstrapper &mdash; deve corresponder ou ser semelhante a um dos seguintes.

| Edition | Nome de arquivo |
|-------------|-----------------------|
|Visual Studio Enterprise | **vs_enterprise.exe** |
|Visual Studio Professional | **vs_professional.exe** |
|Ferramentas de Build do Visual Studio   | **vs_buildtools.exe** |

Outros bootstrapper com suporte incluem **vs_feedbackclient.exe**, **vs_teamexplorer.exe**, **vs_testagent.exe**, **vs_testcontroller.exe** e **vs_testprofessional.exe**.

::: moniker-end

::: moniker range="vs-2019"

Seu executável de instalação &mdash; ou ser mais específico, um arquivo bootstrapper &mdash; deve corresponder ou ser semelhante a um dos itens a seguir.

|Edition | Baixar|
|-------------|-----------------------|
|Visual Studio Enterprise | [**vs_enterprise.exe**](https://visualstudio.microsoft.com/thank-you-downloading-visual-studio/?sku=enterprise&rel=16&utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=network+install&utm_content=download+vs2019) |
|Visual Studio Professional | [**vs_professional.exe**](https://visualstudio.microsoft.com/thank-you-downloading-visual-studio/?sku=professional&rel=16&utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=network+install&utm_content=download+vs2019) |
| Ferramentas de Build do Visual Studio   | [**vs_buildtools.exe**](https://visualstudio.microsoft.com/thank-you-downloading-visual-studio/?sku=buildtools&rel=16&utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=offline+install&utm_content=download+vs2019) |

Outros bootstrapper com suporte incluem [vs_teamexplorer.exe](https://download.visualstudio.microsoft.com/download/pr/f6473c9f-a5f6-4249-af28-c2fd14b6a0fb/4026077127d25d33789f3882998266946608d8ada378b6ed7c8fff8c07f3dde2/vs_TeamExplorer.exe), [vs_testagent.exe](https://download.visualstudio.microsoft.com/download/pr/f6473c9f-a5f6-4249-af28-c2fd14b6a0fb/1383bf8bcda3d0e986a2e42c14114aaea8a7b085d31aa0623c9f70b2bad130e4/vs_TestAgent.exe)e [vs_testcontroller.exe](https://download.visualstudio.microsoft.com/download/pr/f6473c9f-a5f6-4249-af28-c2fd14b6a0fb/54dcf24b76e7cd9fb8be0ac518a9dfba6daf18fe9b2aa1543411b1cda8820918/vs_TestController.exe).

::: moniker-end

>[!TIP]
>Se você tiver baixado anteriormente um arquivo bootstrapper e quiser verificar sua versão, veja como fazer isso. No Windows, abra o explorador de arquivos, clique com o botão direito do mouse no arquivo bootstrapper, escolha **Propriedades**, escolha a guia **detalhes** e, em seguida, exiba o número de **versão do produto** . Para corresponder esse número a uma versão do Visual Studio, consulte a página [números de compilação e datas de lançamento do Visual Studio](visual-studio-build-numbers-and-release-dates.md) .

## <a name="create-an-offline-installation-folder"></a>Criar uma pasta de instalação offline

Você deve ter uma conexão com a Internet para concluir esta etapa. Para criar uma instalação offline com todos os idiomas e todos os recursos, use um comando semelhante a um dos exemplos a seguir. Essa pasta deve permanecer estática e todas as atualizações para o layout devem ser incluídas nessa pasta. 

   > [!IMPORTANT]
   > Um layout completo para uma localidade de idioma único requer cerca de 35 GB de espaço em disco para a Comunidade do Visual Studio e 42 GB para Visual Studio Enterprise. As [localidades de idioma](use-command-line-parameters-to-install-visual-studio.md#list-of-language-locales) adicionais exigem cerca de metade a GB cada. Consulte a seção [Personalizar o layout de rede](#customize-the-network-layout) para obter mais informações.
   >
   > [!TIP]
   > Lembre-se de executar o comando no diretório de Download. Normalmente, isso é `C:\Users\<username>\Downloads` em um computador que executa o Windows 10.

- Para o Visual Studio Enterprise, execute:

  ```vs_enterprise.exe --layout c:\VSLayout```

- Para o Visual Studio Professional, execute:

  ```vs_professional.exe --layout c:\VSLayout```

## <a name="modify-the-responsejson-file"></a>Modificar o arquivo response.json

Você pode modificar response.json para definir valores padrão que serão usados quando a instalação for executada.  Por exemplo, você pode configurar o arquivo `response.json` para selecionar um conjunto específico de cargas de trabalho selecionadas automaticamente. Confira [Automatizar a instalação do Visual Studio com um arquivo de resposta](automated-installation-with-response-file.md) para obter detalhes.

E, se você tiver um problema com o inicializador do Visual Studio gerando um erro ao emparelhar com um response.jsno arquivo, consulte a seção "falha ao analisar a ID do processo pai" em [solucionar erros relacionados à rede ao instalar ou usar o Visual Studio](troubleshooting-network-related-errors-in-visual-studio.md#error-failed-to-parse-id-from-parent-process) página para obter mais informações sobre o que fazer.

## <a name="copy-the-layout-to-a-network-share"></a>Copiar o layout para um compartilhamento de rede

Hospede o layout em um compartilhamento de rede para que ele possa ser executado de outros computadores.

O exemplo a seguir usa [xcopy](/windows-server/administration/windows-commands/xcopy/). Também é possível usar [robocopy](/windows-server/administration/windows-commands/robocopy/), caso queira.

::: moniker range="vs-2017"

Exemplo:

```cmd
xcopy /e c:\VSLayout \\server\products\VS2017
```

::: moniker-end

::: moniker range="vs-2019"

```cmd
xcopy /e c:\VSLayout \\server\products\VS2019
```

::: moniker-end

> [!IMPORTANT]
> Para evitar um erro, verifique se o caminho de instalação completo tem menos do que 80 caracteres.

## <a name="customize-the-network-layout"></a>Personalizar o layout de rede

Há várias opções que você pode usar para personalizar o layout de rede. Você pode criar um layout parcial que contém apenas um conjunto específico de [localidades de idiomas](use-command-line-parameters-to-install-visual-studio.md#list-of-language-locales), [cargas de trabalho, componentes e suas dependências recomendadas ou opcionais](workload-and-component-ids.md). Isso pode ser útil se você sabe que só vai implantar um subconjunto de cargas de trabalho em estações de trabalho cliente. Parâmetros de linha de comando típicos para personalizar o layout incluem:

* `--add` para especificar [IDs de componente ou carga de trabalho](workload-and-component-ids.md). <br>Se `--add` for usado, somente as cargas de trabalho e os componentes especificados com `--add` serão baixados.  Se `--add` não for usado, todas as cargas de trabalho e todos os componentes serão baixados.
* `--includeRecommended` para incluir todos os componentes recomendados para as IDs de carga de trabalho especificadas
* `--includeOptional` para incluir todos os componentes recomendados e opcionais para as IDs de carga de trabalho especificadas.
* `--lang` para especificar as [localidades de idioma](use-command-line-parameters-to-install-visual-studio.md#list-of-language-locales).

Aqui estão alguns exemplos de como criar um layout personalizado parcial.

* Para baixar todas as cargas de trabalho e todos os componentes para um único idioma, execute:

    ```cmd
    vs_enterprise.exe --layout C:\VSLayout --lang en-US
    ```

* Para baixar todas as cargas de trabalho e todos os componentes para vários idiomas, execute:

    ```cmd
    vs_enterprise.exe --layout C:\VSLayout --lang en-US de-DE ja-JP
    ```

* Para baixar uma carga de trabalho para todos os idiomas, execute:

    ```cmd
    vs_enterprise.exe --layout C:\VSLayout --add Microsoft.VisualStudio.Workload.Azure --includeRecommended
    ```

* Para baixar duas cargas de trabalho e um componente opcional para três idiomas, execute:

    ```cmd
    vs_enterprise.exe --layout C:\VSLayout --add Microsoft.VisualStudio.Workload.Azure --add Microsoft.VisualStudio.Workload.ManagedDesktop --add Component.GitHub.VisualStudio --includeRecommended --lang en-US de-DE ja-JP
    ```

* Para baixar duas cargas de trabalho e todos os seus componentes recomendados:

    ```cmd
    vs_enterprise.exe --layout C:\VSLayout --add Microsoft.VisualStudio.Workload.Azure --add Microsoft.VisualStudio.Workload.ManagedDesktop --add Component.GitHub.VisualStudio --includeRecommended
    ```

* Para baixar duas cargas de trabalho e todos os seus componentes opcionais e recomendados, execute:

    ```cmd
    vs_enterprise.exe --layout C:\VSLayout --add Microsoft.VisualStudio.Workload.Azure --add Microsoft.VisualStudio.Workload.ManagedDesktop --add Component.GitHub.VisualStudio --includeOptional
    ```

::: moniker range="vs-2017"

### <a name="new-in-version-153"></a>Novidades na versão 15.3

::: moniker-end

::: moniker range="vs-2019"

### <a name="save-your-layout-options"></a>Salvar suas opções de layout

::: moniker-end

Quando você executa um comando de layout, as opções que você especifica são salvas (por exemplo, as cargas de trabalho e os idiomas). Comandos de layout subsequentes incluirão todas as opções anteriores.  Aqui está um exemplo de um layout com uma carga de trabalho apenas para inglês:

```cmd
vs_enterprise.exe --layout c:\VSLayout --add Microsoft.VisualStudio.Workload.ManagedDesktop --lang en-US
```

Quando você quer atualizar o layout para uma versão mais recente, não é necessário especificar nenhum parâmetro de linha de comando adicional. As configurações anteriores são salvas e usadas por quaisquer comandos de layout subsequentes nesta pasta de layout.  O comando seguinte atualizará o layout parcial existente.

```cmd
vs_enterprise.exe --layout c:\VSLayout
```

Você pode consultar aqui um exemplo de como adicionar uma carga de trabalho adicional. Nesse caso, vamos adicionar a carga de trabalho do Azure e um idioma traduzido.  Agora, tanto a Área de Trabalho Gerenciada quanto o Azure são incluídos neste layout.  Os recursos de idioma para inglês e alemão estão incluídos para todas essas cargas de trabalho. O layout é atualizado para a versão mais recente disponível.

```cmd
vs_enterprise.exe --layout c:\VSLayout --add Microsoft.VisualStudio.Workload.Azure --lang de-DE
```

Se você deseja atualizar um layout existente para um layout completo, use a opção --all, conforme mostrado no exemplo a seguir.

```cmd
vs_enterprise.exe --layout c:\VSLayout --all
```

## <a name="deploy-from-a-network-installation"></a>Implantação por meio de uma instalação de rede

Os administradores podem implantar o Visual Studio em estações de trabalho cliente como parte de um script de instalação. Ou, os usuários que têm direitos de administrador podem executar a instalação diretamente do compartilhamento para instalar o Visual Studio em seu computador.

* Os usuários podem fazer a instalação executando o seguinte comando: <br>

    ```cmd
    \\server\products\VS\vs_enterprise.exe
    ```

* Os administradores podem fazer a instalação em um modo autônomo executando o seguinte comando:

    ```cmd
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

::: moniker range="vs-2019"
> [!IMPORTANT]
> Para instalações offline, se você receber uma mensagem de erro dizendo "um produto correspondente aos seguintes parâmetros não pode ser encontrado", certifique-se de estar usando a `--noweb` opção com a versão 16.3.5 ou posterior.
>
::: moniker-end

Quando você instala com base em um layout, o conteúdo instalado é adquirido do layout. No entanto, se você selecionar um componente que não está no layout, ele será adquirido da Internet.  Se você quiser impedir que a instalação do Visual Studio baixe qualquer conteúdo que está ausente em seu layout, use a opção `--noWeb`. Se `--noWeb` for usado e o layout não tiver qualquer conteúdo selecionado a ser instalado, a configuração falhará.

> [!TIP]
> Se você quiser instalar o de uma fonte offline em um computador conectado que não seja da Internet, especifique `--noWeb` as `--noUpdateInstaller` Opções e. O primeiro impede o download de cargas de trabalho atualizadas, componentes e assim por diante. A última opção impede que o instalador seja atualizado da Web automaticamente.

> [!IMPORTANT]
> A `--noWeb` opção não interrompe a instalação do Visual Studio em um computador conectado à Internet de verificar se há atualizações. Para saber mais, confira a página [Controlar atualizações para implantações do Visual Studio baseadas em rede](controlling-updates-to-visual-studio-deployments.md).

### <a name="error-codes"></a>Códigos do Erro

Se você tiver usado o parâmetro `--wait`, dependendo do resultado da operação, a variável de ambiente `%ERRORLEVEL%` será definida como um dos seguintes valores:

[!INCLUDE[install-error-codes-md](includes/install-error-codes-md.md)]

## <a name="update-a-network-install-layout"></a>Atualizar um layout de instalação de rede

Quando atualizações de produto se tornam disponíveis, pode-se [atualizar o layout de instalação de rede](update-a-network-installation-of-visual-studio.md) para incorporar pacotes atualizados.

## <a name="how-to-create-a-layout-for-a-previous-visual-studio-release"></a>Como criar um layout para uma versão anterior do Visual Studio

::: moniker range="vs-2017"

> [!NOTE]
> Os bootstrappers do Visual Studio disponíveis em [visualstudio.microsoft.com](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=inline+link&utm_content=download+vs2017) baixam e instalam a última versão do Visual Studio disponível sempre que são executados.
>
> Portanto, se você baixar um *bootstrapper* do Visual Studio hoje e executá-lo daqui a seis meses, ele instalará a versão do Visual Studio disponível no momento em que você executar o bootstrapper.
>
> Porém, se você criar um *layout* e, em seguida, fizer a instalação por meio dele, o layout instalará a versão específica do Visual Studio existente nele. Mesmo que uma versão mais recente exista online, você obterá a versão do Visual Studio que está no layout.

::: moniker-end

::: moniker range="vs-2019"

> [!NOTE]
> Os bootstrappers do Visual Studio disponíveis em [visualstudio.microsoft.com](https://visualstudio.microsoft.com/downloads) baixam e instalam a última versão do Visual Studio disponível sempre que são executados.
>
> Portanto, se você baixar um *bootstrapper* do Visual Studio hoje e executá-lo daqui a seis meses, ele instalará a versão do Visual Studio disponível no momento em que você executar o bootstrapper.
>
> Porém, se você criar um *layout* e, em seguida, fizer a instalação por meio dele, o layout instalará a versão específica do Visual Studio existente nele. Mesmo que uma versão mais recente exista online, você obterá a versão do Visual Studio que está no layout.

::: moniker-end

Se você precisar criar um layout para uma versão mais antiga do Visual Studio, vá para [https://my.visualstudio.com](https://my.visualstudio.com) para baixar as versões "fixas" dos inicializadores do Visual Studio.

### <a name="how-to-get-support-for-your-offline-installer"></a>Como obter suporte para o instalador offline

Caso tenha um problema com a instalação offline, gostaríamos de saber a respeito. A melhor maneira de fazer isso é usando a ferramenta [Relatar um Problema](../ide/how-to-report-a-problem-with-visual-studio.md). Ao usar essa ferramenta, é possível enviar-nos a telemetria e os logs necessários para nos ajudar a diagnosticar e corrigir o problema.

Também oferecemos uma opção de suporte por meio de [**chat de instalação**](https://visualstudio.microsoft.com/vs/support/#talktous) (somente em inglês) para problemas relacionados à instalação.

Também temos outras opções de suporte disponíveis. Para obter uma lista, confira nossa página de [comentários](../ide/feedback-options.md).

## <a name="see-also"></a>Consulte também

- [Guia do administrador do Visual Studio](visual-studio-administrator-guide.md)
- [Atualizar uma instalação em rede do Visual Studio](update-a-network-installation-of-visual-studio.md)
- [Solucionar erros relacionados à rede ao instalar ou usar o Visual Studio](troubleshooting-network-related-errors-in-visual-studio.md)
- [Atualizações de controle para implantações do Visual Studio com base em rede](controlling-updates-to-visual-studio-deployments.md)
- [Ciclo de vida do produto Visual Studio e manutenção](/visualstudio/releases/2019/servicing/)
- [Atualizar o Visual Studio enquanto estiver em uma linha de base de manutenção](update-servicing-baseline.md)
- [Usar parâmetros de linha de comando para instalar o Visual Studio](use-command-line-parameters-to-install-visual-studio.md)
- [IDs de carga de trabalho e de componente do Visual Studio](workload-and-component-ids.md)
- [Instalar os certificados necessários para instalação offline do Visual Studio](install-certificates-for-visual-studio-offline.md)
