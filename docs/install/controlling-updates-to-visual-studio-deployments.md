---
title: Controlar atualizações de implantações do Visual Studio
description: Saiba como alterar o local onde o Visual Studio busca atualizações quando você instala usando uma rede.
ms.date: 08/14/2017
ms.technology: vs-acquisition
ms.prod: visual-studio-dev15
ms.topic: conceptual
helpviewer_keywords:
- '{{PLACEHOLDER}}'
- '{{PLACEHOLDER}}'
ms.assetid: 35C7AB05-07D5-4B38-BCAC-AB88444E7368
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 9cfc35698ce87027192031ef453a4c42ecc3c199
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49830425"
---
# <a name="control-updates-to-network-based-visual-studio-deployments"></a>Atualizações de controle para implantações do Visual Studio com base em rede

Geralmente, os administradores corporativos criam um layout e o hospedam em um compartilhamento de arquivo de rede para implantação para seus usuários finais.

## <a name="controlling-where-visual-studio-looks-for-updates"></a>Controlar onde o Visual Studio procura atualizações

Por padrão, o Visual Studio continuará a procurar atualizações online, mesmo se a instalação for implantada de um compartilhamento de rede. Se uma atualização estiver disponível, o usuário poderá instalá-la. Qualquer conteúdo atualizado não encontrado no layout offline é baixado da Web.

Se você quiser controle direto sobre onde o Visual Studio procura por atualizações, modifique o local em que ele procura. Você também pode controlar a versão para a qual os usuários fazem atualização. Para fazer isso, siga estas etapas:

1. Crie um layout offline:
   ```cmd
   vs_enterprise.exe --layout C:\vs2017offline --lang en-US
   ```
2. Copie-o para o compartilhamento de arquivo onde você deseja hospedá-lo:
   ```cmd
   xcopy /e C:\vs2017offline \\server\share\VS2017
   ```
3. Modifique o arquivo response.json no layout e altere o valor `channelUri` para apontar para uma cópia de channelManifest.json que o administrador controla.

   Verifique se você escapou barras invertidas no valor, assim como no exemplo a seguir:

   ```json
   "channelUri":"\\\\server\\share\\VS2017\\ChannelManifest.json"
   ```

   Agora os usuários finais podem executar a instalação deste compartilhamento para instalar o Visual Studio.
   ```cmd
   \\server\share\VS2017\vs_enterprise.exe
   ```

Quando um administrador corporativo determina que é hora de os usuários atualizarem para uma versão mais recente do Visual Studio, eles podem [atualizar a localização do layout](update-a-network-installation-of-visual-studio.md) para incorporar os arquivos atualizados, conforme demonstrado a seguir.

1. Use um comando semelhante ao comando a seguir:
   ```cmd
   vs_enterprise.exe --layout \\server\share\VS2017 --lang en-US
   ```
2. Verifique se o arquivo response.json no layout atualizado ainda contém as personalizações, especificamente a modificação de channelUri, conforme demonstrado a seguir:
   ```json
   "channelUri":"\\\\server\\share\\VS2017\\ChannelManifest.json"
   ```
   Instalações existentes do Visual Studio desse layout procuram atualizações em `\\server\share\VS2017\ChannelManifest.json`. Se o channelManifest.json for mais recente do que o já instalado pelo usuário, o Visual Studio notificará o usuário de que uma atualização está disponível.

   Novas instalações instalam automaticamente a versão atualizada do Visual Studio diretamente do layout.

## <a name="controlling-notifications-in-the-visual-studio-ide"></a>Notificações de controle no IDE do Visual Studio

Conforme descrito anteriormente, o Visual Studio verifica o local do qual foi instalado, tal como um compartilhamento de rede ou a Internet, para ver se há atualizações disponíveis. Quando uma atualização está disponível, o Visual Studio notifica o usuário com um sinalizador de notificação no canto superior direito da janela.

 ![Sinalizador de notificação de atualizações](media/notification-flag.png)

Se não quiser que os usuários finais sejam notificados sobre atualizações, desabilite as notificações. (Por exemplo, você talvez queira desabilitar as notificações se fornecer atualizações por meio de um mecanismo de distribuição de software central.)

Já que o Visual Studio 2017 [Armazena as entradas do Registro em um Registro privado](tools-for-managing-visual-studio-instances.md#editing-the-registry-for-a-visual-studio-instance), você não pode editar diretamente o Registro da maneira típica. No entanto, o Visual Studio inclui um utilitário `vsregedit.exe` que você pode usar para alterar as configurações do Visual Studio. Você pode desativar as notificações com o seguinte comando:

```cmd
vsregedit.exe set "C:\Program Files (x86)\Microsoft Visual Studio\2017\Enterprise" HKCU ExtensionManager AutomaticallyCheckForUpdates2Override dword 0
```

(Verifique se você substituiu o diretório para coincidir com a instância instalada que você deseja editar.)

> [!TIP]
> Use [vswhere.exe](tools-for-managing-visual-studio-instances.md#detecting-existing-visual-studio-instances) para localizar uma instância específica do Visual Studio em uma estação de trabalho cliente.

[!INCLUDE[install_get_support_md](includes/install_get_support_md.md)]

## <a name="see-also"></a>Consulte também

* [Instalar o Visual Studio](install-visual-studio.md)
* [Guia do administrador do Visual Studio](visual-studio-administrator-guide.md)
* [Usar parâmetros de linha de comando para instalar o Visual Studio](use-command-line-parameters-to-install-visual-studio.md)
* [Ferramentas para gerenciar instâncias do Visual Studio](tools-for-managing-visual-studio-instances.md)
