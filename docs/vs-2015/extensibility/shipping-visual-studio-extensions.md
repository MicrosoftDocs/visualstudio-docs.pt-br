---
title: Envio de extensões do Visual Studio | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-sdk
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- VSIX deployment
- deployment, VSIX
- satellite DLLs, in VSIX packages
ms.assetid: 13cd263d-25f7-488e-9c1a-cff908caedb6
caps.latest.revision: 29
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 5b1746b99ccfddef4e831326d88ea21ff9f9129c
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51743060"
---
# <a name="shipping-visual-studio-extensions"></a>Enviando extensões do Visual Studio
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

**Observação**: A Galeria do Visual Studio está sendo substituída pelo Visual Studio Marketplace. Consulte a versão mais recente deste tópico para obter detalhes.

  
Depois de concluir o desenvolvimento de sua extensão, você pode instalá-lo em outros computadores, compartilhá-lo com seus amigos e colegas de trabalho ou publicá-lo na Galeria do Visual Studio. Nesta seção, vamos explicar todas as coisas que você precisa fazer para publicar e manter sua extensão: trabalhar com arquivos. VSIX, publicação, localizando e atualizando.  
  
## <a name="working-with-vsix-extensions"></a>Trabalhando com extensões VSIX  
 Você pode criar extensões de VSIX criando um projeto de VSIX em branco e, em seguida, adicionar modelos de item diferentes a ele. Para obter mais informações, consulte [modelo de projeto do VSIX](../extensibility/vsix-project-template.md).  
  
 Você pode usar o formato VSIX para modelos de projeto de pacote, componentes do modelos, VSPackages, Managed Extensibility Framework (MEF), de item **caixa de ferramentas** controles, assemblies e tipos personalizados (Isso inclui páginas de inicialização personalizada). O formato VSIX usa implantação baseada em arquivo. Para obter mais informações sobre pacotes VSIX, consulte [Anatomia de um pacote VSIX](../extensibility/anatomy-of-a-vsix-package.md).  
  
 O formato VSIX não suporta a instalação de trechos de código. Ele também não suporta outros cenários, como o Cache de Assembly Global (GAC) ou no registro do sistema de escrita. Se você precisar gravar em GAC ou no registro na instalação, você deve usar o instalador do Windows. Para obter mais informações, consulte [Preparando implantação das extensões para o Windows Installer](../extensibility/preparing-extensions-for-windows-installer-deployment.md).  
  
## <a name="publishing-your-extension-to-the-visual-studio-gallery"></a>Publicar sua extensão de galeria do Visual Studio  
 Você pode distribuir sua extensão para outras pessoas simplesmente por enviá-los o arquivo. VSIX ou colocar um servidor. Mas a melhor maneira de obter seu código nas mãos de muita gente é colocá-lo na [Galeria do Visual Studio](http://go.microsoft.com/fwlink/?LinkID=123847). Extensões da Galeria do Visual Studio estão disponíveis para usuários do Visual Studio por meio **extensões e atualizações**. Para obter mais informações, consulte [Localizando e usando extensões do Visual Studio](../ide/finding-and-using-visual-studio-extensions.md).  
  
 Para obter um exemplo completo que mostra como carregar uma extensão para a Galeria do Visual Studio, consulte [instruções passo a passo: publicando uma extensão do Visual Studio](../extensibility/walkthrough-publishing-a-visual-studio-extension.md).  
  
## <a name="private-galleries"></a>Galerias privadas  
 À medida que desenvolve controles, modelos e ferramentas, você pode compartilhá-los com a sua organização, postando-os para uma galeria privada em sua intranet. Para obter mais informações, consulte [Galerias privadas](../extensibility/private-galleries.md).  
  
## <a name="localizing-your-extension"></a>Localizando sua extensão  
 Se você estiver planejando liberar sua extensão em localidades diferentes, considere a possibilidade de localização. Para obter uma explicação do que está envolvido, consulte [Localizando os pacotes VSIX](../extensibility/localizing-vsix-packages.md).  
  
## <a name="updating-and-versioning-your-extension"></a>Atualizando e sua extensão de controle de versão  
 Depois de publicar sua extensão, será fornecido um tempo quando você precisa atualizá-lo. Para saber como atualizar uma extensão que foi publicada na Galeria do Visual Studio, consulte [como: atualizar uma extensão](../extensibility/how-to-update-a-visual-studio-extension.md).  
  
 Você pode definir sua extensão para oferecer suporte a várias versões do Visual Studio. Para obter mais informações, consulte [que dão suporte a várias versões do Visual Studio](../extensibility/supporting-multiple-versions-of-visual-studio.md).  
  
## <a name="related-topics"></a>Tópicos relacionados  
  
|Título|Descrição|  
|-----------|-----------------|  
|[Introdução ao modelo de projeto do VSIX](../extensibility/getting-started-with-the-vsix-project-template.md)|Explica como usar o modelo de projeto do VSIX para instalar um modelo de projeto personalizado.|  
|[Anatomia de um pacote VSIX](../extensibility/anatomy-of-a-vsix-package.md)|Descreve os componentes de um pacote VSIX.|  
|[Modelo de projeto VSIX](../extensibility/vsix-project-template.md)|Fornece instruções passo a passo sobre como empacotar e publicar uma extensão.|  
|[Localizar pacotes VSIX](../extensibility/localizing-vsix-packages.md)|Explica como fornecer o texto localizado para o processo de instalação por meio de arquivos extension.vsixlangpack.|  
|[Como atualizar uma extensão](../extensibility/how-to-update-a-visual-studio-extension.md)|Descreve como atualizar uma extensão em seu sistema e como implantar uma atualização para uma extensão existente do Visual Studio.|  
|[Como adicionar uma dependência a um pacote VSIX](../extensibility/how-to-add-a-dependency-to-a-vsix-package.md)|Descreve como adicionar referências aos pacotes de implantação do VSIX.|  
|[Preparar extensões para a implantação do Windows Installer](../extensibility/preparing-extensions-for-windows-installer-deployment.md)|Explica como implantar sua extensão com o Windows Installer.|  
|[Assinar pacotes VSIX](../extensibility/signing-vsix-packages.md)|Explica como assinar pacotes VSIX.|  
|[Galerias privadas](../extensibility/private-galleries.md)|Explica como criar galerias privadas para extensões.|  
|[Fornecer suporte à várias versões do Visual Studio](../extensibility/supporting-multiple-versions-of-visual-studio.md)|Mostra como fazer com que o suporte de sua extensão várias versões do Visual Studio.|

