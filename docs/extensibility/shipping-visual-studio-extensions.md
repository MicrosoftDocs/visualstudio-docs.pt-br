---
title: Envio de extensões do Visual Studio | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- VSIX deployment
- deployment, VSIX
- satellite DLLs, in VSIX packages
ms.assetid: 13cd263d-25f7-488e-9c1a-cff908caedb6
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 3c646ec2c5159e6c3551776761baa9328e3d62bb
ms.sourcegitcommit: 6a9d5bd75e50947659fd6c837111a6a547884e2a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
ms.locfileid: "31142742"
---
# <a name="shipping-visual-studio-extensions"></a>Envio de extensões do Visual Studio
Depois de concluir o desenvolvimento de sua extensão, você pode instalá-lo em outros computadores, compartilhá-lo com seus colegas e amigos ou publicá-lo no Visual Studio Marketplace. Nesta seção, explicaremos tudo o que você precisa fazer para publicar e manter sua extensão: Trabalhando com arquivos .vsix, publicação, localizando e atualizando.  
  
## <a name="working-with-vsix-extensions"></a>Trabalhando com extensões de VSIX  
 Você pode criar extensões de VSIX criando um projeto do VSIX em branco e, em seguida, adicionando modelos de item diferentes a ele. Para obter mais informações, consulte [modelo de projeto do VSIX](../extensibility/vsix-project-template.md).  
  
 Você pode usar o formato do VSIX para modelos de projeto do pacote, componentes Managed Extensibility Framework (MEF) VSPackages, modelos de item **caixa de ferramentas** controles, assemblies e tipos personalizados (Isso inclui páginas de inicialização personalizada). O formato do VSIX usa implantação baseada em arquivo. Para obter mais informações sobre pacotes VSIX, consulte [Anatomia de um pacote do VSIX](../extensibility/anatomy-of-a-vsix-package.md).  
  
 O formato do VSIX não dá suporte à instalação de trechos de código. Ele também não suporta outros cenários, como escrita para o Cache de Assembly Global (GAC) ou no registro do sistema. Se você precisar gravar GAC ou o registro na instalação, você deve usar o Windows Installer. Para obter mais informações, consulte [Preparando extensões para implantação do Windows Installer](../extensibility/preparing-extensions-for-windows-installer-deployment.md).  
  
## <a name="publishing-your-extension-to-the-visual-studio-marketplace"></a>Publicar sua extensão para o Visual Studio Marketplace  
 Você pode distribuir sua extensão para outras pessoas simplesmente, enviando-o arquivo .vsix ou colocar em um servidor. Mas é a melhor maneira de obter o código nas mãos de muitas pessoas para colocá-la na [Visual Studio Marketplace](https://marketplace.visualstudio.com/vs). Extensões do Visual Studio Marketplace estão disponíveis para usuários do Visual Studio por meio de **extensões e atualizações**. Para obter mais informações, consulte [Localizando e usando extensões do Visual Studio](../ide/finding-and-using-visual-studio-extensions.md).  
  
 Para obter um exemplo completo que mostra como carregar uma extensão para o Visual Studio Marketplace, consulte [passo a passo: publicando uma extensão do Visual Studio](../extensibility/walkthrough-publishing-a-visual-studio-extension.md).  
  
## <a name="private-galleries"></a>Galerias privadas  
 À medida que desenvolve controles, modelos e ferramentas, você pode compartilhá-los com sua organização por meio de postagem em uma galeria privada em sua intranet. Para obter mais informações, consulte [Galerias privadas](../extensibility/private-galleries.md).  
  
## <a name="localizing-your-extension"></a>Localizando a extensão  
 Se você estiver planejando sua extensão em localidades diferentes de versão, você deve considerar a localização. Para obter uma explicação do que está envolvido, consulte [Localizando VSIX pacotes](../extensibility/localizing-vsix-packages.md).  
  
## <a name="updating-and-versioning-your-extension"></a>Atualizando e sua extensão de controle de versão  
 Após ter publicado sua extensão, será fornecido um tempo quando você precisa atualizá-lo. Para saber como atualizar uma extensão que foi publicada no Visual Studio Marketplace, consulte [como: atualizar uma extensão](../extensibility/how-to-update-a-visual-studio-extension.md).  
  
 Você pode definir sua extensão para oferecer suporte a várias versões do Visual Studio. Para obter mais informações, consulte [dando suporte a várias versões do Visual Studio](../extensibility/supporting-multiple-versions-of-visual-studio.md).  
  
## <a name="related-topics"></a>Tópicos relacionados  
  
|Título|Descrição|  
|-----------|-----------------|  
|[Introdução ao modelo de projeto do VSIX](../extensibility/getting-started-with-the-vsix-project-template.md)|Explica como usar o modelo de projeto do VSIX para instalar um modelo de projeto personalizado.|  
|[Anatomia de um pacote VSIX](../extensibility/anatomy-of-a-vsix-package.md)|Descreve os componentes de um pacote do VSIX.|  
|[Modelo de projeto VSIX](../extensibility/vsix-project-template.md)|Fornece instruções passo a passo sobre como empacotar e publicar uma extensão.|  
|[Localizar pacotes VSIX](../extensibility/localizing-vsix-packages.md)|Explica como fornecer o texto localizado para o processo de instalação usando extension.vsixlangpack arquivos.|  
|[Como: atualizar uma extensão](../extensibility/how-to-update-a-visual-studio-extension.md)|Descreve como atualizar uma extensão no seu sistema e como implantar uma atualização em uma extensão existente do Visual Studio.|  
|[Como adicionar uma dependência a um pacote VSIX](../extensibility/how-to-add-a-dependency-to-a-vsix-package.md)|Descreve como adicionar referências aos pacotes de implantação do VSIX.|  
|[Preparar extensões para a implantação do Windows Installer](../extensibility/preparing-extensions-for-windows-installer-deployment.md)|Explica como implantar sua extensão com o Windows Installer.|  
|[Assinar pacotes VSIX](../extensibility/signing-vsix-packages.md)|Explica como assinar pacotes VSIX.|  
|[Galerias privadas](../extensibility/private-galleries.md)|Explica como criar galerias privadas para extensões.|  
|[Fornecer suporte à várias versões do Visual Studio](../extensibility/supporting-multiple-versions-of-visual-studio.md)|Mostra como fazer com que o suporte a extensão de várias versões do Visual Studio.|
|[Localizando o Visual Studio](locating-visual-studio.md)|Descreve como localizar instâncias do Visual Studio para implantação de extensão personalizada.|
