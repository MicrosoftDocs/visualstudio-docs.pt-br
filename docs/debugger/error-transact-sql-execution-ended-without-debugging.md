---
description: Esse erro ocorre quando você está tentando depurar um procedimento Transact-SQL ou SQLCLR e o depurador não recebe mensagens de depuração do SQL Server.
title: A execução do Transact-SQL foi finalizada sem depuração | Microsoft Docs
ms.date: 11/08/2018
ms.topic: error-reference
f1_keywords:
- vs.debug.error.sqlde_sql_executed_but_not_debugged
dev_langs:
- CSharp
- VB
- FSharp
- C++
- SQL
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 40b0b89474b24e53c69df14894e50ee502c6eb9b
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102146490"
---
# <a name="error-transact-sql-execution-ended-without-debugging"></a>Erro: execução de Transact-SQL encerrada sem depuração

Esse erro ocorre quando você está tentando depurar um procedimento Transact-SQL ou SQLCLR e o depurador não recebe mensagens de depuração do SQL Server.

Esse problema pode ser devido a problemas de rede ou problemas na SQL Server, mas a causa mais provável é um problema de permissões.

Há duas contas envolvidas:

- A conta de aplicativo é a conta de usuário como o [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] está sendo executado.

- A conta de conexão é a identidade usada para fazer a conexão com o SQL Server. Essa conta não é necessariamente a mesma que a identidade em que o Visual Studio está sendo executado como se a conexão estiver usando a autenticação do SQL.

  A depuração SQL requer que a conta de aplicativo corresponda à conta de conexão ou que seja um sysadmin.

  Se você estiver usando um nome de conta SQL como SA, a conta de aplicativo deverá ser configurada no SQL Server como um sysadmin. Por padrão, os administradores no computador em que o SQL Server está sendo executado são SQL Server sysadmins.

  Para corrigir esse erro, talvez seja necessário:

  - Verificar suas configurações de permissões. Para obter mais informações, consulte [How to: Set SQL Server Permissions for Debugging](/previous-versions/w1bhybwz(v=vs.100)).

  - Verifique se a depuração do SQL está configurada corretamente.

  - Consulte o administrador de rede ou banco de dados.

## <a name="see-also"></a>Confira também

- [Configurando a depuração SQL](/previous-versions/visualstudio/visual-studio-2010/s4sszxst(v=vs.100))
- [Como configurar permissões para depuração no SQL Server](/previous-versions/w1bhybwz(v=vs.100))
- [Configurações e preparação do depurador](../debugger/debugger-settings-and-preparation.md)
- [Depuração remota](../debugger/remote-debugging.md)
