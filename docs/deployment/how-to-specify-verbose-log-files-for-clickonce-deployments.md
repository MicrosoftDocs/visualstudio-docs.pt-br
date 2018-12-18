---
title: 'Como: especificar arquivos de Log detalhados para implantações do ClickOnce | Microsoft Docs'
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-deployment
ms.topic: conceptual
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
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: bbb3214df1cd51baf731f8a16f39b2c5a59933bb
ms.sourcegitcommit: 8ee7efb70a1bfebcb6dd9855b926a4ff043ecf35
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/17/2018
ms.locfileid: "39078736"
---
# <a name="how-to-specify-verbose-log-files-for-clickonce-deployments"></a>Como: especificar arquivos de log detalhados para implantações do ClickOnce
[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] mantém os arquivos de log de atividades para todas as implantações. Esses logs documentar detalhes referentes à instalação, inicializando, atualizando e desinstalando uma [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] implantação. Para aumentar o detalhe que [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] gravações para esses arquivos de log, use o Editor do registro (*regedit.exe*) para especificar o nível de detalhamento.  
  
> [!CAUTION]
>  Se você usar o Editor do Registro incorretamente, poderá causar sérios problemas que talvez exijam a reinstalação do sistema operacional. Use o Editor do registro por seu próprio risco.  
  
 O procedimento a seguir descreve como especificar o nível de detalhamento para [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] arquivos de log para o usuário atual. Para reduzir o nível de detalhamento, remova esse valor do registro.  
  
### <a name="to-specify-verbose-log-files"></a>Para especificar os arquivos de log detalhados  
  
1.  Abra *Regedit.exe*.  
  
2.  Navegue até o nó **HKEY_CURRENT_USER\Software\Classes\Software\Microsoft\Windows\CurrentVersion\Deployment**.  
  
3.  Se necessário, crie um novo valor de cadeia de caracteres chamado `LogVerbosityLevel`.  
  
4.  Defina as `LogVerbosityLevel` valor `1`.  
  
## <a name="see-also"></a>Consulte também  
 [Solucionar problemas de implantações do ClickOnce](../deployment/troubleshooting-clickonce-deployments.md)