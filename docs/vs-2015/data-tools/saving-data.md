---
title: Salvando dados | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- DataRow.RowState
- DataSet.GetChanges
dev_langs:
- VB
- CSharp
- C++
- aspx
helpviewer_keywords:
- DBDirect methods
- updating data
- data [Visual Studio], saving
- TableAdapter DBDirect methods
- databases, updating
- TableAdapter.Update method
- data [Visual Studio], updating
- saving data
- updating databases
ms.assetid: 21d2b115-62e4-4ac9-a873-dcbb535b8af8
caps.latest.revision: 13
author: gewarren
ms.author: gewarren
manager: ghogen
robots: noindex,nofollow
ms.openlocfilehash: dc671d60ff37e9853dc64a62cbc1b91a6914e0e3
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49249295"
---
# <a name="saving-data"></a>Salvar Dados
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Salvar dados é que o processo de persistência alterou os dados no modelo de dados do aplicativo para o armazenamento de dados original, geralmente um banco de dados relacional como o SQL Server.  
  
 Atualizar uma fonte de dados por meio de um modelo de dados geralmente é um processo em duas etapas. A primeira etapa é atualizar o modelo de dados com novas informações — novos registros, registros alterados ou registros excluídos. A segunda etapa é salvar as alterações no seu modelo de dados no banco de dados.  
  
 Os tópicos a seguir descrevem os conceitos e tarefas associadas para salvar dados.  
  
## <a name="related-topics"></a>Tópicos relacionados  
 [Salvar dados de volta no banco de dados](../data-tools/save-data-back-to-the-database.md)  
 Fornece uma visão geral de como as alterações são feitas em um conjunto de dados e como o conjunto de dados controla informações sobre as alterações para salvar essas alterações em um banco de dados.  
  
 [Salvando dados de entidade](../data-tools/saving-entity-data.md)  
 Descreve como salvar as alterações no [ADO.NET Entity Framework](http://msdn.microsoft.com/library/a437041f-6899-4ae7-96ce-aabf528d7205) e [4.5 do WCF Data Services](http://msdn.microsoft.com/library/73d2bec3-7c92-4110-b905-11bb0462357a) aplicativos.