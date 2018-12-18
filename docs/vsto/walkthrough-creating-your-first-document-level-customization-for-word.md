---
title: 'Passo a passo: Criar a primeira personalização no nível de documento para Word'
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Office development in Visual Studio, creating your first project
- Word [Office development in Visual Studio], creating your first project
- document-level customizations [Office development in Visual Studio], creating your first project
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: 1c5c25163a49e51b0759e57318d6119edec97983
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49928809"
---
# <a name="walkthrough-create-your-first-document-level-customization-for-word"></a>Passo a passo: Criar a primeira personalização no nível de documento para Word
  Este passo a passo introdutório mostra como criar uma personalização no nível de documento para o Microsoft Office Word. Os recursos que você criar nesse tipo de solução estão disponíveis somente quando um documento específico estiver aberto. Você não pode usar uma personalização no nível de documento para fazer alterações em todo o aplicativo, por exemplo, exibindo uma nova guia de faixa de opções quando qualquer documento é aberto.  
  
 [!INCLUDE[appliesto_wdalldoc](../vsto/includes/appliesto-wdalldoc-md.md)]  
  
 Esta explicação passo a passo ilustra as seguintes tarefas:  
  
- Criando um projeto de documento do Word.  
  
- Adicionar texto ao documento que está hospedado no designer do Visual Studio.  
  
- Escrevendo código que usa o modelo de objeto do Word para adicionar texto ao documento personalizado quando ele é aberto.  
  
- Criando e executando o projeto para testá-lo.  
  
- Limpando o projeto para remover arquivos de compilação desnecessárias e as configurações de segurança de seu computador de desenvolvimento.  
  
  [!INCLUDE[note_settings_general](../sharepoint/includes/note-settings-general-md.md)]  
  
## <a name="prerequisites"></a>Pré-requisitos  
 Você precisa dos seguintes componentes para concluir esta instrução passo a passo:  
  
-   [!INCLUDE[vsto_vsprereq](../vsto/includes/vsto-vsprereq-md.md)]  
  
-   Microsoft Word  
  
## <a name="create-the-project"></a>Criar o projeto  
  
### <a name="to-create-a-new-word-document-project-in-visual-studio"></a>Para criar um novo projeto de documento do Word no Visual Studio  
  
1.  Inicie o [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)].  
  
2.  No menu **Arquivo**, aponte para **Novo** e clique em **Projeto**.  
  
3.  No painel de modelos, expanda **Visual c#** ou **Visual Basic**e, em seguida, expanda **Office/SharePoint**.  
  
4.  Sob o expandida **Office/SharePoint** nó, selecione o **suplementos do Office** nó.  
  
5.  Na lista de modelos de projeto, selecione um projeto de documento do VSTO do Word.  
  
6.  No **nome** , digite **FirstDocumentCustomization**.  
  
7.  Clique em **OK**.  
  
     O **Visual Studio Tools for Office Project Wizard** é aberta.  
  
8.  Selecione **criar um novo documento**e clique em **Okey**.  
  
     [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] cria o **FirstDocumentCustomization** do projeto e adiciona os **FirstDocumentCustomization** ThisDocument arquivos de código ao projeto e documentos. O **FirstDocumentCustomization** documento é aberto automaticamente no designer.  
  
## <a name="close-and-reopen-the-document-in-the-designer"></a>Feche e reabra o documento no designer  
 Se você deliberadamente ou acidentalmente fechar o documento no designer enquanto você estiver desenvolvendo seu projeto, você poderá reabri-lo.  
  
### <a name="to-close-and-reopen-the-document-in-the-designer"></a>Feche e reabra o documento no designer  
  
1.  Feche o documento clicando o **fechar** botão (X) para a janela do designer.  
  
2.  No **Gerenciador de soluções**, clique com botão direito do **ThisDocument** arquivo de código e, em seguida, clique em **View Designer**.  
  
     \- ou -  
  
     Na **Gerenciador de soluções**, clique duas vezes o **ThisDocument** arquivo de código.  
  
## <a name="add-text-to-the-document-in-the-designer"></a>Adicionar texto ao documento no designer  
 Você pode criar a interface do usuário (UI) de sua personalização por meio da modificação do documento que está aberto no designer. Por exemplo, você pode adicionar texto, tabelas ou controles do Word. Para obter mais informações sobre como usar o designer, consulte [projetos do Office no ambiente do Visual Studio](../vsto/office-projects-in-the-visual-studio-environment.md).  
  
### <a name="to-add-text-to-your-document-by-using-the-designer"></a>Para adicionar texto ao documento usando o designer  
  
1.  No documento que está aberto no designer, digite o texto a seguir.  
  
     **Este texto foi adicionado usando o designer.**  
  
## <a name="add-text-to-the-document-programmatically"></a>Adicionar texto ao documento programaticamente  
 Em seguida, adicione código ao arquivo de código ThisDocument. O novo código usa o modelo de objeto do Word para adicionar um segundo parágrafo de texto ao documento. Por padrão, o arquivo de código ThisDocument contém o seguinte código gerado:  
  
-   Uma definição parcial do `ThisDocument` classe, que representa o modelo de programação do documento e fornece acesso ao modelo de objeto do Word. Para obter mais informações, consulte [item de host do documento](../vsto/document-host-item.md) e [visão geral do modelo de objeto Word](../vsto/word-object-model-overview.md). O restante do `ThisDocument` classe é definida em um arquivo de código oculto que você não deve modificar.  
  
-   O `ThisDocument_Startup` e `ThisDocument_Shutdown` manipuladores de eventos. Esses manipuladores de eventos são chamados quando o documento é aberto e fechado. Use esses manipuladores de eventos para inicializar sua personalização quando o documento for aberto e para limpar os recursos usados pela sua personalização quando o documento é fechado. Para obter mais informações, consulte [eventos em projetos do Office](../vsto/events-in-office-projects.md).  
  
### <a name="to-add-a-second-paragraph-of-text-to-the-document-by-using-code"></a>Para adicionar um segundo parágrafo de texto ao documento usando código  
  
1.  Na **Gerenciador de soluções**, clique com botão direito **ThisDocument**e, em seguida, clique em **Exibir código**.  
  
     Abre o arquivo de código no Visual Studio.  
  
2.  Substitua o `ThisDocument_Startup` manipulador de eventos com o código a seguir. Quando o documento é aberto, esse código adiciona um segundo parágrafo de texto ao documento.  
  
     [!code-vb[Trin_WordDocumentTutorial#1](../vsto/codesnippet/VisualBasic/FirstDocumentCustomization/ThisDocument.vb#1)]
     [!code-csharp[Trin_WordDocumentTutorial#1](../vsto/codesnippet/CSharp/FirstDocumentCustomization/ThisDocument.cs#1)]  
  
    > [!NOTE]  
    >  Esse código usa o valor de índice 1 para acessar o primeiro parágrafo de <xref:Microsoft.Office.Tools.Word.Document.Paragraphs%2A> propriedade. Embora o Visual Basic e Visual c# usam conjuntos baseados em 0, os limites inferiores da matriz da maioria das coleções no modelo de objeto do Word é 1. Para obter mais informações, consulte [escrever código em soluções do Office](../vsto/writing-code-in-office-solutions.md).  
  
## <a name="test-the-project"></a>O projeto de teste  
  
### <a name="to-test-your-document"></a>Para testar o documento  
  
1.  Pressione **F5** para compilar e executar seu projeto.  
  
     Quando você compila o projeto, o código é compilado em um assembly que está associado ao documento. O Visual Studio coloca uma cópia do documento e o assembly na pasta de saída de compilação para o projeto, e ele define as configurações de segurança no computador de desenvolvimento para habilitar a personalização ser executado. Para obter mais informações, consulte [soluções do Office compilar](../vsto/building-office-solutions.md).  
  
2.  No documento, verifique se o texto a seguir.  
  
     **Este texto foi adicionado usando o designer.**  
  
     **Este texto foi adicionado por meio de código.**  
  
3.  Feche o documento.  
  
## <a name="clean-up-the-project"></a>Limpar o projeto  
 Quando você concluir o desenvolvimento de um projeto, você deve remover os arquivos na pasta de saída de compilação e as configurações de segurança criadas pelo processo de compilação.  
  
### <a name="to-clean-up-the-completed-project-on-your-development-computer"></a>Para limpar o projeto concluído no computador de desenvolvimento  
  
1.  No Visual Studio, sobre o **construir** menu, clique em **limpar solução**.  
  
## <a name="next-steps"></a>Próximas etapas  
 Agora que você criou uma personalização no nível de documento básica para o Word, você pode aprender mais sobre como desenvolver as personalizações com estes tópicos:  
  
-   Tarefas gerais de programação que você pode executar personalizações no nível do documento: [personalizações no nível de documento do programa](../vsto/programming-document-level-customizations.md).  
  
-   Tarefas de programação que são específicas para personalizações no nível de documento para Word: [soluções do Word](../vsto/word-solutions.md).  
  
-   Usando o modelo de objeto do Word: [visão geral do modelo de objeto Word](../vsto/word-object-model-overview.md).  
  
-   Personalizando a interface do usuário do Word, por exemplo, por adicionar uma guia personalizada à faixa de opções ou criar seu próprio painel de ações: [personalização da interface do usuário do Office](../vsto/office-ui-customization.md).  
  
-   Usando objetos estendidos do Word fornecidos por soluções do Office no Visual Studio para executar tarefas que não são possíveis, usando o modelo de objeto do Word (por exemplo, hospedagem de controles gerenciados em documentos e associando controles do Word a dados usando os dados do Windows Forms modelo de vinculação): [automatizar o Word usando objetos estendidos](../vsto/automating-word-by-using-extended-objects.md).  
  
-   Compilar e depurar as personalizações no nível de documento para Word: [soluções do Office compilar](../vsto/building-office-solutions.md).  
  
-   Implantação de personalizações no nível de documento para Word: [implantar uma solução do Office](../vsto/deploying-an-office-solution.md).  
  
## <a name="see-also"></a>Consulte também  
 [Visão geral de desenvolvimento de soluções do Office &#40;VSTO&#41;](../vsto/office-solutions-development-overview-vsto.md)   
 [Soluções do Word](../vsto/word-solutions.md)   
 [Personalizações em nível de documento do programa](../vsto/programming-document-level-customizations.md)   
 [Visão geral do modelo de objeto do Word](../vsto/word-object-model-overview.md)   
 [Automatizar o Word usando objetos estendidos](../vsto/automating-word-by-using-extended-objects.md)   
 [Personalização da interface do usuário do Office](../vsto/office-ui-customization.md)   
 [Compilar soluções do Office](../vsto/building-office-solutions.md)   
 [Implantar uma solução do Office](../vsto/deploying-an-office-solution.md)   
 [Visão geral de modelos de projeto do Office](../vsto/office-project-templates-overview.md)  
  
  