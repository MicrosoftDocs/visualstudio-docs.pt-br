---
title: Controlar atualizações em implantações
description: Saiba como alterar o local onde o Visual Studio busca atualizações quando você instala usando uma rede.
ms.date: 04/06/2021
ms.custom: seodec18
ms.topic: conceptual
helpviewer_keywords:
- '{{PLACEHOLDER}}'
- '{{PLACEHOLDER}}'
ms.assetid: 35C7AB05-07D5-4B38-BCAC-AB88444E7368
author: j-martens
ms.author: jmartens
manager: jmartens
ms.workload:
- multiple
ms.prod: visual-studio-windows
ms.technology: vs-installation
ms.openlocfilehash: 3504e866a7f89de8fa38f92a8bfea501ddd952c9
ms.sourcegitcommit: cc66c898ce82f9f1159bd505647f315792cac9fc
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/10/2021
ms.locfileid: "109666790"
---
# <a name="control-updates-to-network-based-visual-studio-deployments"></a>Atualizações de controle para implantações do Visual Studio com base em rede

Os administradores corporativos geralmente criam um layout e o hospedam em um compartilhamento de arquivos de rede para implantar em seus usuários finais. Esta página descreve como configurar as opções de layout de rede corretamente. 

## <a name="controlling-where-visual-studio-looks-for-updates"></a>Controlar onde o Visual Studio procura atualizações

**Cenário 1: cliente originalmente instalado de um layout, mas está configurado para receber atualizações do local de layout de rede ou da Web**

Por padrão, Visual Studio continua procurando atualizações online mesmo que a instalação seja originalmente implantada de um compartilhamento de rede. Se uma atualização estiver disponível na Web, o usuário poderá instalá-la. Embora o cache de layout de rede seja inspecionado primeiro para qualquer bits de produto atualizado, se eles não são encontrados lá, Visual Studio procurará e baixará os bits de produto atualizados da Web.

**Cenário 2: o cliente originalmente instalado e deve receber apenas atualizações do layout de rede**

Se você quiser controlar onde o cliente do Visual Studio procura atualizações, por exemplo, se o computador cliente não tiver acesso à Internet e você quiser garantir que ele seja somente e sempre instalado do layout, você poderá configurar o local em que o instalador do cliente procura bits de produto atualizados. É melhor garantir que essa configuração seja configurada corretamente antes que o cliente faça a instalação inicial do layout. 

1. Crie um layout offline:

   ```cmd
   vs_enterprise.exe --layout C:\vsoffline --lang en-US
   ```

2. Copie-o para o compartilhamento de arquivo onde você deseja hospedá-lo:

   ```cmd
   xcopy /e C:\vsoffline \\server\share\VS
   ```

3. Modifique o arquivo no layout e altere o valor para apontar para uma cópia do channelManifest.js`response.json` `channelUri` que o administrador controla.

   Verifique se você escapou barras invertidas no valor, assim como no exemplo a seguir:

   ```json
   "channelUri":"\\\\server\\share\\VS\\ChannelManifest.json"
   ```

   Agora os usuários finais podem executar a instalação desse compartilhamento para instalar Visual Studio.

   ```cmd
   \\server\share\VS\vs_enterprise.exe
   ```

Quando um administrador corporativo determina que é hora de os usuários atualizarem para uma versão mais recente do Visual Studio, eles podem [atualizar a localização do layout](update-a-network-installation-of-visual-studio.md) para incorporar os arquivos atualizados, conforme demonstrado a seguir.

1. Use um comando semelhante ao comando a seguir:

   ```cmd
   vs_enterprise.exe --layout \\server\share\VS --lang en-US
   ```

2. Verifique se o arquivo no layout atualizado ainda `response.json` contém suas personalizações, especificamente a modificação channelUri, da seguinte forma:

   ```json
   "channelUri":"\\\\server\\share\\VS\\ChannelManifest.json"
   ```

Instalações existentes do Visual Studio desse layout procuram atualizações em `\\server\share\VS\ChannelManifest.json`. Se o channelManifest.json for mais recente do que o já instalado pelo usuário, o Visual Studio notificará o usuário de que uma atualização está disponível.

Qualquer atualização de instalação iniciada do cliente instalará automaticamente a versão atualizada do Visual Studio diretamente do layout.

**Cenário 3: o cliente originalmente instalado da Web, mas agora só deve receber atualizações de um layout de rede**

Em alguns casos, o computador cliente pode já ter instalado o Visual Studio a partir da Web, mas agora o administrador deseja ter todas as atualizações futuras provenientes de um layout gerenciado. A única maneira com suporte para fazer isso é criar um layout de rede com a versão desejada do produto e, em seguida, no computador cliente, executar o bootstrapper a _partir do local de layout_ (por exemplo, `\\server\share\vs_enterprise.exe` ). O ideal é que a instalação original do cliente tenha ocorrido usando o bootstrapper a partir do layout de rede com o ChannelURI configurado corretamente, mas a execução do bootstrapper atualizado a partir do local de layout de rede também funcionará. Qualquer uma dessas ações seria inserida, no computador cliente, uma conexão com esse local de layout específico. A única limitação para esse cenário funcionar corretamente é que o "ChannelURI" no arquivo do layout `response.json` deve ser o mesmo que o ChannelURI definido no computador do cliente quando a instalação original ocorreu. É mais provável que esse valor tenha sido originalmente definido para o [canal de versão](https://aka.ms/vs/16/release/channel)da Internet. 


## <a name="controlling-notifications-in-the-visual-studio-ide"></a>Notificações de controle no IDE do Visual Studio

::: moniker range="vs-2017"

Conforme descrito anteriormente, o Visual Studio verifica o local do qual foi instalado, tal como um compartilhamento de rede ou a Internet, para ver se há atualizações disponíveis. Quando uma atualização está disponível, o Visual Studio notifica o usuário com um sinalizador de notificação no canto superior direito da janela.

   ![Sinalizador de notificação de atualizações](media/notification-flag.png)

::: moniker-end

::: moniker range="vs-2019&quot;

Conforme descrito anteriormente, o Visual Studio verifica o local do qual foi instalado, tal como um compartilhamento de rede ou a Internet, para ver se há atualizações disponíveis. Quando uma atualização está disponível, o Visual Studio notifica o usuário com um ícone de notificação no canto inferior direito da janela.

   ![O ícone de notificação no IDE do Visual Studio](media/vs-2019/notification-bar.png &quot;O ícone de notificação no IDE do Visual Studio")

::: moniker-end

Você pode desabilitar as notificações se não quiser que os usuários finais sejam notificados sobre as atualizações. (Por exemplo, você talvez queira desabilitar as notificações se fornecer atualizações por meio de um mecanismo de distribuição de software central.)

::: moniker range="vs-2017"

Já que o Visual Studio 2017 [Armazena as entradas do Registro em um Registro privado](tools-for-managing-visual-studio-instances.md#editing-the-registry-for-a-visual-studio-instance), você não pode editar diretamente o Registro da maneira típica. No entanto, o Visual Studio inclui um utilitário `vsregedit.exe` que você pode usar para alterar as configurações do Visual Studio. Você pode desativar as notificações com o seguinte comando:

```cmd
vsregedit.exe set "C:\Program Files (x86)\Microsoft Visual Studio\2017\Enterprise" HKCU ExtensionManager AutomaticallyCheckForUpdates2Override dword 0
```

::: moniker-end

::: moniker range="vs-2019"

Já que o Visual Studio 2019 [armazena as entradas do Registro em um Registro privado](tools-for-managing-visual-studio-instances.md#editing-the-registry-for-a-visual-studio-instance), você não pode editar diretamente o Registro da maneira típica. No entanto, o Visual Studio inclui um utilitário `vsregedit.exe` que você pode usar para alterar as configurações do Visual Studio. Você pode desativar as notificações com o seguinte comando:

```cmd
vsregedit.exe set "C:\Program Files (x86)\Microsoft Visual Studio\2019\Enterprise" HKCU ExtensionManager AutomaticallyCheckForUpdates2Override dword 0
```

::: moniker-end

(Verifique se você substituiu o diretório para coincidir com a instância instalada que você deseja editar.)

> [!TIP]
> Use [vswhere.exe](tools-for-managing-visual-studio-instances.md#detecting-existing-visual-studio-instances) para localizar uma instância específica do Visual Studio em uma estação de trabalho cliente.

[!INCLUDE[install_get_support_md](includes/install_get_support_md.md)]

## <a name="see-also"></a>Confira também

* [Guia do administrador do Visual Studio](visual-studio-administrator-guide.md)
* [Habilitando atualizações do administrador](enabling-administrator-updates.md)
* [Aplicando atualizações do administrador](applying-administrator-updates.md)
* [Usar parâmetros de linha de comando para instalar o Visual Studio](use-command-line-parameters-to-install-visual-studio.md)
* [Ferramentas para gerenciar instâncias do Visual Studio](tools-for-managing-visual-studio-instances.md)
* [Ciclo de vida do produto Visual Studio e manutenção](/visualstudio/releases/2019/servicing/)
