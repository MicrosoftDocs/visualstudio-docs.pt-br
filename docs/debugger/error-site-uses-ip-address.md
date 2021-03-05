---
description: Esse erro ocorre quando o depurador tenta anexar-se automaticamente a um aplicativo Web que está usando um endereço IP.
title: O site usa o endereço IP | Microsoft Docs
ms.date: 11/04/2016
ms.topic: error-reference
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
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: fa18ea975bacbda38a18c27d19d438ab5b4da0b5
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102146732"
---
# <a name="error-site-uses-ip-address"></a>Erro: o site usa endereço IP
Esse erro ocorre quando o depurador tenta anexar-se automaticamente a um aplicativo Web que está usando um endereço IP. Isso ocorrerá se você alterar **Identificação do site** para **usar o endereço IP específico** no IIS.

 Para que o anexo automático funcione, você precisará criar o projeto com o endereço IP específico em vez de apenas o nome do computador. Caso contrário, o depurador alterará o nome do computador para localhost, o que causará uma falha ao enviar o verbo de depuração para o IIS.

### <a name="to-correct-this-error"></a>Para corrigir este erro

1. Use a anexação manual em vez disso (no menu depurar, escolha **Anexar ao Processo**).

     — ou —

2. Altere a configuração de **Identificação do site do IIS**.

## <a name="see-also"></a>Confira também
- [Depurando aplicativos Web: erros e solução de problemas](../debugger/debugging-web-applications-errors-and-troubleshooting.md)
