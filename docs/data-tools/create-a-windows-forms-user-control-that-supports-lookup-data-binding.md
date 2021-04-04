---
title: Usando tabelas de pesquisa na associação de dados-Windows Forms
description: Aprenda a criar um controle de usuário Windows Forms que dá suporte à vinculação de dados de pesquisa, usando a classe LookupBindingPropertiesAttribute no Visual Studio.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- data binding, user controls
- LookupBindingPropertiesAttribute class, examples
- user controls [Visual Basic], creating
ms.assetid: c48b4d75-ccfc-4950-8b14-ff8adbfe4208
author: ghogen
ms.author: ghogen
manager: jmartens
ms.workload:
- data-storage
ms.openlocfilehash: 796fc389a7cd7d0c587f955792a96d0f2f07a20c
ms.sourcegitcommit: 80fc9a72e9a1aba2d417dbfee997fab013fc36ac
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/02/2021
ms.locfileid: "106215962"
---
# <a name="create-a-windows-forms-user-control-that-supports-lookup-data-binding"></a>Criar um controle de usuário do Windows Forms compatível com associação de dados de consulta

Ao exibir dados no Windows Forms, você poderá escolher os controles existentes da **Caixa de Ferramentas** ou criar controles personalizados se o aplicativo exigir alguma funcionalidade que não esteja disponível nos controles padrão. Este passo a passo mostra como criar um controle que implementa o <xref:System.ComponentModel.LookupBindingPropertiesAttribute>. Os controles que implementam o <xref:System.ComponentModel.LookupBindingPropertiesAttribute> contêm três propriedade que podem ser associadas a dados. Tais controles são semelhantes a um <xref:System.Windows.Forms.ComboBox>.

Para obter mais informações sobre a criação de controles, consulte [desenvolvendo Windows Forms controles em tempo de design](/dotnet/framework/winforms/controls/developing-windows-forms-controls-at-design-time).

Ao criar controles para uso em cenários de associação de dados, é necessário implementar um dos seguintes atributos de associação de dados:

|Uso de atributo de vinculação de dados|
| - |
|Implemente o <xref:System.ComponentModel.DefaultBindingPropertyAttribute> em controles simples, como um <xref:System.Windows.Forms.TextBox>, que exibe uma única coluna (ou propriedade) de dados. Para obter mais informações, consulte [criar um Windows Forms controle de usuário que dá suporte à vinculação de dados simples](../data-tools/create-a-windows-forms-user-control-that-supports-simple-data-binding.md).|
|Implemente o <xref:System.ComponentModel.ComplexBindingPropertiesAttribute> nos controles, como um <xref:System.Windows.Forms.DataGridView> que exibe listas (ou tabelas) de dados. Para obter mais informações, consulte [criar um Windows Forms controle de usuário que dá suporte à ligação de dados complexa](../data-tools/create-a-windows-forms-user-control-that-supports-complex-data-binding.md).|
|Implemente o <xref:System.ComponentModel.LookupBindingPropertiesAttribute> nos controles, como um <xref:System.Windows.Forms.ComboBox>que exibe listas (ou tabelas) de dados, mas também precisa apresentar uma única coluna ou propriedade. (Esse processo é descrito nesta página de passo a passo.)|

Este passo a passo cria um controle de pesquisa que se associa aos dados de duas tabelas. Este exemplo usa as tabelas `Customers` e `Orders` do banco de dados de exemplo Northwind. O controle de pesquisa está associado ao `CustomerID` campo da `Orders` tabela. Ele usa esse valor para pesquisar o `CompanyName` da `Customers` tabela.

Durante este passo a passos, você aprenderá a:

- Crie um novo **aplicativo Windows Forms**.

- Adicionar um novo **Controle de Usuário** ao projeto.

- Projetar visualmente o controle do usuário.

- Implementar o atributo `LookupBindingProperty`.

- Crie um conjunto de dados com o assistente de **configuração de fonte de dados** .

- Definir a coluna **CustomerID** na tabela **Pedidos** na janela **Fontes de Dados** para usar o novo controle.

- Criar um formulário para exibir dados no novo controle.

## <a name="prerequisites"></a>Pré-requisitos

Este passo a passos usa SQL Server Express LocalDB e o banco de dados de exemplo Northwind.

1. Se você não tiver SQL Server Express LocalDB, instale-o na [SQL Server Express página de download](https://www.microsoft.com/sql-server/sql-server-editions-express)ou por meio do **instalador do Visual Studio**. No **instalador do Visual Studio**, você pode instalar o SQL Server Express LocalDB como parte da carga de trabalho de **armazenamento e processamento de dados** ou como um componente individual.

2. Instale o banco de dados de exemplo Northwind seguindo estas etapas:

    1. No Visual Studio, abra a janela **pesquisador de objetos do SQL Server** . (O Pesquisador de Objetos do SQL Server é instalado como parte da carga de trabalho de **armazenamento e processamento de dados** no instalador do Visual Studio.) Expanda o nó **SQL Server** . Clique com o botão direito do mouse na instância do LocalDB e selecione **nova consulta**.

       Uma janela do editor de consultas é aberta.

    2. Copie o [script do Transact-SQL Northwind](https://github.com/MicrosoftDocs/visualstudio-docs/blob/master/docs/data-tools/samples/northwind.sql?raw=true) para a área de transferência. Esse script T-SQL cria o banco de dados Northwind a partir do zero e o preenche com os mesmos.

    3. Cole o script T-SQL no editor de consultas e, em seguida, escolha o botão **executar** .

       Após um curto período, a consulta terminará de ser executada e o banco de dados Northwind será criado.

## <a name="create-a-windows-forms-app-project"></a>Criar um projeto de aplicativo Windows Forms

A primeira etapa é criar um projeto de **aplicativo Windows Forms** .

1. No Visual Studio, no menu **Arquivo**, selecione **Novo** > **Projeto**.

2. Expanda o **Visual C#** ou **Visual Basic** no painel esquerdo e, em seguida, selecione **área de trabalho do Windows**.

3. No painel central, selecione o tipo de projeto **Windows Forms aplicativo** .

4. Nomeie o projeto **LookupControlWalkthrough** e escolha **OK**.

     O projeto **LookupControlWalkthrough** é criado e adicionado ao **Gerenciador de Soluções**.

## <a name="add-a-user-control-to-the-project"></a>Adicionar um controle de usuário ao projeto

Este passo a passo cria um controle de pesquisa de um **Controle de Usuário**, portanto, adicione um item de **Controle de Usuário** ao projeto **LookupControlWalkthrough**.

1. No menu **Projeto**, selecione **Adicionar Controle do Usuário**.

2. Digite `LookupBox` a área **nome** e clique em **Adicionar**.

     O controle **LookupBox** é adicionado ao **Gerenciador de Soluções** e abre no designer.

## <a name="design-the-lookupbox-control"></a>Criar o controle LookupBox

Para criar o controle LookupBox, arraste um <xref:System.Windows.Forms.ComboBox> da **caixa de ferramentas** para a superfície de design do controle de usuário.

## <a name="add-the-required-data-binding-attribute"></a>Adicionar o atributo de associação de dados necessário

Para controles de pesquisa que suportam associação de dados, você pode implementar o <xref:System.ComponentModel.LookupBindingPropertiesAttribute>.

1. Mude o controle **LookupBox** para exibição de código. (No menu **Exibir**, escolha **Código**.)

2. Substitua o código no `LookupBox` pelo seguinte:

     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataDisplaying/VB/LookupBox.vb" id="Snippet5":::
     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataDisplaying/CS/LookupBox.cs" id="Snippet5":::

3. No menu **Compilar** , escolha **Compilar solução**.

## <a name="create-a-data-source-from-your-database"></a>Criar uma fonte de dados do seu banco de dados

Esta etapa cria uma fonte de dados usando o **Assistente de Configuração de Fonte de Dados** com base nas tabelas `Customers` e `Orders` no banco de dados de exemplo Northwind.

1. Para abrir a janela **fontes de dados** , no menu **dados** , clique em **mostrar fontes de dados**.

2. Na janela **Fontes de Dados**, selecione **Adicionar Nova Fonte de Dados** para iniciar o assistente de **Configuração de Fonte de Dados**.

3. Selecione **Banco de Dados** na página **Escolher um Tipo de Fonte de Dados** e, em seguida, clique em **Avançar**.

4. Na página **escolher sua conexão de dados** , siga um destes procedimentos:

    - Se uma conexão de dados com o banco de dados de exemplo Northwind estiver disponível na lista suspensa, selecione-o.

    - Selecione **Nova Conexão** para inicializar a caixa de diálogo **Adicionar/Modificar Conexão**.

5. Se o banco de dados exigir uma senha, selecione a opção para incluir dados confidenciais e, em seguida, clique em **Avançar**.

6. Na página **salvar cadeia de conexão no arquivo de configuração do aplicativo** , clique em **Avançar**.

7. Na página **escolher seus objetos de banco de dados** , expanda o nó **tabelas** .

8. Selecione as tabelas `Customers` e `Orders` e, em seguida, clique em **Concluir**.

     O **NorthwindDataSet** é adicionado ao seu projeto e as `Customers` tabelas e `Orders` aparecem na janela **Data Sources** .

## <a name="set-the-customerid-column-of-the-orders-table-to-use-the-lookupbox-control"></a>Definir a coluna CustomerID da tabela Orders para usar o controle LookupBox

Na janela **Fontes de Dados**, você pode definir o controle a ser criado antes de arrastar itens para seu formulário.

1. Abra **Form1** no designer.

2. Expanda o nó **Clientes** na janela **Fontes de Dados**.

3. Expanda o nó **Pedidos** (no nó **Clientes** abaixo da coluna **Fax**).

4. Clique na seta suspensa no nó **Pedidos** e escolha **Detalhes** na lista de controle.

5. Clique na seta suspensa na coluna **CustomerID** (no nó **Pedidos**) e escolha **Personalizar**.

6. Selecione **LookupBox** na lista de **Controles Associados** na caixa de diálogo **Opções de Personalização da Interface do Usuário de Dados**.

7. Clique em **OK**.

8. Clique na seta suspensa na coluna **CustomerID** e escolha **LookupBox**.

## <a name="add-controls-to-the-form"></a>Adicionar controles ao formulário

É possível criar controles de associação de dados ao arrastar itens da janela **Fontes de Dados** para **Form1**.

Para criar controles vinculados a dados no Windows Form, arraste o nó **pedidos** da janela **fontes de dados** para o Windows Form e verifique se o controle **LookupBox** é usado para exibir os dados na `CustomerID` coluna.

## <a name="bind-the-control-to-look-up-companyname-from-the-customers-table"></a>Associar o controle para procurar o CompanyName da tabela Customers

Para configurar as associações de pesquisa, selecione o nó **clientes** principais na janela **fontes de dados** e arraste-o para a caixa de combinação no **CustomerIDLookupBox** no **Form1**.

Isso configura a associação de dados para exibir o `CompanyName` da tabela `Customers` mantendo, ao mesmo tempo, o valor `CustomerID` da tabela `Orders`.

## <a name="run-the-application"></a>Executar o aplicativo

- Pressione **F5** para executar o aplicativo.

- Navegue por alguns registros e verifique se `CompanyName` aparece no controle `LookupBox`.

## <a name="see-also"></a>Confira também

- [Associar controles do Windows Forms a dados no Visual Studio](../data-tools/bind-windows-forms-controls-to-data-in-visual-studio.md)
