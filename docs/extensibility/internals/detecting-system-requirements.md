---
title: Detectando os requisitos do sistema | Microsoft Docs
description: Saiba como configurar o Microsoft Windows Installer para detectar os requisitos do sistema, como a edição do Visual Studio instalada.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- setup, VSPackages
- launch conditions
ms.assetid: 0ba94acf-bf0b-4bb3-8cca-aaac1b5d6737
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: ffb00ca42376f8b7c150552c862bba7a24a5c1fb
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105056760"
---
# <a name="detect-system-requirements"></a>Detectar requisitos do sistema
Um VSPackage não pode funcionar, a menos que o Visual Studio esteja instalado. Ao usar o Microsoft Windows Installer para gerenciar a instalação do seu VSPackage, você pode configurar o instalador para detectar se o Visual Studio está instalado. Você também pode configurá-lo para verificar o sistema em busca de outros requisitos, por exemplo, uma versão específica do Windows ou uma quantidade específica de RAM.

## <a name="detect-visual-studio-editions"></a>Detectar edições do Visual Studio
 Para determinar se uma edição do Visual Studio está instalada, verifique se o valor da chave do registro de **instalação** é *(REG_DWORD) 1* na pasta apropriada, conforme listado na tabela a seguir. Observe que há uma hierarquia das edições do Visual Studio:

1. Enterprise

2. Professional

3. Comunidade

Quando uma edição mais recente é instalada, as chaves do registro para essa edição são adicionadas, bem como as edições anteriores. Ou seja, se o Enterprise Edition estiver instalado, a chave de **instalação** será definida como *1* para a empresa, bem como para as edições Professional e Community. Portanto, você precisa verificar apenas a edição mais recente de que precisa.

> [!NOTE]
> Na versão de 64 bits do editor do registro, as chaves de 32 bits são exibidas em **HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\\**. As chaves do Visual Studio estão **em \\HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\DevDiv\vs\Servicing**.

|Produto|Chave|
|-------------|---------|
|Visual Studio Enterprise 2015|HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\DevDiv\vs\Servicing\14.0\enterprise|
|Visual Studio Professional 2015|HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\DevDiv\vs\Servicing\14.0\professional|
|Visual Studio Community 2015|HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\DevDiv\vs\Servicing\14.0\community|
|Shell do Visual Studio 2015 (integrado e isolado)|HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\DevDiv\vs\Servicing\14.0\isoshell|

## <a name="detect-when-visual-studio-is-running"></a>Detectar quando o Visual Studio está em execução
 Seu VSPackage não poderá ser registrado corretamente se o Visual Studio estiver em execução quando o VSPackage estiver instalado. O instalador deve detectar quando o Visual Studio está em execução e, em seguida, recusar a instalação do programa. Windows Installer não permite que você use entradas de tabela para habilitar tal detecção. Em vez disso, você deve criar uma ação personalizada, da seguinte maneira: usar a `EnumProcesses` função para detectar o *devenv.exe* processo e, em seguida, definir uma propriedade do instalador que é usada em uma condição de inicialização ou exibir condicionalmente uma caixa de diálogo que solicita ao usuário fechar o Visual Studio.

## <a name="see-also"></a>Confira também
- [Instalar o VSPackages com Windows Installer](../../extensibility/internals/installing-vspackages-with-windows-installer.md)
