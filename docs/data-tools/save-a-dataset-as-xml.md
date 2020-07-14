---
title: Salvar um conjunto de dados como XML
ms.date: 11/04/2016
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- XML [Visual Basic], datasets
- data [Visual Studio], saving as XML
- datasets [Visual Basic], saving as XML
- saving data
ms.assetid: 68b8327c-ae05-49ff-b9ba-99183e70b52c
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- data-storage
ms.openlocfilehash: cc8854581903ab58a327ff18be7b3b7c0f860a3b
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/23/2020
ms.locfileid: "85281728"
---
# <a name="save-a-dataset-as-xml"></a>Salvar um conjunto de dados como XML

Acesse os dados XML em um DataSet, chamando os métodos XML disponíveis no conjunto de dados. Para salvar os dados em formato XML, você pode chamar o <xref:System.Data.DataSet.GetXml%2A> método ou o <xref:System.Data.DataSet.WriteXml%2A> método de um <xref:System.Data.DataSet> .

Chamar o <xref:System.Data.DataSet.GetXml%2A> método retorna uma cadeia de caracteres que contém os dados de todas as tabelas de dados no DataSet formatados como XML.

Chamar o <xref:System.Data.DataSet.WriteXml%2A> método envia os dados formatados em XML para um arquivo que você especificar.

## <a name="to-save-the-data-in-a-dataset-as-xml-to-a-variable"></a>Para salvar os dados em um DataSet como XML em uma variável

- O método <xref:System.Data.DataSet.GetXml%2A> retorna um <xref:System.String>. Declare uma variável do tipo <xref:System.String> e atribua a ela os resultados do <xref:System.Data.DataSet.GetXml%2A> método.

     [!code-vb[VbRaddataSaving#12](../data-tools/codesnippet/VisualBasic/save-a-dataset-as-xml_1.vb)]
     [!code-csharp[VbRaddataSaving#12](../data-tools/codesnippet/CSharp/save-a-dataset-as-xml_1.cs)]

## <a name="to-save-the-data-in-a-dataset-as-xml-to-a-file"></a>Para salvar os dados em um DataSet como XML em um arquivo

- O <xref:System.Data.DataSet.WriteXml%2A> método tem várias sobrecargas. Declare uma variável e atribua um caminho válido para salvar o arquivo. O código a seguir mostra como salvar os dados em um arquivo:

     [!code-vb[VbRaddataSaving#13](../data-tools/codesnippet/VisualBasic/save-a-dataset-as-xml_2.vb)]
     [!code-csharp[VbRaddataSaving#13](../data-tools/codesnippet/CSharp/save-a-dataset-as-xml_2.cs)]

## <a name="see-also"></a>Veja também

- [Salvar dados de volta no banco de dados](../data-tools/save-data-back-to-the-database.md)
