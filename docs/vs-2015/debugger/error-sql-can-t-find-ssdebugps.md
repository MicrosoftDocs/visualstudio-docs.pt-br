---
title: 'Erro: SQL pode&#39;t consegue localizar SSDEBUGPS | Microsoft Docs'
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
- vs.debug.error.sqlde_cant_find_ssdebugps
dev_langs:
- FSharp
- VB
- CSharp
- C++
- SQL
ms.assetid: 596425c8-14c7-4c05-8823-e1c52f420f5e
caps.latest.revision: 9
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 47e0557e3ad2022250d54b7bd45844825ff79a03
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51757462"
---
# <a name="error-sql-can39t-find-ssdebugps"></a>Erro: SQL pode&#39;t consegue localizar SSDEBUGPS
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

SSDEBUGPS.dll é o componente do host de depuração do SQL Server.  
  
 Esse erro ocorre quando você está tentando iniciar a depuração e indica que o arquivo especificado não está presente no computador do [!INCLUDE[sqprsqlong](../includes/sqprsqlong-md.md)]. As causas possíveis são que a instalação da Depuração Remota nunca foi executada ou que de alguma forma esse arquivo foi excluído.  
  
 Há duas maneiras de resolver esse erro: executando novamente a instalação da depuração remota e copiando o arquivo para o [!INCLUDE[sqprsqlong](../includes/sqprsqlong-md.md)] máquina.  
  
 Para executar novamente a instalação da depuração remota, siga as instruções em [depuração remota](../debugger/remote-debugging.md).  
  
 Se você puder localizar uma cópia de ssdebugps. dll, você pode copiá-lo no [!INCLUDE[sqprsqlong](../includes/sqprsqlong-md.md)] máquina. Se houver, o arquivo estará no diretório \Arquivos de Programas\ Common Files\Microsoft Shared\SQL Debugging. Você pode encontrá-lo em outro [!INCLUDE[sqprsqlong](../includes/sqprsqlong-md.md)] computador, ou em um computador que tenha [!INCLUDE[vsprvslong](../includes/vsprvslong-md.md)] instalado.  
  
### <a name="to-copy-ssdebugpsdll-onto-the-sql-server-2005-machine"></a>Para copiar o SSDEBUGPS.dll no computador do SQL Server 2005  
  
1.  Copie o arquivo para o diretório com o mesmo nome e caminho no [!INCLUDE[sqprsqlong](../includes/sqprsqlong-md.md)] máquina.  
  
2.  Registre-o abrindo uma **Prompt de comando**e executando o seguinte comando:  
  
    ```  
    regsrv32 ssdebugps.dll  
    ```



