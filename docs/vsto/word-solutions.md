---
title: Soluções do Word
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- solutions [Office development in Visual Studio], Word
- Office projects [Office development in Visual Studio], Word
- application-level add-ins [Office development in Visual Studio], Word
- Word [Office development in Visual Studio]
- projects [Office development in Visual Studio], Word
- Word [Office development in Visual Studio], about Word solutions
- Office solutions [Office development in Visual Studio], Word
- Word [Office development in Visual Studio], application-level add-ins
- documents [Office development in Visual Studio], Word
- Office development in Visual Studio, Word solutions
- add-ins [Office development in Visual Studio], Word
- Word [Office development in Visual Studio], document-level customizations
- user interfaces [Office development in Visual Studio], Word
- Office documents [Office development in Visual Studio, Word
- document-level customizations [Office development in Visual Studio], Word
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: 2b443cd985910cbb6e81ce79016193623bdeb2dd
ms.sourcegitcommit: 6944ceb7193d410a2a913ecee6f40c6e87e8a54b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/06/2018
ms.locfileid: "35669952"
---
# <a name="word-solutions"></a>Soluções do Word
  Visual Studio fornece modelos de projeto, que você pode usar para criar personalizações em nível de documento e suplementos do VSTO para o Microsoft Office Word. Você pode usar essas soluções para automatizar o Word, estender os recursos do Word e personalizar a interface do usuário do Word (UI). Para obter mais informações sobre as diferenças entre personalizações no nível de documento e suplementos do VSTO, consulte [visão geral de desenvolvimento de soluções do Office &#40;VSTO&#41;](../vsto/office-solutions-development-overview-vsto.md).  
  
 [!INCLUDE[appliesto_wdalldocapp](../vsto/includes/appliesto-wdalldocapp-md.md)]  
  
> [!NOTE]  
>  Interessado em desenvolver soluções que estendem a experiência do Office em toda [várias plataformas](https://dev.office.com/add-in-availability)? Confira a nova [modelo de suplementos do Office](https://dev.office.com/docs/add-ins/overview/office-add-ins). Suplementos do Office têm uma superfície pequena em comparação com soluções e suplementos do VSTO, e você pode criá-los usando quase qualquer tecnologia, como HTML5, JavaScript, CSS3 e XML de programação da web.  
  
 Este tópico fornece as seguintes informações:  
  
-   [Automatizar o Word](#automating).  
  
-   [Desenvolver personalizações no nível de documento para Word](#doclevel).  
  
-   [Desenvolver suplementos do VSTO para Word](#applevel).  
  
-   [Personalizar a interface do usuário do Word](#UI).  
  
##  <a name="automating"></a> Automatizar o Word  
 O modelo de objeto do Word expõe vários tipos que você pode usar para automatizar o Word. Por exemplo, você pode programaticamente criar tabelas, documentos de formato e definir o texto em intervalos e os parágrafos. Para obter mais informações, consulte [visão geral do modelo de objeto Word](../vsto/word-object-model-overview.md).  
  
 Ao desenvolver soluções do Word no Visual Studio, você também pode usar *hospedar itens* e *hospedar controles* em suas soluções. Esses são objetos que estendem alguns objetos comumente usados no modelo de objeto do Word, como o <xref:Microsoft.Office.Interop.Word.Document> e <xref:Microsoft.Office.Interop.Word.ContentControl> objetos. Objetos estendidos se comportam como os objetos do Word se baseiam, mas adicionar eventos adicionais e recursos de ligação de dados para os objetos. Para obter mais informações, consulte [automatizar o Word usando objetos estendidos](../vsto/automating-word-by-using-extended-objects.md).  
  
##  <a name="doclevel"></a> Desenvolver personalizações no nível de documento para Word  
 Uma personalização no nível de documento para o Microsoft Office Word consiste em um assembly que está associado um documento específico. O assembly estende o documento normalmente, personalizando a interface do usuário e automatizando o Word. Ao contrário de um suplemento VSTO, que é associado com a palavra propriamente dita, funcionalidade que você implementa em uma personalização está disponível somente quando o documento associado é aberto no Word.  
  
 Para criar um projeto de personalização de nível de documento para Word, use os modelos de projeto de documento do Word ou o modelo do Word na **novo projeto** caixa de diálogo do Visual Studio. Para obter mais informações, consulte [como: projetos do Office de criar no Visual Studio](../vsto/how-to-create-office-projects-in-visual-studio.md).  
  
 Para obter mais informações sobre como funcionam as personalizações no nível do documento como, [arquitetura de personalizações no nível do documento](../vsto/architecture-of-document-level-customizations.md).  
  
### <a name="word-customization-programming-model"></a>Personalização do modelo de programação do Word  
 Quando você cria um projeto de nível de documento para Word, o Visual Studio gera uma classe, chamada `ThisDocument`, que é a base da sua solução. Essa classe representa o documento que está associado com sua solução e fornece um ponto de partida para escrever seu código.  
  
 Para obter mais informações sobre o `ThisDocument` classe e outros recursos que você pode usar em um projeto de nível de documento, consulte [personalizações no nível de documento do programa](../vsto/programming-document-level-customizations.md).  
  
##  <a name="applevel"></a> Desenvolver suplementos do VSTO para Word  
 Um suplemento do VSTO para o Microsoft Office Word consiste em um assembly que é carregado pelo Word. O assembly estende o Word normalmente, personalizando a interface do usuário e automatizando o Word. Ao contrário de uma personalização no nível de documento, que está associada um documento específico, a funcionalidade que você implementa em um suplemento do VSTO não está restrita a nenhum documento.  
  
 Para criar um projeto de suplemento do VSTO para Word, use os modelos de projeto do suplemento do Word na **novo projeto** caixa de diálogo do Visual Studio. Para obter mais informações, consulte [como: projetos do Office de criar no Visual Studio](../vsto/how-to-create-office-projects-in-visual-studio.md).  
  
 Para obter informações gerais sobre o funcionamento do VSTO Add-ins, consulte [arquitetura do VSTO Add-ins](../vsto/architecture-of-vsto-add-ins.md).  
  
### <a name="word-add-in-programming-model"></a>Word Add-in do modelo de programação  
 Quando você cria um projeto de suplemento do VSTO do Word, o Visual Studio gera uma classe, chamada `ThisAddIn`, que é a base da sua solução. Essa classe fornece um ponto de partida para escrever seu código, e ele também expõe o modelo de objeto do Word para seu suplemento do VSTO.  
  
 Para obter mais informações sobre o `ThisAddIn` classe e outros recursos que você pode usar em um suplemento VSTO, consulte [suplementos do VSTO do programa](../vsto/programming-vsto-add-ins.md).  
  
##  <a name="UI"></a> Personalizar a interface do usuário do Word  
 Há várias maneiras diferentes de personalizar a interface do usuário do Word. Algumas opções estão disponíveis a todos os tipos de projeto e outras opções estão disponíveis somente para personalizações no nível do documento ou de suplementos do VSTO.  
  
### <a name="options-for-all-project-types"></a>Opções para todos os tipos de projeto  
 A tabela a seguir lista as opções de personalização que estão disponíveis para personalizações no nível de documento e suplementos do VSTO.  
  
|Tarefa|Para obter mais informações|  
|----------|--------------------------|  
|Personalize a faixa de opções.|[Visão geral da faixa de opções](../vsto/ribbon-overview.md)|  
|Adicione controles dos Windows Forms ou controles estendidos do Word à documentos personalizados (para uma personalização no nível de documento) ou a qualquer documento aberto (para um suplemento VSTO).|[Como: adicionar controles dos Windows Forms a documentos do Office](../vsto/how-to-add-windows-forms-controls-to-office-documents.md)<br /><br /> [Como: adicionar controles content a documentos do Word](../vsto/how-to-add-content-controls-to-word-documents.md)<br /><br /> [Como: adicionar controles de indicador a documentos do Word](../vsto/how-to-add-bookmark-controls-to-word-documents.md)|  
  
### <a name="options-for-document-level-customizations"></a>Opções para personalizações no nível do documento  
 A tabela a seguir lista as opções de personalização que ficam disponíveis somente para personalizações no nível do documento.  
  
|Tarefa|Para obter mais informações|  
|----------|--------------------------|  
|Adicione um painel de ações para o documento.|[Visão geral do painel de ações](../vsto/actions-pane-overview.md)<br /><br /> [Como: adicionar um painel de ações a documentos do Word ou pastas de trabalho do Excel](../vsto/how-to-add-an-actions-pane-to-word-documents-or-excel-workbooks.md)|  
|Adicione controles XMLNode e XMLNodes estendidos à superfície do documento.|[Como: adicionar controles XMLNode a documentos do Word](../vsto/how-to-add-xmlnode-controls-to-word-documents.md)<br /><br /> [Como: adicionar controles XMLNodes a documentos do Word](../vsto/how-to-add-xmlnodes-controls-to-word-documents.md)|  
  
### <a name="options-for-vsto-add-ins"></a>Opções para suplementos VSTO  
 A tabela a seguir lista as opções de personalização que ficam disponíveis somente para suplementos do VSTO.  
  
|Tarefa|Para obter mais informações|  
|----------|--------------------------|  
|Crie um painel de tarefas personalizado.|[Painéis de tarefas personalizados](../vsto/custom-task-panes.md)|  
  
### <a name="related-topics"></a>Tópicos relacionados  
  
|Título|Descrição|  
|-----------|-----------------|  
|[Visão geral do modelo de objeto do Word](../vsto/word-object-model-overview.md)|Fornece uma visão geral dos principais tipos fornecidos pelo modelo de objeto do Word.|  
|[Automatizar o Word usando objetos estendidos](../vsto/automating-word-by-using-extended-objects.md)|Fornece informações sobre os objetos estendidos (fornecidos pelo [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)]) que você pode usar em soluções do Word.|  
|[Controles de formulários do Windows na visão geral de documentos do Office](../vsto/windows-forms-controls-on-office-documents-overview.md)|Descreve como você pode adicionar controles dos Windows Forms a documentos do Word.|  
|[Passo a passo: Criar a primeira personalização no nível de documento para Word](../vsto/walkthrough-creating-your-first-document-level-customization-for-word.md)|Demonstra como criar uma personalização no nível de documento básica para o Word.|  
|[Passo a passo: Criar seu primeiro suplemento VSTO para Word](../vsto/walkthrough-creating-your-first-vsto-add-in-for-word.md)|Demonstra como criar um básico suplemento VSTO para Word.|  
|[Passo a passo: Adicionar controles a um documento em tempo de execução em um suplemento do VSTO](../vsto/walkthrough-adding-controls-to-a-document-at-run-time-in-a-vsto-add-in.md)|Demonstra como adicionar um Windows Forms de botão e um <xref:Microsoft.Office.Tools.Word.RichTextContentControl> a um documento em tempo de execução usando um suplemento do VSTO.|  
|[Word 2010 no desenvolvimento do Office](http://go.microsoft.com/fwlink/?LinkId=199020)|Fornece links para artigos e documentação de referência sobre como desenvolver soluções do Word (não específicas para desenvolvimento do Office usando o Visual Studio).|  
  
  