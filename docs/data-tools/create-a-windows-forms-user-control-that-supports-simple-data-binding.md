---
title: Criar um controle de usuário compatível com associação de dados simples
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- custom controls [Visual Studio], Data Sources Window
- Data Sources Window, controls
ms.assetid: b1488366-6dfb-454e-9751-f42fd3f3ddfb
author: gewarren
ms.author: gewarren
manager: douge
ms.prod: visual-studio-dev15
ms.technology: vs-data-tools
ms.workload:
- data-storage
ms.openlocfilehash: 673e510536ab866f3be90da630d3cfa261bb98c6
ms.sourcegitcommit: 81e9d90843ead658bc73b30c869f25921d99e116
ms.translationtype: MTE95
ms.contentlocale: pt-BR
ms.lasthandoff: 11/26/2018
ms.locfileid: "52305397"
---
# <a name="create-a-windows-forms-user-control-that-supports-simple-data-binding"></a>Criar um controle de usuário do Windows Forms que dá suporte à vinculação de dados simples

Ao exibir dados em formulários nos aplicativos do Windows, você poderá escolher os controles existentes da **Caixa de Ferramentas** ou criar controles personalizados se o aplicativo exigir alguma funcionalidade que não esteja disponível nos controles padrão. Este passo a passo mostra como criar um controle que implementa o <xref:System.ComponentModel.DefaultBindingPropertyAttribute>. Os controles que implementam o <xref:System.ComponentModel.DefaultBindingPropertyAttribute> contêm uma propriedade que pode ser associada a dados. Tais controles são semelhantes a um <xref:System.Windows.Forms.TextBox> ou <xref:System.Windows.Forms.CheckBox>.

Para obter mais informações sobre criação de controle, consulte [desenvolvendo controles dos Windows Forms em tempo de Design](/dotnet/framework/winforms/controls/developing-windows-forms-controls-at-design-time).

Ao criar controles para uso em cenários de vinculação de dados, você deve implementar um dos seguintes atributos de associação de dados:

|Uso do atributo de associação de dados|
| - |
|Implemente o <xref:System.ComponentModel.DefaultBindingPropertyAttribute> em controles simples, como um <xref:System.Windows.Forms.TextBox>, que exibe uma única coluna (ou propriedade) de dados. (Esse processo é descrito nesta página de passo a passo.)|
|Implemente o <xref:System.ComponentModel.ComplexBindingPropertiesAttribute> nos controles, como um <xref:System.Windows.Forms.DataGridView> que exibe listas (ou tabelas) de dados. Para obter mais informações, consulte [criar um controle de usuário do Windows Forms que dá suporte à vinculação de dados complexos](../data-tools/create-a-windows-forms-user-control-that-supports-complex-data-binding.md).|
|Implemente o <xref:System.ComponentModel.LookupBindingPropertiesAttribute> nos controles, como um <xref:System.Windows.Forms.ComboBox>que exibe listas (ou tabelas) de dados, mas também precisa apresentar uma única coluna ou propriedade. Para obter mais informações, consulte [criar um controle de usuário do Windows Forms que dá suporte à vinculação de dados de pesquisa](../data-tools/create-a-windows-forms-user-control-that-supports-lookup-data-binding.md).|

Este passo a passo cria um controle simples que exibe dados de uma única coluna em uma tabela. Este exemplo usa a coluna `Phone` da tabela `Customers` do banco de dados de exemplo Northwind. O controle de usuário simples exibe números de telefone dos clientes em um formato de número de telefone padrão, usando um <xref:System.Windows.Forms.MaskedTextBox> e definindo a máscara para um número de telefone.

Durante este passo a passo, você aprenderá a:

-   Criar um novo **Aplicativo do Windows Forms**.

-   Adicionar um novo **Controle de Usuário** ao projeto.

-   Projetar visualmente o controle do usuário.

-   Implementar o atributo `DefaultBindingProperty`.

-   Criar um conjunto de dados com o **configuração de fonte de dados** assistente.

-   Definir a coluna **Telefone** na janela **Fontes de Dados** para usar o novo controle.

-   Criar um formulário para exibir dados no novo controle.

## <a name="prerequisites"></a>Pré-requisitos

Este passo a passo usa o SQL Server Express LocalDB e o banco de dados de exemplo Northwind.

1.  Se você não tiver o SQL Server Express LocalDB, instalá-lo a partir de [página de download do SQL Server Express](https://www.microsoft.com/sql-server/sql-server-editions-express), ou por meio de **instalador do Visual Studio**. No **instalador do Visual Studio**, você pode instalar o SQL Server Express LocalDB como parte do **armazenamento de dados e processamento** carga de trabalho, ou como um componente individual.

2.  Instale o banco de dados de exemplo Northwind, seguindo estas etapas:

    1. No Visual Studio, abra o **SQL Server Object Explorer** janela. (Pesquisador de objetos do SQL Server é instalado como parte dos **armazenamento de dados e processamento** carga de trabalho na **instalador do Visual Studio**.) Expanda o **SQL Server** nó. Clique com botão direito na instância do LocalDB e selecione **nova consulta**.

       Abre uma janela do editor de consulta.

    2. Cópia de [script Transact-SQL Northwind](https://github.com/MicrosoftDocs/visualstudio-docs/blob/master/docs/data-tools/samples/northwind.sql?raw=true) na área de transferência. Este script T-SQL cria o banco de dados Northwind do zero e a preenche com dados.

    3. Cole o script T-SQL no editor de consultas e, em seguida, escolha o **Execute** botão.

       Após alguns instantes, a consulta termina a execução e o banco de dados Northwind é criado.

## <a name="create-a-windows-forms-application"></a>Criar um aplicativo do Windows Forms

A primeira etapa é criar uma **aplicativo do Windows Forms**:

1. No Visual Studio, sobre o **arquivo** menu, selecione **New** > **projeto**.

2. Expanda o **Visual c#** ou **Visual Basic** no painel esquerdo, em seguida, selecione **área de trabalho do Windows**.

3. No painel central, selecione a **aplicativo do Windows Forms** tipo de projeto.

4. Nomeie o projeto **SimpleControlWalkthrough**e, em seguida, escolha **Okey**.

     O projeto **SimpleControlWalkthrough** é criado e adicionado ao **Gerenciador de Soluções**.

## <a name="add-a-user-control-to-the-project"></a>Adicionar um controle de usuário ao projeto

Este passo a passo cria um simples controle associável a dados de um **controle de usuário**. Adicionar um **controle de usuário** de item para o **SimpleControlWalkthrough** projeto:

1.  No menu **Projeto**, escolha **Adicionar Controle do Usuário**.

2.  Digite **PhoneNumberBox** na área Nome e clique em **Adicionar**.

     O controle **PhoneNumberBox** é adicionado ao **Gerenciador de Soluções** e abre no designer.

## <a name="design-the-phonenumberbox-control"></a>Projetar o controle PhoneNumberBox

Este passo a passo expande existente <xref:System.Windows.Forms.MaskedTextBox> para criar o **PhoneNumberBox** controle:

1.  Arraste um <xref:System.Windows.Forms.MaskedTextBox> da **Caixa de Ferramentas** para a superfície de design do controle de usuário.

2.  Selecione a smart tag no <xref:System.Windows.Forms.MaskedTextBox> que você acabou de arrastar e selecione **Definir Máscara**.

3.  Selecione **Número do telefone** na caixa de diálogo **Máscara de Entrada** e clique em **OK** para configurar a máscara.

## <a name="add-the-required-data-binding-attribute"></a>Adicione o atributo obrigatório de associação de dados

Para controles simples que dão suporte à associação de dados, implemente o <xref:System.ComponentModel.DefaultBindingPropertyAttribute>:

1.  Opção de **PhoneNumberBox** controle a exibição de código. (No menu **Exibir**, escolha **Código**.)

2.  Substitua o código na **PhoneNumberBox** com o seguinte:

     [!code-csharp[VbRaddataDisplaying#3](../data-tools/codesnippet/CSharp/create-a-windows-forms-user-control-that-supports-simple-data-binding_1.cs)]
     [!code-vb[VbRaddataDisplaying#3](../data-tools/codesnippet/VisualBasic/create-a-windows-forms-user-control-that-supports-simple-data-binding_1.vb)]

3.  No menu **Compilação**, escolha **Compilar Solução**.

## <a name="create-a-data-source-from-your-database"></a>Criar uma fonte de dados do banco de dados

Esta etapa usa o **Assistente de Configuração de Fonte de Dados** para criar uma fonte de dados com base na tabela `Customers` no banco de dados de exemplo Northwind. É preciso ter acesso ao banco de dados de exemplo Northwind para criar a conexão. Para obter informações sobre como configurar o banco de dados de exemplo Northwind, consulte [como: instalar bancos de dados de exemplo](../data-tools/installing-database-systems-tools-and-samples.md).

1.  Para abrir o **fontes de dados** janela diante de **dados** menu, clique em **Mostrar fontes de dados**.

2.  Na janela **Fontes de Dados**, selecione **Adicionar Nova Fonte de Dados** para iniciar o assistente de **Configuração de Fonte de Dados**.

3.  Na página **Escolher um Tipo de Fonte de Dados**, selecione **Banco de Dados** e clique em **Avançar**.

4.  Na página **Escolha a Conexão de Dados**, faça o seguinte:

    -   Se uma conexão de dados com o banco de dados de exemplo Northwind estiver disponível na lista suspensa, selecione-o.

    -   Selecione **Nova Conexão** para inicializar a caixa de diálogo **Adicionar/Modificar Conexão**.

5.  Se o banco de dados exigir uma senha, selecione a opção para incluir dados confidenciais e, em seguida, clique em **Avançar**.

6.  Sobre o **salvar a cadeia de caracteres de conexão para o arquivo de configuração de aplicativo** , clique em **próxima**.

7.  Sobre o **Choose your Database Objects** página, expanda o **tabelas** nó.

8.  Selecione a tabela `Customers` e clique em **Concluir**.

     O **NorthwindDataSet** é adicionado ao projeto e a tabela `Customers` aparece na janela **Fontes de Dados**.

## <a name="set-the-phone-column-to-use-the-phonenumberbox-control"></a>Definir a coluna telefone para usar o controle PhoneNumberBox

Na janela **Fontes de Dados**, você pode definir o controle a ser criado antes de arrastar itens para seu formulário:

1.  Abra **Form1** no designer.

2.  Expanda o nó **Clientes** na janela **Fontes de Dados**.

3.  Clique na seta suspensa no nó **Clientes** e escolha **Detalhes** na lista de controle.

4.  Clique na seta suspensa na coluna **Telefone** e escolha **Personalizar**.

5.  Selecione **PhoneNumberBox** na lista de **Controles Associados** na caixa de diálogo **Opções de Personalização da Interface do Usuário de Dados**.

6.  Clique na seta suspensa na coluna **Telefone** e escolha **PhoneNumberBox**.

## <a name="add-controls-to-the-form"></a>Adicionar controles ao formulário

É possível criar controles de associação de dados ao arrastar itens da janela **Fontes de Dados** para o formulário.

Para criar controles associados a dados no formulário, arraste principal **clientes** nó a partir o **fontes de dados** janela para o formulário e verificar se o **PhoneNumberBox** controle é usado para exibir os dados do **Phone** coluna.

     Data-bound controls with descriptive labels appear on the form, along with a tool strip (<xref:System.Windows.Forms.BindingNavigator>) for navigating records. A [NorthwindDataSet](../data-tools/dataset-tools-in-visual-studio.md), CustomersTableAdapter, <xref:System.Windows.Forms.BindingSource>, and <xref:System.Windows.Forms.BindingNavigator> appear in the component tray.

## <a name="run-the-application"></a>Executar o aplicativo

Pressione **F5** para executar o aplicativo.

## <a name="next-steps"></a>Próximas etapas

Dependendo dos requisitos do aplicativo, existem várias etapas que você pode realizar após criar um controle com suporte a associação de dados. Algumas etapas seguintes típicas incluem:

-   Colocando os controles personalizados em uma biblioteca de controles para que você possa reutilizá-los em outros aplicativos.

-   Criando controles que suportam cenários de associação de dados mais complexos. Para obter mais informações, consulte [criar um controle de usuário do Windows Forms que dá suporte à vinculação de dados complexos](../data-tools/create-a-windows-forms-user-control-that-supports-complex-data-binding.md) e [criar um controle de usuário do Windows Forms que dá suporte à vinculação de dados de pesquisa](../data-tools/create-a-windows-forms-user-control-that-supports-lookup-data-binding.md).

## <a name="see-also"></a>Consulte também

- [Associando controles do Windows Forms a dados no Visual Studio](../data-tools/bind-windows-forms-controls-to-data-in-visual-studio.md)
- [Definir o controle a ser criado quando arrastado da janela Fontes de Dados](../data-tools/set-the-control-to-be-created-when-dragging-from-the-data-sources-window.md)