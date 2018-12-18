---
title: Criando soluções de fluxo de trabalho do SharePoint | Microsoft Docs
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
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
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: c4e808d93d2ae3039d4c5d79d1c14c65360bba32
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49892305"
---
# <a name="create-sharepoint-workflow-solutions"></a>Criar soluções de fluxo de trabalho do SharePoint

[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] fornece ferramentas para ajudá-lo a criar fluxos de trabalho personalizados que gerenciam o ciclo de vida de documentos e itens de lista em um site do SharePoint. Itens fornecidos incluem um designer, um conjunto de controles de atividade e as referências de assembly necessárias. [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] também inclui o **Assistente para personalização do SharePoint**, para ajudar a criar e configurar os fluxos de trabalho.

Para obter mais informações sobre o SharePoint, consulte [tecnologias e produtos do Microsoft SharePoint](http://go.microsoft.com/fwlink/?LinkId=178470).

## <a name="workflows-in-sharepoint"></a>Fluxos de trabalho no SharePoint
 Quando você adiciona um fluxo de trabalho a uma lista ou biblioteca do SharePoint, você pode impor um processo de negócios em todos os itens na lista ou biblioteca. Um fluxo de trabalho descreve as ações que o sistema ou os usuários devem executar em cada item, como enviar o item a ser editado e, em seguida, revisado. Essas ações, conhecidas como *atividades*, são os blocos de construção do fluxo de trabalho.

 Você pode criar fluxos de trabalho do SharePoint no [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] e implantá-los em um site do SharePoint. Depois que um fluxo de trabalho é implantado no SharePoint, você pode associá-lo com uma biblioteca ou lista. Ele pode então ser iniciado automaticamente, por um processo, ou manualmente, por um usuário. Para obter mais informações sobre a operação de fluxo de trabalho, consulte [SharePoint desenvolver fluxos de trabalho usando o Visual Studio](https://docs.microsoft.com/sharepoint/dev/general-development/develop-sharepoint-workflows-using-visual-studio).

## <a name="create-custom-sharepoint-workflows"></a>Criar fluxos de trabalho do SharePoint personalizados
 Dois projetos de fluxo de trabalho do SharePoint estão disponíveis no [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]: **fluxo de trabalho sequencial** e **State Machine Workflow**.

 Um *fluxo de trabalho sequencial* representa uma série de etapas. As etapas são executadas uma após a outra, até que a última atividade esteja concluída. Fluxos de trabalho sequenciais sempre são estritamente sequenciais em sua execução. Porque eles podem receber eventos externos e incluir fluxos de lógica paralela, a ordem exata de execução pode variar. A ilustração a seguir mostra um exemplo de um fluxo de trabalho sequencial.

 ![Fluxo de trabalho sequencial](../sharepoint/media/sp-sequential.png "fluxo de trabalho sequencial")

 Um *fluxo de trabalho de máquina de estado* representa um conjunto de estados, transições e ações. As etapas em um fluxo de trabalho de máquina de estado executar de forma assíncrona. Isso significa que eles não são necessariamente executados uma após a outra, mas em vez disso, são disparados pelas ações e os estados. Um estado é atribuído como o estado inicial e, em seguida, uma transição com base em um evento, é feita para outro estado. A máquina de estado pode ter um estado final que determina o final do fluxo de trabalho. O diagrama a seguir mostra um exemplo de um fluxo de trabalho de máquina de estado.

 ![Fluxo de trabalho de máquina de estado](../sharepoint/media/sp-state.png "fluxo de trabalho de máquina de estado")

 Para obter mais informações sobre os tipos de fluxo de trabalho, consulte [tipos de fluxo de trabalho](http://go.microsoft.com/fwlink/?LinkId=178995).

### <a name="use-the-wizard"></a>Use o Assistente
 Quando você cria um projeto de fluxo de trabalho do SharePoint no [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)], primeiro você especifique suas configurações na **Assistente para personalização do SharePoint**. O assistente usa essas configurações para criar um projeto no **Gerenciador de soluções**. Este projeto contém um arquivo de código, vários arquivos que são usados para implantar o fluxo de trabalho, e as referências a assemblies que são necessárias para criar um fluxo de trabalho personalizado do SharePoint.

 Depois de criar o fluxo de trabalho, você pode modificar suas propriedades na janela Propriedades. Embora a maioria das propriedades de fluxo de trabalho pode ser alterado diretamente na janela Propriedades, alguns exigem que você clicar em um botão de reticências (![elipse do Designer de dispositivo móvel do ASP.NET](../sharepoint/media/mwellipsis.gif "elipse do Designer de dispositivo móvel do ASP.NET")) para Altere seus valores. Esse botão reinicia a **Assistente para personalização do SharePoint**. Depois de fazer a propriedade valor alterações, escolha o **concluir** botão para finalizar a eles.

> [!NOTE]
>  O **tipo de fluxo de trabalho** propriedade é somente leitura e não pode ser alterada. Se você quiser alterar o tipo de fluxo de trabalho, você deve criar outro fluxo de trabalho.

## <a name="design-a-sharepoint-workflow"></a>Criar um fluxo de trabalho do SharePoint
 Depois de definir todas as etapas do processo de negócios, use o [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] designer de fluxo de trabalho para criar o fluxo de trabalho do SharePoint. Para abrir o designer, clique duas vezes em Workflow1.cs ou Workflow1.vb na **Gerenciador de soluções**, ou abra o menu de atalho para qualquer um desses arquivos e, em seguida, escolha **abrir**.

### <a name="activities"></a>Atividades
 Para criar um fluxo de trabalho, adicionar atividades do **caixa de ferramentas** para um *agenda de fluxo de trabalho* no designer. Uma agenda de fluxo de trabalho contém a sequência de atividades na ordem em que eles devem ser executados.

 Há dois tipos de atividades:

- *As atividades simples* executam uma única unidade de trabalho, como "retardar por 1 dia" ou "iniciar o serviço Web".

- *Atividades compostas* contêm outras atividades; por exemplo, uma atividade condicional pode conter duas ramificações.

  Ambos os tipos de atividades estão disponíveis na **caixa de ferramentas**.

  As atividades podem ter propriedades, métodos e eventos. Use o **propriedades** janela para definir as propriedades de uma atividade.

  Você também pode criar uma atividade personalizada. Para obter mais informações, consulte [instruções passo a passo: criar uma atividade de fluxo de trabalho de site personalizada](../sharepoint/walkthrough-create-a-custom-site-workflow-activity.md).

  As atividades são organizadas nas seguintes guias na **caixa de ferramentas**:

- **Fluxo de trabalho do SharePoint**

- **Windows Workflow v3.0**

- **Windows Workflow v3.5**

  Nem todas as atividades de fluxo de trabalho principais são suportadas pelo SharePoint. Para obter mais informações, consulte [fluxo de trabalho para o Windows SharePoint Services visão geral das atividades](http://go.microsoft.com/fwlink/?LinkID=156094).

#### <a name="sharepoint-workflow-activities"></a>Atividades de fluxo de trabalho do SharePoint
 O **fluxo de trabalho do SharePoint** guias contêm atividades especializadas para uso em [!INCLUDE[wss_14_long](../sharepoint/includes/wss-14-long-md.md)]. Essas atividades simplificam e facilitar o desenvolvimento de fluxos de trabalho ciclo de vida do documento. Para obter mais informações sobre as atividades listadas na **fluxo de trabalho do SharePoint** guia, consulte [fluxo de trabalho para o Windows SharePoint Services visão geral das atividades](http://go.microsoft.com/fwlink/?LinkID=156094).

#### <a name="windows-workflow-activities"></a>Atividades de fluxo de trabalho do Windows
 O **fluxo de trabalho do Windows** guias contêm as atividades que são fornecidas pelo [!INCLUDE[TLA#tla_workflow](../sharepoint/includes/tlasharptla-workflow-md.md)]. Você pode usar essas atividades para criar agendas de fluxo de trabalho de qualquer tipo de aplicativo de fluxo de trabalho do Windows.

 Para obter mais informações sobre as atividades listadas na **fluxos de trabalho do Windows** guia, consulte [atividades do Windows Workflow Foundation](http://go.microsoft.com/fwlink/?LinkID=156096). Para obter mais informações sobre o Windows Workflow Foundation, consulte [visão geral do Windows Workflow Foundation](http://go.microsoft.com/fwlink/?LinkID=128632).

### <a name="work-with-activities-in-the-designer"></a>Trabalhar com atividades no designer
 Sua programação de fluxo de trabalho pode conter uma combinação de atividades de fluxo de trabalho do Windows e as atividades de fluxo de trabalho do SharePoint.

 O designer exibe indicações visuais para ajudar a posicionar e configurar as atividades corretamente. Quando você arrasta ou uma atividade para a programação de fluxo de trabalho de cópia, o designer exibe ícones de verde-sinal de adição (+) que mostram locais válidos para aquela atividade no fluxo de trabalho. Você não pode posicionar uma atividade em um local em que ela não seria válida. Por exemplo, você não pode posicionar uma atividade enviar como a primeira atividade em uma ramificação de atividade escutar. Para obter mais informações, consulte [Central de desenvolvedores do SharePoint Designer](http://go.microsoft.com/fwlink/?LinkId=178476).

## <a name="collect-information-during-the-workflow"></a>Coletar informações durante o fluxo de trabalho
 Você talvez queira coletar informações de usuários em momentos predefinidos no fluxo de trabalho. Você pode coletar informações por meio de formulários ou propriedades do item.

### <a name="forms"></a>Formulários
 Os formulários são semelhantes a caixas de diálogo que contêm perguntas e fornecem maneiras para os usuários fornecer respostas.

 Há quatro tipos de formulários que podem ser usados em um fluxo de trabalho:

- Associação

- Iniciação

- Modificação

- Tarefa

  Dentre eles, [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] inclui modelos de item para formulários de associação e iniciação. Um exemplo de um *formulário de associação* é o que permite que o administrador que está instalando o fluxo de trabalho insira parâmetros relacionados ao fluxo de trabalho, como um limite de gastos para um fluxo de trabalho de despesas. Um exemplo de um *formulário de iniciação* é aquela que permite que o usuário de um fluxo de trabalho de despesas insira a quantidade que eles passam o fluxo de trabalho. Para obter mais informações sobre esses tipos de formulários, consulte [SharePoint modelos de item de projeto e projeto](../sharepoint/sharepoint-project-and-project-item-templates.md).

### <a name="item-properties"></a>Propriedades do item
 Você também pode coletar informações de usuários usando as propriedades de um item na lista ou biblioteca do SharePoint. O arquivo de código principal (Workflow1.cs ou Workflow1.vb) declara uma instância da classe Microsoft.SharePoint.Workflow.SPWorkflowActivationProperties.WorkflowProperties chamada `workflowProperties`. Use o `workflowProperties` objeto para acessar as propriedades da biblioteca ou lista no código. Por exemplo, consulte [instruções passo a passo: criar e depurar uma solução de fluxo de trabalho do SharePoint](../sharepoint/walkthrough-creating-and-debugging-a-sharepoint-workflow-solution.md).

## <a name="debug-a-sharepoint-workflow-template"></a>Depurar um modelo de fluxo de trabalho do SharePoint
 Você pode depurar um projeto de fluxo de trabalho do SharePoint o mesmo durante a depuração outros [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] projetos baseados na Web. Quando você inicia o [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] depurador, [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] usa as configurações que você especificar na **Assistente para personalização do SharePoint** para abrir o site da Web do SharePoint apropriado e associe automaticamente o modelo de fluxo de trabalho com a lista ou biblioteca apropriada. [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] também anexa a [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] do depurador para o [!INCLUDE[wss_14_long](../sharepoint/includes/wss-14-long-md.md)] processo chamado *w3wp.exe*.

 Para testar o fluxo de trabalho, você deve iniciá-lo manualmente. Para obter mais informações, consulte a seção "Depuração fluxos de trabalho" em [depurando soluções do SharePoint](../sharepoint/debugging-sharepoint-solutions.md). Para obter mais informações sobre [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] Web de depuração do aplicativo, consulte [depurar aplicativos web e script](../debugger/debugging-web-applications-and-script.md).

## <a name="deploy-a-sharepoint-workflow-template"></a>Implantar um modelo de fluxo de trabalho do SharePoint
 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] Implantação de projetos de fluxo de trabalho do SharePoint como outro [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] projetos do SharePoint. Para obter mais informações, consulte [soluções de pacote e implantar o SharePoint](../sharepoint/packaging-and-deploying-sharepoint-solutions.md).

## <a name="import-globally-reusable-workflows"></a>Importar fluxos de trabalho reutilizáveis globalmente
 Além de criar fluxos de trabalho reutilizáveis específicos do site, o SharePoint Designer permite que você crie *fluxos de trabalho reutilizáveis globalmente*, que são fluxos de trabalho que podem ser usados por qualquer site do SharePoint. O projeto de importar fluxo de trabalho reutilizável no [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] no momento, não importa os fluxos de trabalho reutilizáveis globalmente. No entanto, você pode usar o SharePoint Designer para converter um fluxo de trabalho reutilizável globalmente em um fluxo de trabalho reutilizável, ou importar o fluxo de trabalho como um fluxo de trabalho declarativo não convertido. Para obter mais informações, consulte [importar itens de um site do SharePoint existente](../sharepoint/importing-items-from-an-existing-sharepoint-site.md).

## <a name="related-topics"></a>Tópicos relacionados

|Título|Descrição|
|-----------|-----------------|
|[Passo a passo: Criar e depurar uma solução de fluxo de trabalho do SharePoint](../sharepoint/walkthrough-creating-and-debugging-a-sharepoint-workflow-solution.md)|Orienta você passo a passo pela criação e depuração de um simples [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] fluxo de trabalho.|
|[Passo a passo: Criar um fluxo de trabalho com formulários de associação e iniciação](../sharepoint/walkthrough-creating-a-workflow-with-association-and-initiation-forms.md)|Orienta você passo a passo para criar um mais completos [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] conclui o fluxo de trabalho com formulários de associação e iniciação.|
|[Passo a passo: Adicionar uma página de aplicativo a um fluxo de trabalho](../sharepoint/walkthrough-add-an-application-page-to-a-workflow.md)|Se baseia no tópico [instruções passo a passo: criar um fluxo de trabalho com formulários de associação e iniciação](../sharepoint/walkthrough-creating-a-workflow-with-association-and-initiation-forms.md) adicionando adicional *. aspx* página que relata os dados inseridos no fluxo de trabalho do aplicativo.|
|[Passo a passo: Criar uma atividade de fluxo de trabalho de site personalizada](../sharepoint/walkthrough-create-a-custom-site-workflow-activity.md)|Demonstra como executar duas tarefas principais: criar um fluxo de trabalho de nível de site e criar uma atividade de fluxo de trabalho personalizado.|
|[Passo a passo: Importar um fluxo de trabalho reutilizável do SharePoint Designer no Visual Studio](../sharepoint/walkthrough-import-a-sharepoint-designer-reusable-workflow-into-visual-studio.md)|Demonstra como importar reutilizáveis fluxos de trabalho declarativos criados no SharePoint Designer 2010 em um [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] projeto do SharePoint.|

## <a name="see-also"></a>Consulte também

- [Desenvolver soluções do SharePoint](../sharepoint/developing-sharepoint-solutions.md)
- [Compilar e depurar soluções do SharePoint](../sharepoint/building-and-debugging-sharepoint-solutions.md)
- [Criar páginas de aplicativo do SharePoint](../sharepoint/creating-application-pages-for-sharepoint.md)