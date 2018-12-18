---
title: Usar tabelas de pesquisa na associação de dados - controles dos Windows Forms | Microsoft Docs
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
author: gewarren
ms.author: gewarren
manager: douge
ms.prod: visual-studio-dev15
ms.technology: vs-data-tools
ms.workload:
- data-storage
ms.openlocfilehash: 07c9cf40952eabcafe9d1587d3e2ae4aa02de3a0
ms.sourcegitcommit: 81e9d90843ead658bc73b30c869f25921d99e116
ms.translationtype: MTE95
ms.contentlocale: pt-BR
ms.lasthandoff: 11/26/2018
ms.locfileid: "52305072"
---
# <a name="create-a-windows-forms-user-control-that-supports-lookup-data-binding"></a>Criar um controle de usuário do Windows Forms compatível com associação de dados de consulta

Ao exibir dados no Windows Forms, você poderá escolher os controles existentes da **Caixa de Ferramentas** ou criar controles personalizados se o aplicativo exigir alguma funcionalidade que não esteja disponível nos controles padrão. Este passo a passo mostra como criar um controle que implementa o <xref:System.ComponentModel.LookupBindingPropertiesAttribute>. Os controles que implementam o <xref:System.ComponentModel.LookupBindingPropertiesAttribute> contêm três propriedade que podem ser associadas a dados. Tais controles são semelhantes a um <xref:System.Windows.Forms.ComboBox>.

Para obter mais informações sobre criação de controle, consulte [controla o desenvolvimento de Windows Forms em tempo de design](/dotnet/framework/winforms/controls/developing-windows-forms-controls-at-design-time).

Ao criar controles para uso em cenários de associação de dados, é necessário implementar um dos seguintes atributos de associação de dados:

|Uso do atributo de associação de dados|
| - |
|Implemente o <xref:System.ComponentModel.DefaultBindingPropertyAttribute> em controles simples, como um <xref:System.Windows.Forms.TextBox>, que exibe uma única coluna (ou propriedade) de dados. Para obter mais informações, consulte [criar um controle de usuário do Windows Forms que dá suporte à vinculação de dados simples](../data-tools/create-a-windows-forms-user-control-that-supports-simple-data-binding.md).|
|Implemente o <xref:System.ComponentModel.ComplexBindingPropertiesAttribute> nos controles, como um <xref:System.Windows.Forms.DataGridView> que exibe listas (ou tabelas) de dados. Para obter mais informações, consulte [criar um controle de usuário do Windows Forms que dá suporte à vinculação de dados complexos](../data-tools/create-a-windows-forms-user-control-that-supports-complex-data-binding.md).|
|Implemente o <xref:System.ComponentModel.LookupBindingPropertiesAttribute> nos controles, como um <xref:System.Windows.Forms.ComboBox>que exibe listas (ou tabelas) de dados, mas também precisa apresentar uma única coluna ou propriedade. (Esse processo é descrito nesta página de passo a passo.)|

Este passo a passo cria um controle de pesquisa que se associa aos dados de duas tabelas. Este exemplo usa as tabelas `Customers` e `Orders` do banco de dados de exemplo Northwind. O controle de pesquisa está associado para o `CustomerID` campo o `Orders` tabela. Ele usa esse valor para pesquisar o `CompanyName` do `Customers` tabela.

Durante este passo a passo, você aprenderá como:

-   Criar um novo **Aplicativo do Windows Forms**.

-   Adicionar um novo **Controle de Usuário** ao projeto.

-   Projetar visualmente o controle do usuário.

-   Implementar o atributo `LookupBindingProperty`.

-   Criar um conjunto de dados com o **configuração de fonte de dados** assistente.

-   Definir a coluna **CustomerID** na tabela **Pedidos** na janela **Fontes de Dados** para usar o novo controle.

-   Criar um formulário para exibir dados no novo controle.

## <a name="prerequisites"></a>Pré-requisitos

Este passo a passo usa o SQL Server Express LocalDB e o banco de dados de exemplo Northwind.

1.  Se você não tiver o SQL Server Express LocalDB, instalá-lo a partir de [página de download do SQL Server Express](https://www.microsoft.com/sql-server/sql-server-editions-express), ou por meio de **instalador do Visual Studio**. No **instalador do Visual Studio**, você pode instalar o SQL Server Express LocalDB como parte do **armazenamento de dados e processamento** carga de trabalho, ou como um componente individual.

2.  Instale o banco de dados de exemplo Northwind, seguindo estas etapas:

    1. No Visual Studio, abra o **SQL Server Object Explorer** janela. (Pesquisador de objetos do SQL Server é instalado como parte dos **armazenamento de dados e processamento** carga de trabalho no instalador do Visual Studio.) Expanda o **SQL Server** nó. Clique com botão direito na instância do LocalDB e selecione **nova consulta**.

       Abre uma janela do editor de consulta.

    2. Cópia de [script Transact-SQL Northwind](https://github.com/MicrosoftDocs/visualstudio-docs/blob/master/docs/data-tools/samples/northwind.sql?raw=true) na área de transferência. Este script T-SQL cria o banco de dados Northwind do zero e a preenche com dados.

    3. Cole o script T-SQL no editor de consultas e, em seguida, escolha o **Execute** botão.

       Após alguns instantes, a consulta termina a execução e o banco de dados Northwind é criado.

## <a name="create-a-windows-forms-app-project"></a>Criar um projeto de aplicativo do Windows Forms

A primeira etapa é criar uma **aplicativo do Windows Forms** projeto.

1. No Visual Studio, sobre o **arquivo** menu, selecione **New** > **projeto**.

2. Expanda o **Visual c#** ou **Visual Basic** no painel esquerdo, em seguida, selecione **área de trabalho do Windows**.

3. No painel central, selecione a **aplicativo do Windows Forms** tipo de projeto.

4. Nomeie o projeto **LookupControlWalkthrough**e, em seguida, escolha **Okey**.

     O projeto **LookupControlWalkthrough** é criado e adicionado ao **Gerenciador de Soluções**.

## <a name="add-a-user-control-to-the-project"></a>Adicionar um controle de usuário ao projeto

Este passo a passo cria um controle de pesquisa de um **Controle de Usuário**, portanto, adicione um item de **Controle de Usuário** ao projeto **LookupControlWalkthrough**.

1.  No menu **Projeto**, selecione **Adicionar Controle do Usuário**.

2.  Tipo de `LookupBox` no **nome** área e depois clique em **Add**.

     O controle **LookupBox** é adicionado ao **Gerenciador de Soluções** e abre no designer.

## <a name="design-the-lookupbox-control"></a>Criar o controle LookupBox

Para criar o controle LookupBox, arraste uma <xref:System.Windows.Forms.ComboBox> do **caixa de ferramentas** na superfície de design do controle de usuário.

## <a name="add-the-required-data-binding-attribute"></a>Adicione o atributo obrigatório de associação de dados

Para controles de pesquisa que suportam associação de dados, você pode implementar o <xref:System.ComponentModel.LookupBindingPropertiesAttribute>.

1.  Mude o controle **LookupBox** para exibição de código. (No menu **Exibir**, escolha **Código**.)

2.  Substitua o código no `LookupBox` pelo seguinte:

     [!code-vb[VbRaddataDisplaying#5](../data-tools/codesnippet/VisualBasic/create-a-windows-forms-user-control-that-supports-lookup-data-binding_1.vb)]
     [!code-csharp[VbRaddataDisplaying#5](../data-tools/codesnippet/CSharp/create-a-windows-forms-user-control-that-supports-lookup-data-binding_1.cs)]

3.  No menu **Compilação**, escolha **Compilar Solução**.

## <a name="create-a-data-source-from-your-database"></a>Criar uma fonte de dados do banco de dados

Esta etapa cria uma fonte de dados usando o **Assistente de Configuração de Fonte de Dados** com base nas tabelas `Customers` e `Orders` no banco de dados de exemplo Northwind.

1.  Para abrir o **fontes de dados** janela diante de **dados** menu, clique em **Mostrar fontes de dados**.

2.  Na janela **Fontes de Dados**, selecione **Adicionar Nova Fonte de Dados** para iniciar o assistente de **Configuração de Fonte de Dados**.

3.  Selecione **Banco de Dados** na página **Escolher um Tipo de Fonte de Dados** e, em seguida, clique em **Avançar**.

4.  Na página **Escolha a Conexão de Dados**, faça o seguinte:

    -   Se uma conexão de dados com o banco de dados de exemplo Northwind estiver disponível na lista suspensa, selecione-o.

    -   Selecione **Nova Conexão** para inicializar a caixa de diálogo **Adicionar/Modificar Conexão**.

5.  Se o banco de dados exigir uma senha, selecione a opção para incluir dados confidenciais e, em seguida, clique em **Avançar**.

6.  Sobre o **salvar a cadeia de caracteres de conexão para o arquivo de configuração de aplicativo** , clique em **próxima**.

7.  Sobre o **Choose your Database Objects** página, expanda o **tabelas** nó.

8.  Selecione as tabelas `Customers` e `Orders` e, em seguida, clique em **Concluir**.

     O **NorthwindDataSet** é adicionado ao projeto e as tabelas `Customers` e `Orders` aparecem na janela **Fontes de Dados**.

## <a name="set-the-customerid-column-of-the-orders-table-to-use-the-lookupbox-control"></a>Definir a coluna CustomerID da tabela Orders para usar o controle LookupBox

Na janela **Fontes de Dados**, você pode definir o controle a ser criado antes de arrastar itens para seu formulário.

1.  Abra **Form1** no designer.

2.  Expanda o nó **Clientes** na janela **Fontes de Dados**.

3.  Expanda o nó **Pedidos** (no nó **Clientes** abaixo da coluna **Fax**).

4.  Clique na seta suspensa no nó **Pedidos** e escolha **Detalhes** na lista de controle.

5.  Clique na seta suspensa na coluna **CustomerID** (no nó **Pedidos**) e escolha **Personalizar**.

6.  Selecione **LookupBox** na lista de **Controles Associados** na caixa de diálogo **Opções de Personalização da Interface do Usuário de Dados**.

7.  Clique em **OK**.

8.  Clique na seta suspensa na coluna **CustomerID** e escolha **LookupBox**.

## <a name="add-controls-to-the-form"></a>Adicionar controles ao formulário

É possível criar controles de associação de dados ao arrastar itens da janela **Fontes de Dados** para **Form1**.

Para criar controles associados a dados do formulário do Windows, arraste a **pedidos** nó a partir o **fontes de dados** janela para o formulário do Windows e verificar se o **LookupBox** controle é usado para exibir os dados no `CustomerID` coluna.

## <a name="bind-the-control-to-look-up-companyname-from-the-customers-table"></a>Associar o controle para pesquisar o CompanyName da tabela Customers

Para configurar as associações de pesquisa, selecione a principal **clientes** nó no **fontes de dados** janela e arraste-os à caixa de combinação de caixa de **CustomerIDLookupBox** em **Form1**.

Isso configura a associação de dados para exibir o `CompanyName` da tabela `Customers` mantendo, ao mesmo tempo, o valor `CustomerID` da tabela `Orders`.

## <a name="run-the-application"></a>Executar o aplicativo

-   Pressione **F5** para executar o aplicativo.

-   Navegue por alguns registros e verifique se `CompanyName` aparece no controle `LookupBox`.

## <a name="see-also"></a>Consulte também

- [Associando controles do Windows Forms a dados no Visual Studio](../data-tools/bind-windows-forms-controls-to-data-in-visual-studio.md)