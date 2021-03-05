---
description: A depuração do Procedimento Armazenado sp_enable_sql_debug não pode ser executada no servidor.
title: O usuário não pôde executar o procedimento armazenado sp_enable_sql_debug | Microsoft Docs
ms.date: 11/04/2016
ms.topic: error-reference
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
ms.openlocfilehash: 8c7597acb201aa810d34fe0df0f0aebbbd2f70fe
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102146282"
---
# <a name="error-user-could-not-execute-stored-procedure-sp_enable_sql_debug"></a>Erro: o usuário não conseguiu executar o procedimento armazenado sp_enable_sql_debug

A depuração do Procedimento Armazenado sp_enable_sql_debug não pode ser executada no servidor. Isso pode ser causado por:

- Um problema de conexão. Você precisa ter uma conexão estável com o servidor.

- Falta das permissões necessárias no servidor. Para depurar no SQL Server 2005, a conta que executa o Visual Studio e a conta usada para conectar-se ao SQL Server devem ser membros da função sysadmin. A conta usada para se conectar ao SQL Server é sua conta de usuário do Windows (se você estiver usando a autenticação do Windows) ou uma conta com ID de usuário e senha (se você usar a autenticação do SQL).

Para obter mais informações, consulte [How to: Set SQL Server Permissions for Debugging](/previous-versions/w1bhybwz(v=vs.100)).

## <a name="see-also"></a>Confira também

- [Como configurar permissões para depuração no SQL Server](/previous-versions/w1bhybwz(v=vs.100))
- [Configurando a depuração SQL](/previous-versions/visualstudio/visual-studio-2010/s4sszxst\(v\=vs.100\))
