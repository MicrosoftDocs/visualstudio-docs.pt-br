---
title: 'Erro: SQL pode&#39;t consegue localizar SSDEBUGPS | Microsoft Docs'
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-debug
ms.topic: troubleshooting
f1_keywords:
- vs.debug.error.sqlde_cant_find_ssdebugps
dev_langs:
- CSharp
- VB
- FSharp
- C++
- SQL
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 1498a287bdb474751dfaa5b4b23c30bc302544e7
ms.sourcegitcommit: 0bf2aff6abe485e3fe940f5344a62a885ad7f44e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/27/2018
ms.locfileid: "37058250"
---
# <a name="error-sql-can39t-find-ssdebugps"></a>Erro: SQL pode&#39;t consegue localizar SSDEBUGPS

SSDEBUGPS.dll é o componente do host de depuração do SQL Server.

Esse erro ocorre quando você está tentando iniciar a depuração e indica que o arquivo especificado não está presente no computador do [!INCLUDE[sqprsqlong](../debugger/includes/sqprsqlong_md.md)]. As causas possíveis são que a instalação da Depuração Remota nunca foi executada ou que de alguma forma esse arquivo foi excluído.

Há duas maneiras de resolver esse erro: executando novamente a instalação da depuração remota e copiando o arquivo para o [!INCLUDE[sqprsqlong](../debugger/includes/sqprsqlong_md.md)] máquina.

Para executar novamente a instalação da depuração remota, siga as instruções em [depuração remota](../debugger/remote-debugging.md).

Se você puder localizar uma cópia de ssdebugps. dll, você pode copiá-lo no [!INCLUDE[sqprsqlong](../debugger/includes/sqprsqlong_md.md)] máquina. Se houver, o arquivo estará no diretório \Arquivos de Programas\ Common Files\Microsoft Shared\SQL Debugging. Você pode encontrá-lo em outro [!INCLUDE[sqprsqlong](../debugger/includes/sqprsqlong_md.md)] computador, ou em um computador que tenha o Visual Studio 2005 instalado.

Para copiar o ssdebugps. dll no computador SQL Server 2005:

1. Copie o arquivo para o diretório com o mesmo nome e caminho no [!INCLUDE[sqprsqlong](../debugger/includes/sqprsqlong_md.md)] máquina.

2. Registre-o abrindo uma **Prompt de comando**e executando o seguinte comando:

    ```cmd
    regsrv32 ssdebugps.dll
    ```
