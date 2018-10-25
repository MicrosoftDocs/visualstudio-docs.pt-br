---
title: 'Erro: O usuário não conseguiu executar procedimento armazenado sp_enable_sql_debug | Microsoft Docs'
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-debug
ms.topic: troubleshooting
f1_keywords:
- vs.debug.error.sqlde_accessdenied
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
ms.openlocfilehash: f13eb0b7deb9295ac20e04f4ba1111e128efa0c0
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49903979"
---
# <a name="error-user-could-not-execute-stored-procedure-spenablesqldebug"></a>Erro: o usuário não conseguiu executar o procedimento armazenado sp_enable_sql_debug
A depuração do Procedimento Armazenado sp_enable_sql_debug não pode ser executada no servidor. Isso pode ser causado por:  
  
- Um problema de conexão. Você precisa ter uma conexão estável com o servidor.  
  
- Falta das permissões necessárias no servidor. Para depurar no SQL Server 2005, a conta que executa o Visual Studio e a conta usada para conectar-se ao SQL Server devem ser membros da função sysadmin. A conta usada para se conectar ao SQL Server é sua conta de usuário do Windows (se você estiver usando a autenticação do Windows) ou uma conta com ID de usuário e senha (se você usar a autenticação do SQL).  
  
  Para obter mais informações, consulte [como: definir permissões do SQL Server para depuração](http://msdn.microsoft.com/en-us/84e088d0-0409-41d4-841b-f5d4b0fda414).  
  
## <a name="see-also"></a>Consulte também  
 [Como: definir permissões do SQL Server para depuração](http://msdn.microsoft.com/en-us/84e088d0-0409-41d4-841b-f5d4b0fda414)   
 [Configuração de depuração de SQL](http://msdn.microsoft.com/en-us/3db09e68-edcc-42de-9c22-4e97cfd55ab3)