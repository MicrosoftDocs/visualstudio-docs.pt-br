---
title: Ocorreu um erro de DCOM durante a tentativa de contatar o computador remoto. O acesso foi negado. | Microsoft Docs
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
- vs.debug.remote.dcom_access_denied
dev_langs:
- FSharp
- VB
- CSharp
- C++
- JScript
helpviewer_keywords:
- remote debugging, DCOM error
- remote DCOM access denied error
- DCOM, access errors
ms.assetid: 9d7dfc1b-9fe0-4f54-9c50-9c0e0f8358c5
caps.latest.revision: 30
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: ec23d23934268ebb50699bc1de3d17b75d357d3a
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51770283"
---
# <a name="a-dcom-error-occurred-trying-to-contact-the-remote-computer-access-is-denied"></a>Ocorreu um erro de DCOM durante a tentativa de contatar o computador remoto. O acesso foi negado.
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Depuração remota usa DCOM para se comunicar entre os computadores locais e remotos nas seguintes situações:  
  
- O depurador está definido como **modo de compatibilidade nativa** ou **modo de compatibilidade gerenciado** check-in a **Ferramentas / opções / depuração** página  
  
- Você está depurando C++ gerenciado (C + + / CLI) código.  
  
- No Visual Studio 2013, quando **habilitar nativo editar e continuar** check-in a **Ferramentas / opções / depuração** página  
  
- Alguns cenários de depuração de terceiros  
  
  Esse erro ocorre quando o processo do Visual Studio não puder se autenticar (ou as credenciais fornecidas forem julgadas insuficientes) para o processo remoto do depurador sobre DCOM. Uma ou mais das seguintes alternativas podem resolver o problema:  
  
- Desative **modo de compatibilidade nativa** e **modo de compatibilidade gerenciado**.  
  
- No Visual Studio 2013, desative **habilitar nativo editar e continuar**.  
  
- Reinicializar ambos os computadores.  
  
- Se a depuração remota exigir a inserção de credenciais, verifique a opção para salvar as credenciais.  
  
## <a name="see-also"></a>Consulte também  
 [Solução de problemas e erros de depuração remota](../debugger/remote-debugging-errors-and-troubleshooting.md)   
 [Depuração remota](../debugger/remote-debugging.md)



