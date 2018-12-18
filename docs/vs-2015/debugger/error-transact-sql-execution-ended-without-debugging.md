---
title: 'Erro: Execução de Transact-SQL terminou sem depuração | Microsoft Docs'
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
- vs.debug.error.sqlde_sql_executed_but_not_debugged
dev_langs:
- FSharp
- VB
- CSharp
- C++
- SQL
ms.assetid: 7a4d4999-3973-4339-ba6a-f0d19bcb1d4a
caps.latest.revision: 12
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: b67900f02a81a6a28279268c3fe6fa067bcdaedc
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51787634"
---
# <a name="error-transact-sql-execution-ended-without-debugging"></a>Erro: execução de Transact-SQL encerrada sem depuração
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Esse erro ocorre quando você está tentando depurar um procedimento do Transact-SQL ou SQLCLR e o depurador não recebe mensagens de depuração do SQL Server.  
  
 Isso pode ocorrer devido a problemas de rede ou problemas no SQL Server, mas a causa mais provável é um problema de permissões.  
  
 Há duas contas envolvidas:  
  
- A conta de aplicativo é a conta de usuário como o [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] está sendo executado.  
  
- A conta de conexão é a identidade usada para fazer a conexão com o SQL Server. Isso não é necessariamente o mesmo que a identidade que o Visual Studio está executando como se a conexão estivesse usando a autenticação do SQL.  
  
  A depuração de SQL exige que a conta do aplicativo deva corresponder à conta de conexão ou ser sysadmin.  
  
  Se você estiver usando um logon do SQL como sa, a conta de aplicativo deverá ser configurada no SQL Server como um sysadmin. Por padrão, os administradores no computador em que o SQL está sendo executado são sysadmins do SQL Server.  
  
  Para corrigir esse erro, talvez seja necessário:  
  
- Verificar suas configurações de permissões. Para obter mais informações, consulte [como: definir permissões do SQL Server para depuração](http://msdn.microsoft.com/en-us/84e088d0-0409-41d4-841b-f5d4b0fda414).  
  
- Verifique se a depuração do SQL está configurada corretamente.  
  
- Consulte o administrador de rede ou banco de dados.  
  
## <a name="see-also"></a>Consulte também  
 [Configuração de depuração de SQL](http://msdn.microsoft.com/en-us/3db09e68-edcc-42de-9c22-4e97cfd55ab3)   
 [Como: definir permissões do SQL Server para depuração](http://msdn.microsoft.com/en-us/84e088d0-0409-41d4-841b-f5d4b0fda414)   
 [Preparação e configurações do depurador](../debugger/debugger-settings-and-preparation.md)   
 [Depuração remota](../debugger/remote-debugging.md)



