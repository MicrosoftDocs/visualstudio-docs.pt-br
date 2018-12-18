---
title: 'Passo a passo: Importar um fluxo de trabalho reutilizável do SharePoint Designer no Visual Studio | Microsoft Docs'
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
f1_keywords:
- VS.SharePointTools.WSPImport.ImportWF
dev_langs:
- VB
- CSharp
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, importing reusable workflows
- reusable workflows [SharePoint development in Visual Studio]
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: 249799bc9daf13992bd9fe03dff8c86263f91263
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49851472"
---
# <a name="walkthrough-import-a-sharepoint-designer-reusable-workflow-into-visual-studio"></a>Passo a passo: Importar um fluxo de trabalho reutilizável do SharePoint Designer no Visual Studio
  Este passo a passo demonstra como importar um fluxo de trabalho reutilizável criado no SharePoint Designer 2010 em um [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] o projeto de fluxo de trabalho do SharePoint.  
  
 Fluxos de trabalho criados no SharePoint Designer, ou *fluxos de trabalho declarativos*, consistem em [!INCLUDE[TLA2#tla_xml](../sharepoint/includes/tla2sharptla-xml-md.md)] instruções em vez de código. O SharePoint Designer 2010 introduz *fluxos de trabalho reutilizáveis*, que são portáteis e declarativos fluxos de trabalho que podem ser usados por listas diferentes em sites do SharePoint.  
  
 Fluxos de trabalho criados no [!INCLUDE[vs_dev11_long](../sharepoint/includes/vs-dev11-long-md.md)], como fluxos de trabalho sequencial e de estado de máquina, são chamados *fluxos de trabalho de código*. Fluxos de trabalho de código consistem em arquivos XML e módulos de código em que os usuários podem personalizar o comportamento do fluxo de trabalho.  
  
 Visual Studio permite que você importar fluxos de trabalho reutilizáveis criados no SharePoint Designer 2010 e convertê-los em fluxos de trabalho de código para uso em seus sites do SharePoint.  
  
 Este passo a passo demonstra as seguintes tarefas:  
  
- Criando um fluxo de trabalho simple e reutilizável no SharePoint Designer.  
  
- Exportar o fluxo de trabalho reutilizável do SharePoint Designer para uma *. wsp* arquivo e no SharePoint.  
  
- Importando o *. wsp* o arquivo em [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] usando o projeto de fluxo de trabalho reutilizável de importação.  
  
- Alterando o fluxo de trabalho com a adição de código.  
  
- Usando o fluxo de trabalho importado em um site do SharePoint.  
  
  [!INCLUDE[note_settings_general](../sharepoint/includes/note-settings-general-md.md)]  
  
## <a name="prerequisites"></a>Pré-requisitos  
 Você precisa dos seguintes componentes para concluir esta instrução passo a passo:  
  
-   Edições com suporte do [!INCLUDE[TLA#tla_win](../sharepoint/includes/tlasharptla-win-md.md)] e do SharePoint.  
  
-   Visual Studio.  
  
-   Microsoft [!INCLUDE[TLA2#tla_office](../sharepoint/includes/tla2sharptla-office-md.md)] SharePoint Designer 2010.  
  
## <a name="create-target-sharepoint-subsites"></a>Criar subsites do SharePoint de destino
 Primeiro, você cria dois novos subsites do SharePoint: um para hospedar os fluxos de trabalho reutilizáveis do SharePoint Designer, outro para hospedar os fluxos de trabalho convertidos.  
  
#### <a name="to-create-sharepoint-subsites"></a>Para criar subsites do SharePoint  
  
1. No SharePoint Designer 2010, na barra de menus, escolha **arquivo** > **novo Site em branco**.  
  
2. No **novo Site em branco** caixa de diálogo, navegue até um site do SharePoint onde você deseja criar o fluxo de trabalho, ou use o valor de http://<em>SystemName</em>/ e, em seguida, escolha o **Okey** botão.  
  
    A Home page é exibida.  
  
3. No **Subsites** , escolha o **New** botão.  
  
4. No **New** diálogo caixa, escolha **modelos do SharePoint** da lista no painel esquerdo e escolha **Site de equipe** da lista no painel direito.  
  
5. No **especifique o local do site da Web** caixa, substitua a palavra **subsite** na URL com **SPD1**e, em seguida, escolha o **Okey** botão.  
  
    Isso abre o novo subsite no SharePoint Designer. Fechar esta instância do SharePoint Designer e volte para a primeira instância (o site de nível superior).  
  
6. Repita as etapas 3 a 5 para criar o segundo subsite, desta vez, substituindo a palavra **subsite** na [!INCLUDE[TLA2#tla_url](../sharepoint/includes/tla2sharptla-url-md.md)] com **SPD2**.  
  
## <a name="create-a-sharepoint-designer-reusable-workflow"></a>Criar um fluxo de trabalho reutilizável do SharePoint Designer
 Porque o SharePoint não inclui quaisquer fluxos de trabalho reutilizáveis que você pode usar para este exemplo, você criará um. Esse fluxo de trabalho simple, quando um usuário insere uma nova tarefa na lista de tarefas que tem um título específico, a tarefa é atribuída a esse usuário.  
  
#### <a name="to-create-a-sharepoint-designer-reusable-workflow"></a>Para criar um fluxo de trabalho reutilizável do SharePoint Designer
  
1.  No **Subsites** , escolha o **SPD1** site modificá-lo.  
  
2.  Na faixa de opções, escolha o **fluxo de trabalho reutilizável** botão.  
  
     O assistente criar fluxo de trabalho reutilizável é exibido.  
  
3.  No **nome** , digite **fluxo de trabalho de tarefa SPD**.  
  
4.  No **tipo de conteúdo** , escolha **tarefa**e, em seguida, escolha o **Okey** botão.  
  
     O fluxo de trabalho é aberto no designer de fluxo de trabalho do SharePoint Designer.  
  
5.  No designer de fluxo de trabalho, escolha a etapa 1 e, em seguida, na faixa de opções, escolha o **condição** botão.  
  
6.  Na lista de condições, escolha **se o campo do item atual é igual ao valor**.  
  
     Esta etapa adiciona uma condição que é denominada **se o campo é igual ao valor**.  
  
7.  No **se o campo é igual ao valor** condição, escolha o **campo** link.  
  
8.  Na lista de valores, escolha **título**.  
  
9. No **se o campo é igual ao valor** condição, escolha o **valor** link.  
  
10. Na caixa, digite **nova tarefa**.  
  
     A instrução de condição agora lê **se Current Item: Title é igual a nova tarefa**.  
  
11. Escolha a linha em que a instrução de condição e, em seguida, na faixa de opções, escolha o **ação** botão.  
  
12. Na lista de ações, escolha **conjunto de campo no item atual**.  
  
13. No **campo de conjunto para o valor** ação, escolha o **campo** vincular e, em seguida, na lista, escolha **atribuído ao**.  
  
14. No **campo de conjunto para o valor** ação, escolha o **valor** vincular e, em seguida, na lista de grupos e usuários existentes, escolha **usuário que criou o item**.  
  
15. Escolha o **Add** botão e, em seguida, escolha o **Okey** botão.  
  
     A instrução de ação agora lê **definir atribuído para a atual Item: CreatedBy**.  
  
## <a name="save-and-deploy-the-reusable-workflow"></a>Salvar e implantar o fluxo de trabalho reutilizável
 Porque [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] pode importar somente *wsp* arquivos, você deve salvar o fluxo de trabalho reutilizável, como um *. wsp* de arquivo e implantá-lo no SharePoint antes de importá-lo em [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)].  
  
> [!IMPORTANT]  
>  Se você receber um erro de tempo de execução executar o procedimento a seguir, você precisa executar o procedimento em um sistema que tem acesso ao site do SharePoint.  
  
#### <a name="to-save-and-deploy-the-reusable-workflow"></a>Para salvar e implantar o fluxo de trabalho reutilizável  
  
1.  Na parte superior do SharePoint Designer, escolha o **salvar** botão para salvar seu progresso e, em seguida, escolha o **Publish** botão para implantar o fluxo de trabalho para o **SPD1** site do SharePoint .  
  
2.  No painel de navegação, escolha o **fluxos de trabalho** objeto.  
  
3.  Sob **fluxo de trabalho reutilizável**, escolha **fluxo de trabalho de tarefa SPD**.  
  
4.  Na faixa de opções, escolha o **Salvar como modelo** botão para salvar o fluxo de trabalho como um *wsp* arquivo.  
  
5.  Abra o **SPD1** site do SharePoint em um navegador para exibir o *. wsp* arquivo no SharePoint.  
  
6.  Na barra de início rápido, escolha o **bibliotecas** link.  
  
7.  No **bibliotecas de documentos** , escolha o **ativos de Site** link.  
  
     O **fluxo de trabalho de tarefa SPD** arquivo é listado com outros ativos de site.  
  
8.  Na lista de arquivos, escolha o nome do arquivo  
  
9. No **Download de arquivo** caixa de diálogo, escolha o **salve** botão para salvar o *. wsp* arquivo em seu sistema local.  
  
## <a name="import-the-wsp-file-into-visual-studio"></a>Importar o arquivo. wsp no Visual Studio
 Importar o *. wsp* o arquivo em [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] usando um projeto de fluxo de trabalho reutilizável de importação. Este projeto converte o fluxo de trabalho de um fluxo de trabalho reutilizável e declarativo em um fluxo de trabalho de código. Depois que o fluxo de trabalho é convertido, você usará o código para modificar seu comportamento.  
  
#### <a name="to-import-a-workflow-from-a-wsp-file-and-modify-it"></a>Para importar um fluxo de trabalho a partir de um arquivo .wsp e modificá-lo  
  
1. Na [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)], na barra de menus, escolha **arquivo** > **New** > **projeto**.  
  
2. No **novo projeto** diálogo caixa, expanda o **SharePoint** nó em um **Visual c#** ou **Visual Basic**e, em seguida, escolha o **2010** nó.  
  
3. No **modelos** painel, escolha o **fluxo de trabalho de importação reutilizável do SharePoint 2010** modelo, deixe o nome do projeto como **WorkflowImportProject1**e, em seguida, escolha o **Okey** botão.  
  
    O Assistente para personalização do SharePoint é exibida.  
  
4. Sobre o **especificar o nível de site e segurança para depuração** página, insira o [!INCLUDE[TLA2#tla_url](../sharepoint/includes/tla2sharptla-url-md.md)] para o segundo subsite do SharePoint que você criou anteriormente: http://<em>nome do sistema</em>/SPD2.  
  
5. No **qual é o nível de confiança para essa solução do SharePoint?** , escolha o **implantar como uma solução de farm** botão de opção e, em seguida, escolha o **próxima** botão.  
  
    Para obter mais informações sobre a área restrita em comparação com soluções de farm, consulte [considerações sobre a solução em área restrita](../sharepoint/sandboxed-solution-considerations.md).  
  
6. No **especifique a nova origem do projeto** página, navegue até o local no sistema onde você salvou anteriormente a *. wsp* do arquivo, abra o arquivo e, em seguida, escolha o **próxima** botão.  
  
   > [!NOTE]  
   >  Escolha o **terminar** botão para importar todos os itens disponíveis na *. wsp* arquivo.  
  
    Isso exibe uma lista de fluxos de trabalho reutilizáveis disponíveis para a importação.  
  
7. No **selecionar itens para importar** , escolha o **fluxo de trabalho de tarefa SPD** fluxo de trabalho e, em seguida, escolha o **concluir** botão.  
  
    Depois que a operação de importação for concluída, um projeto chamado **WorkflowImportProject1** é criado contendo um fluxo de trabalho denominado **SPD_Workflow_TestFT**. Essa pasta é o arquivo de definição do fluxo de trabalho *Elements. XML* e o arquivo de designer de fluxo de trabalho (*xoml*). O designer contém dois arquivos: o arquivo de regras (. Rules) e o arquivo code-behind (qualquer um dos *. CS* ou *. vb*, dependendo da linguagem de programação do projeto).  
  
8. Na **Gerenciador de soluções**, exclua o **outros arquivos importados** pasta.  
  
9. No *Elements. XML* do arquivo, excluir `InstantiationURL="_layouts/IniErkflIP.sspx"`.  
  
10. Na **Gerenciador de soluções**, escolha **WorkflowImportProject1**e em seguida, na barra de menus, escolha **projeto** > **definir como projeto de inicialização**  para definir **WorkflowImportProject1** como o Item de inicialização.  
  
     Isso exibe a lista imediatamente quando você depurar o projeto.  
  
11. Porque o **importação do SharePoint 2010 fluxo de trabalho reutilizável** modelo não importa os valores de propriedade de associação para o fluxo de trabalho importado, você deverá inseri-los. Para fazer isso:  
  
    1.  Na **Gerenciador de soluções**, escolha o **SPD_Workflow_TestFT** nó.  
  
    2.  Escolha as reticências (![elipse do Designer de dispositivo móvel do ASP.NET](../sharepoint/media/mwellipsis.gif "elipse do Designer de dispositivo móvel do ASP.NET")) botão ao lado de uma lista de propriedades, como o **lista destino** propriedade.  
  
    3.  Preencha os valores ausentes no Assistente de personalização do SharePoint e, em seguida, escolha o **concluir** botão.  
  
12. Escolha o arquivo. xoml e, em seguida, na barra de menus, escolha **modo de exibição** > **Designer** para exibir o fluxo de trabalho importado no designer de fluxo de trabalho.  
  
13. No **Windows Workflow v3.0** nó do **caixa de ferramentas**, execute uma das seguintes etapas:  
  
    - Abra o menu de atalho para o **código** atividade e, em seguida, escolha **cópia**. No designer de fluxo de trabalho, abra o menu de atalho para a linha sob o **SequenceActivity1** atividade e, em seguida, escolha **colar**.  
  
    - Arraste o **código** atividade da **caixa de ferramentas** para o designer de fluxo de trabalho e conectá-lo para a linha no **SequenceActivity1** atividade.  
  
      Isso adiciona uma atividade para o designer de fluxo de trabalho chamado **CodeActivity1**. Essa atividade, você adicionará uma ação de código que cria um comunicado da lista anúncios quando o usuário inicia o fluxo de trabalho.  
  
14. Realize um dos seguintes conjuntos de etapas:  
  
    -   Clique duas vezes em **CodeActivity1** para gerar um manipulador de eventos e exibir o código.  
  
    -   No **propriedades** janela para **CodeActivity1**, defina o valor da **ExecuteCode** propriedade **codeActivity_ExecuteCode**.  
  
15. Adicione o seguinte em existente **usando** ou **Imports** instruções:  
  
     [!code-csharp[SP_SPDWFImport#1](../sharepoint/codesnippet/CSharp/workflowimportproject1/workflows/spd_task_workflowft/spd task workflow.xoml.cs#1)]
     [!code-vb[SP_SPDWFImport#1](../sharepoint/codesnippet/VisualBasic/workflowimportproject1/workflows/spd_task_workflowft/spd task workflow.xoml.vb#1)]  
  
16. Substitua `codeActivity1_ExecuteCode` com o seguinte:  
  
     [!code-csharp[SP_SPDWFImport#2](../sharepoint/codesnippet/CSharp/workflowimportproject1/workflows/spd_task_workflowft/spd task workflow.xoml.cs#2)]
     [!code-vb[SP_SPDWFImport#2](../sharepoint/codesnippet/VisualBasic/workflowimportproject1/workflows/spd_task_workflowft/spd task workflow.xoml.vb#2)]  
  
## <a name="deploy-the-project-and-associate-the-workflow"></a>Implantar o projeto e associar o fluxo de trabalho
 Em seguida, executar WorkflowImportProject1 para implantá-lo em um site do SharePoint e associar o fluxo de trabalho com a lista de tarefas para exibir e testar a modificação, convertidos em fluxo de trabalho.  
  
#### <a name="to-deploy-the-project-and-associate-the-workflow"></a>Para implantar o projeto e associar o fluxo de trabalho  
  
1.  Na [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)], escolha o **F5** tecla para executar e implantar o projeto de fluxo de trabalho convertido.  
  
2.  Na barra de início rápido, escolha o **tarefas** link para exibir a lista de tarefas.  
  
3.  Sobre o **ferramentas de lista** guia, escolha o **itens** botão e, em seguida, escolha o **Novo Item** botão.  
  
     O **tarefas - Novo Item** caixa de diálogo é aberta.  
  
4.  No **Title** , digite **nova tarefa**e, em seguida, escolha o **salvar** botão.  
  
5.  Sobre o **ferramentas de lista** guia, escolha o **lista** botão e, em seguida, escolha o **as configurações da lista** botão.  
  
     O **as configurações da lista** página será exibida.  
  
6.  No **permissões e gerenciamento** , escolha o **configurações de fluxo de trabalho** link.  
  
     O **configurações de fluxo de trabalho** página será exibida.  
  
7.  Escolha o **adicionar um fluxo de trabalho** link.  
  
8.  No **fluxo de trabalho** , escolha **WorkflowImportProject1 - teste de fluxo de trabalho SPD**.  
  
9. No **nome** , digite **teste de fluxo de trabalho SPD**e, em seguida, escolha o **Okey** botão.  
  
10. Na barra de início rápido, escolha o **tarefas** lista.  
  
11. Escolha a seta ao lado **nova tarefa**e em seguida, na lista, escolha **fluxos de trabalho**.  
  
12. No **iniciar um novo fluxo de trabalho** , escolha o link para **teste de fluxo de trabalho SPD**e, em seguida, escolha o **iniciar** botão para iniciar o fluxo de trabalho.  
  
    > [!NOTE]  
    >  Como alternativa, você pode auto-associação um fluxo de trabalho com uma lista executando o Assistente de configurações de fluxo de trabalho e definindo o fluxo de trabalho para associar automaticamente.  
  
     Observe que duas ações são executadas pelo fluxo de trabalho: seu nome é exibido na tarefa de **atribuído a** coluna e um aviso será exibida a **anúncios** lista.  
  
## <a name="see-also"></a>Consulte também
 [Importar itens de um site do SharePoint existente](../sharepoint/importing-items-from-an-existing-sharepoint-site.md)   
 [Desenvolver soluções do SharePoint](../sharepoint/developing-sharepoint-solutions.md)   
 [Criar controles reutilizáveis para web parts ou páginas de aplicativo](../sharepoint/creating-reusable-controls-for-web-parts-or-application-pages.md)  
  
