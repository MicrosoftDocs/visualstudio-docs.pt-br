---
title: Salvar um conjunto de dados como XML | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
dev_langs:
- VB
- CSharp
- C++
- aspx
helpviewer_keywords:
- XML [Visual Basic], datasets
- data [Visual Studio], saving as XML
- datasets [Visual Basic], saving as XML
- saving data
ms.assetid: 68b8327c-ae05-49ff-b9ba-99183e70b52c
caps.latest.revision: 14
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: a91bc594f2f028f7dfc7a11263b7aac23150b7f5
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49287567"
---
# <a name="save-a-dataset-as-xml"></a>Salvar um conjunto de dados como XML
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

  
Os dados XML em um conjunto de dados podem ser acessados chamando os métodos XML disponíveis no conjunto de dados. Para salvar os dados em formato XML, você pode chamar o <xref:System.Data.DataSet.GetXml%2A> método ou o <xref:System.Data.DataSet.WriteXml%2A> método de um <xref:System.Data.DataSet>.  
  
 Chamar o <xref:System.Data.DataSet.GetXml%2A> método retorna uma cadeia de caracteres que contém os dados de todas as tabelas de dados no conjunto de dados que está formatado como XML.  
  
 Chamar o <xref:System.Data.DataSet.WriteXml%2A> método envia os dados formatados em XML para um arquivo que você especifica.  
  
### <a name="to-save-the-data-in-a-dataset-as-xml-to-a-variable"></a>Para salvar os dados em um conjunto de dados como XML em uma variável  
  
-   O <xref:System.Data.DataSet.GetXml%2A> método retorna um <xref:System.String>. Isso significa que você declare uma variável do tipo <xref:System.String> e atribua a ele os resultados do <xref:System.Data.DataSet.GetXml%2A> método.  
  
     [!code-csharp[VbRaddataSaving#12](../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataSaving/CS/Class1.cs#12)]
     [!code-vb[VbRaddataSaving#12](../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataSaving/VB/Class1.vb#12)]  
  
### <a name="to-save-the-data-in-a-dataset-as-xml-to-a-file"></a>Para salvar os dados em um conjunto de dados como XML em um arquivo  
  
-   O <xref:System.Data.DataSet.WriteXml%2A> método tem várias sobrecargas. O código a seguir mostra como salvar os dados em um arquivo. Declare uma variável e atribuí-lo em um caminho válido para salvar o arquivo.  
  
     [!code-csharp[VbRaddataSaving#13](../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataSaving/CS/Class1.cs#13)]
     [!code-vb[VbRaddataSaving#13](../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataSaving/VB/Class1.vb#13)]  
  
## <a name="see-also"></a>Consulte também  
 [Salvar dados de volta no banco de dados](../data-tools/save-data-back-to-the-database.md)

