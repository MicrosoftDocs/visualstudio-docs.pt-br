---
title: Criar um controle de usuário do Windows Forms com associação de dados
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- data binding, user controls
- data binding, complex
- user controls [Visual Studio], complex data binding
author: gewarren
ms.author: gewarren
manager: douge
ms.prod: visual-studio-dev15
ms.technology: vs-data-tools
ms.workload:
- data-storage
ms.openlocfilehash: 7de5cbfe7de8919143cd30517c18f9e5ad6ba598
ms.sourcegitcommit: 81e9d90843ead658bc73b30c869f25921d99e116
ms.translationtype: MTE95
ms.contentlocale: pt-BR
ms.lasthandoff: 11/26/2018
ms.locfileid: "52305241"
---
# <a name="create-a-windows-forms-user-control-that-supports-complex-data-binding"></a>Criar um controle de usuário do Windows Forms que dá suporte à vinculação de dados complexos

Ao exibir dados em formulários nos aplicativos do Windows, você pode escolher os controles existentes da Caixa de Ferramentas** ou criar controles personalizados se seu aplicativo exigir alguma funcionalidade que não esteja disponível nos controles padrão. Este passo a passo mostra como criar um controle que implementa o <xref:System.ComponentModel.ComplexBindingPropertiesAttribute>. Os controles que implementam o <xref:System.ComponentModel.ComplexBindingPropertiesAttribute> contêm uma propriedade de `DataSource` e `DataMember` que pode ser associada a dados. Tais controles são semelhantes a um <xref:System.Windows.Forms.DataGridView> ou <xref:System.Windows.Forms.ListBox>.

Para obter mais informações sobre criação de controle, consulte [controla o desenvolvimento de Windows Forms em tempo de design](/dotnet/framework/winforms/controls/developing-windows-forms-controls-at-design-time).

Ao criar controles para uso em cenários de associação de dados, é necessário implementar um dos seguintes atributos de associação de dados:

|Uso do atributo de associação de dados|
| - |
|Implemente o <xref:System.ComponentModel.DefaultBindingPropertyAttribute> em controles simples, como um <xref:System.Windows.Forms.TextBox>, que exibe uma única coluna (ou propriedade) de dados. Para obter mais informações, consulte [criar um controle de usuário do Windows Forms que dá suporte à vinculação de dados simples](../data-tools/create-a-windows-forms-user-control-that-supports-simple-data-binding.md).|
|Implemente o <xref:System.ComponentModel.ComplexBindingPropertiesAttribute> nos controles, como um <xref:System.Windows.Forms.DataGridView> que exibe listas (ou tabelas) de dados. (Esse processo é descrito nesta página de passo a passo.)|
|Implemente o <xref:System.ComponentModel.LookupBindingPropertiesAttribute> nos controles, como um <xref:System.Windows.Forms.ComboBox>que exibe listas (ou tabelas) de dados, mas também precisa apresentar uma única coluna ou propriedade. Para obter mais informações, consulte [criar um controle de usuário do Windows Forms que dá suporte à vinculação de dados de pesquisa](../data-tools/create-a-windows-forms-user-control-that-supports-lookup-data-binding.md).|

Este passo a passo cria um controle complexo que exibe linhas de dados de uma tabela. Este exemplo usa a tabela `Customers` do banco de dados de exemplo Northwind. O controle de usuário complexo exibirá a tabela de clientes em uma <xref:System.Windows.Forms.DataGridView> no controle personalizado.

Durante este passo a passo, você aprenderá a:

- Criar um novo aplicativo Windows Form.

- Adicionar um novo Controle de Usuário** ao projeto.

- Projetar visualmente o controle do usuário.

- Implementar o atributo `ComplexBindingProperty`.

- Criar um conjunto de dados com o [Data Source Configuration Wizard](../data-tools/media/data-source-configuration-wizard.png).

- Defina as **clientes** na tabela a [janela fontes de dados](add-new-data-sources.md#data-sources-window) para usar o novo controle complexo.

- Adicionar o novo controle, arrastando-o da janela Fontes de Dados **para Form1**.

## <a name="prerequisites"></a>Pré-requisitos

Este passo a passo usa o SQL Server Express LocalDB e o banco de dados de exemplo Northwind.

1. Se você não tiver o SQL Server Express LocalDB, instalá-lo a partir de [página de download do SQL Server Express](https://www.microsoft.com/sql-server/sql-server-editions-express), ou por meio de **instalador do Visual Studio**. No **instalador do Visual Studio**, você pode instalar o SQL Server Express LocalDB como parte do **armazenamento de dados e processamento** carga de trabalho, ou como um componente individual.

1. Instale o banco de dados de exemplo Northwind, seguindo estas etapas:

    1. No Visual Studio, abra o **SQL Server Object Explorer** janela. (Pesquisador de objetos do SQL Server é instalado como parte dos **armazenamento de dados e processamento** carga de trabalho no instalador do Visual Studio.) Expanda o **SQL Server** nó. Clique com botão direito na instância do LocalDB e selecione **nova consulta**.

       Abre uma janela do editor de consulta.

    1. Cópia de [script Transact-SQL Northwind](https://github.com/MicrosoftDocs/visualstudio-docs/blob/master/docs/data-tools/samples/northwind.sql?raw=true) na área de transferência. Este script T-SQL cria o banco de dados Northwind do zero e a preenche com dados.

    1. Cole o script T-SQL no editor de consultas e, em seguida, escolha o **Execute** botão.

       Após alguns instantes, a consulta termina a execução e o banco de dados Northwind é criado.

## <a name="create-a-windows-forms-application"></a>Criar um aplicativo do Windows Forms.

A primeira etapa é criar uma **aplicativo do Windows Forms**:

1. No Visual Studio, sobre o **arquivo** menu, selecione **New** > **projeto**.

1. Expanda o **Visual c#** ou **Visual Basic** no painel esquerdo, em seguida, selecione **área de trabalho do Windows**.

1. No painel central, selecione a **aplicativo do Windows Forms** tipo de projeto.

1. Nomeie o projeto **ComplexControlWalkthrough**e, em seguida, escolha **Okey**.

    O projeto ComplexControlWalkthrough **é criado e adicionado ao Gerenciador de Soluções**.

## <a name="add-a-user-control-to-the-project"></a>Adicionar um controle de usuário ao projeto

Porque este passo a passo cria um controle associável a dados complexo de um **controle de usuário**, adicione uma **controle de usuário** item ao projeto:

1. No menu Projeto **, escolha Adicionar Controle do Usuário**.

1. Digite ComplexDataGridView na área Nome **e clique em Adicionar**.

    O controle ComplexDataGridView **é adicionado ao Gerenciador de Soluções** e abre no designer.

## <a name="design-the-complexdatagridview-control"></a>Criar o controle ComplexDataGridView

Para adicionar um <xref:System.Windows.Forms.DataGridView> ao controle de usuário, arraste um <xref:System.Windows.Forms.DataGridView> da **caixa de ferramentas** na superfície de design do controle de usuário.

## <a name="add-the-required-data-binding-attribute"></a>Adicione o atributo obrigatório de associação de dados

Para controles complexos que suportam associação de dados, você pode implementar o <xref:System.ComponentModel.ComplexBindingPropertiesAttribute>.

1. Alterne o controle ComplexDataGridView** para exibição de código. (No menu Exibir **, selecione Código**.)

1. Substitua o código no `ComplexDataGridView` pelo seguinte:

    [!code-csharp[VbRaddataDisplaying#4](../data-tools/codesnippet/CSharp/create-a-windows-forms-user-control-that-supports-complex-data-binding_1.cs)]
    [!code-vb[VbRaddataDisplaying#4](../data-tools/codesnippet/VisualBasic/create-a-windows-forms-user-control-that-supports-complex-data-binding_1.vb)]

1. No menu **Compilação**, escolha **Compilar Solução**.

## <a name="create-a-data-source-from-your-database"></a>Criar uma fonte de dados do banco de dados

Use o **Data Source Configuration** Assistente para criar uma fonte de dados com base no `Customers` tabela no banco de dados de exemplo Northwind:

1.  Para abrir o **fontes de dados** janela diante de **dados** menu, clique em **Mostrar fontes de dados**.

2.  Na janela Fontes de Dados **, selecione Adicionar Nova Fonte de Dados** para iniciar o Assistente de Configuração de Fonte de Dados **.

3.  Selecione Base de dados **na página Escolher um Tipo de Fonte de Dados** e, em seguida, clique em Próximo **.

4.  Na página Escolha a Conexão de Dados **, faça o seguinte:

    - Se uma conexão de dados com o banco de dados de exemplo Northwind estiver disponível na lista suspensa, selecione-o.

    - Selecione Nova Conexão **para iniciar a caixa de diálogo Adicionar/Modificar Conexão**.

5.  Se o banco de dados exigir uma senha, selecione a opção para incluir dados confidenciais e, em seguida, clique em Próximo **.

6.  Sobre o **salvar a cadeia de caracteres de conexão para o arquivo de configuração de aplicativo** , clique em **próxima**.

7.  Sobre o **Choose your Database Objects** página, expanda o **tabelas** nó.

8.  Selecione a tabela `Customers` e clique em Concluir **.

    O NorthwindDataSet**é adicionado ao projeto e a tabela** aparece na janela Fontes de Dados`Customers`.

## <a name="set-the-customers-table-to-use-the-complexdatagridview-control"></a>Definir a tabela de clientes para usar o controle ComplexDataGridView

Na janela Fontes de Dados **, você pode definir o controle a ser criado antes de arrastar itens para seu formulário.

1. Abra **Form1** no designer.

1. Expanda o nó Clientes **na janela Fontes de Dados**.

1. Clique na seta suspensa no nó Clientes **e escolha Personalizar**.

1. Selecione ComplexDataGridView **na lista de Controles Associados** na caixa de diálogo Opções de Personalização da IU de Dados **.

1. Clique na seta suspensa na tabela `Customers` e escolha ComplexDataGridView** na lista de controle.

## <a name="add-controls-to-the-form"></a>Adicionar controles ao formulário.

Você pode criar controles de associação de dados arrastando itens da janela Fontes de Dados** para um formulário. Arraste o nó principal Clientes **da janela Fontes de Dados** para o formulário. Verifique se que o **ComplexDataGridView** controle é usado para exibir os dados da tabela.

## <a name="run-the-application"></a>Executar o aplicativo

Pressione **F5** para executar o aplicativo.

## <a name="next-steps"></a>Próximas etapas

Dependendo dos requisitos do aplicativo, existem várias etapas que você pode realizar após criar um controle com suporte a associação de dados. Algumas etapas seguintes típicas incluem:

- Colocando os controles personalizados em uma biblioteca de controles para que você possa reutilizá-los em outros aplicativos.

- Criando controles que suportam cenários de pesquisa. Para obter mais informações, consulte [criar um controle de usuário do Windows Forms que dá suporte à vinculação de dados de pesquisa](../data-tools/create-a-windows-forms-user-control-that-supports-lookup-data-binding.md).

## <a name="see-also"></a>Consulte também

- [Associando controles do Windows Forms a dados no Visual Studio](../data-tools/bind-windows-forms-controls-to-data-in-visual-studio.md)
- [Definir o controle a ser criado quando arrastado da janela Fontes de Dados](../data-tools/set-the-control-to-be-created-when-dragging-from-the-data-sources-window.md)
- [Controles dos Windows Forms](/dotnet/framework/winforms/controls/index)