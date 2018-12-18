---
title: Você selecionou um objeto de banco de dados de um provedor de banco de dados sem suporte | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: c0f1298e-31aa-471e-ae19-1bafffd2ae40
caps.latest.revision: 8
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: 1027be99525081ad4df959908b856727e9ebe399
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49211688"
---
# <a name="you-have-selected-a-database-object-from-an-unsupported-database-provider"></a>Você tiver selecionado um objeto de base de dados de um provedor de base de dados sem suporte
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

O [!INCLUDE[vs_ordesigner_long](../includes/vs-ordesigner-long-md.md)] ([!INCLUDE[vs_ordesigner_short](../includes/vs-ordesigner-short-md.md)]) dá suporte a apenas o .NET Framework Data Provider para SQL Server (<xref:System.Data.SqlClient>). Embora você possa clique **Okey** e continuar a trabalhar com objetos de provedores de banco de dados sem suporte, você pode enfrentar um comportamento inesperado em tempo de execução.  
  
> [!NOTE]
>  Somente as conexões de dados que usam o provedor de dados. NET Framework para SQL Server são suportadas.  
  
### <a name="to-correct-this-error"></a>Para corrigir este erro  
  
-   Clique em **Okey** para continuar a criar as classes de entidade que mapeiam para a conexão que usa o provedor de banco de dados sem suporte. Você pode apresentar comportamento inesperado quando você usa provedores de base de dados sem suporte.  
  
     -ou-  
  
-   Clique em **Cancelar**.  
  
     A ação é interrompida. Crie ou use uma conexão de dados que usa o provedor do. NET Framework para SQL Server.  
  
## <a name="see-also"></a>Consulte também  
 [Ferramentas LINQ to SQL no Visual Studio](../data-tools/linq-to-sql-tools-in-visual-studio2.md)   
 [LINQ to SQL](http://msdn.microsoft.com/library/73d13345-eece-471a-af40-4cc7a2f11655)   
 [Provedores de dados do .NET framework](http://msdn.microsoft.com/library/03a9fc62-2d24-491a-9fe6-d6bdb6dcb131)   
 [Conectando-se a dados no Visual Studio](../data-tools/connecting-to-data-in-visual-studio.md)

