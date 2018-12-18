---
title: Assemblies no Visual Studio Tools para Office runtime
titleSuffix: ''
ms.custom: ''
ms.date: 02/02/2017
ms.technology: office-development
ms.prod: visual-studio-dev15
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Visual Studio Tools for Office runtime, assemblies
author: John-Hart
ms.author: johnhart
manager: douge
ms.workload:
- office
ms.openlocfilehash: 66ee95d4f102ac4206a9ed55a1fc97fc251c4f9c
ms.sourcegitcommit: 20c0991d737c540750c613c380cd4cf5bb07de51
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/11/2018
ms.locfileid: "53248105"
---
# <a name="assemblies-in-the-visual-studio-tools-for-office-runtime"></a>Assemblies no Visual Studio Tools para Office runtime
  Quando você cria um projeto do Office, o Visual Studio adiciona automaticamente referências para o [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] assemblies que são usados para o tipo de projeto e o destino do .NET Framework do projeto. Há diferentes assemblies nas extensões do Office para o .NET Framework 3.5 [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)], e [!INCLUDE[net_v45](../vsto/includes/net-v45-md.md)]. Para obter mais informações sobre as extensões do Office, consulte [Visual Studio Tools for Office runtime overview](../vsto/visual-studio-tools-for-office-runtime-overview.md).  
  
## <a name="assemblies-in-the-office-extensions-for-the-net-framework-4-and-the-includenetv45vstoincludesnet-v45-mdmd"></a>Assemblies nas extensões do Office para o .NET Framework 4 e o [!INCLUDE[net_v45](../vsto/includes/net-v45-md.md)]  
 A tabela a seguir lista os módulos que estão incluídos nas extensões do Office para o [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] e o [!INCLUDE[net_v45](../vsto/includes/net-v45-md.md)]. Para obter documentação sobre os tipos esses assemblies e namespaces, consulte [referência gerenciada do &#40;desenvolvimento do Office no Visual Studio&#41;](../vsto/managed-reference-office-development-in-visual-studio.md).  
  
|Nome do assembly|Descrição|  
|-------------------|-----------------|  
|Microsoft.Office.Tools.Common.dll|Fornece os seguintes tipos:<br /><br /> -Tipos para a criação de marcas inteligentes e personalizações da faixa de opções. **Observação:**      As marcas inteligentes foram preteridas no [!INCLUDE[Excel_14_short](../vsto/includes/excel-14-short-md.md)] e [!INCLUDE[Word_14_short](../vsto/includes/word-14-short-md.md)].<br />-Tipos para a criação de painéis de ações em personalizações no nível de documento e painéis de tarefas personalizados no VSTO Add-Ins.|  
|Microsoft.Office.Tools.Excel.dll|Fornece interfaces que representam itens de host e controles de host para projetos do Excel e tipos de suporte. Para obter mais informações, consulte [automatizar o Excel usando objetos estendidos](../vsto/automating-excel-by-using-extended-objects.md).|  
|Microsoft.Office.Tools.Outlook.dll|Fornece tipos que você pode usar para criar regiões de formulário personalizadas nos suplementos do VSTO do Outlook.|  
|Microsoft.Office.Tools.Word.dll|Fornece interfaces que representam itens de host e controles de host para projetos do Word e tipos de suporte. Para obter mais informações, consulte [automatizar o Word usando objetos estendidos](../vsto/automating-word-by-using-extended-objects.md).|  
|Microsoft.Office.Tools.v4.0.Framework.dll|Fornece os seguintes tipos:<br /><br /> -As exceções que podem ser lançadas pelo Visual Studio Tools for Office runtime.<br />-Você pode usar ao criar o Outlook atributos regiões do formulário.|  
|Microsoft.Office.Tools.dll|Fornece tipos que fazem parte do Visual Studio Tools para infraestrutura de tempo de execução do Office e não se destina a ser usado diretamente do seu código.|  
|Microsoft.VisualStudio.Tools.Applications.Runtime.dll|Fornece os seguintes tipos:<br /><br /> -A <xref:Microsoft.VisualStudio.Tools.Applications.Runtime.CachedAttribute> atributo e <xref:Microsoft.VisualStudio.Tools.Applications.Runtime.ICachedType> interface, que você pode usar para objetos de cache de dados em uma personalização no nível de documento. Para obter mais informações, consulte [armazenar em Cache dados](../vsto/caching-data.md).<br />-O <xref:Microsoft.VisualStudio.Tools.Applications.Deployment.IAddInPostDeploymentAction> interface, que você pode implementar para executar etapas de instalação adicionais como a etapa final do instalador do ClickOnce para uma solução do Office. Para obter mais informações, consulte [implantar uma solução do Office usando o ClickOnce](../vsto/deploying-an-office-solution-by-using-clickonce.md).<br />-As exceções que podem ser lançadas pelo Visual Studio Tools for Office runtime.<br />-Outros tipos que fazem parte do Visual Studio Tools para infraestrutura de tempo de execução do Office e não se destina a ser usado diretamente do seu código.|  
|Microsoft.VisualStudio.Tools.Applications.ServerDocument.dll|Fornece os seguintes tipos:<br /><br /> -A <xref:Microsoft.VisualStudio.Tools.Applications.ServerDocument> classe, que você pode usar para anexar os assemblies de personalização a documentos e acessar os dados armazenados em cache em documentos. Para obter mais informações, consulte [gerenciar documentos em um servidor usando a classe ServerDocument](../vsto/managing-documents-on-a-server-by-using-the-serverdocument-class.md).<br />-Várias classes que representam a hierarquia dos dados em uma personalização no nível de documento armazenados em cache. Para obter mais informações, consulte [acessar dados em documentos no servidor](../vsto/accessing-data-in-documents-on-the-server.md).|  
  
 Projetos que se destinam a [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] ou o [!INCLUDE[net_v45](../vsto/includes/net-v45-md.md)] também os seguintes assemblies de referência. Esses assemblies não são parte do [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] redistribuível. Em vez disso, eles são assemblies dependentes que devem ser implantados com sua solução. Por padrão, eles são copiados para a pasta de saída de compilação para seu projeto (o **Copy Local** propriedade para esses assemblies são definidos como **verdadeiro**). Se você implantar seu projeto usando o ClickOnce, esses assemblies são incluídos no pacote gerado.  
  
|Nome do assembly|Descrição|  
|-------------------|-----------------|  
|Microsoft.Office.Tools.Common.v4.0.Utilities.dll|Fornece as classes base para a geração `ThisAddIn` classe na classe Ribbon gerada em todos os projetos e de projetos de suplemento do VSTO.|  
|Microsoft.Office.Tools.Excel.v4.0.Utilities.dll|Fornece os seguintes tipos:<br /><br /> -Classes para a geração de base `ThisWorkbook` e `Sheet` classes no nível de documento projetos para Excel.<br />-Controles de formulários do Windows que você pode usar em planilhas em projetos do Excel.|  
|Microsoft.Office.Tools.Outlook.v4.0.Utilities.dll|Fornece classes base para a geração `ThisAddIn` e classes de região de formulário em projetos do Outlook.|  
|Microsoft.Office.Tools.Word.v4.0.Utilities.dll|Fornece os seguintes tipos:<br /><br /> -Classes para a geração de base `ThisDocument` classe nos projetos em nível de documento para Word.<br />-Controles de formulários do Windows que podem ser usados em documentos em projetos do Word.|  
  
## <a name="assemblies-in-the-office-extensions-for-the-net-framework-35"></a>Assemblies nas extensões do Office para o .NET Framework 3.5  
 A tabela a seguir lista os assemblies que estão incluídos nas extensões do Office para o .NET Framework 3.5. Para obter a documentação sobre os namespaces e classes nesses assemblies, consulte a seguinte seção de referência na documentação do Visual Studio 2008: [ http://go.microsoft.com/fwlink/?LinkId=160658 ](http://go.microsoft.com/fwlink/?LinkId=160658).  
  
|Nome do assembly|Descrição|  
|-------------------|-----------------|  
|Microsoft.Office.Tools.Common.v9.0.dll|Fornece os seguintes tipos:<br /><br /> -A classe base Microsoft.Office.Tools.AddIn para suplementos do VSTO.<br />-Classes para criar personalizações da faixa de opções e marcas inteligentes. **Observação:**      As marcas inteligentes foram preteridas no [!INCLUDE[Excel_14_short](../vsto/includes/excel-14-short-md.md)] e [!INCLUDE[Word_14_short](../vsto/includes/word-14-short-md.md)].<br />-Classes para criar painéis de ações em personalizações no nível de documento e painéis de tarefas personalizados nos suplementos do VSTO.|  
|Microsoft.Office.Tools.Excel.v9.0.dll|Fornece os itens de host e controles de host para soluções do Excel. Para obter mais informações, consulte [automatizar o Excel usando objetos estendidos](../vsto/automating-excel-by-using-extended-objects.md).|  
|Microsoft.Office.Tools.Outlook.v9.0.dll|Fornece classes que você pode usar para criar regiões de formulário personalizadas nos suplementos do VSTO do Outlook.|  
|Microsoft.Office.Tools.Word.v9.0.dll|Fornece os itens de host e controles de host para soluções do Word. Para obter mais informações, consulte [automatizar o Word usando objetos estendidos](../vsto/automating-word-by-using-extended-objects.md).|  
|Microsoft.Office.Tools.v9.0.dll|Fornece os seguintes tipos:<br /><br /> -A [RemoteBindableComponent](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2008/bb546360(v=vs.90)) classe, que fornece os recursos de associação de dados para hospedar controles em nível de documento personalizações.<br />-Outros tipos que fazem parte do Visual Studio Tools para infraestrutura de tempo de execução do Office e não se destina a ser usado diretamente do seu código.|  
|Microsoft.VisualStudio.Tools.Applications.Runtime.v9.0.dll|Fornece os seguintes tipos:<br /><br /> -A <xref:Microsoft.VisualStudio.Tools.Applications.Runtime.CachedAttribute> atributo e <xref:Microsoft.VisualStudio.Tools.Applications.Runtime.ICachedType> interface, que você pode usar para objetos de cache de dados em uma personalização no nível de documento. Para obter mais informações, consulte [armazenar em Cache dados](../vsto/caching-data.md).<br />-As exceções que podem ser lançadas pelo Visual Studio Tools for Office runtime.<br />-Outros tipos que fazem parte do Visual Studio Tools para infraestrutura de tempo de execução do Office e não se destina a ser usado diretamente do seu código.|  
|Microsoft.VisualStudio.Tools.Applications.Runtime.v10.0.dll|Fornece o <xref:Microsoft.VisualStudio.Tools.Applications.Deployment.IAddInPostDeploymentAction> interface, que você pode implementar para executar etapas de instalação adicionais como a etapa final do instalador do ClickOnce para uma solução do Office. Para obter mais informações, consulte [implantação de solução do Office avançada](/previous-versions/visualstudio/visual-studio-2010/dd234217(v=vs.100)).|  
|Microsoft.VisualStudio.Tools.Applications.ServerDocument.v10.0.dll|Fornece os seguintes tipos:<br /><br /> -A <xref:Microsoft.VisualStudio.Tools.Applications.ServerDocument> classe, que você pode usar para anexar programaticamente os assemblies de personalização a documentos e acessar os dados armazenados em cache em documentos. Para obter mais informações, consulte [gerenciar documentos em um servidor usando a classe ServerDocument](../vsto/managing-documents-on-a-server-by-using-the-serverdocument-class.md).<br />-Várias classes que representam a hierarquia dos dados em uma personalização no nível de documento armazenados em cache. Para obter mais informações, consulte [acessar dados em documentos no servidor](../vsto/accessing-data-in-documents-on-the-server.md).|  
|Microsoft.VisualStudio.Tools.Office.Runtime.v10.0.dll|Fornece os seguintes tipos:<br /><br /> -As classes Microsoft.VisualStudio.Tools.Office.Runtime.Security.AddInSecurityEntry e Microsoft.VisualStudio.Tools.Office.Runtime.Security.UserInclusionList, que você pode usar para criar entradas de lista para conceder confiança ao escritório de inclusão de usuário soluções que direcionam o .NET Framework 3.5.<br />-Outros tipos que fazem parte do Visual Studio Tools para infraestrutura de tempo de execução do Office e não se destina a ser usado diretamente do seu código.|  
  
## <a name="see-also"></a>Consulte também  
 [Visual Studio Tools for Office runtime overview](../vsto/visual-studio-tools-for-office-runtime-overview.md)   
 [Ferramentas do Visual Studio para cenários de instalação de tempo de execução do Office](../vsto/visual-studio-tools-for-office-runtime-installation-scenarios.md)  
  
  