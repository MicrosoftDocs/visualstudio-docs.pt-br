---
title: Criar um controle de usuário Windows Forms com associação de dados
description: Entenda como criar um controle de usuário Windows Forms que dá suporte à vinculação de dados complexa, implementando a classe ComplexBindingPropertiesAttribute.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- data binding, user controls
- data binding, complex
- user controls [Visual Studio], complex data binding
author: ghogen
ms.author: ghogen
manager: jmartens
ms.workload:
- data-storage
ms.openlocfilehash: ff8c641cc0b817b5f2a145af49c5e0accdc295d0
ms.sourcegitcommit: 80fc9a72e9a1aba2d417dbfee997fab013fc36ac
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/02/2021
ms.locfileid: "106216326"
---
# <a name="create-a-windows-forms-user-control-that-supports-complex-data-binding"></a>Criar um controle de usuário do Windows Forms que dá suporte à vinculação de dados complexos

Ao exibir dados em formulários em aplicativos do Windows, você pode escolher controles existentes na **caixa de ferramentas**. Ou, você pode criar controles personalizados se seu aplicativo exigir funcionalidade que não esteja disponível nos controles padrão. Este passo a passo mostra como criar um controle que implementa o <xref:System.ComponentModel.ComplexBindingPropertiesAttribute>. Os controles que implementam o <xref:System.ComponentModel.ComplexBindingPropertiesAttribute> contêm uma propriedade de `DataSource` e `DataMember` que pode ser associada a dados. Tais controles são semelhantes a um <xref:System.Windows.Forms.DataGridView> ou <xref:System.Windows.Forms.ListBox>.

Para obter mais informações sobre a criação de controles, consulte [desenvolvendo Windows Forms controles em tempo de design](/dotnet/framework/winforms/controls/developing-windows-forms-controls-at-design-time).

Ao criar controles para uso em cenários de associação de dados, é necessário implementar um dos seguintes atributos de associação de dados:

|Uso de atributo de vinculação de dados|
| - |
|Implemente o <xref:System.ComponentModel.DefaultBindingPropertyAttribute> em controles simples, como um <xref:System.Windows.Forms.TextBox>, que exibe uma única coluna (ou propriedade) de dados. Para obter mais informações, consulte [criar um Windows Forms controle de usuário que dá suporte à vinculação de dados simples](../data-tools/create-a-windows-forms-user-control-that-supports-simple-data-binding.md).|
|Implemente o <xref:System.ComponentModel.ComplexBindingPropertiesAttribute> nos controles, como um <xref:System.Windows.Forms.DataGridView> que exibe listas (ou tabelas) de dados. (Esse processo é descrito nesta página de passo a passo.)|
|Implemente o <xref:System.ComponentModel.LookupBindingPropertiesAttribute> nos controles, como um <xref:System.Windows.Forms.ComboBox>que exibe listas (ou tabelas) de dados, mas também precisa apresentar uma única coluna ou propriedade. Para obter mais informações, consulte [criar um Windows Forms controle de usuário que dá suporte à vinculação de dados de pesquisa](../data-tools/create-a-windows-forms-user-control-that-supports-lookup-data-binding.md).|

Este passo a passo cria um controle complexo que exibe linhas de dados de uma tabela. Este exemplo usa a tabela `Customers` do banco de dados de exemplo Northwind. O controle de usuário complexo exibirá a tabela de clientes em uma <xref:System.Windows.Forms.DataGridView> no controle personalizado.

Durante este passo a passos, você aprenderá a:

- Adicionar um novo **Controle de Usuário** ao projeto.

- Projetar visualmente o controle do usuário.

- Implementar o atributo `ComplexBindingProperty`.

- Crie um conjunto de dados com o [Assistente de configuração de fonte de dados](../data-tools/media/data-source-configuration-wizard.png).

- Defina a tabela **Customers** na [janela Data Sources](add-new-data-sources.md#data-sources-window) para usar o novo controle complexo.

- Adicionar o novo controle, arrastando-o da **janela Fontes de Dados** para **Form1**.

## <a name="prerequisites"></a>Pré-requisitos

Este passo a passos usa SQL Server Express LocalDB e o banco de dados de exemplo Northwind.

1. Se você não tiver SQL Server Express LocalDB, instale-o na [SQL Server Express página de download](https://www.microsoft.com/sql-server/sql-server-editions-express)ou por meio do **instalador do Visual Studio**. No **instalador do Visual Studio**, você pode instalar o SQL Server Express LocalDB como parte da carga de trabalho de **armazenamento e processamento de dados** ou como um componente individual.

1. Instale o banco de dados de exemplo Northwind seguindo estas etapas:

    1. No Visual Studio, abra a janela **pesquisador de objetos do SQL Server** . (O Pesquisador de Objetos do SQL Server é instalado como parte da carga de trabalho de **armazenamento e processamento de dados** no instalador do Visual Studio.) Expanda o nó **SQL Server** . Clique com o botão direito do mouse na instância do LocalDB e selecione **nova consulta**.

       Uma janela do editor de consultas é aberta.

    1. Copie o [script do Transact-SQL Northwind](https://github.com/MicrosoftDocs/visualstudio-docs/blob/master/docs/data-tools/samples/northwind.sql?raw=true) para a área de transferência. Esse script T-SQL cria o banco de dados Northwind a partir do zero e o preenche com os mesmos.

    1. Cole o script T-SQL no editor de consultas e, em seguida, escolha o botão **executar** .

       Após um curto período, a consulta terminará de ser executada e o banco de dados Northwind será criado.

## <a name="create-a-windows-forms-app-project"></a>Criar um projeto de aplicativo Windows Forms

A primeira etapa é criar um projeto de **aplicativo Windows Forms** para C# ou Visual Basic. Nomeie o projeto como **ComplexControlWalkthrough**.

## <a name="add-a-user-control-to-the-project"></a>Adicionar um controle de usuário ao projeto

Como este passo a passos cria um controle vinculável de dados complexo de um **controle de usuário**, adicione um item de **controle de usuário** ao projeto:

1. No menu **Projeto**, escolha **Adicionar Controle do Usuário**.

1. Digite **ComplexDataGridView** na área **Nome** e clique em **Adicionar**.

    O controle **ComplexDataGridView** é adicionado ao **Gerenciador de Soluções** e abre no designer.

## <a name="design-the-complexdatagridview-control"></a>Criar o controle ComplexDataGridView

Para adicionar um <xref:System.Windows.Forms.DataGridView> ao controle de usuário, arraste um <xref:System.Windows.Forms.DataGridView> da **caixa de ferramentas** para a superfície de design do controle de usuário.

## <a name="add-the-required-data-binding-attribute"></a>Adicionar o atributo de associação de dados necessário

Para controles complexos que dão suporte à associação de dados, você pode implementar o <xref:System.ComponentModel.ComplexBindingPropertiesAttribute>:

1. Alterne o controle **ComplexDataGridView** para exibição de código. (No menu **Exibir**, selecione **Código**.)

1. Substitua o código no `ComplexDataGridView` pelo seguinte:

    :::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataDisplaying/CS/ComplexDataGridView.cs" id="Snippet4":::
    :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataDisplaying/VB/ComplexDataGridView.vb" id="Snippet4":::

1. No menu **Compilar** , escolha **Compilar solução**.

## <a name="create-a-data-source-from-your-database"></a>Criar uma fonte de dados do seu banco de dados

Use o assistente de **configuração de fonte de dados** para criar uma fonte de dados com base na `Customers` tabela no banco de dados de exemplo Northwind:

1. Para abrir a janela **fontes de dados** , no menu **dados** , clique em **mostrar fontes de dados**.

2. Na janela **Fontes de Dados**, selecione **Adicionar Nova Fonte de Dados** para iniciar o assistente de **Configuração de Fonte de Dados**.

3. Selecione **Banco de Dados** na página **Escolher um Tipo de Fonte de Dados** e, em seguida, clique em **Avançar**.

4. Na página **escolher sua conexão de dados** , siga um destes procedimentos:

   - Se uma conexão de dados com o banco de dados de exemplo Northwind estiver disponível na lista suspensa, selecione-o.

   - Selecione **Nova Conexão** para inicializar a caixa de diálogo **Adicionar/Modificar Conexão**.

5. Se o banco de dados exigir uma senha, selecione a opção para incluir dados confidenciais e, em seguida, clique em **Avançar**.

6. Na página **salvar cadeia de conexão no arquivo de configuração do aplicativo** , clique em **Avançar**.

7. Na página **escolher seus objetos de banco de dados** , expanda o nó **tabelas** .

8. Selecione a tabela `Customers` e clique em **Concluir**.

   O **NorthwindDataSet** é adicionado ao seu projeto e a `Customers` tabela é exibida na janela **Data Sources** .

## <a name="set-the-customers-table-to-use-the-complexdatagridview-control"></a>Definir a tabela Customers para usar o controle ComplexDataGridView

Na janela **fontes de dados** , você pode definir o controle a ser criado antes de arrastar itens para o formulário:

1. Abra **Form1** no designer.

1. Expanda o nó **Clientes** na janela **Fontes de Dados**.

1. Clique na seta suspensa no nó **Clientes** e escolha **Personalizar**.

1. Selecione **ComplexDataGridView** na lista de **Controles Associados** na caixa de diálogo **Opções de Personalização da Interface do Usuário de Dados**.

1. Clique na seta suspensa na tabela `Customers` e escolha **ComplexDataGridView** na lista de controle.

## <a name="add-controls-to-the-form"></a>Adicionar controles ao formulário

Você pode criar os controles associados a dados arrastando itens da janela **fontes de dados** para o formulário. Arraste o nó principal **Clientes** da janela **Fontes de Dados** para o formulário. Verifique se o controle **ComplexDataGridView** é usado para exibir os dados da tabela.

## <a name="run-the-application"></a>Executar o aplicativo

Pressione **F5** para executar o aplicativo.

## <a name="next-steps"></a>Próximas etapas

Dependendo dos requisitos do aplicativo, existem várias etapas que você pode realizar após criar um controle com suporte a associação de dados. Algumas etapas seguintes típicas incluem:

- Colocando os controles personalizados em uma biblioteca de controles para que você possa reutilizá-los em outros aplicativos.

- Criando controles que suportam cenários de pesquisa. Para obter mais informações, consulte [criar um Windows Forms controle de usuário que dá suporte à vinculação de dados de pesquisa](../data-tools/create-a-windows-forms-user-control-that-supports-lookup-data-binding.md).

## <a name="see-also"></a>Confira também

- [Associar controles do Windows Forms a dados no Visual Studio](../data-tools/bind-windows-forms-controls-to-data-in-visual-studio.md)
- [Definir o controle a ser criado quando arrastado da janela Fontes de Dados](../data-tools/set-the-control-to-be-created-when-dragging-from-the-data-sources-window.md)
- [Controles de Windows Forms](/dotnet/framework/winforms/controls/index)
