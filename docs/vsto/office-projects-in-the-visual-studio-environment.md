---
title: Projetos do Office no ambiente do Visual Studio
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
f1_keywords:
- VST.ProjectItem.WordDocument
- VST.ProjectItem.ExcelWorkbook
- VST.ProjectItem.ExcelTemplate
- VST.ProjectItem.ExcelSheet
- VST.ProjectItem.BlueprintCode
- VST.ProjectItem.Word
- VST.ProjectItem.Excel
- VST.ProjectItem.AddinProject
- Designer_Microsoft.VisualStudio.OfficeTools.Excel.Design.WorksheetDesigner
- VST.ProjectItem.ExtendedBluePrint
- VST.ProjectItem.WordTemplate
- Designer_Microsoft.VisualStudio.OfficeTools.Word.Design.DocumentDesigner
- VST.Designer.ExcelVST.Designer.Word
- VST.ProjectItem.ExtendedBlueprintCode
- VST.ProjectItem.BluePrint
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- documents [Office development in Visual Studio]
- hidden files [Office development in Visual Studio]
- project files [Office development in Visual Studio], hidden
- Office development in Visual Studio, documents in Visual Studio
- design view, Excel
- designers, Office development in Visual Studio
- Office documents [Office development in Visual Studio]
- Office documents [Office development in Visual Studio], about documents in Visual Studio
- designers [Office development in Visual Studio]
- Word designer
- Word [Office development in Visual Studio], Word designer
- Visual Studio, Office documents in
- worksheets [Office development in Visual Studio]
- VST.Designer.ExcelVST.Designer.Word
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: 8149e8029dbe39d37ab3979df9af38386af84d6b
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49867410"
---
# <a name="office-projects-in-the-visual-studio-environment"></a>Projetos do Office no ambiente do Visual Studio
  Os projetos do Microsoft Office têm uma experiência de desenvolvimento semelhante a outros tipos de projeto no Visual Studio, como projetos do Windows Forms. Quando você cria ou abre um projeto do Office, os itens de projeto aparecem no **Gerenciador de soluções**. Para projetos no nível de documento, o documento (isto é, o documento do Word ou a pasta de trabalho do Excel) é aberto no Visual Studio e se comporta como um designer visual.  
  
 [!INCLUDE[appliesto_all](../vsto/includes/appliesto-all-md.md)]  
  
## <a name="project-items-in-solution-explorer"></a>Itens de projeto no Gerenciador de soluções  
 Em um projeto de nível de documento **Gerenciador de soluções** exibe os seguintes itens padrão:  
  
- Nós do documento, da pasta de trabalho e das folhas que são personalizados pelo projeto. Esses nós servem como contêineres para os arquivos de código que são associados ao documento, à pasta de trabalho e às folhas.  
  
- Arquivos de código que são associados ao documento, à pasta de trabalho e às folhas que são personalizados pelo projeto. Em projetos do Word, os arquivos de código são associados ao documento ou modelo do Word. Em projetos do Excel, os arquivos de código são associados à pasta de trabalho ou ao modelo do Excel, e a cada planilha e planilha de gráfico na pasta de trabalho ou no modelo.  
  
- Arquivos de projeto que você não tem pretensão de editar diretamente. Para obter mais informações, consulte [arquivos de projeto ocultos](#hiddenfiles).  
  
  Em um projeto do suplemento do VSTO **Gerenciador de soluções** exibe os seguintes itens padrão:  
  
- O nó do aplicativo. Este nó tem o mesmo nome que o aplicativo host, tais como **Word**, **Excel**, ou **Outlook**. O nó do aplicativo contém o arquivo de código ThisAddIn. Ele também fornece o **Namespace para Item de Host** propriedade. Para obter mais informações sobre essa propriedade, consulte [propriedades em projetos do Office](../vsto/properties-in-office-projects.md).  
  
- O arquivo de código ThisAddIn. Esse arquivo contém o gerado `ThisAddIn` classe para o suplemento do VSTO. Para obter mais informações sobre essa classe, consulte [programa de suplementos do VSTO](../vsto/programming-vsto-add-ins.md).  
  
- Arquivos de projeto que você não tem pretensão de editar diretamente. Para obter mais informações, consulte [arquivos de projeto ocultos](#hiddenfiles).  
  
### <a name="temporary-certificates"></a>Certificados temporários  
 Projetos do Office também incluem um certificado temporário chamado *nome do projeto*temporarykey. Esse certificado é usado para assinar o aplicativo e os manifestos de implantação do projeto durante o desenvolvimento. Para obter mais informações, consulte [conceder confiança a soluções do Office](../vsto/granting-trust-to-office-solutions.md) e [soluções do Office Secure](../vsto/securing-office-solutions.md).  
  
###  <a name="hiddenfiles"></a> Arquivos de projeto ocultos  
 Vários arquivos de projeto são ocultados por padrão. Esses arquivos são gerados pelo Visual Studio e diferem por tipo de projeto. Para exibir arquivos ocultos, clique em **Show All Files** na **Gerenciador de soluções**.  
  
 Não modifique os arquivos de projeto ocultos. A alteração direta desses arquivos não tem suporte e pode corromper seu projeto. Os arquivos de projeto ocultos são regenerados sempre que determinadas alterações ocorrerem no documento. Se você fizer alterações manuais em um arquivo de projeto oculto, essas alterações serão perdidas quando o arquivo for regenerado.  
  
## <a name="document-designer-in-document-level-projects"></a>Designer do documento em projetos de nível de documento  
 Os projetos no nível de documento do Excel e Word fornecem um designer que hospeda o documento que é associado ao seu projeto no Visual Studio. O designer permite modificar o documento sem precisar sair do ambiente do Visual Studio.  
  
 Para abrir um documento no designer, clique duas vezes no arquivo de código em **Gerenciador de soluções** que está associado com o documento. Por exemplo, para abrir a planilha **Sheet1** no designer de um projeto do Excel, clique duas vezes o **Sheet1** arquivo de código.  
  
 Ao modificar o documento no designer, você pode aproveitar a funcionalidade nativa do aplicativo do Office. Por exemplo, é possível digitar texto no documento ou em uma planilha, ou usar a Faixa de Opções para executar tarefas como adicionar uma tabela ou um gráfico. Por padrão, o mapeamento do atalho de teclado é padronizado para o mapeamento do Visual Studio. Para usar o Office mapeamentos de atalho de teclado em vez disso, altere as configurações na **configurações de teclado do Microsoft Office** nó na **opções** caixa de diálogo na **ferramentas** menu .  
  
### <a name="controls-on-documents"></a>Controles em documentos  
 Você pode arrastar *hospedar controles* e controles dos Windows Forms do Visual Studio **caixa de ferramentas** para a superfície de design do documento. Os controles de host são versões especializadas de objetos do Office, como controles de conteúdo do Word e intervalos do Excel, que podem ser usados em projetos do Office criados usando o Visual Studio. Os controles de host têm recursos adicionais que não estão disponíveis nos objetos do Office correspondentes, como associação de dados e eventos adicionais.  
  
 Para obter mais informações, consulte [hospedam itens e visão geral dos controles](../vsto/host-items-and-host-controls-overview.md) e [controles na visão geral de documentos do Office do Windows forms](../vsto/windows-forms-controls-on-office-documents-overview.md).  
  
### <a name="excel-worksheets-and-workbooks-in-the-designer"></a>Pastas de trabalho no Designer e planilhas do Excel  
 Ao abrir uma planilha no designer, você pode modificá-la da mesma forma que o faz quando ela é aberta diretamente no Excel. Se você clicar duas vezes na célula de uma planilha, a célula é alterada para o modo de edição. Se você clique duas vezes em uma célula que contém um controle de host, o Editor de códigos abre e Visual Studio gera o manipulador de eventos padrão para o controle. Para navegar para outras planilhas, você pode clicar nas guias da planilha na parte inferior do designer.  
  
 Quando você abre a pasta de trabalho no designer, não há superfície de design. O modo de exibição de design da pasta de trabalho é uma grande bandeja de componente que preenche o designer.  
  
 A pasta de trabalho e cada folha dela têm um arquivo de código associado. Cada arquivo de código contém uma gerada *item de host* classe que representa a pasta de trabalho ou planilha. Para obter mais informações, consulte [automatizar o Excel usando objetos estendidos](../vsto/automating-excel-by-using-extended-objects.md).  
  
### <a name="word-documents-in-the-designer"></a>Documentos do Word no designer  
 Ao abrir o documento no designer, você pode modificá-lo da mesma forma que o faz quando ele é aberto diretamente no Word. Se você clicar duas vezes em uma palavra no documento, essa palavra será selecionada. No entanto, se a palavra estiver dentro de um controle de host, o editor de códigos será aberto e o Visual Studio vai gerar o manipulador de eventos padrão para o controle.  
  
 O documento tem um arquivo de código associado. O arquivo de código contém uma gerada *item de host* classe que representa o documento. Para obter mais informações, consulte [item de host do documento](../vsto/document-host-item.md).  
  
### <a name="design-mode-vs-runtime-mode"></a>Modo de design vs. modo de tempo de execução  
 Quando um documento é aberto no ambiente do Visual Studio, é sempre no *modo de design*. Algumas tarefas, como arrastar um controle de host para a superfície de documento, podem ser executadas somente no modo de design.  
  
 Para exibir o documento na *modo de tempo de execução*, você deve abrir o aplicativo e o documento fora do Visual Studio. Também é possível compilar e executar o projeto, que abrirá automaticamente o documento e o aplicativo fora do Visual Studio.  
  
## <a name="code-editor"></a>Editor de Códigos  
 O Editor de Códigos permite exibir e modificar os arquivos de código visíveis na sua solução. Esses arquivos contêm o código que define o comportamento da sua solução.  
  
 Para obter mais informações sobre o Editor de código, consulte [escrever código no editor de código e texto](/visualstudio/ide/writing-code-in-the-code-and-text-editor). Para obter mais informações sobre como escrever código em projetos do Office, consulte [escrever código em soluções do Office](../vsto/writing-code-in-office-solutions.md).  
  
## <a name="properties-window"></a>Janela de Propriedades  
 O **propriedades** janela exibe propriedades para itens de projeto que estão selecionados na **Gerenciador de soluções**e para elementos de interface do usuário que são selecionados no designer, como controles ou documento em um projeto de nível de documento. Algumas propriedades são específicas do aplicativo e do documento, enquanto outras são iguais em todos os projetos.  
  
## <a name="data-sources-window"></a>janela Fontes de Dados  
 Você pode usar o **fontes de dados** janela em projetos do Office em nível de documento para arrastar uma fonte de dados para seu documento e criar um controle que está associada à fonte de dados. Para obter mais informações, consulte [associar controles a dados no Visual Studio](/visualstudio/data-tools/bind-controls-to-data-in-visual-studio).  
  
## <a name="see-also"></a>Consulte também  
 [Projetar e criar soluções do Office](../vsto/designing-and-creating-office-solutions.md)   
 [Visão geral de modelos de projeto do Office](../vsto/office-project-templates-overview.md)   
 [Como: criar projetos do Office no Visual Studio](../vsto/how-to-create-office-projects-in-visual-studio.md)   
 [Propriedades em projetos do Office](../vsto/properties-in-office-projects.md)  
  
  