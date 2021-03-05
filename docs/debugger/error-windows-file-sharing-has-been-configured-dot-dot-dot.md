---
description: O compartilhamento de arquivos do Windows foi configurado de forma que você se conectará ao computador remoto usando um nome do usuário diferente.
title: O compartilhamento de arquivos do Windows foi configurado... | Microsoft Docs
ms.date: 11/04/2016
ms.topic: error-reference
f1_keywords:
- vs.debug.error.remote_credentials_prohibited
dev_langs:
- CSharp
- VB
- FSharp
- C++
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: cc34e269d609837d9080cd1e84787fbabf45ce76
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102146243"
---
# <a name="error-windows-file-sharing-has-been-configured"></a>Erro: o compartilhamento de arquivos do Windows foi configurado...
O compartilhamento de arquivos do Windows foi configurado de forma que você se conectará ao computador remoto usando um nome do usuário diferente. Isso é incompatível com a depuração remota

 A configuração de compartilhamento de arquivos atual está configurada para conectar ao computador remoto usando um nome do usuário diferente. A depuração remota não é possível nesse cenário.

 Para corrigir esse erro, faça logon no computador usando outro nome de conta ou altere o compartilhamento de arquivos para usar o nome de conta com a qual você está depurando.

 Se você quiser se conectar ao computador remoto usando esse nome de usuário, deverá primeiro desconectar do computador remoto.

### <a name="to-correct-this-error"></a>Para corrigir este erro

1. Faça logon em seu computador local, o computador do qual você está depurando, usando o outro nome da conta.

     — ou —

     . Desconecte-se do computador remoto e reconfigure o compartilhamento de arquivos para se conectar ao outro computador usando seu nome de conta:

    1. No menu **Iniciar**, aponte para **Acessórios** e clique em **Prompt de Comando**.

    2. No prompt de comando do Windows, digite:

         `net use /delete computer_name`

    3. Modificar as configurações de compartilhamento de arquivos usando qualquer um dos métodos documentados na Ajuda do Windows.
