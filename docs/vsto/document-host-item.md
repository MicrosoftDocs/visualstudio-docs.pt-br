---
title: Item de host do documento
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- documents [Office development in Visual Studio]
- documents [Office development in Visual Studio], document host items
- document host items
- Word [Office development in Visual Studio], Word documents
- Word [Office development in Visual Studio]
- Word documents
- host items [Office development in Visual Studio], Document
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: 10dabdf0cf2db043a5df1b21f5f780645864ae8c
ms.sourcegitcommit: 1466ac0f49ebf7448ea4507ae3f79acb25d51d3e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/22/2018
ms.locfileid: "34448370"
---
# <a name="document-host-item"></a>Item de host do documento
  O <xref:Microsoft.Office.Tools.Word.Document> item de host é um tipo que estende o <xref:Microsoft.Office.Interop.Word.Document> tipo do assembly de interoperabilidade primária para o Word. O <xref:Microsoft.Office.Tools.Word.Document> item de host fornece todas as mesmas propriedades, métodos e eventos como um <xref:Microsoft.Office.Interop.Word.Document> objeto, mas ele também expõe eventos adicionais e atua como um contêiner para controles de host e controles de formulários do Windows.  
  
 [!INCLUDE[appliesto_wdalldocapp](../vsto/includes/appliesto-wdalldocapp-md.md)]  
  
 Em projetos de nível de documento, há um padrão <xref:Microsoft.Office.Tools.Word.Document> item de host que representa o documento em seu projeto. Em projetos de suplemento do VSTO, você pode gerar <xref:Microsoft.Office.Tools.Word.Document> itens de host em tempo de execução.  
  
## <a name="understand-the-document-host-item-in-document-level-projects"></a>Entender o item de host do documento em projetos no nível de documento  
 Para acessar o documento em seu projeto, use o `ThisDocument` classe. Quando você cria um projeto no nível do documento, o Visual Studio gera o `ThisDocument` classe para servir como o link de comunicação entre o Word e o código de personalização. O `ThisDocument` classe fornece acesso a membros de <xref:Microsoft.Office.Tools.Word.Document> item de host para executar tarefas básicas em sua personalização, como executar código quando o documento for aberto ou fechado. Você também pode usar a classe para adicionar controles ao documento. Combinando conjuntos diferentes de controles e escrever código, que você pode vincular os controles a dados, coletar informações do usuário e responder a ações do usuário. Para obter mais informações, consulte [programa personalizações no nível do documento](../vsto/programming-document-level-customizations.md).  
  
 O `ThisDocument` classe fornece um local no qual começar a gravar código no seu projeto. Porque a classe fornece todas as mesmas propriedades, métodos e eventos como o <xref:Microsoft.Office.Interop.Word.Document> do objeto no assembly de interoperabilidade primário para o Word, você também pode usar `ThisDocument` para acessar o modelo de objeto do Word. Para obter mais informações, consulte [visão geral de modelo de objeto do Word](../vsto/word-object-model-overview.md).  
  
### <a name="limitations-of-the-document-host-item-in-document-level-projects"></a>Limitações do item de host do documento em projetos no nível de documento  
 Um projeto no nível do documento pode conter apenas um <xref:Microsoft.Office.Tools.Word.Document> item de host (ou seja, a `ThisDocument` classe). Não é possível adicionar novos <xref:Microsoft.Office.Tools.Word.Document> itens de host para seu projeto no tempo de design, e você não pode criar novos <xref:Microsoft.Office.Tools.Word.Document> hospedar itens em tempo de execução de uma personalização no nível do documento.  
  
 Se você criar um novo documento do Word em tempo de execução, ele será do tipo <xref:Microsoft.Office.Interop.Word.Document>. Porque ele não é um item de host, ele não pode conter quaisquer controles de host ou controles de formulários do Windows. Para obter mais informações sobre a criação de documentos em tempo de execução, consulte [como: criar novos documentos programaticamente](../vsto/how-to-programmatically-create-new-documents.md).  
  
## <a name="understand-document-host-items-in-application-level-projects"></a>Entender os itens de host de documento em projetos no nível de aplicativo  
 Em projetos de suplemento do VSTO, você pode gerar um <xref:Microsoft.Office.Tools.Word.Document> item de host em tempo de execução para qualquer documento que está aberto no Word. Você pode usar o <xref:Microsoft.Office.Tools.Word.Document> item de host para adicionar controles para o documento associado ou manipular eventos que não estão disponíveis em <xref:Microsoft.Office.Interop.Word.Document> objetos.  
  
 Para gerar um <xref:Microsoft.Office.Tools.Word.Document> item de host, use o `GetVstoObject` método. Para obter mais informações, consulte [documentos de estender o Word e pastas de trabalho do Excel no suplemento do VSTO em tempo de execução](../vsto/extending-word-documents-and-excel-workbooks-in-vsto-add-ins-at-run-time.md).  
  
## <a name="see-also"></a>Consulte também  
 [Itens de host e visão geral dos controles de host](../vsto/host-items-and-host-controls-overview.md)   
 [Automatizar o Word usando objetos estendidos](../vsto/automating-word-by-using-extended-objects.md)   
 [Visão geral do modelo de objeto do Word](../vsto/word-object-model-overview.md)   
 [Limitações programáticas de itens de host e controles de host](../vsto/programmatic-limitations-of-host-items-and-host-controls.md)   
 [Estender a documentos do Word e pastas de trabalho do Excel no suplemento do VSTO em tempo de execução](../vsto/extending-word-documents-and-excel-workbooks-in-vsto-add-ins-at-run-time.md)  
  
  