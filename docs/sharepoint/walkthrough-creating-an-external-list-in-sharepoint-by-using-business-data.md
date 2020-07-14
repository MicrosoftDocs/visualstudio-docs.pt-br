---
title: Criar lista externa no SharePoint usando dados corporativos
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Business Data Connectivity service [SharePoint development in Visual Studio], business data in a Web Part
- BDC [SharePoint development in Visual Studio], external list
- Business Data Connectivity service [SharePoint development in Visual Studio], business data in a SharePoint list
- BDC [SharePoint development in Visual Studio], business data in a SharePoint list
- BDC [SharePoint development in Visual Studio], business data in a Web Part
- BDC [SharePoint development in Visual Studio], entity backed list
- Business Data Connectivity service [SharePoint development in Visual Studio], entity backed list
- Business Data Connectivity service [SharePoint development in Visual Studio], external list
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 29f6c4e170bce8ae7bacfc7178ebd9386f2d4416
ms.sourcegitcommit: f9e44f5ab6a1dfb56c945c9986730465e1adb6fc
ms.contentlocale: pt-BR
ms.lasthandoff: 07/06/2020
ms.locfileid: "86015824"
---
# <a name="walkthrough-create-an-external-list-in-sharepoint-by-using-business-data"></a>Walkthrough: criar uma lista externa no SharePoint usando dados corporativos

O serviço corporativo de conectividade de dados (BDC) permite que o SharePoint exiba dados de negócios de aplicativos de servidor back-end, serviços Web e bancos de dado.

Este tutorial mostra como criar um modelo para o serviço BDC que retorna informações sobre contatos em um banco de dados de exemplo. Em seguida, você criará uma lista externa no SharePoint usando esse modelo.

Este passo a passo ilustra as seguintes tarefas:

- Criando um projeto.
- Adicionando uma entidade ao modelo.
- Adicionando um método localizador.
- Adicionando um método localizador específico.
- Testando o projeto.

## <a name="prerequisites"></a>Pré-requisitos

Você precisará dos seguintes componentes para concluir este passo a passo:

- Edições com suporte do Windows e do SharePoint.

- Acesso ao banco de dados de exemplo AdventureWorks. Para obter mais informações sobre como instalar o banco de dados AdventureWorks, consulte [SQL Server bancos](https://github.com/Microsoft/sql-server-samples/releases/tag/adventureworks)de dados de exemplo.

## <a name="create-a-project-that-contains-a-bdc-model"></a>Criar um projeto que contém um modelo de BDC

1. Na barra de menus no Visual Studio, escolha **arquivo**  >  **novo**  >  **projeto**.

     A caixa de diálogo **Novo Projeto** será aberta.

2. Em **Visual C#** ou **Visual Basic**, expanda o nó do **SharePoint** e escolha o item **2010** .

3. No painel **modelos** , escolha **projeto do SharePoint 2010**, nomeie o projeto **AdventureWorksTest**e, em seguida, escolha o botão **OK** .

     O **Assistente para personalização do SharePoint** é exibido. Neste assistente, você pode especificar o site que será usado para depurar o projeto e definir o nível de confiança da solução.

4. Escolha o botão de opção **implantar como uma solução de farm** para definir o nível de confiança.

5. Escolha o botão **concluir** para aceitar o site do SharePoint local padrão.

6. Em **Gerenciador de soluções**, escolha o nó do projeto do SharePoint.

7. Na barra de menus, escolha **projeto**  >  **Adicionar novo item**.

     A caixa de diálogo **Adicionar Novo Item** é aberta.

8. No painel **modelos** , escolha **modelo de conectividade de dados corporativos (somente solução de farm)**, nomeie o projeto **AdventureWorksContacts**e, em seguida, escolha o botão **Adicionar** .

## <a name="add-data-access-classes-to-the-project"></a>Adicionar classes de acesso a dados ao projeto

1. Na barra de menus, escolha **ferramentas**  >  **conectar ao banco de dados**.

     A caixa de diálogo **Adicionar conexão** é aberta.

2. Adicione uma conexão ao banco de dados de exemplo SQL Server AdventureWorks.

     Para obter mais informações, consulte [Adicionar/Modificar conexão (Microsoft SQL Server)](https://msdn.microsoft.com/fa400910-26c3-4df7-b9d1-115e688b4ea3).

3. Em **Gerenciador de soluções**, escolha o nó do projeto.

4. Na barra de menus, escolha **projeto**  >  **Adicionar novo item**.

5. No painel **modelos instalados** , escolha o nó de **dados** .

6. No painel **modelos** , escolha **LINQ to SQL classes**.

7. Na caixa **nome** , especifique **AdventureWorks**e, em seguida, escolha o botão **Adicionar** .

     Um arquivo. dbml é adicionado ao projeto e o Object Relational Designer (O/R Designer) é aberto.

8. Na barra de menus, escolha **Exibir**  >  **Gerenciador de servidores**.

9. Em **Gerenciador de servidores**, expanda o nó que representa o banco de dados de exemplo AdventureWorks e, em seguida, expanda o nó **tabelas** .

10. Adicione a tabela **contato (Person)** ao o/R Designer.

     Uma classe de entidade é criada e aparece na superfície de design. A classe de entidade tem propriedades que são mapeadas para as colunas na tabela contato (pessoa).

## <a name="remove-the-default-entity-from-the-bdc-model"></a>Remover a entidade padrão do modelo BDC

O projeto de **modelo de conectividade de dados corporativos** adiciona uma entidade padrão chamada Entity1 ao modelo. Remova esta entidade. Posteriormente, você adicionará uma nova entidade. Começar com um modelo vazio reduz o número de etapas necessárias para concluir o passo a passos.

1. No **Gerenciador de soluções**, expanda o nó **BdcModel1** e, em seguida, abra o arquivo *BdcModel1. bdcm* .

2. O arquivo de modelo de conectividade de dados corporativos é aberto no BDC designer.

3. No designer, abra o menu de atalho para **Entity1**e, em seguida, escolha **excluir**.

4. No **Gerenciador de soluções**, abra o menu de atalho para *Entity1. vb* (em Visual Basic) ou *Entity1.cs* (em C#) e, em seguida, escolha **excluir**.

5. Abra o menu de atalho para *Entity1Service. vb* (em Visual Basic) ou *Entity1Service.cs* (em C#) e, em seguida, escolha **excluir**.

## <a name="add-an-entity-to-the-model"></a>Adicionar uma entidade ao modelo

Adicione uma entidade ao modelo. Você pode adicionar entidades da **caixa de ferramentas** do Visual Studio para o BDC designer.

1. Na barra de menus, escolha **Exibir**  >  **caixa de ferramentas**.

2. Na guia **BusinessDataConnectivity** da caixa de **ferramentas**, adicione uma **entidade** no designer do BDC.

     A nova entidade aparece no designer. O Visual Studio adiciona um arquivo chamado *EntityService. vb* (em Visual Basic) ou *EntityService.cs* (em C#) ao projeto.

3. Na barra de menus, escolha **Exibir**  >  **Properties**  >  **janela**de propriedades.

4. Na janela **Propriedades** , defina o valor da propriedade **Name** como **Contact**.

5. No designer, abra o menu de atalho da entidade, escolha **Adicionar**e, em seguida, escolha **identificador**.

     Um novo identificador é exibido na entidade.

6. Na janela **Propriedades** , altere o nome do identificador para **ContactID**.

7. Na lista **nome do tipo** , escolha **System. Int32**.

## <a name="add-a-specific-finder-method"></a>Adicionar um método localizador específico

Para habilitar o serviço BDC para exibir um contato específico, você deve adicionar um método localizador específico. O serviço BDC chama o método localizador específico quando um usuário escolhe um item em uma lista e escolhe o botão **Exibir item** na faixa de visão.

Adicione um método localizador específico à entidade Contact usando a janela **detalhes do método do BDC** . Para retornar uma entidade específica, adicione o código ao método.

1. No BDC designer, escolha a entidade **contato** .

2. Na barra de menus, escolha **Exibir**  >  **outros**  >  **detalhes do método**do Windows BDC.

     A janela detalhes do método BDC é aberta.

3. Na lista **Adicionar um método** , escolha **criar método localizador específico**.

     O Visual Studio adiciona os seguintes elementos ao modelo. Esses elementos aparecem na janela **detalhes do método BDC** .

    - Um método chamado ReadItem.

    - Um parâmetro de entrada para o método.

    - Um parâmetro de retorno para o método.

    - Um descritor de tipo para cada parâmetro.

    - Uma instância de método para o método.

4. Na janela **detalhes do método BDC** , abra a lista que aparece para o descritor de tipo de **contato** e escolha **Editar**.

     O **BDC Explorer** é aberto e fornece uma exibição hierárquica do modelo.

5. Na janela **Propriedades** , abra a lista ao lado da propriedade **TypeName** , escolha a guia **projeto atual** e, em seguida, escolha a propriedade **contato** .

6. No **Gerenciador do BDC**, abra o menu de atalho do **contato**e escolha **Adicionar descritor de tipo**.

     Um novo descritor de tipo chamado **TypeDescriptor1** aparece no **BDC Explorer**.

7. Na janela **Propriedades** , defina o valor da propriedade **Name** como **ContactID**.

8. Abra a lista ao lado da propriedade **TypeName** e escolha **Int32**.

9. Abra a lista ao lado da propriedade **identificador** e escolha **ContactID**.

10. Repita a etapa 6 para criar um descritor de tipo para cada um dos campos a seguir.

    |Nome|Nome do Tipo|
    |----------|---------------|
    |Nome|System.String|
    |LastName|System.String|
    |Telefone|System.String|
    |EmailAddress|System.String|
    |EmailPromotion|System.Int32|
    |NameStyle|System.Boolean|
    |PasswordHash|System.String|
    |PasswordSalt|System.String|

11. No BDC designer, na entidade **contato** , abra o método **ReadItem** .

     O arquivo de código do serviço de contato é aberto no editor de código.

12. Na `ContactService` classe, substitua o `ReadItem` método pelo código a seguir. Esse código executa as seguintes tarefas:

    - Recupera um registro da tabela de contatos do banco de dados AdventureWorks.

    - Retorna uma entidade de contato para o serviço BDC.

    > [!NOTE]
    > Substitua o valor do `ServerName` campo pelo nome do seu servidor.

     [!code-csharp[SP_BDC#3](../sharepoint/codesnippet/CSharp/SP_BDC/bdcmodel1/contactservice.cs#3)]
     [!code-vb[SP_BDC#3](../sharepoint/codesnippet/VisualBasic/sp_bdc/bdcmodel1/contactservice.vb#3)]

## <a name="add-a-finder-method"></a>Adicionar um método localizador

Para habilitar o serviço BDC para exibir os contatos em uma lista, você deve adicionar um método localizador. Adicione um método Finder à entidade Contact usando a janela **detalhes do método do BDC** . Para retornar uma coleção de entidades para o serviço do BDC, adicione o código ao método.

1. No BDC designer, escolha a entidade **contato** .

2. Na janela **detalhes do método BDC** , recolha o nó **ReadItem** .

3. Na lista **Adicionar um método** sob o método **ReadList** , escolha **criar método Finder**.

     O Visual Studio adiciona um método, um parâmetro de retorno e um descritor de tipo.

4. No BDC designer, na entidade **contato** , abra o método **ReadList** .

     O arquivo de código para o serviço de contato é aberto no editor de código.

5. Na `ContactService` classe, substitua o `ReadList` método pelo código a seguir. Esse código executa as seguintes tarefas:

   - Recupera dados da tabela Contacts do banco de dados AdventureWorks.

   - Retorna uma lista de entidades de contato para o serviço BDC.

     > [!NOTE]
     > Substitua o valor do `ServerName` campo pelo nome do seu servidor.

     [!code-csharp[SP_BDC#2](../sharepoint/codesnippet/CSharp/SP_BDC/bdcmodel1/contactservice.cs#2)]
     [!code-vb[SP_BDC#2](../sharepoint/codesnippet/VisualBasic/sp_bdc/bdcmodel1/contactservice.vb#2)]

## <a name="test-the-project"></a>Teste do projeto

Quando você executa o projeto, o site do SharePoint é aberto e o Visual Studio adiciona seu modelo ao serviço de conectividade de dados corporativos. Crie uma lista externa no SharePoint que faça referência à entidade Contact. Os dados de contatos no banco de dados AdventureWorks aparecem na lista.

> [!NOTE]
> Talvez você precise modificar suas configurações de segurança no SharePoint antes de poder depurar sua solução. Para obter mais informações, consulte [criar um modelo de conectividade de dados corporativos](../sharepoint/designing-a-business-data-connectivity-model.md).

1. Pressione a tecla **F5**.

     O site do SharePoint é aberto.

2. No menu **ações do site** , escolha o comando **mais opções** .

3. Na página **criar** , escolha o modelo de **lista externa** e, em seguida, escolha o botão **criar** .

4. Nomeie a lista personalizada **contatos**.

5. Escolha o botão procurar ao lado do campo **tipo de conteúdo externo** .

6. Na caixa de diálogo **seletor de tipo de conteúdo externo** , escolha o item **AdventureWorksContacts. BdcModel1. Contact** e, em seguida, escolha o botão **criar** .

     O SharePoint cria uma lista externa que contém contatos do banco de dados de exemplo AdventureWorks.

7. Para testar o método localizador específico, escolha um contato na lista.

8. Na faixa de seleção, escolha a guia **itens** e, em seguida, escolha o comando **Exibir item** .

     Os detalhes do contato que você escolheu aparecem em um formulário.

## <a name="next-steps"></a>Próximas etapas

Você pode aprender mais sobre como projetar modelos para o serviço BDC no SharePoint a partir destes tópicos:

- [Como adicionar um método de criador](../sharepoint/how-to-add-a-creator-method.md).
- [Como adicionar um método de atualizador](../sharepoint/how-to-add-an-updater-method.md).
- [Como adicionar um método excluidor](../sharepoint/how-to-add-a-deleter-method.md).

## <a name="see-also"></a>Consulte também

[Criar um modelo](../sharepoint/designing-a-business-data-connectivity-model.md) 
 de conectividade de dados corporativos [Criar um modelo](../sharepoint/creating-a-business-data-connectivity-model.md) 
 de conectividade de dados corporativos [Visão geral](../sharepoint/bdc-model-design-tools-overview.md) 
 das ferramentas de design de modelo do BDC [Integre dados corporativos ao SharePoint](../sharepoint/integrating-business-data-into-sharepoint.md)
