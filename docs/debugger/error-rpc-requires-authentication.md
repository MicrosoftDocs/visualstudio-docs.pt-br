---
title: 'Erro: RPC requer autenticação | Microsoft Docs'
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-debug
ms.topic: troubleshooting
f1_keywords:
- vs.debug.error.rpc_requires_authentication
dev_langs:
- CSharp
- VB
- FSharp
- C++
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 214dafa5acc925434cf3569570f20ab7f3331bfb
ms.sourcegitcommit: 3d10b93eb5b326639f3e5c19b9e6a8d1ba078de1
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/18/2018
ms.locfileid: "31471610"
---
# <a name="error-rpc-requires-authentication"></a>Erro: RPC requer autenticação
O depurador do Visual Studio não pode se conectar ao computador remoto. Uma política RPC está habilitada no computador local, impedindo a depuração remota.  
  
### <a name="to-correct-this-error"></a>Para corrigir este erro  
  
1.  Executar `\` *windir*`\system32\regedt32.exe`  
  
2.  Localize e exclua `HKEY_LOCAL_MACHINE\Software\Policies\Microsoft\Windows NT\RPC\RestrictRemoteClients`.  
  
3.  Reinicie o computador para que a alteração do Registro entre em vigor.  
  
4.  Se o problema persistir, entre em contato com seu administrador de domínio sobre o **configuração do computador > modelos administrativos > sistema > chamada de procedimento remoto > restrições para os clientes não autenticados RPC** política de grupo configuração.