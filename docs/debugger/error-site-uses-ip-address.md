---
title: 'Erro: O Site usa endereço IP | Microsoft Docs'
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-debug
ms.topic: troubleshooting
f1_keywords:
- vs.debug.error.webdbg_siteusesipaddress
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- debugger, Web application errors
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: b726902c57cc95b694f2ab7e656a444ed42a0ba9
ms.sourcegitcommit: 3d10b93eb5b326639f3e5c19b9e6a8d1ba078de1
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/18/2018
ms.locfileid: "31470898"
---
# <a name="error-site-uses-ip-address"></a>Erro: o site usa endereço IP
Esse erro ocorre quando o depurador tenta anexar-se automaticamente a um aplicativo Web que está usando um endereço IP. Isso ocorre se você alterar **identificação de site** para **usar endereço IP específico** no IIS.  
  
 Para que o anexo automático funcione, você precisará criar o projeto com o endereço IP específico em vez de apenas o nome do computador. Caso contrário, o depurador alterará o nome do computador para localhost, o que causará uma falha ao enviar o verbo de depuração para o IIS.  
  
### <a name="to-correct-this-error"></a>Para corrigir este erro  
  
1.  Manual use em vez disso, anexe (no menu Depurar, escolha **anexar ao processo**).  
  
     —ou—  
  
2.  Alterar o **identificação de site da Web do IIS** configuração.  
  
## <a name="see-also"></a>Consulte também  
 [Depurando aplicativos Web: erros e solução de problemas](../debugger/debugging-web-applications-errors-and-troubleshooting.md)