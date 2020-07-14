---
title: A conexão selecionada usa um provedor de base de dados sem suporte
ms.date: 11/04/2016
ms.topic: error-reference
ms.assetid: 4d25dfa1-8fa4-4529-9b90-973bc2ec2993
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- data-storage
ms.openlocfilehash: 52b88e1de91c2b2da629b6b9034ac552b8d88d5d
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/23/2020
ms.locfileid: "85281312"
---
# <a name="the-selected-connection-uses-an-unsupported-database-provider"></a>A conexão selecionada usa um provedor de base de dados sem suporte

Essa mensagem é exibida quando você arrasta itens que não usam o .NET Framework Provedor de Dados para SQL Server de **Gerenciador de servidores** ou **Gerenciador de banco de dados** nas [ferramentas de LINQ to SQL no Visual Studio](../data-tools/linq-to-sql-tools-in-visual-studio2.md).

O o **/R Designer** dá suporte apenas a conexões de dados que usam o provedor de .NET Framework para SQL Server. Somente as conexões a Microsoft SQL Server ou o Arquivo base de dados do Microsoft SQL Server são válidos.

Para corrigir esse erro, adicione somente itens de conexões de dados que usam o .NET Framework Provedor de Dados para SQL Server ao o **/R Designer**.

## <a name="see-also"></a>Veja também

- <xref:System.Data.SqlClient>
- [Ferramentas do LINQ to SQL no Visual Studio](../data-tools/linq-to-sql-tools-in-visual-studio2.md)
