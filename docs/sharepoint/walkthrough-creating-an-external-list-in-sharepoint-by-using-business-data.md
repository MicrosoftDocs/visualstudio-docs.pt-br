---
title: 'Passo a passo: Criando uma lista externa no SharePoint usando dados de negócios | Microsoft Docs'
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
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
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: 18848f0ebd6ffa289ea09553de82f5b9eb893181
ms.sourcegitcommit: 0a8ac5f2a685270d9ca79bb39d26fd90099bfa29
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2018
ms.locfileid: "51295833"
---
# <a name="walkthrough-create-an-external-list-in-sharepoint-by-using-business-data"></a>Passo a passo: Criar uma lista externa no SharePoint usando dados corporativos

O serviço de conectividade de dados comerciais (BDC) permite que o SharePoint exibir dados de negócios de aplicativos de servidor back-end, Web services e bancos de dados.

Este passo a passo mostra como criar um modelo para o serviço BDC que retorna informações sobre contatos em um banco de dados de exemplo. Você, em seguida, criará uma lista externa no SharePoint usando esse modelo.

Esta explicação passo a passo ilustra as seguintes tarefas:

- Criando um projeto.
- Adicionando uma entidade no modelo.
- Adicionando um método de localizador.
- Adicionando um método Finder específico.
- Testar o projeto.

## <a name="prerequisites"></a>Pré-requisitos

Você precisa dos seguintes componentes para concluir esta instrução passo a passo:

- Edições com suporte do Windows e do SharePoint.

- Acesso ao banco de dados de exemplo AdventureWorks. Para obter mais informações sobre como instalar o banco de dados AdventureWorks, consulte [bancos de dados de exemplo do SQL Server](http://go.microsoft.com/fwlink/?LinkID=117483).

## <a name="create-a-project-that-contains-a-bdc-model"></a>Criar um projeto que contém um modelo BDC

1. Na barra de menus no Visual Studio, escolha **arquivo** > **New** > **projeto**.

     A caixa de diálogo **Novo Projeto** é aberta.

2. Em um **Visual c#** ou **Visual Basic**, expanda o **SharePoint** nó e, em seguida, escolha o **2010** item.

3. No **modelos** painel, escolha **o projeto do SharePoint 2010**, nomeie o projeto **AdventureWorksTest**e, em seguida, escolha o **Okey** botão .

     O **Assistente para personalização do SharePoint** é exibida. Nesse assistente, você pode especificar o site que você usará para depurar o projeto e defina o nível de confiança da solução.

4. Escolha o **implantar como uma solução de farm** botão de opção para definir o nível de confiança.

5. Escolha o **concluir** botão para aceitar o site do SharePoint local padrão.

6. Na **Gerenciador de soluções**, escolha o nó do projeto do SharePoint.

7. Na barra de menus, escolha **Projeto** > **Adicionar Novo Item**.

     A caixa de diálogo **Adicionar Novo Item** é aberta.

8. No **modelos** painel, escolha **modelo de conectividade de dados corporativos (somente solução de Farm)**, nomeie o projeto **AdventureWorksContacts**e, em seguida, escolha o **Adicionar** botão.

## <a name="add-data-access-classes-to-the-project"></a>Adicionar classes de acesso a dados ao projeto

1. Na barra de menus, escolha **ferramentas** > **conectar-se ao banco de dados**.

     O **Adicionar Conexão** caixa de diálogo é aberta.

2. Adicione uma conexão ao banco de dados de exemplo AdventureWorks do SQL Server.

     Para obter mais informações, consulte [Adicionar/Modificar Conexão (Microsoft SQL Server)](https://msdn.microsoft.com/fa400910-26c3-4df7-b9d1-115e688b4ea3).

3. Na **Gerenciador de soluções**, escolha o nó do projeto.

4. Na barra de menus, escolha **Projeto** > **Adicionar Novo Item**.

5. No **modelos instalados** painel, escolha o **dados** nó.

6. No **modelos** painel, escolha **Classes LINQ to SQL**.

7. No **nome** , especifique **AdventureWorks**e, em seguida, escolha o **Add** botão.

     Um arquivo. dbml é adicionado ao projeto e abre o Object Relational Designer (O/R Designer).

8. Na barra de menus, escolha **modo de exibição** > **Gerenciador de servidores**.

9. Na **Gerenciador de servidores**, expanda o nó que representa o banco de dados de exemplo AdventureWorks e, em seguida, expanda o **tabelas** nó.

10. Adicione a **contato (pessoa)** tabela para o Designer relacional de objetos.

     Uma classe de entidade é criada e aparece na superfície de design. A classe de entidade tem propriedades que mapeiam para as colunas na tabela Contact (pessoa).

## <a name="remove-the-default-entity-from-the-bdc-model"></a>Remover a entidade padrão do modelo BDC

O **modelo de conectividade de dados corporativos** projeto adiciona uma entidade padrão chamada Entity1 ao modelo. Remova esta entidade. Posteriormente, você adicionará uma nova entidade. Começando com um modelo vazio reduz o número de etapas necessárias para concluir o passo a passo.

1. Na **Gerenciador de soluções**, expanda o **BdcModel1** nó e, em seguida, abra o *BdcModel1.bdcm* arquivo.

2. O arquivo de modelo de conectividade de dados corporativos é aberto no designer de BDC.

3. No designer, abra o menu de atalho **Entity1**e, em seguida, escolha **excluir**.

4. Na **Gerenciador de soluções**, abra o menu de atalho *Entity1.vb* (no Visual Basic) ou *Entity1.cs* (em c#) e, em seguida, escolha **excluir** .

5. Abra o menu de atalho *Entity1Service.vb* (no Visual Basic) ou *Entity1Service.cs* (em c#) e, em seguida, escolha **excluir**.

## <a name="add-an-entity-to-the-model"></a>Adicionar uma entidade no modelo

Adicione uma entidade no modelo. Você pode adicionar entidades do Visual Studio **caixa de ferramentas** para o designer BDC.

1. Na barra de menus, escolha **modo de exibição** > **caixa de ferramentas**.

2. Sobre o **BusinessDataConnectivity** guia da **caixa de ferramentas**, adicionar um **entidade** para o designer BDC.

     A nova entidade é exibida no designer. O Visual Studio adiciona um arquivo chamado *EntityService.vb* (no Visual Basic) ou *EntityService.cs* (em c#) para o projeto.

3. Na barra de menus, escolha **modo de exibição** > **as propriedades** > **janela**.

4. No **propriedades** janela, defina as **nome** valor da propriedade **entre em contato com**.

5. No designer, abra o menu de atalho para a entidade, escolha **Add**e, em seguida, escolha **identificador**.

     Um novo identificador aparece na entidade.

6. No **propriedades** janela, altere o nome do identificador ao **ContactID**.

7. No **nome do tipo** , escolha **System.Int32**.

## <a name="add-a-specific-finder-method"></a>Adicionar um método Finder específico

Para habilitar o serviço BDC exibir um contato específico, você deve adicionar um método Finder específico. O serviço de BDC chama o método de localizador específico quando um usuário escolhe um item em uma lista e, em seguida, escolhe a **Item de exibição** botão na faixa de opções.

Adicionar um método Finder específico para a entidade Contact usando o **detalhes do método BDC** janela. Para retornar uma entidade específica, adicione código ao método.

1. No designer de BDC, escolha o **entre em contato com** entidade.

2. Na barra de menus, escolha **modo de exibição** > **Other Windows** > **detalhes do método BDC**.

     Abre a janela de detalhes do método BDC.

3. No **adicionar um método** , escolha **criar método de localizador específico**.

     Visual Studio adiciona os seguintes elementos ao modelo. Esses elementos aparecem na **detalhes do método BDC** janela.

    - Um método chamado ReadItem.

    - Um parâmetro de entrada para o método.

    - Um parâmetro de retorno do método.

    - Um descritor de tipo para cada parâmetro.

    - Uma instância de método para o método.

4. No **detalhes do método BDC** janela, abra a lista que aparece para o **contato** descritor de tipo e, em seguida, escolha **editar**.

     O **BDC Explorer** é aberta e oferece uma exibição hierárquica do modelo.

5. No **propriedades** janela, abra a lista ao lado a **TypeName** propriedade, escolha o **projeto atual** guia e, em seguida, escolha o **contato**propriedade.

6. No **BDC Explorer**, abra o menu de atalho do **contato**e, em seguida, escolha **Adicionar descritor de tipo**.

     Um novo descritor de tipo que é denominado **TypeDescriptor1** aparece na **BDC Explorer**.

7. No **propriedades** janela, defina as **nome** valor da propriedade **ContactID**.

8. Abra a lista ao lado de **TypeName** propriedade e, em seguida, escolha **Int32**.

9. Abra a lista ao lado de **identificador** propriedade e, em seguida, escolha **ContactID**.

10. Repita a etapa 6 para criar um descritor de tipo para cada um dos campos a seguir.

    |Nome|Nome do tipo|
    |----------|---------------|
    |FirstName|System.String|
    |LastName|System.String|
    |Telefone|System.String|
    |Endereço de email|System.String|
    |EmailPromotion|System.Int32|
    |NameStyle|System.Boolean|
    |PasswordHash|System.String|
    |PasswordSalt|System.String|

11. No designer de BDC, sobre o **entre em contato com** entidade, abra o **ReadItem** método.

     O arquivo de código do serviço de contato é aberto no Editor de código.

12. No `ContactService` classe, substitua o `ReadItem` método com o código a seguir. Esse código executa as seguintes tarefas:

    - Recupera um registro da tabela de contatos do banco de dados AdventureWorks.

    - Retorna uma entidade de contato para o serviço de BDC.

    > [!NOTE]
    > Substitua o valor da `ServerName` campo com o nome do seu servidor.

     [!code-csharp[SP_BDC#3](../sharepoint/codesnippet/CSharp/SP_BDC/bdcmodel1/contactservice.cs#3)]
     [!code-vb[SP_BDC#3](../sharepoint/codesnippet/VisualBasic/sp_bdc/bdcmodel1/contactservice.vb#3)]

## <a name="add-a-finder-method"></a>Adicionar um método finder

Para habilitar o serviço BDC exibir os contatos em uma lista, você deve adicionar um método de localizador. Adicionar um método Finder para a entidade Contact usando o **detalhes do método BDC** janela. Para retornar uma coleção de entidades para o serviço de BDC, adicione código ao método.

1. No designer de BDC, escolha o **entre em contato com** entidade.

2. No **detalhes do método BDC** janela, recolha a **ReadItem** nó.

3. No **adicionar um método** na lista de **ReadList** método, escolha **criar método de localizador**.

     Visual Studio adiciona um método, um parâmetro de retorno e um descritor de tipo.

4. No designer de BDC, sobre o **entre em contato com** entidade, abra o **ReadList** método.

     O arquivo de código para o serviço de contato é aberto no Editor de código.

5. No `ContactService` classe, substitua o `ReadList` método com o código a seguir. Esse código executa as seguintes tarefas:

   - Recupera dados da tabela de contatos do banco de dados AdventureWorks.

   - Retorna uma lista de entidades de contato para o serviço de BDC.

     > [!NOTE]
     > Substitua o valor da `ServerName` campo com o nome do seu servidor.

     [!code-csharp[SP_BDC#2](../sharepoint/codesnippet/CSharp/SP_BDC/bdcmodel1/contactservice.cs#2)]
     [!code-vb[SP_BDC#2](../sharepoint/codesnippet/VisualBasic/sp_bdc/bdcmodel1/contactservice.vb#2)]

## <a name="test-the-project"></a>O projeto de teste

Quando você executa o projeto, o site do SharePoint é aberta e o Visual Studio adiciona o modelo para o serviço de conectividade de dados corporativos. Crie uma lista externa no SharePoint que faz referência à entidade de contato. Os dados para os contatos no banco de dados AdventureWorks aparecem na lista.

> [!NOTE]
> Você talvez precise modificar as configurações de segurança no SharePoint antes de você pode depurar sua solução. Para obter mais informações, consulte [criar um modelo de conectividade de dados corporativos](../sharepoint/designing-a-business-data-connectivity-model.md).

1. Pressione a tecla **F5**.

     Abre o site do SharePoint.

2. Sobre o **ações do Site** menu, escolha o **mais opções** comando.

3. Sobre o **criar** , escolha o **lista externa** modelo e, em seguida, escolha o **criar** botão.

4. Nomeie a lista personalizada **contatos**.

5. Escolha o botão Procurar ao lado de **tipo de conteúdo externo** campo.

6. No **seletor de tipo de conteúdo externo** diálogo caixa, escolha o **AdventureWorksContacts.BdcModel1.Contact** item e, em seguida, escolha o **criar** botão.

     O SharePoint cria uma lista externa que contenha contatos do banco de dados de exemplo AdventureWorks.

7. Para testar o método de localizador específico, escolha um contato na lista.

8. Na faixa de opções, escolha o **itens** guia e, em seguida, escolha o **Exibir Item** comando.

     Os detalhes do contato que você escolheu aparecem em um formulário.

## <a name="next-steps"></a>Próximas etapas

Você pode aprender mais sobre como criar modelos para o serviço BDC no SharePoint com estes tópicos:

- [Como: adicionar um método Creator](../sharepoint/how-to-add-a-creator-method.md).
- [Como: adicionar um método Updater](../sharepoint/how-to-add-an-updater-method.md).
- [Como: adicionar um método Deleter](../sharepoint/how-to-add-a-deleter-method.md).

## <a name="see-also"></a>Consulte também

[Criar um modelo de conectividade de dados corporativos](../sharepoint/designing-a-business-data-connectivity-model.md)  
[Criar um modelo de conectividade de dados corporativos](../sharepoint/creating-a-business-data-connectivity-model.md)  
[Visão geral de ferramentas de design de modelo BDC](../sharepoint/bdc-model-design-tools-overview.md)  
[Integre dados corporativos no SharePoint](../sharepoint/integrating-business-data-into-sharepoint.md)
