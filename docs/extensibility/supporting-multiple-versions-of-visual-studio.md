---
title: Oferecendo suporte a várias versões do Visual Studio | Microsoft Docs
description: Saiba como você pode dar suporte a várias versões do Visual Studio, com seu VSPackages capaz de carregar em diferentes versões.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Visual Studio, supporting multiple versions
- VSPackages, side-by-side compatibility
ms.assetid: 0047aa90-1ed4-40d3-8772-622b2719a4b1
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 3d455ebf18ee8817e2adac2fa266592594ca7e6c
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105056097"
---
# <a name="supporting-multiple-versions-of-visual-studio"></a>Suporte a várias versões do Visual Studio
O termo de *lado a lado* significa que você pode instalar e manter várias versões de um produto no mesmo computador. Para VSPackages, isso significa que um usuário pode ter várias versões do Visual Studio instaladas no mesmo computador. No entanto, você não pode ter versões lado a lado de seu VSPackages carregadas em uma única versão do Visual Studio.

 Antes de tornar o VSPackage capaz de ser carregado em versões lado a lado do Visual Studio, considere o seguinte:

- Você deve determinar qual estratégia de implementação lado a lado você deseja seguir.

   Para obter mais informações, consulte [escolhendo entre VSPackages compartilhadas e com controle de versão](../extensibility/choosing-between-shared-and-versioned-vspackages.md).

- Seus formatos de arquivo de solução e de projeto devem se ajustar à sua estratégia de implementação.

   Para obter mais informações, consulte [Atualizando projetos personalizados](../extensibility/internals/upgrading-projects.md#upgrading-custom-projects) e [registrando extensões de nome de arquivo para implantações lado a lado](../extensibility/registering-file-name-extensions-for-side-by-side-deployments.md).

- O instalador deve lidar com sua estratégia de implementação para que os componentes com controle de versão, e também os componentes compartilhados em todas as versões, sejam corretamente instalados e registrados.

   Para obter mais informações, consulte [instalando o VSPackages com Windows Installer](../extensibility/internals/installing-vspackages-with-windows-installer.md) e também [Gerenciamento de componentes](../extensibility/internals/component-management.md).

  > [!NOTE]
  > A instalação de uma versão do Visual Studio também instala uma versão correspondente do .NET Framework. Por exemplo, a instalação do Visual Studio 2010 e do Visual Studio 2012 no mesmo computador também instala as versões 4,0 e 4,5 do .NET Framework, respectivamente.

## <a name="in-this-section"></a>Nesta seção
- [Escolhendo entre VSPackages compartilhadas e com controle de versão](../extensibility/choosing-between-shared-and-versioned-vspackages.md) Explica como resolver problemas lado a lado no seu VSPackage.

- [Registrando extensões de nome de arquivo para implantações lado a lado](../extensibility/registering-file-name-extensions-for-side-by-side-deployments.md) Descreve como seu VSPackage pode registrar associações de arquivo em um cenário lado a lado.

## <a name="related-sections"></a>Seções relacionadas
- [Instalando VSPackages com o Windows Installer](../extensibility/internals/installing-vspackages-with-windows-installer.md)
