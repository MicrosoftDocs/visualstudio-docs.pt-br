---
title: Enviando extensões do Visual Studio | Microsoft Docs
description: Saiba como publicar e manter sua extensão do SDK do Visual Studio, incluindo o trabalho com arquivos. vsix, publicação, localização e atualização.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- VSIX deployment
- deployment, VSIX
- satellite DLLs, in VSIX packages
ms.assetid: 13cd263d-25f7-488e-9c1a-cff908caedb6
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: c88c80ffbc1e80815b8370a940a75c0eb197ff78
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105090129"
---
# <a name="shipping-visual-studio-extensions"></a>Enviando extensões do Visual Studio
Depois de terminar de desenvolver sua extensão, você pode instalá-la em outros computadores, compartilhá-lo com seus amigos e colegas de trabalho ou publicá-lo na Visual Studio Marketplace. Nesta seção, explicaremos todas as coisas que você precisa fazer para publicar e manter sua extensão: trabalhando com arquivos. vsix, publicação, localização e atualização.

## <a name="working-with-vsix-extensions"></a>Trabalhando com extensões VSIX
 Você pode criar uma extensão VSIX criando um projeto VSIX em branco e, em seguida, adicionando modelos de item diferentes a ele. Para obter mais informações, consulte [modelo de projeto VSIX](../extensibility/vsix-project-template.md).

 Você pode usar o formato VSIX para empacotar modelos de projeto, modelos de item, VSPackages, Managed Extensibility Framework (MEF) componentes, controles de **caixa de ferramentas** , assemblies e tipos personalizados (isso inclui páginas de início personalizadas para o Visual Studio 2017). O formato VSIX usa a implantação baseada em arquivo. Para obter mais informações sobre pacotes VSIX, consulte [anatomia de um pacote VSIX](../extensibility/anatomy-of-a-vsix-package.md).

 O formato VSIX não oferece suporte à instalação de trechos de código. Ele também não dá suporte a alguns outros cenários, como gravar no cache de assembly global (GAC) ou no registro do sistema. Se precisar gravar no GAC ou no registro na instalação, você deverá usar o Windows Installer. Para obter mais informações, consulte [preparando extensões para implantação de Windows Installer](../extensibility/preparing-extensions-for-windows-installer-deployment.md).

## <a name="publishing-your-extension-to-the-visual-studio-marketplace"></a>Publicando sua extensão no Visual Studio Marketplace
 Você pode distribuir sua extensão para outras pessoas simplesmente enviando-as por email ao arquivo. vsix ou colocando em um servidor. Mas a melhor maneira de obter seu código nas mãos de muitas pessoas é colocá-lo na [Visual Studio Marketplace](https://marketplace.visualstudio.com/vs). Visual Studio Marketplace extensões estão disponíveis para os usuários do Visual Studio por meio de **extensões e atualizações**. Para obter mais informações, consulte [localizando e usando extensões do Visual Studio](../ide/finding-and-using-visual-studio-extensions.md).

 Para obter um exemplo completo que mostra como carregar uma extensão para o Visual Studio Marketplace, consulte [passo a passos: publicando uma extensão do Visual Studio](../extensibility/walkthrough-publishing-a-visual-studio-extension.md).

## <a name="private-galleries"></a>Galerias privadas
 Ao desenvolver controles, modelos e ferramentas, você pode compartilhá-los com sua organização postando-os em uma galeria privada em sua intranet. Para obter mais informações, consulte [galerias particulares](../extensibility/private-galleries.md).

## <a name="localizing-your-extension"></a>Localizando sua extensão
 Se você estiver planejando liberar sua extensão em localidades diferentes, considere a possibilidade de localizá-la. Para obter uma explicação do que está envolvido, consulte [localizando pacotes VSIX](../extensibility/localizing-vsix-packages.md).

## <a name="updating-and-versioning-your-extension"></a>Atualizando e proversionando sua extensão
 Depois de publicar sua extensão, haverá um horário em que você precisa atualizá-la. Para saber como atualizar uma extensão que foi publicada no Visual Studio Marketplace, consulte [como: atualizar uma extensão](../extensibility/how-to-update-a-visual-studio-extension.md).

 Você pode definir sua extensão para dar suporte a várias versões do Visual Studio. Para obter mais informações, consulte [dando suporte a várias versões do Visual Studio](../extensibility/supporting-multiple-versions-of-visual-studio.md).

## <a name="related-topics"></a>Tópicos relacionados

|Título|Descrição|
|-----------|-----------------|
|[Introdução ao modelo de projeto do VSIX](../extensibility/getting-started-with-the-vsix-project-template.md)|Explica como usar o modelo de projeto VSIX para instalar um modelo de projeto personalizado.|
|[Anatomia de um pacote VSIX](../extensibility/anatomy-of-a-vsix-package.md)|Descreve os componentes de um pacote VSIX.|
|[Modelo de projeto VSIX](../extensibility/vsix-project-template.md)|Apresenta instruções passo a passo sobre como empacotar e publicar uma extensão.|
|[Localizar pacotes VSIX](../extensibility/localizing-vsix-packages.md)|Explica como fornecer texto localizado para o processo de instalação usando arquivos de extensão. vsixlangpack.|
|[Como atualizar uma extensão](../extensibility/how-to-update-a-visual-studio-extension.md)|Descreve como atualizar uma extensão no seu sistema e como implantar uma atualização em uma extensão existente do Visual Studio.|
|[Como adicionar uma dependência a um pacote VSIX](../extensibility/how-to-add-a-dependency-to-a-vsix-package.md)|Descreve como adicionar referências a pacotes de implantação VSIX.|
|[Preparando extensões para a implantação do Windows Installer](../extensibility/preparing-extensions-for-windows-installer-deployment.md)|Explica como implantar sua extensão com Windows Installer.|
|[Assinando pacotes VSIX](../extensibility/signing-vsix-packages.md)|Explica como assinar pacotes VSIX.|
|[Galerias particulares](../extensibility/private-galleries.md)|Explica como criar galerias particulares para extensões.|
|[Fornecer suporte à várias versões do Visual Studio](../extensibility/supporting-multiple-versions-of-visual-studio.md)|Mostra como fazer com que sua extensão dê suporte a várias versões do Visual Studio.|
|[Localizando o Visual Studio](locating-visual-studio.md)|Descreve como localizar instâncias do Visual Studio para implantação de extensão personalizada.|
