---
title: 'Como: armazenar em Cache dados para uso offline ou em um servidor'
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
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
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: a53b3539d71383d4fad95838250380c5849e8c5b
ms.sourcegitcommit: 34f7d23ce3bd140dcae875b602d5719bb4363ed1
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/11/2018
ms.locfileid: "35254206"
---
# <a name="how-to-cache-data-for-use-offline-or-on-a-server"></a>Como: armazenar em Cache dados para uso offline ou em um servidor
  Você pode marcar um item de dados sejam armazenados em cache no documento, para que ele esteja disponível offline. Isso também torna possível para os dados do documento ser manipulados por outro código quando o documento é armazenado em um servidor.  
  
 [!INCLUDE[appliesto_alldoc](../vsto/includes/appliesto-alldoc-md.md)]  
  
 Você pode marcar um item de dados sejam armazenados em cache quando o item de dados é declarado em seu código, ou, se você estiver usando um <xref:System.Data.DataSet>, definindo uma propriedade de **propriedades** janela. Se você estiver armazenando em cache um item de dados que não é um <xref:System.Data.DataSet> ou <xref:System.Data.DataTable>, certifique-se de que ele atende aos critérios para serem armazenados em cache no documento. Para obter mais informações, consulte [armazenar em Cache dados](../vsto/caching-data.md).  
  
> [!NOTE]  
>  Conjuntos de dados criados usando o Visual Basic que são marcados como **em cache** e **WithEvents** (incluindo os conjuntos de dados que são arrastados do **fontes de dados** janela ou **Caixa de ferramentas** que têm o **CacheInDocument** propriedade definida como **verdadeira**) tem um sublinhado prefixado com seus nomes no cache. Por exemplo, se você cria um conjunto de dados e nomeá-lo **clientes**, o <xref:Microsoft.VisualStudio.Tools.Applications.CachedDataItem> nome será **_Customers** no cache. Quando você usa <xref:Microsoft.VisualStudio.Tools.Applications.ServerDocument> para acessar este item em cache, você deve especificar **_Customers** em vez de **clientes**.  
  
### <a name="to-cache-data-in-the-document-using-code"></a>Os dados em cache no documento usando código  
  
1.  Declarar um campo ou propriedade pública para o item de dados como um membro de uma classe de item de host em seu projeto, como o `ThisDocumen`classe t em um projeto do Word ou o `ThisWorkbook` classe em um projeto do Excel.  
  
2.  Aplicar o <xref:Microsoft.VisualStudio.Tools.Applications.Runtime.CachedAttribute> de atributo para o membro para marcar o item de dados a ser armazenado no cache de dados do documento. O exemplo a seguir se aplica a esse atributo a uma declaração de campo para um <xref:System.Data.DataSet>.  
  
     [!code-csharp[Trin_VstcoreDataExcel#11](../vsto/codesnippet/CSharp/Trin_VstcoreDataExcelCS/Sheet1.cs#11)]
     [!code-vb[Trin_VstcoreDataExcel#11](../vsto/codesnippet/VisualBasic/Trin_VstcoreDataExcelVB/Sheet1.vb#11)]  
  
3.  Adicione código para criar uma instância do item de dados e, se aplicável, carregá-los do banco de dados.  
  
     O item de dados é carregado apenas quando ele é criado pela primeira vez; Depois disso, o cache permanece com o documento e você deve escrever outro código para atualizá-lo.  
  
### <a name="to-cache-a-dataset-in-the-document-by-using-the-properties-window"></a>Para armazenar em cache um conjunto de dados do documento usando a janela de propriedades  
  
1.  Adicionar o conjunto de dados ao projeto usando as ferramentas no designer do Visual Studio, por exemplo, adicionando uma fonte de dados ao seu projeto usando o **fontes de dados** janela.  
  
2.  Crie uma instância do conjunto de dados se você tiver um e selecione a instância no designer.  
  
3.  No **propriedades** janela, defina as **CacheInDocument** propriedade a ser **verdadeiro**.  
  
     Para obter mais informações, consulte [propriedades em projetos do Office](../vsto/properties-in-office-projects.md).  
  
4.  No **propriedades** janela, defina as **modificadores** propriedade a ser **público** (por padrão, é **interno**).  
  
## <a name="see-also"></a>Consulte também  
 [Dados de cache](../vsto/caching-data.md)   
 [Como: armazenar em cache programaticamente uma fonte de dados em um documento do Office](../vsto/how-to-programmatically-cache-a-data-source-in-an-office-document.md)   
 [Como: armazenar em Cache os dados em um documento protegido por senha](../vsto/how-to-cache-data-in-a-password-protected-document.md)   
 [Acessar dados em documentos no servidor](../vsto/accessing-data-in-documents-on-the-server.md)   
 [Salvar dados](/visualstudio/data-tools/saving-data)  
  
  