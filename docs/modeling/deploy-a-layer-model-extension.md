---
title: Implantar uma extensão de modelo de camada
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- dependency diagrams, deploying extensions
- layer models, deploying extensions
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.prod: visual-studio-dev15
ms.technology: vs-ide-modeling
ms.openlocfilehash: 98697642135627173c5a6f31e90bf1dd1d0caeaf
ms.sourcegitcommit: 8cdc6e2ad2341f34bd6b02859a7c975daa0c9320
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/12/2018
ms.locfileid: "53307746"
---
# <a name="deploy-a-layer-model-extension"></a>Implantar uma extensão de modelo de camada

Outros usuários do Visual Studio podem instalar extensões que você criar usando o Visual Studio de modelagem da camada.

## <a name="install-your-extension"></a>Instalar sua extensão

Sua extensão é compilada em um arquivo VSIX, que pode ser instalado em outros computadores. Você também pode instalá-lo no seu computador de desenvolvimento, para disponibilizar a extensão na instância principal do Visual Studio.

### <a name="to-install-the-extension"></a>Para instalar a extensão

1. No projeto que contém **source.vsix.manifest**, abra o *bin* diretório no Explorador de arquivos.

2. Cópia de  **\*VSIX** arquivo para o computador no qual você deseja instalar a extensão.

3. No computador de destino, clique duas vezes o arquivo VSIX no Windows Explorer.

    O instalador do VSIX é aberto.

### <a name="to-uninstall-the-extension"></a>Para desinstalar a extensão

1.  No Visual Studio, sobre o **ferramentas** menu, clique em **extensões e atualizações**.

2.  Clique no nome da extensão e, em seguida, clique em **desinstalação**.

## <a name="install-an-extension-on-team-foundation-server"></a>Instalar uma extensão no Team Foundation Server

Servidores do Team Foundation Server normalmente não tenha instalado o Visual Studio e, portanto, não é possível instalar o VSIX clicando duas vezes nele. Você deve instalar a extensão manualmente.

### <a name="to-install-your-layer-extension-on-a-team-foundation-server-server"></a>Para instalar a extensão de camada em um servidor do Team Foundation Server

1.  Copiar o. *vsix* arquivos do seu computador de desenvolvimento para o computador do Team Foundation Server (TFS).

     Coloque o arquivo VSIX em um dos seguintes locais:

    -   Para instalar para todos os usuários e serviços:

         %ProgramFiles%\Microsoft visual Studio [versão] \Common7\IDE\Extensions\Microsoft

    -   Para instalar somente para o serviço de rede que executa a compilação:

         %WinDir%\ServiceProfiles\NetworkService\AppData\Local\Microsoft\VisualStudio\\[version]\Extensions\Microsoft

    -   Se você tiver configurado a compilação para executar no modo interativo como um usuário específico, você pode instalar apenas para esse usuário:

         %LocalAppData%\Microsoft\VisualStudio\\\Extensions\Microsoft [versão]

2.  Expanda cada arquivo VSIX em uma pasta no mesmo local:

    1.  Alterar a extensão de nome de arquivo **. VSIX** à **. zip**.

    2.  Extraia o conteúdo do arquivo. zip para uma pasta.

    3.  Excluir o arquivo. zip

3.  Reinicie o TFS.
