---
title: Propriedades em projetos do Office
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Trust Assemblies Location property
- Cache in Document property
- properties [Office development in Visual Studio]
- Namespace for Host Item property
- Office projects [Office development in Visual Studio], properties
- projects [Office development in Visual Studio], properties
- Value2 property
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: 9369a42f1f4a8497df42f940bb8bd23453803a26
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49862145"
---
# <a name="properties-in-office-projects"></a>Propriedades em projetos do Office
  Há várias propriedades importantes que estão disponíveis para projetos do Office no Visual Studio. Essas propriedades podem ser acessadas na **propriedades** janela.  
  
 [!INCLUDE[appliesto_all](../vsto/includes/appliesto-all-md.md)]  
  
## <a name="namespace-for-host-item"></a>Namespace para item de host  
 Use o **Namespace para Item de Host** propriedade para alterar o namespace para classes de item de host (por exemplo, o `ThisAddIn`, `ThisWorkbook`, ou `ThisDocument` classes) em projetos do Visual c#. Essa propriedade é exibida na **propriedades** janela quando você seleciona o nó de documento em um projeto de nível de documento (como *ExcelWorkbook1.xlsx* ou *WordDocument1.docx* ) ou o nó de aplicativo em um projeto do suplemento do VSTO (por exemplo, Excel ou Word) no **Gerenciador de soluções**.  
  
 Quando você cria um projeto do Visual c# Office, itens de host recebem um namespace com base no nome do projeto. É recomendável que você use o **Namespace para Item de Host** arquivos de propriedade para alterar o namespace em vez de editar o código diretamente. Quando você usa essa propriedade, o namespace é alterado nos arquivos de código (oculto) gerado, bem como nos arquivos de código visíveis.  
  
## <a name="cacheindocument"></a>CacheInDocument  
 O **CacheInDocument** propriedade aparece na **propriedades** janela para projetos de nível de documento, quando você seleciona uma instância de um <xref:System.Data.DataSet> no designer do Visual Studio. Somente membros públicos podem ser armazenados em cache; Certifique-se de que o **modificadores** estiver definida como **pública** se você deseja armazenar em cache um <xref:System.Data.DataSet>.  
  
 Essa propriedade tem um valor booliano:  
  
- Selecione **verdadeira** para armazenar em cache o conjunto de dados no documento.  
  
- Selecione **falsos** se você não quiser que o conjunto de dados sejam armazenados em cache no documento.  
  
  Para obter mais informações sobre o cache de dados, consulte [armazenado em cache dados personalizações no nível do documento](../vsto/cached-data-in-document-level-customizations.md).  
  
## <a name="value2"></a>Value2  
 O **Value2** propriedade só está disponível para projetos de modelo ou a pasta de trabalho do Excel. Ele aparece sob o **Databindings** no nó da propriedade o **propriedades** janela quando você seleciona um <xref:Microsoft.Office.Tools.Excel.NamedRange> controle no designer de planilha.  
  
 Use o **Value2** propriedade no **propriedades** window para vincular a <xref:Microsoft.Office.Tools.Excel.NamedRange.Value2%2A> propriedade do <xref:Microsoft.Office.Tools.Excel.NamedRange> a um campo na fonte de dados.  
  
## <a name="see-also"></a>Consulte também  
 [Projetar e criar soluções do Office](../vsto/designing-and-creating-office-solutions.md)   
 [Visão geral de modelos de projeto do Office](../vsto/office-project-templates-overview.md)   
 [Eventos em projetos do Office](../vsto/events-in-office-projects.md)  
  
  