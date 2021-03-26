---
title: A instância experimental | Microsoft Docs
description: Saiba como o SDK do Visual Studio fornece um espaço experimental para executar aplicativos não testados no modo de depuração.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- experimental builds
- VSPackages, experimental builds
- VSIP, experimental builds
ms.assetid: ead0df4e-6f88-4b42-9297-581b7902f050
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: aefac4efc706d195d8471952da3914d35d27ddc2
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105055876"
---
# <a name="the-experimental-instance"></a>A instância experimental
Para proteger seu ambiente de desenvolvimento do Visual Studio de aplicativos não testados que podem alterá-lo, o VSSDK fornece um espaço experimental que você pode usar para experimentar. Você desenvolve novos aplicativos usando o Visual Studio como de costume, mas os executa usando essa instância experimental.

 Cada aplicativo que tem um pacote VSIX inicia a instância experimental do Visual Studio no modo de depuração.

 Se você quiser iniciar a instância experimental do Visual Studio fora de uma solução específica, execute o seguinte comando na janela de comando:

 Exp. de *\<Visual studio installation path>* /RootSuffix "\Common7\IDE\devenv.exe"

> [!NOTE]
> A instância experimental é gravada no registro nos `<version number>Exp` nós e `<version number>Exp_Config` . Por exemplo, a área de registro experimental do Visual Studio 2015 é
>
> `HKCU\Software\Microsoft\VisualStudio\14.0Exp` e `HKCU\Software\Microsoft\VisualStudio\14.0Exp_Config`

 Recomendamos que você execute sua extensão na instância experimental enquanto estiver desenvolvendo. Quando você implanta a extensão, ela é executada na instância de desenvolvimento. Para obter mais informações sobre como registrar aplicativos, consulte [registrando VSPackages](../extensibility/internals/registering-vspackages.md).
