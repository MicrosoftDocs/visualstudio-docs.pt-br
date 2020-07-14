---
title: Erro-não é possível conectar-se ao nome do computador &lt; &gt; . Não foi possível encontrar o computador na rede. | Microsoft Docs
ms.date: 11/04/2016
ms.topic: error-reference
f1_keywords:
- vs.debug.remote.dcom_disabled
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- DCOM, unable to connect error
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 8618a15ab4dcd6c9bbc0d9d8ab9bf347552883b1
ms.sourcegitcommit: 66f31cc4ce1236e638ab58d2f70d3646206386fa
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85460137"
---
# <a name="error-unable-to-connect-to-the-machine-ltnamegt-the-machine-cannot-be-found-on-the-network"></a>Erro: não é possível conectar-se ao nome do computador &lt; &gt; . Não foi possível encontrar o computador na rede.
Esse comportamento ocorre se uma das seguintes condições for verdadeira:

- Sua conexão com o computador remoto foi interrompida.

- Sua conta de usuário no computador remoto está desabilitada.

- Sua senha no computador remoto expirou.

### <a name="to-resolve-this-behavior"></a>Para resolver esse comportamento:

- Verifique se o computador local e o computador remoto estão na mesma rede. Para fazer isso, use o Microsoft Windows Explorer (ou Pesquisador de Arquivos) para tentar acessar o computador remoto.

     — e —

- Verifique se a conta de usuário que você está usando para se conectar ao computador remoto está habilitada.

     — e —

- Verifique se a senha que você está usando para se conectar ao computador remoto está válida e não expirou.

## <a name="see-also"></a>Veja também
- [Depuração remota](../debugger/remote-debugging.md)
- [Preparação e configurações do depurador](../debugger/debugger-settings-and-preparation.md)