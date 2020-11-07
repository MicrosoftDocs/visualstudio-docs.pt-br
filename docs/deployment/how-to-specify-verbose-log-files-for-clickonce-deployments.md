---
title: Especificar arquivos de log detalhados (implantações ClickOnce)
description: Saiba como especificar o detalhamento para os logs de atividade que o ClickOnce mantém para instalação, inicialização, atualização e desinstalação de uma implantação do ClickOnce.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- logs, ClickOnce deployment
- ClickOnce deployment, logging
ms.assetid: 0807a28d-2e40-4a51-ab10-308d808ded6b
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 0da285cfef49bd495fbecf39131e49cacd0476a5
ms.sourcegitcommit: 75bfdaab9a8b23a097c1e8538ed1cde404305974
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/07/2020
ms.locfileid: "94350914"
---
# <a name="how-to-specify-verbose-log-files-for-clickonce-deployments"></a>Como especificar arquivos de log detalhados para implantações do ClickOnce
[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] mantém arquivos de log de atividades para todas as implantações. Esses logs documentam detalhes referentes à instalação, inicialização, atualização e desinstalação de uma [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] implantação. Para aumentar os detalhes que [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] gravam nesses arquivos de log, use o editor do registro ( *regedit.exe* ) para especificar o nível de verbosidade.

> [!CAUTION]
> Se você usar o editor do registro incorretamente, poderá causar sérios problemas que podem exigir a reinstalação do sistema operacional. Use o Editor do Registro por sua conta e risco.

 O procedimento a seguir descreve como especificar o nível de verbosidade para [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] arquivos de log para o usuário atual. Para reduzir o nível de detalhamento, remova esse valor de registro.

### <a name="to-specify-verbose-log-files"></a>Para especificar arquivos de log detalhados

1. Abra *Regedit.exe*.

2. Navegue até o nó **HKEY_CURRENT_USER\Software\Classes\Software\Microsoft\Windows\CurrentVersion\Deployment**.

3. Se necessário, crie um novo valor de cadeia de caracteres chamado `LogVerbosityLevel` .

4. Defina o `LogVerbosityLevel` valor como `1` .

## <a name="see-also"></a>Veja também
- [Solucionar problemas de implantações do ClickOnce](../deployment/troubleshooting-clickonce-deployments.md)