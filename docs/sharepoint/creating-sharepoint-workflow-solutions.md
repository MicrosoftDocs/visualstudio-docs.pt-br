---
title: Criando soluções de fluxo de trabalho do SharePoint | Microsoft Docs
ms.date: 02/02/2017
ms.topic: overview
f1_keywords:
- VSTO.NewSharePointWorkflowWizard.Page3
- VS.SharePointTools.Workflow.WorkflowName
- VSTO.NewSharePointWorkflowWizard.Page2
- VSTO.NewSharePointWorkflowWizard.Page1
dev_langs:
- VB
- CSharp
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, workflows
- workflows [SharePoint development in Visual Studio]
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 2c787009577735213437140513ec095f81c3f43b
ms.sourcegitcommit: f9e44f5ab6a1dfb56c945c9986730465e1adb6fc
ms.contentlocale: pt-BR
ms.lasthandoff: 07/06/2020
ms.locfileid: "86015287"
---
# <a name="create-sharepoint-workflow-solutions"></a>Criar soluções de fluxo de trabalho do SharePoint

[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]fornece ferramentas para ajudá-lo a criar fluxos de trabalho personalizados que gerenciam o ciclo de vida de documentos e itens de lista em um site do SharePoint. Os itens fornecidos incluem um designer, um conjunto de controles de atividade e as referências de assembly necessárias. [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]também inclui o **Assistente para personalização do SharePoint**, para ajudar a criar e configurar os fluxos de trabalho.

Para obter mais informações sobre o SharePoint, consulte [produtos e tecnologias do Microsoft SharePoint](/sharepoint/dev/).

## <a name="workflows-in-sharepoint"></a>Fluxos de trabalho no SharePoint
 Ao adicionar um fluxo de trabalho a uma biblioteca ou lista do SharePoint, você impõe um processo de negócios em todos os itens na biblioteca ou lista. Um fluxo de trabalho descreve as ações que o sistema ou os usuários devem executar em cada item, como enviar o item a ser editado e, em seguida, revisar. Essas ações, conhecidas como *atividades*, são os blocos de construção do fluxo de trabalho.

 Você pode criar fluxos de trabalho do SharePoint no [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] e implantá-los em um site do SharePoint. Depois que um fluxo de trabalho é implantado no SharePoint, você o associa a uma biblioteca ou lista. Em seguida, ele pode ser iniciado automaticamente, por um processo, ou manualmente, por um usuário. Para obter mais informações sobre a operação de fluxo de trabalho, consulte [desenvolver fluxos de trabalho do SharePoint usando o Visual Studio](/sharepoint/dev/general-development/develop-sharepoint-workflows-using-visual-studio).

## <a name="create-custom-sharepoint-workflows"></a>Criar fluxos de trabalho personalizados do SharePoint
 Dois projetos de fluxo de trabalho do SharePoint estão disponíveis para você: fluxo de trabalho [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] **sequencial** e fluxo de trabalho da **máquina de estado**.

 Um *fluxo de trabalho Sequencial* representa uma série de etapas. As etapas são executadas uma após a outra até que a última atividade seja concluída. Fluxos de trabalho seqüenciais são sempre estritamente sequenciais em sua execução. Como eles podem receber eventos externos e incluir fluxos lógicos paralelos, a ordem exata de execução pode variar. A ilustração a seguir mostra um exemplo de fluxo de trabalho Sequencial.

 ![Fluxo de trabalho Sequencial](../sharepoint/media/sp-sequential.png "Fluxo de trabalho Sequencial")

 Um *fluxo de trabalho de máquina de estado* representa um conjunto de Estados, transições e ações. As etapas em um fluxo de trabalho de máquina de estado são executadas de forma assíncrona. Isso significa que eles não são necessariamente executados um após o outro, mas, em vez disso, são disparados por ações e Estados. Um estado é atribuído como o estado de início e, em seguida, com base em um evento, é feita uma transição para outro Estado. O computador de estado pode ter um estado final que determina o final do fluxo de trabalho. O diagrama a seguir mostra um exemplo de fluxo de trabalho de máquina de estado.

 ![Fluxo de trabalho da máquina de estado](../sharepoint/media/sp-state.png "Fluxo de trabalho da máquina de estado")

 Para obter mais informações sobre tipos de fluxo de trabalho, consulte [tipos de fluxo de trabalho](/previous-versions/office/developer/sharepoint-2010/ms468447(v=office.14)).

### <a name="use-the-wizard"></a>Usar o assistente
 Ao criar um projeto de fluxo de trabalho do SharePoint no [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] , você primeiro especifica suas configurações no **Assistente para personalização do SharePoint**. O assistente usa essas configurações para criar um projeto no **Gerenciador de soluções**. Este projeto contém um arquivo de código, vários arquivos que são usados para implantar o fluxo de trabalho e referências a assemblies que são necessários para criar um fluxo de trabalho personalizado do SharePoint.

 Depois de criar o fluxo de trabalho, você pode modificar suas propriedades no janela Propriedades. Embora a maioria das propriedades de fluxo de trabalho possa ser alterada diretamente no janela Propriedades, algumas exigem que você clique em um botão de reticências (![elipse do designer móvel ASP.net](../sharepoint/media/mwellipsis.gif "Elipse do designer móvel ASP.NET")) para alterar seus valores. Esse botão reinicia o **Assistente para personalização do SharePoint**. Depois de fazer as alterações no valor da propriedade, escolha o botão **concluir** para finalizá-las.

> [!NOTE]
> A propriedade do **tipo de fluxo de trabalho** é somente leitura e não pode ser alterada. Se você quiser alterar o tipo de fluxo de trabalho, deverá criar outro fluxo de trabalho.

## <a name="design-a-sharepoint-workflow"></a>Criar um fluxo de trabalho do SharePoint
 Depois de definir todas as etapas no processo de negócios, use o [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] Designer de fluxo de trabalho para criar o fluxo de trabalho do SharePoint. Para abrir o designer, clique duas vezes em Workflow1.cs ou Workflow1. vb no **Gerenciador de soluções**, ou abra o menu de atalho para qualquer um desses arquivos e, em seguida, escolha **abrir**.

### <a name="activities"></a>Atividades
 Para criar um fluxo de trabalho, adicione atividades da **caixa de ferramentas** a um agendamento de fluxo de *trabalho* no designer. Uma agenda de fluxo de trabalho contém a sequência de atividades na ordem em que elas devem ser executadas.

 Há dois tipos de atividades:

- *Atividades simples* executam uma única unidade de trabalho, como "atraso para 1 dia" ou "Iniciar serviço Web".

- *As atividades compostas* contêm outras atividades; por exemplo, uma atividade condicional pode conter duas ramificações.

  Ambos os tipos de atividades estão disponíveis na **caixa de ferramentas**.

  As atividades podem ter propriedades, métodos e eventos. Use a janela **Propriedades** para definir as propriedades de uma atividade.

  Você também pode criar uma atividade personalizada. Para obter mais informações, consulte [Walkthrough: criar uma atividade personalizada de fluxo de trabalho do site](../sharepoint/walkthrough-create-a-custom-site-workflow-activity.md).

  As atividades são organizadas nas seguintes guias na **caixa de ferramentas**:

- **Fluxo de trabalho do SharePoint**

- **Windows Workflow v 3.0**

- **Windows Workflow v 3.5**

  Nem todas as atividades de fluxo de trabalho principais têm suporte no SharePoint. Para obter mais informações, consulte [visão geral de atividades de fluxo de trabalho para o Windows SharePoint Services](/previous-versions/office/developer/sharepoint-2010/ms446847(v=office.14)).

#### <a name="sharepoint-workflow-activities"></a>Atividades de fluxo de trabalho do SharePoint
 As guias de **fluxo de trabalho do SharePoint** contêm atividades especializadas para uso no [!INCLUDE[wss_14_long](../sharepoint/includes/wss-14-long-md.md)] . Essas atividades simplificam e simplificam o desenvolvimento de fluxos de trabalho do ciclo de vida do documento. Para obter mais informações sobre as atividades listadas na guia **fluxo de trabalho do SharePoint** , consulte [visão geral de atividades de fluxo de trabalho para o Windows SharePoint Services](/previous-versions/office/developer/sharepoint-2010/ms446847(v=office.14)).

#### <a name="windows-workflow-activities"></a>Atividades de fluxo de trabalho do Windows
 As guias de **fluxo de trabalho do Windows** contêm atividades fornecidas pelo [!INCLUDE[TLA#tla_workflow](../sharepoint/includes/tlasharptla-workflow-md.md)] . Você pode usar essas atividades para criar agendas de fluxo de trabalho para qualquer tipo de aplicativo de fluxo de trabalho do Windows.

 Para obter mais informações sobre as atividades listadas na guia **fluxos de trabalho do Windows** , consulte [Windows Workflow Foundation atividades](/previous-versions/dotnet/netframework-3.5/ms733615(v=vs.90)). Para obter mais informações sobre o Windows Workflow Foundation, consulte [Windows Workflow Foundation visão geral](/previous-versions/dotnet/netframework-3.5/ms734631(v=vs.90)).

### <a name="work-with-activities-in-the-designer"></a>Trabalhar com atividades no designer
 Seu agendamento de fluxo de trabalho pode conter uma combinação de atividades do Windows Workflow e atividades de fluxo de trabalho do SharePoint.

 O designer exibe indicações visuais para ajudá-lo a posicionar e configurar as atividades corretamente. Quando você arrasta ou copia uma atividade na agenda de fluxo de trabalho, o designer exibe ícones verdes de sinal de adição (+) que mostram os locais válidos para essa atividade no fluxo de trabalho. Não é possível posicionar uma atividade em um local onde ela não seria válida. Por exemplo, você não pode posicionar uma atividade de envio como a primeira atividade em uma ramificação de atividade de escuta. Para obter mais informações, consulte [SharePoint Designer Developer Center](https://developer.microsoft.com/office/docs).

## <a name="collect-information-during-the-workflow"></a>Coletar informações durante o fluxo de trabalho
 Talvez você queira coletar informações de usuários em momentos predefinidos no fluxo de trabalho. Você pode coletar informações usando formulários ou propriedades de item.

### <a name="forms"></a>Formulários
 Formulários são como caixas de diálogo que contêm perguntas e fornecem maneiras para os usuários fornecerem respostas.

 Há quatro tipos de formulários que podem ser usados em um fluxo de trabalho:

- Associação

- Necessária

- Modification

- Tarefa

  Desses, [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] inclui modelos de item para formulários de associação e de inicialização. Um exemplo de um *formulário de associação* é aquele que permite ao administrador instalar o fluxo de trabalho insira parâmetros relacionados ao fluxo de trabalho, como um limite de gastos para um fluxo de trabalho de despesas. Um exemplo de um *formulário de inicialização* é aquele que permite que o usuário de um fluxo de trabalho de despesas Insira o valor que ele gastou no fluxo de trabalho. Para obter mais informações sobre esses tipos de formulários, consulte [projeto do SharePoint e modelos de item de projeto](../sharepoint/sharepoint-project-and-project-item-templates.md).

### <a name="item-properties"></a>Propriedades do item
 Você também pode coletar informações de usuários usando as propriedades de um item na biblioteca ou lista do SharePoint. O arquivo de código principal (Workflow1.cs ou Workflow1. vb) declara uma instância da classe Microsoft. SharePoint. Workflow. SPWorkflowActivationProperties. WorkflowProperties denominada `workflowProperties` . Use o `workflowProperties` objeto para acessar as propriedades da biblioteca ou da lista no código. Para obter um exemplo, consulte [Walkthrough: criar e depurar uma solução de fluxo de trabalho do SharePoint](../sharepoint/walkthrough-creating-and-debugging-a-sharepoint-workflow-solution.md).

## <a name="debug-a-sharepoint-workflow-template"></a>Depurar um modelo de fluxo de trabalho do SharePoint
 Você pode depurar um projeto de fluxo de trabalho do SharePoint da mesma forma que depura outros [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] projetos baseados na Web. Quando você inicia o [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] depurador, [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] o usa as configurações especificadas no Assistente para **personalização do SharePoint** para abrir o site apropriado do SharePoint e associar automaticamente o modelo de fluxo de trabalho com a biblioteca ou lista apropriada. [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]também anexa o [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] depurador ao [!INCLUDE[wss_14_long](../sharepoint/includes/wss-14-long-md.md)] processo chamado *w3wp.exe*.

 Para testar o fluxo de trabalho, você deve iniciá-lo manualmente. Para obter mais informações, consulte a seção "depuração de fluxos de trabalho" em [Depurando soluções do SharePoint](../sharepoint/debugging-sharepoint-solutions.md). Para obter mais informações sobre [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] depuração de aplicativo Web, consulte [depurar aplicativos Web e script](../debugger/how-to-enable-debugging-for-aspnet-applications.md).

## <a name="deploy-a-sharepoint-workflow-template"></a>Implantar um modelo de fluxo de trabalho do SharePoint
 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]Os projetos de fluxo de trabalho do SharePoint implantam assim como outros [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] projetos do SharePoint. Para obter mais informações, consulte [empacotar e implantar soluções do SharePoint](../sharepoint/packaging-and-deploying-sharepoint-solutions.md).

## <a name="import-globally-reusable-workflows"></a>Importar fluxos de trabalho reutilizáveis globalmente
 Além de criar fluxos de trabalho reutilizáveis específicos do site, o SharePoint Designer permite criar *fluxos de trabalho reutilizáveis globalmente*, que são fluxos de trabalho que podem ser usados por qualquer site do SharePoint. O projeto importar fluxo de trabalho reutilizável [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] atualmente não importa fluxos de trabalho reutilizáveis globalmente. No entanto, você pode usar o SharePoint Designer para converter um fluxo de trabalho reutilizável globalmente em um fluxo de trabalho reutilizável ou importar o fluxo de trabalho como um fluxo de trabalho declarativo não convertido. Para obter mais informações, consulte [importar itens de um site existente do SharePoint](../sharepoint/importing-items-from-an-existing-sharepoint-site.md).

## <a name="related-topics"></a>Tópicos relacionados

|Title|Descrição|
|-----------|-----------------|
|[Walkthrough: criar e depurar uma solução de fluxo de trabalho do SharePoint](../sharepoint/walkthrough-creating-and-debugging-a-sharepoint-workflow-solution.md)|O leva você passo a passo por meio da criação e da depuração de um [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] fluxo de trabalho simples.|
|[Walkthrough: criar um fluxo de trabalho com formulários de associação e de inicialização](../sharepoint/walkthrough-creating-a-workflow-with-association-and-initiation-forms.md)|O leva você passo a passo para criar um fluxo de trabalho com recursos completos completo [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] com formulários de associação e inicialização.|
|[Walkthrough: adicionar uma página de aplicativo a um fluxo de trabalho](../sharepoint/walkthrough-add-an-application-page-to-a-workflow.md)|Baseia-se no tópico [Walkthrough: criar um fluxo de trabalho com formulários de associação e de inicialização](../sharepoint/walkthrough-creating-a-workflow-with-association-and-initiation-forms.md) adicionando uma página adicional de aplicativo *. aspx* que relata os dados inseridos no fluxo de trabalho.|
|[Walkthrough: criar uma atividade de fluxo de trabalho de site personalizada](../sharepoint/walkthrough-create-a-custom-site-workflow-activity.md)|Demonstra como executar duas tarefas principais: criar um fluxo de trabalho de nível de site e criar uma atividade de fluxo de trabalho personalizada.|
|[Walkthrough: importar um fluxo de trabalho reutilizável do SharePoint Designer para o Visual Studio](../sharepoint/walkthrough-import-a-sharepoint-designer-reusable-workflow-into-visual-studio.md)|Demonstra como importar fluxos de trabalho declarativos reutilizáveis criados no SharePoint Designer 2010 para um [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] projeto do SharePoint.|

## <a name="see-also"></a>Consulte também

- [Desenvolver soluções do SharePoint](../sharepoint/developing-sharepoint-solutions.md)
- [Compilar e depurar soluções do SharePoint](../sharepoint/building-and-debugging-sharepoint-solutions.md)
- [Criar páginas de aplicativo para o SharePoint](../sharepoint/creating-application-pages-for-sharepoint.md)