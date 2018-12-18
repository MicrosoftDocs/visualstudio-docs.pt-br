---
title: -SafeMode (devenv.exe)
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-ide-general
ms.topic: reference
helpviewer_keywords:
- /SafeMode Devenv switch
- Devenv, /SafeMode switch
- SafeMode switch
ms.assetid: b191f6a5-8f12-47ec-bcc7-b68149a22aa8
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 6df78ec4be1fc94951634b84a98e80dc1403a41b
ms.sourcegitcommit: 54c65f81a138fc1e8ff1826f7bd9dcec710618cc
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/19/2018
ms.locfileid: "51948732"
---
# <a name="safemode-devenvexe"></a>/SafeMode (devenv.exe)
Inicia o [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] no modo de segurança, carregando apenas o ambiente e os serviços padrão.

## <a name="syntax"></a>Sintaxe

```cmd
devenv /SafeMode
```

## <a name="remarks"></a>Comentários
 Essa opção impede que todos os VSPackages de terceiros sejam carregados quando o [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] é iniciado, garantindo assim uma execução estável.

## <a name="description"></a>Descrição
 O exemplo a seguir inicia o [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] no modo de segurança.

## <a name="code"></a>Código

```cmd
Devenv.exe /SafeMode
```

## <a name="see-also"></a>Consulte também

- [Opções de linha de comando do Devenv](../../ide/reference/devenv-command-line-switches.md)