---
title: Soluções do Excel
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- application-level add-ins [Office development in Visual Studio], Excel
- Excel [Office development in Visual Studio], application-level add-ins
- Office solutions [Office development in Visual Studio], Excel
- solutions [Office development in Visual Studio], Excel
- add-ins [Office development in Visual Studio], Excel
- Excel [Office development in Visual Studio], about Excel solutions
- Excel [Office development in Visual Studio]
- documents [Office development in Visual Studio], Excel
- Office documents [Office development in Visual Studio, Excel
- projects [Office development in Visual Studio], Excel
- Excel [Office development in Visual Studio], document-level customizations
- user interfaces [Office development in Visual Studio], Excel
- Office development in Visual Studio, Excel solutions
- document-level customizations [Office development in Visual Studio], Excel
- Office projects [Office development in Visual Studio], Excel
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: 917a83a434dc27074b0d786f64fcdbdc5fd294d3
ms.sourcegitcommit: 5c049194fa256b876ad303f491af11edd505756c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/07/2018
ms.locfileid: "53027387"
---
# <a name="excel-solutions"></a>Soluções do Excel
  Visual Studio fornece modelos de projeto, que você pode usar para criar personalizações em nível de documento e suplementos do VSTO para o Microsoft Office Excel. Você pode usar essas soluções para automatizar o Excel, estender os recursos do Excel e personalizar a interface de usuário (IU) do Excel. Para obter mais informações sobre as diferenças entre personalizações no nível de documento e suplementos do VSTO, consulte [visão geral de desenvolvimento de soluções do Office &#40;VSTO&#41;](../vsto/office-solutions-development-overview-vsto.md).  

 [!INCLUDE[appliesto_xlalldocapp](../vsto/includes/appliesto-xlalldocapp-md.md)]  

> [!NOTE]  
>  Interessado em desenvolver soluções que estendem a experiência do Office em toda [várias plataformas](https://dev.office.com/add-in-availability)? Confira a nova [modelo de suplementos do Office](https://dev.office.com/docs/add-ins/overview/office-add-ins). Suplementos do Office têm uma superfície pequena em comparação com soluções e suplementos do VSTO, e você pode criá-los usando quase qualquer tecnologia, como HTML5, JavaScript, CSS3 e XML de programação da web.  

 Este tópico fornece as seguintes informações:  

-   [Automatizar o Excel](#automating).  

-   [Desenvolver personalizações no nível de documento para Excel](#doclevel).  

-   [Desenvolver suplementos do VSTO para Excel](#applevel).  

-   [Personalizar a interface do usuário do Excel](#UI).  

##  <a name="automating"></a> Automatizar o Excel  
 O modelo de objeto do Excel expõe vários tipos que você pode usar para automatizar o Excel. Por exemplo, você pode programaticamente criar gráficos, formatar planilhas e defina os valores das células e intervalos. Para obter mais informações, consulte [visão geral do modelo de objeto do Excel](../vsto/excel-object-model-overview.md).  

 Ao desenvolver soluções do Excel no Visual Studio, você também pode usar *hospedar itens* e *hospedar controles* em suas soluções. Esses são objetos que estendem alguns objetos comumente usados no modelo de objeto do Excel, como o <xref:Microsoft.Office.Interop.Excel.Worksheet> e <xref:Microsoft.Office.Interop.Excel.Range> objetos. Objetos estendidos se comportam como os objetos do Excel se baseiam, mas adicionar eventos adicionais e recursos de ligação de dados para os objetos. Para obter mais informações, consulte [automatizar o Excel usando objetos estendidos](../vsto/automating-excel-by-using-extended-objects.md).  

##  <a name="doclevel"></a> Desenvolver personalizações no nível de documento para Excel  
 Uma personalização no nível de documento do Microsoft Office Excel consiste em um assembly que está associado uma pasta de trabalho específica. O assembly estende normalmente a pasta de trabalho, personalizando a interface do usuário e automatizando o Excel. Ao contrário de um suplemento VSTO, que é associado com o Excel em si, a funcionalidade que você implementa em uma personalização está disponível apenas quando a pasta de trabalho associada é aberta no Excel.  

 Para criar um projeto de personalização de nível de documento para Excel, use a pasta de trabalho do Excel ou modelos de projeto de modelo do Excel na **novo projeto** caixa de diálogo do Visual Studio. Para obter mais informações, consulte [como: projetos do Office de criar no Visual Studio](../vsto/how-to-create-office-projects-in-visual-studio.md).  

 Para obter mais informações sobre como funcionam as personalizações no nível do documento como, consulte [arquitetura de personalizações no nível do documento](../vsto/architecture-of-document-level-customizations.md).  

### <a name="excel-customization-programming-model"></a>Modelo de programação de personalização do Excel  
 Quando você cria um projeto de nível de documento para Excel, o Visual Studio gera várias classes que são a base de sua solução: `ThisWorkbook`, `Sheet1`, `Sheet2`, e `Sheet3`. Essas classes representam a pasta de trabalho e planilhas que estão associadas com sua solução, e eles fornecem um ponto de partida para escrever seu código.  

 Para obter mais informações sobre esses gerado as classes e outros recursos que você pode usar em um projeto de nível de documento, consulte [personalizações no nível de documento do programa](../vsto/programming-document-level-customizations.md).  

##  <a name="applevel"></a> Desenvolver suplementos do VSTO para Excel  
 Um suplemento do VSTO para o Microsoft Office Excel consiste em um assembly que é carregado pelo Excel. O assembly estende o Excel normalmente, personalizando a interface do usuário e automatizando o Excel. Ao contrário de uma personalização no nível de documento, que está associada uma pasta de trabalho específica, a funcionalidade que você implementa em um suplemento do VSTO não está restrita a única pasta de trabalho.  

 Para criar um projeto de suplemento do VSTO para Excel, use a pasta de trabalho do Excel ou modelos de projeto de modelo do Excel na **novo projeto** caixa de diálogo do Visual Studio. Para obter mais informações, consulte [como: projetos do Office de criar no Visual Studio](../vsto/how-to-create-office-projects-in-visual-studio.md).  

 Para obter informações gerais sobre o funcionamento do VSTO Add-ins, consulte [arquitetura do VSTO Add-ins](../vsto/architecture-of-vsto-add-ins.md).

### <a name="excel-add-in-programming-model"></a>Excel Add-in do modelo de programação  
 Quando você cria um projeto de suplemento do VSTO do Excel, o Visual Studio gera uma classe, chamada `ThisAddIn`, que é a base da sua solução. Essa classe fornece um ponto de partida para escrever seu código, e ele também expõe o modelo de objeto do Excel para o suplemento do VSTO.  

 Para obter mais informações sobre o `ThisAddIn` classe e outros recursos do Visual Studio você pode usar em um suplemento VSTO, consulte [programa de suplementos do VSTO](../vsto/programming-vsto-add-ins.md).  

##  <a name="UI"></a> Personalizar a interface do usuário do Excel  
 Há várias maneiras diferentes de personalizar a interface do usuário do Excel. Algumas opções estão disponíveis a todos os tipos de projeto e outras opções estão disponíveis somente para personalizações no nível do documento ou de suplementos do VSTO.  

### <a name="options-for-all-project-types"></a>Opções para todos os tipos de projeto  
 A tabela a seguir lista as opções de personalização que estão disponíveis para personalizações no nível de documento e suplementos do VSTO.  

|Tarefa|Para obter mais informações|  
|----------|--------------------------|  
|Personalize a faixa de opções.|[Visão geral da faixa de opções](../vsto/ribbon-overview.md)|  
|Adicione controles dos Windows Forms ou controles estendidos do Excel em uma planilha na pasta de trabalho personalizada para uma personalização no nível de documento, ou em qualquer pasta de trabalho para um suplemento do VSTO.|[Como: adicionar controles dos Windows forms a documentos do Office](../vsto/how-to-add-windows-forms-controls-to-office-documents.md)<br /><br /> [Como: adicionar controles Chart a planilhas](../vsto/how-to-add-chart-controls-to-worksheets.md)<br /><br /> [Como: adicionar controles ListObject a planilhas](../vsto/how-to-add-listobject-controls-to-worksheets.md)<br /><br /> [Como: adicionar controles NamedRange a planilhas](../vsto/how-to-add-namedrange-controls-to-worksheets.md)|  

### <a name="options-for-document-level-customizations"></a>Opções para personalizações no nível do documento  
 A tabela a seguir lista as opções de personalização que ficam disponíveis somente para personalizações no nível do documento.  

|Tarefa|Para obter mais informações|  
|----------|--------------------------|  
|Adicione um painel de ações para a pasta de trabalho.|[Visão geral do painel de ações](../vsto/actions-pane-overview.md)<br /><br /> [Como: adicionar um painel de ações a documentos do Word ou pastas de trabalho do Excel](../vsto/how-to-add-an-actions-pane-to-word-documents-or-excel-workbooks.md)|  
|Adicione controles de intervalo estendido que são mapeados para nós XML para uma planilha.|[Como: adicionar controles XMLMappedRange a planilhas](../vsto/how-to-add-xmlmappedrange-controls-to-worksheets.md)|  

### <a name="options-for-vsto-add-ins"></a>Opções para suplementos VSTO  
 A tabela a seguir lista as opções de personalização que ficam disponíveis somente para suplementos do VSTO.  

|Tarefa|Para obter mais informações|  
|----------|--------------------------|  
|Crie um painel de tarefas personalizado.|[Painéis de tarefas personalizados](../vsto/custom-task-panes.md)|  

### <a name="related-topics"></a>Tópicos relacionados  

| Título | Descrição |
| - | - |
| [Visão geral do modelo de objeto do Excel](../vsto/excel-object-model-overview.md) | Fornece uma visão geral dos principais tipos fornecidos pelo modelo de objeto do Excel. |
| [Automatizar o Excel usando objetos estendidos](../vsto/automating-excel-by-using-extended-objects.md) | Fornece informações sobre os objetos estendidos (fornecidos pelo [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)]) que você pode usar em soluções do Excel. |
| [Globalização e localização de soluções do Excel](../vsto/globalization-and-localization-of-excel-solutions.md) | Contém informações sobre considerações especiais para soluções do Excel que serão executadas em computadores que têm configurações diferentes do inglês para Windows. |
| [Controles de formulários do Windows na visão geral de documentos do Office](../vsto/windows-forms-controls-on-office-documents-overview.md) | Descreve como você pode adicionar controles dos Windows Forms a planilhas do Excel. |
| [Passo a passo: Criar a primeira personalização no nível de documento para Excel](../vsto/walkthrough-creating-your-first-document-level-customization-for-excel.md) | Demonstra como criar uma personalização básica de nível de documento para Excel. |
| [Passo a passo: Criar seu primeiro suplemento VSTO para Excel](../vsto/walkthrough-creating-your-first-vsto-add-in-for-excel.md) | Demonstra como criar um básico suplemento VSTO para Excel. |
| [Passo a passo: Adicionar controles a uma planilha em tempo de execução no projeto do suplemento do VSTO](../vsto/walkthrough-adding-controls-to-a-worksheet-at-run-time-in-vsto-add-in-project.md) | Demonstra como adicionar um botão dos Windows Forms, um <xref:Microsoft.Office.Tools.Excel.NamedRange>e um <xref:Microsoft.Office.Tools.Excel.ListObject> para uma planilha em tempo de execução usando um suplemento do VSTO. |
| [Entender a coautoria e suplementos](./understanding-coauthoring-and-addins.md) | Descreve os ajustes que talvez você precise fazer suas soluções para acomodar a coautoria. |
| [Excel 2010 no desenvolvimento do Office](http://go.microsoft.com/fwlink/?LinkId=199011) | Fornece links para artigos e documentação de referência sobre como desenvolver soluções do Excel. Esses não são específicas para desenvolvimento do Office usando o Visual Studio. |

