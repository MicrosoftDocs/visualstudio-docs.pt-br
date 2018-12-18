---
title: Suporte a várias versões do Visual Studio | Microsoft Docs
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
- Visual Studio, supporting multiple versions
- VSPackages, side-by-side compatibility
ms.assetid: 0047aa90-1ed4-40d3-8772-622b2719a4b1
caps.latest.revision: 21
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: c7a1a19cf512d39bce44cfeb1376fdde422f037f
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51759852"
---
# <a name="supporting-multiple-versions-of-visual-studio"></a>Suporte a várias versões do Visual Studio
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

O termo *side-by-side* significa que você pode instalar e manter várias versões de um produto no mesmo computador. VSPackages, isso significa que um usuário pode ter várias versões do Visual Studio instaladas no mesmo computador. No entanto, você não pode ter versões lado a lado de seu VSPackages carregados em uma única versão do Visual Studio.  
  
 Antes de fazer o VSPackage capaz de ser carregado em versões lado a lado do Visual Studio, considere o seguinte:  
  
-   Você deve determinar qual estratégia de implementação lado a lado que devem ser seguidas.  
  
     Para obter mais informações, consulte [escolhendo entre compartilhados e com controle de versão VSPackages](../extensibility/choosing-between-shared-and-versioned-vspackages.md).  
  
-   Seus formatos de arquivo de solução e projeto devem se ajustar sua estratégia de implementação.  
  
     Para obter mais informações, consulte [atualização de projetos personalizados](../misc/upgrading-custom-projects.md) e [registrando extensões de nome de arquivo para implantações lado a lado](../extensibility/registering-file-name-extensions-for-side-by-side-deployments.md).  
  
-   O instalador deve lidar com a sua estratégia de implementação para que os componentes com controle de versão e componentes compartilhados por todas as versões, estão corretamente instalados e registrados.  
  
     Para obter mais informações, consulte [instalando VSPackages com o Windows Installer](../extensibility/internals/installing-vspackages-with-windows-installer.md) e também [gerenciamento de componente](../extensibility/internals/component-management.md).  
  
    > [!NOTE]
    >  Instalar uma versão do Visual Studio também instala uma versão correspondente do [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)]. Por exemplo, instalar o Visual Studio 2010 e o Visual Studio 2012 no mesmo computador também instala versões 4.0 e 4.5 do [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)], respectivamente.  
  
## <a name="in-this-section"></a>Nesta seção  
 [Escolher entre VSPackages compartilhados e com controle de versão](../extensibility/choosing-between-shared-and-versioned-vspackages.md)  
 Explica como resolver problemas de lado a lado em seu VSPackage.  
  
 [Registrar extensões de nome de arquivo para implantações lado a lado](../extensibility/registering-file-name-extensions-for-side-by-side-deployments.md)  
 Descreve como o VSPackage pode registrar as associações de arquivo em um cenário lado a lado.  
  
## <a name="related-sections"></a>Seções relacionadas  
 [Instalando VSPackages](../misc/installing-vspackages.md)  
 Discute como criar e instalar VSPackages e como dar suporte a usuários que estão executando várias versões do Visual Studio ao mesmo tempo.

