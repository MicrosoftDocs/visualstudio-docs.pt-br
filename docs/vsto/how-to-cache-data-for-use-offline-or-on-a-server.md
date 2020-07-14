---
title: Como armazenar em cache dados para uso offline ou em um servidor
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- data caching [Office development in Visual Studio], server use
- Office applications [Office development in Visual Studio], data
- datasets [Office development in Visual Studio], caching
- offline data [Office development in Visual Studio]
- data [Office development in Visual Studio], caching
- data caching [Office development in Visual Studio], offline use
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: ce295e299e4accb2d79655675f6264a1497b8d69
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85546179"
---
# <a name="how-to-cache-data-for-use-offline-or-on-a-server"></a>Como armazenar em cache dados para uso offline ou em um servidor
  Você pode marcar um item de dados para ser armazenado em cache no documento, para que ele esteja disponível offline. Isso também possibilita que os dados no documento sejam manipulados por outro código quando o documento é armazenado em um servidor.

 [!INCLUDE[appliesto_alldoc](../vsto/includes/appliesto-alldoc-md.md)]

 Você pode marcar um item de dados para ser armazenado em cache quando o item de dados é declarado em seu código ou, se você estiver usando um <xref:System.Data.DataSet> , definindo uma propriedade na janela **Propriedades** . Se você estiver armazenando em cache um item de dados que não seja um <xref:System.Data.DataSet> ou <xref:System.Data.DataTable> , verifique se ele atende aos critérios para serem armazenados em cache no documento. Para obter mais informações, consulte [armazenar dados em cache](../vsto/caching-data.md).

> [!NOTE]
> Os conjuntos de dados criados usando Visual Basic que são marcados como **armazenados em cache** e **WithEvents** (incluindo conjuntos de dados que são arrastados da janela **Data Sources** ou da **caixa de ferramentas** que têm a propriedade **CacheInDocument** definida como **true**) têm um sublinhado prefixado para seus nomes no cache. Por exemplo, se você criar um conjunto de um e nomeá-lo como **Customers**, o <xref:Microsoft.VisualStudio.Tools.Applications.CachedDataItem> nome será **_Customers** no cache. Ao usar <xref:Microsoft.VisualStudio.Tools.Applications.ServerDocument> o para acessar esse item em cache, você deve especificar **_Customers** em vez de **clientes**.

### <a name="to-cache-data-in-the-document-using-code"></a>Para armazenar em cache dados no documento usando código

1. Declare um campo público ou uma propriedade para o item de dados como um membro de uma classe de item de host em seu projeto, como a `ThisDocumen` classe t em um projeto do Word ou a `ThisWorkbook` classe em um projeto do Excel.

2. Aplique o <xref:Microsoft.VisualStudio.Tools.Applications.Runtime.CachedAttribute> atributo ao membro para marcar o item de dados a ser armazenado no cache de dados do documento. O exemplo a seguir aplica esse atributo a uma declaração de campo para um <xref:System.Data.DataSet> .

     [!code-csharp[Trin_VstcoreDataExcel#11](../vsto/codesnippet/CSharp/Trin_VstcoreDataExcelCS/Sheet1.cs#11)]
     [!code-vb[Trin_VstcoreDataExcel#11](../vsto/codesnippet/VisualBasic/Trin_VstcoreDataExcelVB/Sheet1.vb#11)]

3. Adicione o código para criar uma instância do item de dados e, se aplicável, para carregá-lo a partir dele.

     O item de dados é carregado somente quando é criado pela primeira vez; Depois disso, o cache permanece com o documento e você deve escrever outro código para atualizá-lo.

### <a name="to-cache-a-dataset-in-the-document-by-using-the-properties-window"></a>Para armazenar em cache um conjunto de um DataSet no documento usando o janela Propriedades

1. Adicione o conjunto de dados ao projeto usando ferramentas no designer do Visual Studio, por exemplo, adicionando uma fonte de dado ao seu projeto usando a janela **fontes de dados** .

2. Crie uma instância do conjunto de um, se você ainda não tiver um, e selecione a instância no designer.

3. Na janela **Propriedades** , defina a propriedade **CacheInDocument** como **true**.

     Para obter mais informações, consulte [Propriedades em projetos do Office](../vsto/properties-in-office-projects.md).

4. Na janela **Propriedades** , defina a propriedade **modificadores** como **público** (por padrão, ela é **interna**).

## <a name="see-also"></a>Consulte também
- [Dados de cache](../vsto/caching-data.md)
- [Como: armazenar em cache uma fonte de dados programaticamente em um documento do Office](../vsto/how-to-programmatically-cache-a-data-source-in-an-office-document.md)
- [Como armazenar dados em cache em um documento protegido por senha](../vsto/how-to-cache-data-in-a-password-protected-document.md)
- [Acessar dados em documentos no servidor](../vsto/accessing-data-in-documents-on-the-server.md)
- [Salvar dados](../data-tools/save-data-back-to-the-database.md)
