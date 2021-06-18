---
title: Atualizar o Visual Studio enquanto estiver em uma linha de base de manutenção
description: Aprenda como atualizar o Visual Studio enquanto estiver em uma linha de base de manutenção.
ms.date: 07/17/2019
ms.custom: seodec18
ms.topic: conceptual
ms.assetid: ''
author: j-martens
ms.author: jmartens
manager: jmartens
ms.workload:
- multiple
ms.prod: visual-studio-windows
ms.technology: vs-installation
monikerRange: '>=vs-2019'
ms.openlocfilehash: 03a192657a46c2db15cb2d1121735905f06da478
ms.sourcegitcommit: 5fb4a67a8208707e79dc09601e8db70b16ba7192
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2021
ms.locfileid: "112306664"
---
# <a name="update-visual-studio-while-on-a-servicing-baseline"></a>Atualizar o Visual Studio enquanto estiver em uma linha de base de manutenção

Atualizamos o Visual Studio com frequência durante seu ciclo de vida de produto. Há dois tipos de atualizações:

* **Atualizações de versão secundárias** &mdash; por exemplo, 16.0 a 16.1 &mdash; que incluem novos recursos e componentes.  
* **Atualizações de manutenção**, por exemplo, 16.0.4 a 16.0.5, que incluem apenas correções direcionadas para problemas críticos.

Os administradores do Enterprise podem optar por manter seus clientes em uma linha de base de manutenção. Uma linha de base de manutenção é compatível com as atualizações de manutenção por um ano após o lançamento da próxima linha de base de manutenção.

A opção de linha de base de manutenção proporciona aos desenvolvedores e administradores maior flexibilidade na adoção de novos recursos, correções de bug ou componentes incluídos nas novas atualizações secundárias. A primeira linha de base de manutenção é a 16.0.x. Para saber mais, confira [Opções de suporte para clientes empresariais e profissionais](/visualstudio/releases/2019/servicing#support-options-for-enterprise-and-professional-customers).

## <a name="how-to-get-onto-a-servicing-baseline"></a>Como obter uma linha de base de manutenção

Para começar a usar uma linha de base de manutenção, baixe um inicializador do instalador da versão corrigida do Visual Studio em [My.VisualStudio.com](https://my.visualstudio.com/Downloads?q=visual%20studio%202019%20version%2016.0). Os inicializadores têm links para as configurações do produto, as cargas de trabalho e componentes dessa versão específica.

> [!NOTE]
> Tenha cuidado ao distinguir entre os inicializadores de versão corrigida e padrão. Os inicializadores padrão são configurados para usar a versão mais recente disponível do Visual Studio. Os inicializadores padrão têm um número no nome do arquivo (por exemplo, vs_enterprise__123456789-123456789.exe) quando eles são baixados de My.VisualStudio.com.

Durante a instalação, os administradores de empresa devem configurar seus clientes para impedir que eles atualizem para a versão mais recente. Há várias maneiras de fazer isso:
- [Altere a `channelUri` configuração no arquivo de configuração de resposta](update-servicing-baseline.md#install-a-servicing-baseline-on-a-network) para usar um manifesto do canal na pasta local ou de layout.
- [Modifique o channelUri executando a linha de comando](update-servicing-baseline.md#install-a-servicing-baseline-via-the-internet) para usar um arquivo inexistente.
- [Defina políticas no sistema cliente para desabilitar atualizações](update-servicing-baseline.md#use-policy-settings-to-disable-clients-from-updating) para impedir a atualização automática nos clientes.

### <a name="install-a-servicing-baseline-on-a-network"></a>Instalar uma linha de base de manutenção em uma rede

Os administradores que usam uma instalação de layout de rede devem modificar o valor `channelUri` no arquivo *response.json* no layout para usar o arquivo *channelmanifest.json* que está na mesma pasta. Para saber as etapa a seguir, confira [Controlar atualizações para implantações do Visual Studio baseadas em rede](controlling-updates-to-visual-studio-deployments.md). Alterar o valor `channelUri` permite que os clientes procurem atualizações no local de layout.

### <a name="install-a-servicing-baseline-via-the-internet"></a>Instalar uma linha de base de manutenção via internet

Para uma instalação baseada na internet, adicione `--channelUri` com um manifesto de canal inexistente à linha de comando usada para iniciar a instalação. Isso desabilita o Visual Studio de usar a versão mais recente disponível para uma atualização. Aqui está um exemplo:

```shell
vs_enterprise.exe --channelUri c:\doesnotexist.chman
```

### <a name="use-policy-settings-to-disable-clients-from-updating"></a>Use as configurações de política para desabilitar clientes da atualização

Outra opção para controlar as atualizações em um cliente é [desativar as notificações de atualização](controlling-updates-to-visual-studio-deployments.md). Use esta opção se o valor de channelUri não tiver sido alterado na instalação. Ele impedirá que o cliente receba links da última versão disponível. Um inicializador de versão fixa ainda é necessário para atualizar para uma versão específica no cliente.

## <a name="how-to-stay-on-a-servicing-baseline"></a>Como manter-se em uma linha de base de manutenção

Quando uma atualização para uma linha de base de manutenção estiver disponível, os arquivos do inicializador de versão fixa serão disponibilizados para a atualização da manutenção do [My.VisualStudio.com](https://my.visualstudio.com/Downloads?q=visual%20studio%202019%20version%2016.0).

Para administradores que implantam usando uma instalação de layout de rede, o administrador deve atualizar a [localização do layout](update-a-network-installation-of-visual-studio.md). Os clientes que instalaram do local receberão as notificações de atualização. Se a atualização precisar ser implantada em clientes, siga [estas instruções](update-a-network-installation-of-visual-studio.md#deploy-an-update-to-client-machines). Ao modificar o 'response.json' para uma atualização, não adicione cargas de trabalho, componentes ou idiomas adicionais. O gerenciamento dessas configurações deve ser feito como uma implantação 'modificar', depois que o produto foi atualizado.

Para uma instalação baseada na internet, execute o novo instalador de versão fixa com o parâmetro `--channelUri` apontando para um manifesto de canal inexistente no cliente. Se a atualização for implantada no modo silencioso ou passivo, use dois comandos separados:

1. Atualize o Instalador do Visual Studio:

    ```shell
    vs_enterprise.exe --quiet --update
    ```

::: moniker range="vs-2019"
 
2. Atualize o aplicativo do Visual Studio em si:
    ```shell
    vs_enterprise.exe update --installPath "C:\Program Files (x86)\Microsoft Visual Studio\2019\Enterprise" --quiet --wait --norestart --channelUri c:\doesnotexist.chman
    ```

::: moniker-end

::: moniker range=">=vs-2022"

2. Atualize o aplicativo do Visual Studio em si:
    ```shell
    vs_enterprise.exe update --installPath "C:\Program Files\Microsoft Visual Studio\2022\Enterprise" --quiet --wait --norestart --channelUri c:\doesnotexist.chman
    ```

::: moniker-end

[!INCLUDE[install_get_support_md](includes/install_get_support_md.md)]

## <a name="see-also"></a>Confira também

* [Instalar o Visual Studio](install-visual-studio.md)
* [Guia do administrador do Visual Studio](visual-studio-administrator-guide.md)
* [Usar parâmetros de linha de comando para instalar o Visual Studio](use-command-line-parameters-to-install-visual-studio.md)
* [Ferramentas para detectar e gerenciar instâncias do Visual Studio](tools-for-managing-visual-studio-instances.md)
* [Como definir as configurações em um arquivo de resposta](automated-installation-with-response-file.md)
* [Atualizações de controle para implantações do Visual Studio com base em rede](controlling-updates-to-visual-studio-deployments.md)
* [Visual Studio ciclo de vida e manutenção do produto](/visualstudio/releases/2019/servicing/)
