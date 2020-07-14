---
title: 'Walkthrough: importar um fluxo de trabalho reutilizável do SharePoint Designer para o Visual Studio | Microsoft Docs'
ms.date: 02/02/2017
ms.topic: how-to
f1_keywords:
- VS.SharePointTools.WSPImport.ImportWF
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, importing reusable workflows
- reusable workflows [SharePoint development in Visual Studio]
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 6a589f14ea60d50c0062d85be81523f27c81b455
ms.sourcegitcommit: f9e44f5ab6a1dfb56c945c9986730465e1adb6fc
ms.contentlocale: pt-BR
ms.lasthandoff: 07/06/2020
ms.locfileid: "86015701"
---
# <a name="walkthrough-import-a-sharepoint-designer-reusable-workflow-into-visual-studio"></a>Walkthrough: importar um fluxo de trabalho reutilizável do SharePoint Designer para o Visual Studio
  Este tutorial demonstra como importar um fluxo de trabalho reutilizável criado no SharePoint Designer 2010 para um [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] projeto de fluxo de trabalho do SharePoint.

 Os fluxos de trabalho criados no SharePoint Designer, ou *fluxos de trabalho declarativos*, consistem em [!INCLUDE[TLA2#tla_xml](../sharepoint/includes/tla2sharptla-xml-md.md)] instruções em vez de código. O SharePoint Designer 2010 apresenta fluxos de trabalho *reutilizáveis*, que são fluxos de trabalho portáteis e declarativos que podem ser usados por listas diferentes em sites do SharePoint.

 Os fluxos de trabalho criados no [!INCLUDE[vs_dev11_long](../sharepoint/includes/vs-dev11-long-md.md)] , como fluxos de trabalho de máquina de estado e sequenciais, são chamados de *fluxos de trabalho de código*. Os fluxos de trabalho de código consistem em arquivos XML e módulos de código nos quais os usuários podem personalizar o comportamento do fluxo de trabalho.

 O Visual Studio permite que você importe fluxos de trabalho reutilizáveis criados no SharePoint Designer 2010 e converta-os em fluxos de trabalho de código para uso em seus sites do SharePoint.

 Este tutorial demonstra as seguintes tarefas:

- Criar um fluxo de trabalho simples e reutilizável no SharePoint Designer.

- Exportar o fluxo de trabalho reutilizável do SharePoint Designer para um arquivo *. wsp* e para o SharePoint.

- Importando o arquivo *. wsp* no usando [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] o projeto importar fluxo de trabalho reutilizável.

- Alterando o fluxo de trabalho adicionando código.

- Usando o fluxo de trabalho importado em um site do SharePoint.

  [!INCLUDE[note_settings_general](../sharepoint/includes/note-settings-general-md.md)]

## <a name="prerequisites"></a>Pré-requisitos
 Você precisará dos seguintes componentes para concluir este passo a passo:

- Edições com suporte do [!INCLUDE[TLA#tla_win](../sharepoint/includes/tlasharptla-win-md.md)] e SharePoint.

- Visual Studio.

- Microsoft [!INCLUDE[TLA2#tla_office](../sharepoint/includes/tla2sharptla-office-md.md)] SharePoint Designer 2010.

## <a name="create-target-sharepoint-subsites"></a>Criar subsites do SharePoint de destino
 Primeiro, você cria dois novos subsites do SharePoint: um para hospedar os fluxos de trabalho reutilizáveis do SharePoint Designer, outro para hospedar os fluxos de trabalho convertidos.

#### <a name="to-create-sharepoint-subsites"></a>Para criar subsites do SharePoint

1. No SharePoint Designer 2010, na barra de menus, escolha **arquivo**  >  **novo site em branco**.

2. Na caixa de diálogo **novo site em branco** , navegue até um site do SharePoint no qual você deseja criar o fluxo de trabalho ou use o valor de http://<em>SystemName</em>/e, em seguida, escolha o botão **OK** .

    A Home Page é exibida.

3. Na seção **subsites** , escolha o botão **novo** .

4. Na caixa de diálogo **novo** , escolha **modelos do SharePoint** na lista no painel esquerdo e escolha site de **equipe** na lista no painel à direita.

5. Na caixa **especificar o local do site** , substitua o **subsite** do Word na URL por **SPD1**e, em seguida, escolha o botão **OK** .

    Isso abre o novo subsite no SharePoint Designer. Feche esta instância do SharePoint Designer e volte para a primeira instância (o site de nível superior).

6. Repita as etapas 3-5 para criar o segundo subsite, desta vez substituindo o **subsite** do Word no [!INCLUDE[TLA2#tla_url](../sharepoint/includes/tla2sharptla-url-md.md)] com **SPD2**.

## <a name="create-a-sharepoint-designer-reusable-workflow"></a>Criar um fluxo de trabalho reutilizável do SharePoint Designer
 Como o SharePoint não inclui nenhum fluxo de trabalho reutilizável que você possa usar para este exemplo, você criará um. Nesse fluxo de trabalho simples, quando um usuário insere uma nova tarefa na lista de tarefas que tem um título específico, a tarefa é atribuída a esse usuário.

#### <a name="to-create-a-sharepoint-designer-reusable-workflow"></a>Para criar um fluxo de trabalho reutilizável do SharePoint Designer

1. Na seção **subsites** , escolha o site **SPD1** para modificá-lo.

2. Na faixa de seleção, escolha o botão de **fluxo de trabalho reutilizável** .

     O assistente para criar fluxo de trabalho reutilizável é exibido.

3. Na caixa **nome** , insira **fluxo de trabalho da tarefa SPD**.

4. Na lista **tipo de conteúdo** , escolha **tarefa**e, em seguida, escolha o botão **OK** .

     O fluxo de trabalho é aberto no designer de fluxo de trabalho do SharePoint Designer.

5. No designer de fluxo de trabalho, escolha etapa 1 e, na faixa de seleção, escolha o botão **condição** .

6. Na lista de condições, escolha **se campo item atual é igual a valor**.

     Esta etapa adiciona uma condição que é nomeada **se o campo for igual a valor**.

7. No **campo se for igual** a condição de valor, escolha o link do **campo** .

8. Na lista de valores, escolha **título**.

9. No **campo se for igual** a condição de valor, escolha o link **valor** .

10. Na caixa, digite **nova tarefa**.

     A instrução Condition agora lê **se o item atual: title é igual a nova tarefa**.

11. Escolha a linha sob a instrução condição e, em seguida, na faixa de seleção, escolha o botão **ação** .

12. Na lista de ações, escolha **definir campo no item atual**.

13. Na ação **definir campo para valor** , escolha o link do **campo** e, em seguida, na lista, escolha **atribuído a**.

14. Na ação **definir campo para valor** , escolha o link **valor** e, em seguida, na lista de usuários e grupos existentes, escolha **usuário que criou o item**.

15. Escolha o botão **Adicionar** e, em seguida, escolha o botão **OK** .

     A instrução de ação agora lê o **conjunto atribuído ao item atual: CreatedBy**.

## <a name="save-and-deploy-the-reusable-workflow"></a>Salvar e implantar o fluxo de trabalho reutilizável
 Como [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] o pode importar somente arquivos *. wsp* , você deve salvar o fluxo de trabalho reutilizável como um arquivo *. wsp* e implantá-lo no SharePoint antes de importá-lo para o [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] .

> [!IMPORTANT]
> Se você receber um erro de tempo de execução executando o procedimento a seguir, será necessário executar o procedimento em um sistema que tenha acesso ao site do SharePoint.

#### <a name="to-save-and-deploy-the-reusable-workflow"></a>Para salvar e implantar o fluxo de trabalho reutilizável

1. Na parte superior do SharePoint Designer, escolha o botão **salvar** para salvar seu progresso e, em seguida, escolha o botão **publicar** para implantar o fluxo de trabalho no site do SharePoint do **SPD1** .

2. No painel de navegação, escolha o objeto **fluxos de trabalho** .

3. Em **fluxo de trabalho reutilizável**, escolha **fluxo de trabalho da tarefa SPD**.

4. Na faixa de seleção, escolha o botão **salvar como modelo** para salvar o fluxo de trabalho como um arquivo *. wsp* .

5. Abra o site do SharePoint do **SPD1** em um navegador para exibir o arquivo *. wsp* no SharePoint.

6. Na barra de início rápido, escolha o link **bibliotecas** .

7. Na seção **bibliotecas de documentos** , escolha o link **ativos do site** .

     O arquivo de **fluxo de trabalho da tarefa SPD** é listado com outros ativos do site.

8. Na lista de arquivos, escolha o nome desse arquivo

9. Na caixa de diálogo **download de arquivo** , escolha o botão **salvar** para salvar o arquivo *. wsp* no sistema local.

## <a name="import-the-wsp-file-into-visual-studio"></a>Importar o arquivo. wsp para o Visual Studio
 Importe o arquivo *. wsp* no usando [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] um projeto de fluxo de trabalho de importação reutilizável. Este projeto converte o fluxo de trabalho de um fluxo de trabalho reutilizável e declarativo em um fluxo de trabalho de código. Depois que o fluxo de trabalho for convertido, você usará o código para modificar seu comportamento.

#### <a name="to-import-a-workflow-from-a-wsp-file-and-modify-it"></a>Para importar um fluxo de trabalho a partir de um arquivo .wsp e modificá-lo

1. No [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] , na barra de menus, escolha **arquivo**  >  **novo**  >  **projeto**.

2. Na caixa de diálogo **novo projeto** , expanda o nó do **SharePoint** em **Visual C#** ou **Visual Basic**e, em seguida, escolha o nó **2010** .

3. No painel **modelos** , escolha o modelo **importar fluxo de trabalho do SharePoint 2010 reutilizável** , deixe o nome do projeto como **WorkflowImportProject1**e, em seguida, escolha o botão **OK** .

    O assistente para personalização do SharePoint é exibido.

4. Na página **especificar o site e o nível de segurança para depuração** , insira o [!INCLUDE[TLA2#tla_url](../sharepoint/includes/tla2sharptla-url-md.md)] para o segundo subsite do SharePoint que você criou anteriormente: http://<em>nome do sistema</em>/SPD2.

5. Na seção **o que é o nível de confiança para esta solução do SharePoint?** , escolha o botão de opção **implantar como uma solução de farm** e, em seguida, escolha o botão **Avançar** .

    Para obter mais informações sobre soluções de farm em área restrita, consulte [Considerações sobre a solução em área restrita](../sharepoint/sandboxed-solution-considerations.md).

6. Na página **especificar a nova origem do projeto** , navegue até o local no sistema em que você salvou o arquivo *. wsp* anteriormente, abra o arquivo e, em seguida, escolha o botão **Avançar** .

   > [!NOTE]
   > Escolha o botão **concluir** para importar todos os itens disponíveis no arquivo *. wsp* .

    Isso exibe uma lista de fluxos de trabalho reutilizáveis disponíveis para importação.

7. Na caixa **selecionar itens a serem importados** , escolha o fluxo de trabalho do fluxo de trabalho **tarefa SPD** e escolha o botão **concluir** .

    Depois que a operação de importação for concluída, um projeto chamado **WorkflowImportProject1** será criado contendo um fluxo de trabalho chamado **SPD_Workflow_TestFT**. Nessa pasta está o arquivo de definição do fluxo de trabalho *Elements.xml* e o arquivo do designer de fluxo de trabalho (*. xoml*). O designer contém dois arquivos: o arquivo de regras (. Rules) e o arquivo code-behind ( *. cs* ou *. vb*, dependendo da linguagem de programação do seu projeto).

8. Em **Gerenciador de soluções**, exclua a pasta **outros arquivos importados** .

9. No arquivo *Elements.xml* , exclua `InstantiationURL="_layouts/IniErkflIP.sspx"` .

10. Em **Gerenciador de soluções**, escolha **WorkflowImportProject1**e, na barra de menus, escolha **projeto**  >  **definido como projeto de inicialização** para definir **WorkflowImportProject1** como o item de inicialização.

     Isso exibe a lista imediatamente quando você depura o projeto.

11. Como o modelo **importar fluxo de trabalho do SharePoint 2010** não importa os valores de propriedade de associação para o fluxo de trabalho importado, você deve inseri-los. Para fazer isso:

    1. Em **Gerenciador de soluções**, escolha o nó **SPD_Workflow_TestFT** .

    2. Escolha o botão de reticências (![elipse do designer móvel ASP.net](../sharepoint/media/mwellipsis.gif "Elipse do designer móvel ASP.NET")) ao lado de uma das propriedades da lista, como a propriedade da **lista de destino** .

    3. Preencha os valores ausentes no Assistente para personalização do SharePoint e, em seguida, escolha o botão **concluir** .

12. Escolha o arquivo. xoml e, na barra de menus, escolha Designer de **exibição**  >  **Designer** para exibir o fluxo de trabalho importado no designer de fluxo de trabalho.

13. No nó **Windows Workflow v 3.0** da caixa de **ferramentas**, execute uma das seguintes etapas:

    - Abra o menu de atalho para a atividade de **código** e escolha **copiar**. No designer de fluxo de trabalho, abra o menu de atalho da linha sob a atividade **SequenceActivity1** e escolha **colar**.

    - Arraste a atividade de **código** da **caixa de ferramentas** para o designer de fluxo de trabalho e conecte-a à linha sob a atividade **SequenceActivity1** .

      Isso adiciona uma atividade ao designer de fluxo de trabalho chamado **CodeActivity1**. Nessa atividade, você adicionará uma ação de código que cria um comunicado na lista comunicados quando o usuário inicia o fluxo de trabalho.

14. Realize um dos seguintes conjuntos de etapas:

    - Clique duas vezes em **CodeActivity1** para gerar um manipulador de eventos e exibir o código.

    - Na janela **Propriedades** de **CodeActivity1**, defina o valor da propriedade **ExecuteCode** como **codeActivity_ExecuteCode**.

15. Adicione o seguinte nas diretivas **usando** ou **Imports** existentes:

     [!code-csharp[SP_SPDWFImport#1](../sharepoint/codesnippet/CSharp/workflowimportproject1/workflows/spd_task_workflowft/spd task workflow.xoml.cs#1)]
     [!code-vb[SP_SPDWFImport#1](../sharepoint/codesnippet/VisualBasic/workflowimportproject1/workflows/spd_task_workflowft/spd task workflow.xoml.vb#1)]

16. Substitua `codeActivity1_ExecuteCode` pelo seguinte:

     [!code-csharp[SP_SPDWFImport#2](../sharepoint/codesnippet/CSharp/workflowimportproject1/workflows/spd_task_workflowft/spd task workflow.xoml.cs#2)]
     [!code-vb[SP_SPDWFImport#2](../sharepoint/codesnippet/VisualBasic/workflowimportproject1/workflows/spd_task_workflowft/spd task workflow.xoml.vb#2)]

## <a name="deploy-the-project-and-associate-the-workflow"></a>Implantar o projeto e associar o fluxo de trabalho
 Em seguida, execute WorkflowImportProject1 para implantá-lo em um site do SharePoint e associe o fluxo de trabalho à lista de tarefas para exibir e testar o fluxo de trabalho modificado e convertido.

#### <a name="to-deploy-the-project-and-associate-the-workflow"></a>Para implantar o projeto e associar o fluxo de trabalho

1. No [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] , escolha a tecla **F5** para executar e implantar o projeto de fluxo de trabalho convertido.

2. Na barra de início rápido, escolha o link **tarefas** para exibir a lista de tarefas.

3. Na guia **ferramentas de lista** , escolha o botão **itens** e, em seguida, escolha o botão **novo item** .

     A caixa de diálogo **tarefas – novo item** é aberta.

4. Na caixa **título** , digite **nova tarefa**e, em seguida, escolha o botão **salvar** .

5. Na guia **ferramentas de lista** , escolha o botão **lista** e, em seguida, escolha o botão **configurações de lista** .

     A página **configurações da lista** é exibida.

6. Na seção **permissões e gerenciamento** , escolha o link **configurações de fluxo de trabalho** .

     A página **configurações de fluxo de trabalho** é exibida.

7. Escolha o link **Adicionar um fluxo de trabalho** .

8. Na lista **fluxo de trabalho** , escolha **teste de fluxo de trabalho WorkflowImportProject1-SPD**.

9. Na caixa **nome** , insira **teste de fluxo de trabalho SPD**e, em seguida, escolha o botão **OK** .

10. Na barra de início rápido, escolha a lista **tarefas** .

11. Escolha a seta ao lado de **nova tarefa**e, em seguida, na lista, escolha **fluxos de trabalho**.

12. Na seção **Iniciar um novo fluxo de trabalho** , escolha o link para **teste de fluxo de trabalho SPD**e, em seguida, escolha o botão **Iniciar** para iniciar o fluxo de trabalho.

    > [!NOTE]
    > Como alternativa, você pode associar automaticamente um fluxo de trabalho a uma lista executando o assistente de configurações de fluxo de trabalho e definindo o fluxo de trabalho para associar automaticamente.

     Observe que duas ações são executadas pelo fluxo de trabalho: seu nome aparece na coluna **atribuído à** tarefa e um anúncio é exibido na lista **comunicados** .

## <a name="see-also"></a>Consulte também
- [Importar itens de um site existente do SharePoint](../sharepoint/importing-items-from-an-existing-sharepoint-site.md)
- [Desenvolver soluções do SharePoint](../sharepoint/developing-sharepoint-solutions.md)
- [Criar controles reutilizáveis para Web Parts ou páginas de aplicativo](../sharepoint/creating-reusable-controls-for-web-parts-or-application-pages.md)
