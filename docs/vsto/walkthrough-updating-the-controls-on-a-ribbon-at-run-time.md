---
title: 'Explicação passo a passo: Os controles em uma faixa de opções em tempo de execução de atualização'
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- controls [Office development in Visual Studio], Ribbon
- Ribbon [Office development in Visual Studio], controls
- updating Ribbon controls
- Ribbon [Office development in Visual Studio], dynamic menu
- dynamic menus [Office development in Visual Studio]
- Ribbon [Office development in Visual Studio], updating
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: 40072b1dcd6b24f552a3c87c8241ea4498229053
ms.sourcegitcommit: dd839de3aa24ed7cd69f676293648c6c59c6560a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/27/2018
ms.locfileid: "52389144"
---
# <a name="walkthrough-update-the-controls-on-a-ribbon-at-runtime"></a>Explicação passo a passo: Os controles em uma faixa de opções em tempo de execução de atualização

Este passo a passo demonstra como usar o modelo de objeto da faixa de opções para atualizar os controles em uma faixa de opções, depois que a faixa de opções é carregada no aplicativo do Office.

[!INCLUDE[appliesto_ribbon](../vsto/includes/appliesto-ribbon-md.md)]

O exemplo recebe dados do banco de dados de exemplo Northwind para preencher uma caixa de combinação e menu no Microsoft Office Outlook. Itens que você selecione nesses controles automaticamente preencher os campos, como **à** e **assunto** em uma mensagem de email.

Esta explicação passo a passo ilustra as seguintes tarefas:

-   Crie um novo projeto de suplemento do VSTO do Outlook.

-   Crie um grupo de faixa de opções personalizado.

-   Adicione o grupo personalizado a uma guia interna.

-   Atualize controles na faixa de opções em tempo de execução.

> [!NOTE]
> Seu computador pode mostrar diferentes nomes ou locais para alguns dos elementos de interface do usuário do Visual Studio nas instruções a seguir. A edição do Visual Studio que você possui e as configurações que você usa determinam esses elementos. Para obter mais informações, confira [Personalizar o IDE do Visual Studio](../ide/personalizing-the-visual-studio-ide.md).

## <a name="prerequisites"></a>Pré-requisitos

Você precisa dos seguintes componentes para concluir esta instrução passo a passo:

-   [!INCLUDE[vsto_vsprereq](../vsto/includes/vsto-vsprereq-md.md)]

-   Microsoft Outlook

## <a name="create-a-new-outlook-vsto-add-in-project"></a>Criar um novo projeto de suplemento do VSTO do Outlook

Primeiro, crie um projeto de suplemento do VSTO do Outlook.

### <a name="to-create-a-new-outlook-vsto-add-in-project"></a>Para criar um novo projeto de suplemento do VSTO do Outlook

1.  Na [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)], crie um projeto de suplemento do VSTO do Outlook com o nome **Ribbon_Update_At_Runtime**.

2.  No **novo projeto** caixa de diálogo, selecione **criar diretório para solução**.

3.  Salve o projeto no diretório de projeto padrão.

     Para obter mais informações, consulte [como: projetos do Office de criar no Visual Studio](../vsto/how-to-create-office-projects-in-visual-studio.md).

## <a name="design-a-custom-ribbon-group"></a>Criar um grupo de faixa de opções personalizado

A faixa de opções para este exemplo será exibido quando um usuário compõe uma nova mensagem de email. Para criar um grupo personalizado para a faixa de opções, primeiro adicione um item da faixa de opções ao seu projeto e, em seguida, o grupo no Designer de faixa de opções de design. Este grupo personalizado ajudará você a gerar mensagens de email de acompanhamento para os clientes, efetuando o pull de nomes e ordenar os históricos de um banco de dados.

### <a name="to-design-a-custom-group"></a>Para criar um grupo personalizado

1.  No menu **Projeto**, clique em **Adicionar Novo Item**.

2.  No **Adicionar Novo Item** caixa de diálogo, selecione **faixa de opções (Visual Designer)**.

3.  Altere o nome da nova faixa de opções para **CustomerRibbon**e, em seguida, clique em **Add**.

     O *CustomerRibbon.cs* ou *CustomerRibbon.vb* arquivo é aberto no Designer de faixa de opções e exibe um guia padrão e um grupo.

4.  Clique para selecioná-lo, o Designer de faixa de opções.

5.  No **propriedades** janela, clique na seta suspensa ao lado de **RibbonType** propriedade e clique **Microsoft.Outlook.Mail.Compose**.

     Isso permite que a faixa de opções que aparecem quando o usuário compõe uma nova mensagem de email no Outlook.

6.  No Designer de faixa de opções, clique em **Group1** para selecioná-lo.

7.  No **propriedades** janela, defina **rótulo** para **compras do cliente**.

8.  Do **controles de faixa de opções do Office** guia da **caixa de ferramentas**, arraste uma **ComboBox** até o **compras do cliente** grupo.

9. Clique em **ComboBox1** para selecioná-lo.

10. No **propriedades** janela, defina **rótulo** para **clientes**.

11. Do **controles de faixa de opções do Office** guia da **caixa de ferramentas**, arraste uma **Menu** até o **compras do cliente** grupo.

12. No **propriedades** janela, defina **rótulo** para **produto comprado**.

13. Definir **dinâmica** à **verdadeiro**.

     Isso permite que você adicione e remova os controles no menu no tempo de execução depois que a faixa de opções é carregada no aplicativo do Office.

## <a name="add-the-custom-group-to-a-built-in-tab"></a>Adicionar o grupo personalizado a uma guia interna

Uma guia interna é uma guia que já está na faixa de opções do Outlook Explorer ou Inspector. Neste procedimento, você adiciona o grupo personalizado a uma guia interna e, em seguida, especificar a posição do grupo personalizado na guia.

### <a name="to-add-the-custom-group-to-a-built-in-tab"></a>Para adicionar o grupo personalizado a uma guia interna

1.  Clique o **TabAddins (interno)** tab para selecioná-lo.

2.  No **propriedades** janela, expanda o **ControlId** propriedade e, em seguida, defina **OfficeId** para **TabNewMailMessage**.

     Isso adiciona o **compras do cliente** grupo para o **mensagens** guia da faixa de opções que aparece em uma nova mensagem de email.

3.  Clique o **compras do cliente** grupo para selecioná-lo.

4.  No **propriedades** janela, expanda o **posição** propriedade, clique na seta suspensa ao lado de **PositionType** propriedade e, em seguida, clique  **BeforeOfficeId**.

5.  Defina as **OfficeId** propriedade **GroupClipboard**.

     Isso posiciona o **compras do cliente** grupo antes do **área de transferência** grupo dos **mensagens** guia.

## <a name="create-the-data-source"></a>Criar a fonte de dados

Use o **fontes de dados** janela para adicionar um conjunto de dados tipado ao seu projeto.

### <a name="to-create-the-data-source"></a>Para criar a fonte de dados

1.  Sobre o **dados** menu, clique em **Add New Data Source**.

     Isso inicia o **Data Source Configuration Wizard**.

2.  Selecione **banco de dados**e, em seguida, clique em **próxima**.

3.  Selecione **Dataset**e, em seguida, clique em **próxima**.

4.  Selecione uma conexão de dados para o banco de dados do Microsoft SQL Server Compact 4.0 de exemplo Northwind, ou adicionar uma nova conexão usando o **nova Conexão** botão.

5.  Depois que uma conexão foi selecionado ou criado, clique em **próxima**.

6.  Clique em **próxima** para salvar a cadeia de conexão.

7.  Sobre o **Choose Your Database Objects** página, expanda **tabelas**.

8.  Marque a caixa de seleção ao lado de cada uma das seguintes tabelas:

    1.  **Clientes**

    2.  **Detalhes do pedido**

    3.  **Pedidos**

    4.  **Produtos**

9. Clique em **Finalizar**.

## <a name="update-controls-in-the-custom-group-at-runtime"></a>Atualizar controles no grupo personalizado em tempo de execução

Use o modelo de objeto da faixa de opções para executar as seguintes tarefas:

-   Adicionar nomes de cliente para o **clientes** caixa de combinação.

-   Adicionar controles menu e o botão para o **produtos comprados** menu que representam pedidos de vendas e produtos vendidos.

-   Popular para, assunto e corpo campos de novas mensagens de email usando dados das **clientes** caixa de combinação e **produtos comprados** menu.

### <a name="to-update-controls-in-the-custom-group-by-using-the-ribbon-object-model"></a>Para atualizar os controles no grupo personalizado usando o modelo de objeto da faixa de opções

1. No menu **Projeto**, clique em **Adicionar Referência**.

2. No **adicionar referência** caixa de diálogo, clique o **.NET** guia, selecione o **System** assembly e depois clique em **Okey**.

    Esse assembly contém classes para usar consultas integrada à linguagem (LINQ). Você usará o LINQ para popular os controles no grupo personalizado com os dados do banco de dados Northwind.

3. Na **Gerenciador de soluções**, clique em **CustomerRibbon.cs** ou **CustomerRibbon.vb** para selecioná-lo.

4. Sobre o **modo de exibição** menu, clique em **código**.

    O arquivo de código da faixa de opções é aberto no Editor de códigos.

5. Adicione as seguintes instruções à parte superior do arquivo de código da faixa de opções. Estas instruções fornecem acesso fácil aos namespaces do LINQ e ao namespace a assembly de interoperabilidade primária (PIA) do Outlook.

    [!code-csharp[Trin_Ribbon_Update_At_Runtime#1](../vsto/codesnippet/CSharp/Ribbon_Update_At_Runtime/CustomerRibbon.cs#1)]
    [!code-vb[Trin_Ribbon_Update_At_Runtime#1](../vsto/codesnippet/VisualBasic/Ribbon_Update_At_Runtime/CustomerRibbon.vb#1)]

6. Adicione o seguinte código dentro de `CustomerRibbon` classe. Esse código declara a tabela de dados e adaptadores de tabela que você usará para armazenar informações do cliente, pedidos, detalhes do pedido e tabelas de produtos do banco de dados Northwind.

    [!code-csharp[Trin_Ribbon_Update_At_Runtime#2](../vsto/codesnippet/CSharp/Ribbon_Update_At_Runtime/CustomerRibbon.cs#2)]
    [!code-vb[Trin_Ribbon_Update_At_Runtime#2](../vsto/codesnippet/VisualBasic/Ribbon_Update_At_Runtime/CustomerRibbon.vb#2)]

7. Adicione o seguinte bloco de código para o `CustomerRibbon` classe. Esse código adiciona três métodos auxiliares que criar controles para a faixa de opções em tempo de execução.

    [!code-csharp[Trin_Ribbon_Update_At_Runtime#3](../vsto/codesnippet/CSharp/Ribbon_Update_At_Runtime/CustomerRibbon.cs#3)]
    [!code-vb[Trin_Ribbon_Update_At_Runtime#3](../vsto/codesnippet/VisualBasic/Ribbon_Update_At_Runtime/CustomerRibbon.vb#3)]

8. Substitua o `CustomerRibbon_Load` método do manipulador de eventos com o código a seguir. Esse código usa uma consulta LINQ para executar as seguintes tarefas:

   - Popular o **clientes** caixa de combinação usando a ID e nome de 20 clientes no banco de dados Northwind.

   - Chamadas a `PopulateSalesOrderInfo` método auxiliar. Esse método atualiza o **ProductsPurchased** menu com números de ordem de venda que pertencem ao cliente selecionado no momento.

     [!code-csharp[Trin_Ribbon_Update_At_Runtime#4](../vsto/codesnippet/CSharp/Ribbon_Update_At_Runtime/CustomerRibbon.cs#4)]
     [!code-vb[Trin_Ribbon_Update_At_Runtime#4](../vsto/codesnippet/VisualBasic/Ribbon_Update_At_Runtime/CustomerRibbon.vb#4)]

9. Adicione o seguinte código para o `CustomerRibbon` classe. Esse código usa consultas LINQ para executar as seguintes tarefas:

   - Adiciona um submenu para o **ProductsPurchased** menu para cada ordem de venda relacionadas ao cliente selecionado.

   - Adiciona botões cada submenu para os produtos relacionados à ordem de venda.

   - Adiciona manipuladores de eventos para cada botão.

     [!code-csharp[Trin_Ribbon_Update_At_Runtime#6](../vsto/codesnippet/CSharp/Ribbon_Update_At_Runtime/CustomerRibbon.cs#6)]
     [!code-vb[Trin_Ribbon_Update_At_Runtime#6](../vsto/codesnippet/VisualBasic/Ribbon_Update_At_Runtime/CustomerRibbon.vb#6)]

10. Na **Gerenciador de soluções**, clique duas vezes no arquivo de código da faixa de opções.

     Abre o Designer de faixa de opções.

11. No Designer de faixa de opções, clique duas vezes o **clientes** caixa de combinação.

     O arquivo de código da faixa de opções é aberto no Editor de códigos e o `ComboBox1_TextChanged` manipulador de eventos é exibida.

12. Substitua o `ComboBox1_TextChanged` manipulador de eventos com o código a seguir. Esse código executa as seguintes tarefas:

    - Chamadas a `PopulateSalesOrderInfo` método auxiliar. Esse método atualiza o **produtos comprados** menu com ordens de venda relacionadas ao cliente selecionado.

    - Chamadas a `PopulateMailItem` método auxiliar e passa o texto atual, que é o nome do cliente selecionado. Esse método popula para, assunto e corpo campos de novas mensagens de email.

      [!code-csharp[Trin_Ribbon_Update_At_Runtime#5](../vsto/codesnippet/CSharp/Ribbon_Update_At_Runtime/CustomerRibbon.cs#5)]
      [!code-vb[Trin_Ribbon_Update_At_Runtime#5](../vsto/codesnippet/VisualBasic/Ribbon_Update_At_Runtime/CustomerRibbon.vb#5)]

13. Adicione o seguinte `Click` manipulador de eventos para o `CustomerRibbon` classe. Esse código adiciona o nome dos produtos selecionados para o campo de corpo de novas mensagens de email.

     [!code-csharp[Trin_Ribbon_Update_At_Runtime#8](../vsto/codesnippet/CSharp/Ribbon_Update_At_Runtime/CustomerRibbon.cs#8)]
     [!code-vb[Trin_Ribbon_Update_At_Runtime#8](../vsto/codesnippet/VisualBasic/Ribbon_Update_At_Runtime/CustomerRibbon.vb#8)]

14. Adicione o seguinte código para o `CustomerRibbon` classe. Esse código executa as seguintes tarefas:

    - Preenche a linha para novas mensagens de email usando o endereço de email do cliente selecionado no momento.

    - Adiciona texto aos campos assunto e corpo de novas mensagens de email.

      [!code-csharp[Trin_Ribbon_Update_At_Runtime#7](../vsto/codesnippet/CSharp/Ribbon_Update_At_Runtime/CustomerRibbon.cs#7)]
      [!code-vb[Trin_Ribbon_Update_At_Runtime#7](../vsto/codesnippet/VisualBasic/Ribbon_Update_At_Runtime/CustomerRibbon.vb#7)]

## <a name="test-the-controls-in-the-custom-group"></a>Testar os controles no grupo personalizado

Quando você abre um novo formulário de email no Outlook, um grupo personalizado chamado **compras do cliente** aparece na **mensagens** guia da faixa de opções.

Para criar uma mensagem de email de acompanhamento do cliente, selecione um cliente e, em seguida, selecione os produtos comprados pelo cliente. Controles de **compras do cliente** grupo são atualizados em tempo de execução com os dados do banco de dados Northwind.

### <a name="to-test-the-controls-in-the-custom-group"></a>Para testar os controles no grupo personalizado

1.  Pressione **F5** para executar o projeto.

     O Outlook inicia.

2.  No Outlook, sobre o **arquivo** , aponte para **New**e, em seguida, clique em **mensagem de email**.

     Ocorrem as seguintes ações:

    -   Uma nova janela do Inspetor de mensagem de email é exibida.

    -   No **mensagem** guia da faixa de opções, o **compras do cliente** grupo aparece antes do **área de transferência** grupo.

    -   O **clientes** caixa de combinação no grupo é atualizada com os nomes dos clientes no banco de dados Northwind.

3.  No **mensagem** guia da faixa de opções, no **compras do cliente** de grupo, selecione um cliente da **clientes** caixa de combinação.

     Ocorrem as seguintes ações:

    -   O **produtos comprados** menu é atualizado para mostrar cada pedido de vendas para o cliente selecionado.

    -   Cada submenu de ordem de venda é atualizada para mostrar os produtos adquiridos nessa ordem.

    -   Endereço de email do cliente selecionado é adicionado para o **para** linha da mensagem de email e o assunto e corpo da mensagem de email são preenchidos com texto.

4.  Clique o **compras de produtos** menu, aponte para qualquer pedido de vendas e, em seguida, clique em um produto da ordem de venda.

     O nome do produto é adicionado ao corpo da mensagem de email.

## <a name="next-steps"></a>Próximas etapas

Você pode aprender mais sobre como personalizar a interface do usuário do Office nesses tópicos:

-   Adicione com base no contexto da interface do usuário para qualquer personalização de nível de documento. Para obter mais informações, consulte [visão geral do painel de ações](../vsto/actions-pane-overview.md).

-   Estenda um formulário personalizado ou padrão do Microsoft Office Outlook. Para obter mais informações, consulte [instruções passo a passo: criar uma região de formulário do Outlook](../vsto/walkthrough-designing-an-outlook-form-region.md).

-   Adicione um painel de tarefas personalizado para o Outlook. Para obter mais informações, consulte [painéis de tarefas personalizados](../vsto/custom-task-panes.md).

## <a name="see-also"></a>Consulte também

- [Acesso a faixa de opções em tempo de execução](../vsto/accessing-the-ribbon-at-run-time.md)
- [Visão geral da faixa de opções](../vsto/ribbon-overview.md)
- [LINQ (Consulta Integrada à Linguagem)](/dotnet/csharp/linq/index)
- [Como: Introdução à personalização da faixa de opções](../vsto/how-to-get-started-customizing-the-ribbon.md)
- [Designer da faixa de opções](../vsto/ribbon-designer.md)
- [Passo a passo: Criar uma guia personalizada usando o Designer de faixa de opções](../vsto/walkthrough-creating-a-custom-tab-by-using-the-ribbon-designer.md)
- [Visão geral do modelo de objeto da faixa de opções](../vsto/ribbon-object-model-overview.md)
- [Personalizar uma faixa de opções do Outlook](../vsto/customizing-a-ribbon-for-outlook.md)
- [Como: alterar a posição de uma guia na faixa de opções](../vsto/how-to-change-the-position-of-a-tab-on-the-ribbon.md)
- [Como: personalizar uma guia interna](../vsto/how-to-customize-a-built-in-tab.md)
- [Como: adicionar controles ao modo de exibição Backstage](../vsto/how-to-add-controls-to-the-backstage-view.md)
- [Como: exportar uma faixa de opções do Designer da faixa de opções para o XML da faixa de opções](../vsto/how-to-export-a-ribbon-from-the-ribbon-designer-to-ribbon-xml.md)
- [Como: Add-in de mostrar erros de interface do usuário](../vsto/how-to-show-add-in-user-interface-errors.md)