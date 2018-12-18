---
title: 'Erro: O Site usa endereço IP | Microsoft Docs'
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-debug
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- vs.debug.error.webdbg_siteusesipaddress
dev_langs:
- FSharp
- VB
- CSharp
- C++
helpviewer_keywords:
- debugger, Web application errors
ms.assetid: b2b8ddc8-746d-46e3-87a6-b956b1ee048d
caps.latest.revision: 11
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: daa9ed74df46dd6be66a27d09cbbd7c311e03de4
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51793666"
---
# <a name="error-site-uses-ip-address"></a>Erro: o site usa endereço IP
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Esse erro ocorre quando o depurador tenta anexar-se automaticamente a um aplicativo Web que está usando um endereço IP. Isso ocorre se você alterar **identificação de site** à **usar endereço IP específico** no IIS.  
  
 Para que o anexo automático funcione, você precisará criar o projeto com o endereço IP específico em vez de apenas o nome do computador. Caso contrário, o depurador alterará o nome do computador para localhost, o que causará uma falha ao enviar o verbo de depuração para o IIS.  
  
### <a name="to-correct-this-error"></a>Para corrigir este erro  
  
1.  Use a anexação manual em vez disso (no menu Depurar, escolha **anexar ao processo**).  
  
     —ou—  
  
2.  Alterar o **identificação do site da Web do IIS** configuração.  
  
## <a name="see-also"></a>Consulte também  
 [Depurando aplicativos Web: erros e solução de problemas](../debugger/debugging-web-applications-errors-and-troubleshooting.md)



