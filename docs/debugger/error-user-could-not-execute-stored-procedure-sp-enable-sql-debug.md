---
title: Erro-o usuário não pôde executar o procedimento armazenado sp_enable_sql_debug | Microsoft Docs
ms.date: 11/04/2016
ms.topic: error-reference
dev_langs:
- CSharp
- VB
- FSharp
- C++
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: c1da494b5bb8c168775e2183f41113f00d021792
ms.sourcegitcommit: 66f31cc4ce1236e638ab58d2f70d3646206386fa
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85460059"
---
# <a name="error-user-could-not-execute-stored-procedure-sp_enable_sql_debug"></a>Erro: o usuário não conseguiu executar o procedimento armazenado sp_enable_sql_debug

A depuração do Procedimento Armazenado sp_enable_sql_debug não pode ser executada no servidor. Isso pode ser causado por:

- Um problema de conexão. Você precisa ter uma conexão estável com o servidor.

- Falta das permissões necessárias no servidor. Para depurar no SQL Server 2005, a conta que executa o Visual Studio e a conta usada para conectar-se ao SQL Server devem ser membros da função sysadmin. A conta usada para se conectar ao SQL Server é sua conta de usuário do Windows (se você estiver usando a autenticação do Windows) ou uma conta com ID de usuário e senha (se você usar a autenticação do SQL).

Para obter mais informações, consulte [How to: Set SQL Server Permissions for Debugging](https://msdn.microsoft.com/84e088d0-0409-41d4-841b-f5d4b0fda414).

## <a name="see-also"></a>Veja também

- [Como configurar permissões para depuração no SQL Server](https://msdn.microsoft.com/84e088d0-0409-41d4-841b-f5d4b0fda414)
- [Configurando a depuração SQL](/previous-versions/visualstudio/visual-studio-2010/s4sszxst\(v\=vs.100\))