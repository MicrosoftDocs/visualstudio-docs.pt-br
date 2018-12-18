---
title: Alterações no design dos projetos do Office destinados ao .NET Framework
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Office development in Visual Studio, what's new
- what's new [Office development in Visual Studio]
author: John-Hart
ms.author: johnhart
manager: douge
ms.workload:
- office
ms.openlocfilehash: b200c5b0df5f150e0d34b351a3e36a8a986f3ed6
ms.sourcegitcommit: 20c0991d737c540750c613c380cd4cf5bb07de51
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/11/2018
ms.locfileid: "53248238"
---
# <a name="changes-to-the-design-of-office-projects-that-target-the-net-framework-4-or-the-net-framework-45"></a>Alterações no design dos projetos do Office destinados ao .NET Framework 4 ou o .NET Framework 4.5
  A partir [!INCLUDE[vs_dev10_long](../sharepoint/includes/vs-dev10-long-md.md)], o Visual Studio introduziu algumas alterações no design dos projetos do Office que se destinam a [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] ou posterior. Se você estiver familiarizado com projetos do Office em versões anteriores do Visual Studio, você deve estar atento essas alterações antes de desenvolver projetos do Office que se destinam a essas versões do .NET Framework 4.0 ou posterior. Por padrão, todos os projetos que você cria usando o Visual Studio 2013 ou posterior direcionam o .NET Framework 4.0 ou posterior.  
  
 As seções a seguir descrevem essas alterações de design de projeto do Office.  
  
## <a name="understand-the-interface-based-design-of-the-visual-studio-2010-tools-for-office-runtime"></a>Entender o design baseado em interface do Visual Studio 2010 Tools para Office runtime  
 Quando você desenvolve um projeto do Office que tem como alvo o [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] ou posterior, a maioria dos tipos que você usar no Visual Studio 2010 Tools para Office runtime é interfaces. Isso é uma alteração importante de versões anteriores do [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)], onde esses tipos são classes. Por exemplo, quando você seleciona os [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] ou posterior, o <xref:Microsoft.Office.Tools.Excel.Worksheet> e <xref:Microsoft.Office.Tools.Word.Document> tipos são interfaces em vez de classes. Para obter mais informações, consulte [Visual Studio Tools for Office runtime overview](../vsto/visual-studio-tools-for-office-runtime-overview.md).  
  
 Para todos os tipos que você pode instanciar diretamente nas versões anteriores dos [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)], você usa métodos do `Globals.Factory` objeto para obter instâncias desses tipos. Por exemplo, para obter um objeto que implemente a interface <xref:Microsoft.Office.Tools.Excel.SmartTag>, use o método `Globals.Factory.CreateSmartTag`. Para mais informações, consulte os seguintes tópicos:  
  
-   [Atualizar projetos do Excel e Word migrados para o .NET Framework 4 ou o .NET Framework 4.5](../vsto/updating-excel-and-word-projects-that-you-migrate-to-the-dotnet-framework-4-or-the-dotnet-framework-4-5.md)  
  
-   [Atualizar personalizações da faixa de opções em projetos do Office que você migrar para o .NET Framework 4 ou o .NET Framework 4.5](../vsto/updating-ribbon-customizations-in-office-projects-that-you-migrate-to-the-dotnet-framework-4-or-the-dotnet-framework-4-5.md)  
  
-   [Atualizar as regiões do formulário em projetos do Outlook que você migrar para o .NET Framework 4 ou o .NET Framework 4.5](../vsto/updating-form-regions-in-outlook-projects-that-you-migrate-to-the-dotnet-framework-4-or-the-dotnet-framework-4-5.md)  
  
### <a name="new-base-classes-in-office-projects"></a>Novas classes base em projetos do Office  
 O novo design baseado em interface do Visual Studio 2010 Tools para Office runtime afeta as classes geradas em projetos do Office, como `ThisDocument`, `ThisWorkbook`, e `ThisAddIn`. Em projetos do Office destinados ao .NET Framework 3.5 e versões anteriores do framework, essas classes geradas derivam de classes de [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] , como `Microsoft.Office.Tools.Word.Document`, `Microsoft.Office.Tools.Excel.Worksheet`, e `Microsoft.Office.Tools.AddIn`. Em projetos que se destinam a [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] ou posterior, eles [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] classes agora são interfaces. Portanto as classes geradas em projetos do Office não podem derivar sua implementação deles. Em vez disso, as classes geradas derivam novas classes base, como <xref:Microsoft.Office.Tools.Word.DocumentBase>, <xref:Microsoft.Office.Tools.Excel.WorksheetBase>, e <xref:Microsoft.Office.Tools.AddInBase>. Para obter mais informações, consulte [programa VSTO Add-ins](../vsto/programming-vsto-add-ins.md) e [personalizações no nível de documento do programa](../vsto/programming-document-level-customizations.md).  
  
 As classes base não são parte do [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] redistribuível. Em vez disso, eles são definidos em assemblies de utilitários que são incluídos com o Visual Studio. Esses assemblies são copiados para a pasta de saída quando você compila projetos do Office e deve ser implantado com sua solução. Para obter mais informações sobre os assemblies de utilitários, consulte [Assemblies no Visual Studio Tools para Office runtime](../vsto/assemblies-in-the-visual-studio-tools-for-office-runtime.md).  
  
## <a name="breaking-changes-in-office-projects-that-are-retargeted-to-the-net-framework-4"></a>Alterações significativas nos projetos do Office que são redirecionados para o .NET Framework 4  
 A tabela a seguir lista as alterações de quebra principal que você pode encontrar nos projetos do Office que são redirecionados para o [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] ou posterior. Para obter mais detalhes, consulte [soluções do Office de migrar para o .NET Framework 4 ou posterior](../vsto/migrating-office-solutions-to-the-dotnet-framework-4-or-later.md).  
  
|Alteração significativa|Consequência|  
|---------------------|-----------------|  
|O <xref:System.Security.SecurityTransparentAttribute> não é usado ou tem suporte em projetos do Office.|Você deve remover esse atributo do arquivo de código AssemblyInfo em projetos do Office que você atualizar do Visual Studio 2008. Para obter mais informações, consulte [exigiu alterações para executar projetos do Office migrados para o .NET Framework 4 ou o .NET Framework 4.5](../vsto/required-changes-to-run-office-projects-that-you-migrate-to-the-dotnet-framework-4-or-the-dotnet-framework-4-5.md).|  
|O **ExcelLocale1033Attribute** não é usado ou tem suporte em projetos do Excel.|Você deve remover esse atributo do *AssemblyInfo* arquivo de código em projetos do Excel. Para obter mais informações, consulte [atualização do Excel e Word projetos que você migrar para o .NET Framework 4 ou o .NET Framework 4.5](../vsto/updating-excel-and-word-projects-that-you-migrate-to-the-dotnet-framework-4-or-the-dotnet-framework-4-5.md).|  
|O modelo de programação do **faixa de opções (Visual Designer)** itens de projeto foi alterado.|Você deve modificar o arquivo code-behind para todos os itens da faixa de opções em seu projeto. Você também deve modificar qualquer código que cria uma instância de controles da faixa de opções em tempo de execução, manipula os eventos da faixa de opções ou define a posição de um componente de faixa de opções por meio de programação. Para obter mais informações, consulte [personalizações da faixa de opções de atualização em projetos do Office que você migrar para o .NET Framework 4 ou o .NET Framework 4.5](../vsto/updating-ribbon-customizations-in-office-projects-that-you-migrate-to-the-dotnet-framework-4-or-the-dotnet-framework-4-5.md).|  
|O modelo de programação de regiões de formulário do Outlook foi alterado.|Você deve modificar o arquivo code-behind para quaisquer regiões de formulário em seu projeto e qualquer código que cria uma instância de determinadas classes de região de formulário em tempo de execução. Para obter mais informações, consulte [atualizar regiões de formulário em projetos do Outlook que você migrar para o .NET Framework 4 ou o .NET Framework 4.5](../vsto/updating-form-regions-in-outlook-projects-that-you-migrate-to-the-dotnet-framework-4-or-the-dotnet-framework-4-5.md).|  
|O modelo de programação de marcas inteligentes em projetos do Excel e Word foi alterado. As marcas inteligentes foram preteridas no [!INCLUDE[Excel_14_short](../vsto/includes/excel-14-short-md.md)] e [!INCLUDE[Word_14_short](../vsto/includes/word-14-short-md.md)].|Se sua solução usar marcas inteligentes, ocorrerão erros quando você compila o projeto. Como as marcas inteligentes foram preteridas no [!INCLUDE[Excel_14_short](../vsto/includes/excel-14-short-md.md)] e [!INCLUDE[Word_14_short](../vsto/includes/word-14-short-md.md)], você deve remover as marcas, antes de testar e depurar a solução em [!INCLUDE[vs_dev12](../vsto/includes/vs-dev12-md.md)] ou posterior.|  
|A sintaxe do `GetVstoObject` e `HasVstoObject` métodos foi alterado|Você deve passar o `Globals.Factory` objeto para esses métodos quando você acessá-los em objetos nativos de assemblies de interoperabilidade primários (PIAs), ou você pode acessar esses métodos no objeto que é retornado pelo `Globals.Factory` propriedade em seu projeto. Para obter mais informações, consulte [atualização do Excel e Word projetos que você migrar para o .NET Framework 4 ou o .NET Framework 4.5](../vsto/updating-excel-and-word-projects-that-you-migrate-to-the-dotnet-framework-4-or-the-dotnet-framework-4-5.md).|  
|Os eventos de controles de conteúdo do Word são associados a novos delegados.|Você deve modificar qualquer código que manipula os eventos de controles de conteúdo do Word para especificar os delegados de novo. Para obter mais informações, consulte [atualização do Excel e Word projetos que você migrar para o .NET Framework 4 ou o .NET Framework 4.5](../vsto/updating-excel-and-word-projects-that-you-migrate-to-the-dotnet-framework-4-or-the-dotnet-framework-4-5.md).|  
|O `OLEObject` e `OLEControl` classes foram renomeadas.|Você deve modificar qualquer código que usa as instâncias dessas classes para usar <xref:Microsoft.Office.Tools.Excel.ControlSite> ou <xref:Microsoft.Office.Tools.Word.ControlSite> objetos em vez disso. Para obter mais informações, consulte [atualização do Excel e Word projetos que você migrar para o .NET Framework 4 ou o .NET Framework 4.5](../vsto/updating-excel-and-word-projects-that-you-migrate-to-the-dotnet-framework-4-or-the-dotnet-framework-4-5.md).|  
|Classes de item de host, como `ThisWorkbook`, `Sheet` *n*, `ThisDocument`, e `ThisAddIn`, não mais fornecem um `Dispose` método que pode ser substituído.|Você deve mover qualquer código na `Dispose` método de substituição para o `Shutdown` manipulador de eventos na classe de item host, por exemplo, `ThisAddIn_Shutdown`e remover o `Dispose` método substituir da sua classe de item de host.|  
  
## <a name="see-also"></a>Consulte também  
 [Migrar soluções do Office para o .NET Framework 4 ou posterior](../vsto/migrating-office-solutions-to-the-dotnet-framework-4-or-later.md)   
 [O que há de novo no desenvolvimento do Office](https://msdn.microsoft.com/library/bf054af2-c896-4723-aa15-6381145b14bb)   
 [Visual Studio Tools for Office runtime overview](../vsto/visual-studio-tools-for-office-runtime-overview.md)  
  
  