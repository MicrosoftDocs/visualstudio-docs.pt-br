---
title: Implantar uma extensão de modelo de camada | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-tfs-dev14
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- layer diagrams, deploying extensions
- layer models, deploying extensions
ms.assetid: 00a4675b-d20e-487e-8fd5-be2b1e0ba238
caps.latest.revision: 29
author: gewarren
ms.author: gewarren
manager: douge
ms.openlocfilehash: a31413f5332ddfec8dc6021da85e2135d691f930
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51735116"
---
# <a name="deploy-a-layer-model-extension"></a>Implantar uma extensão de modelo de camada
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Outros usuários do Visual Studio podem instalar extensões que você criar usando o Visual Studio de modelagem da camada.  
  
## <a name="installing-your-extension"></a>Instalando sua extensão  
 Sua extensão é compilada em um arquivo VSIX, que pode ser instalado em outros computadores. Você também pode instalá-lo no seu computador de desenvolvimento, para disponibilizar a extensão na instância principal do Visual Studio.  
  
#### <a name="to-install-the-extension"></a>Para instalar a extensão  
  
1. No projeto que contém **source.vsix.manifest**, abra **bin\\\\*** no Explorador de arquivos.  
  
2. Cópia de  **\*VSIX** arquivo para o computador no qual você deseja instalar a extensão.  
  
3. No computador de destino, clique duas vezes o arquivo VSIX no Windows Explorer.  
  
    O instalador do VSIX é aberto.  
  
#### <a name="to-uninstall-the-extension"></a>Para desinstalar a extensão  
  
1.  No Visual Studio, sobre o **ferramentas** menu, clique em **extensões e atualizações**.  
  
2.  Clique no nome da extensão e, em seguida, clique em **desinstalação**.  
  
## <a name="installing-an-extension-on-a-team-foundation-build-server"></a>Instalar uma extensão em um servidor de compilação do Team Foundation  
 [!INCLUDE[esprbuild](../includes/esprbuild-md.md)] servidores normalmente não tenha instalado o Visual Studio e, portanto, não é possível instalar o VSIX clicando duas vezes nele. A instalação do [!INCLUDE[esprbuild](../includes/esprbuild-md.md)] inclui alguns componentes que permitem que uma extensão do VSIX ser executado, mas você deve instalar a extensão manualmente.  
  
#### <a name="to-install-your-layer-extension-on-a-includeesprbuildincludesesprbuild-mdmd-server"></a>Para instalar a extensão de camada em um [!INCLUDE[esprbuild](../includes/esprbuild-md.md)] Server  
  
1.  Cópia de **. VSIX** arquivos do seu computador de desenvolvimento para o [!INCLUDE[esprbuild](../includes/esprbuild-md.md)] computador.  
  
     Coloque o arquivo VSIX em um dos seguintes locais:  
  
    -   Para instalar para todos os usuários e serviços:  
  
         %ProgramFiles%\Microsoft visual Studio [versão] \Common7\IDE\Extensions\Microsoft  
  
    -   Instalar somente para o serviço de rede que executa [!INCLUDE[esprbuild](../includes/esprbuild-md.md)]:  
  
         %WinDir%\ServiceProfiles\NetworkService\AppData\Local\Microsoft\VisualStudio\\[version]\Extensions\Microsoft  
  
    -   Se você tiver configurado o [!INCLUDE[esprbuild](../includes/esprbuild-md.md)] para executar no modo interativo como um usuário específico, você pode instalar apenas para esse usuário:  
  
         %LocalAppData%\Microsoft\VisualStudio\\\Extensions\Microsoft [versão]  
  
        > [!NOTE]
        >  % LocalAppData % é normalmente *DriveName*: os usuários*nome de usuário*AppDataLocal.  
  
2.  Expanda cada arquivo VSIX em uma pasta no mesmo local:  
  
    1.  Alterar a extensão de nome de arquivo **. VSIX** à **. zip**.  
  
    2.  Extraia o conteúdo do arquivo. zip para uma pasta.  
  
    3.  Excluir o arquivo. zip  
  
3.  Reinicie o [!INCLUDE[esprbuild](../includes/esprbuild-md.md)].



