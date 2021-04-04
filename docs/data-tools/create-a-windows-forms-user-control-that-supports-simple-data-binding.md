---
title: Criar controles de usuário que dão suporte à vinculação de dados simples
description: Aprenda a criar um controle de usuário Windows Forms que dá suporte à vinculação de dados simples, usando a classe DefaultBindingPropertyAttribute no Visual Studio.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- custom controls [Visual Studio], Data Sources Window
- Data Sources Window, controls
ms.assetid: b1488366-6dfb-454e-9751-f42fd3f3ddfb
author: ghogen
ms.author: ghogen
manager: jmartens
ms.workload:
- data-storage
ms.openlocfilehash: 7f26de2f26a132fc210920d94742ec7883612d66
ms.sourcegitcommit: 80fc9a72e9a1aba2d417dbfee997fab013fc36ac
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/02/2021
ms.locfileid: "106216300"
---
# <a name="create-a-windows-forms-user-control-that-supports-simple-data-binding"></a>Criar um controle de usuário do Windows Forms que dá suporte à vinculação de dados simples

Ao exibir dados em formulários nos aplicativos do Windows, você poderá escolher os controles existentes da **Caixa de Ferramentas** ou criar controles personalizados se o aplicativo exigir alguma funcionalidade que não esteja disponível nos controles padrão. Este passo a passo mostra como criar um controle que implementa o <xref:System.ComponentModel.DefaultBindingPropertyAttribute>. Os controles que implementam o <xref:System.ComponentModel.DefaultBindingPropertyAttribute> contêm uma propriedade que pode ser associada a dados. Tais controles são semelhantes a um <xref:System.Windows.Forms.TextBox> ou <xref:System.Windows.Forms.CheckBox>.

Para obter mais informações sobre a criação de controles, consulte [desenvolvendo Windows Forms controles em tempo de design](/dotnet/framework/winforms/controls/developing-windows-forms-controls-at-design-time).

Ao criar controles para uso em cenários de vinculação de dados, você deve implementar um dos seguintes atributos de vinculação de dados:

|Uso de atributo de vinculação de dados|
| - |
|Implemente o <xref:System.ComponentModel.DefaultBindingPropertyAttribute> em controles simples, como um <xref:System.Windows.Forms.TextBox>, que exibe uma única coluna (ou propriedade) de dados. (Esse processo é descrito nesta página de passo a passo.)|
|Implemente o <xref:System.ComponentModel.ComplexBindingPropertiesAttribute> nos controles, como um <xref:System.Windows.Forms.DataGridView> que exibe listas (ou tabelas) de dados. Para obter mais informações, consulte [criar um Windows Forms controle de usuário que dá suporte à ligação de dados complexa](../data-tools/create-a-windows-forms-user-control-that-supports-complex-data-binding.md).|
|Implemente o <xref:System.ComponentModel.LookupBindingPropertiesAttribute> nos controles, como um <xref:System.Windows.Forms.ComboBox>que exibe listas (ou tabelas) de dados, mas também precisa apresentar uma única coluna ou propriedade. Para obter mais informações, consulte [criar um Windows Forms controle de usuário que dá suporte à vinculação de dados de pesquisa](../data-tools/create-a-windows-forms-user-control-that-supports-lookup-data-binding.md).|

Este passo a passo cria um controle simples que exibe dados de uma única coluna em uma tabela. Este exemplo usa a coluna `Phone` da tabela `Customers` do banco de dados de exemplo Northwind. O controle de usuário simples exibe os números de telefone dos clientes em um formato de número de telefone padrão, usando um <xref:System.Windows.Forms.MaskedTextBox> e definindo a máscara para um número de telefone.

Durante este passo a passo, você aprenderá a:

- Crie um novo **aplicativo Windows Forms**.

- Adicionar um novo **Controle de Usuário** ao projeto.

- Projetar visualmente o controle do usuário.

- Implementar o atributo `DefaultBindingProperty`.

- Crie um conjunto de dados com o assistente de **configuração de fonte de dados** .

- Definir a coluna **Telefone** na janela **Fontes de Dados** para usar o novo controle.

- Criar um formulário para exibir dados no novo controle.

## <a name="prerequisites"></a>Pré-requisitos

Este passo a passos usa SQL Server Express LocalDB e o banco de dados de exemplo Northwind.

1. Se você não tiver SQL Server Express LocalDB, instale-o na [SQL Server Express página de download](https://www.microsoft.com/sql-server/sql-server-editions-express)ou por meio do **instalador do Visual Studio**. No **instalador do Visual Studio**, você pode instalar o SQL Server Express LocalDB como parte da carga de trabalho de **armazenamento e processamento de dados** ou como um componente individual.

2. Instale o banco de dados de exemplo Northwind seguindo estas etapas:

    1. No Visual Studio, abra a janela **pesquisador de objetos do SQL Server** . (O Pesquisador de Objetos do SQL Server é instalado como parte da carga de trabalho de **armazenamento e processamento de dados** no **instalador do Visual Studio**.) Expanda o nó **SQL Server** . Clique com o botão direito do mouse na instância do LocalDB e selecione **nova consulta**.

       Uma janela do editor de consultas é aberta.

    2. Copie o [script do Transact-SQL Northwind](https://github.com/MicrosoftDocs/visualstudio-docs/blob/master/docs/data-tools/samples/northwind.sql?raw=true) para a área de transferência. Esse script T-SQL cria o banco de dados Northwind a partir do zero e o preenche com os mesmos.

    3. Cole o script T-SQL no editor de consultas e, em seguida, escolha o botão **executar** .

       Após um curto período, a consulta terminará de ser executada e o banco de dados Northwind será criado.

## <a name="create-a-windows-forms-application"></a>Criar um aplicativo do Windows Forms

A primeira etapa é criar um **aplicativo Windows Forms**:

1. No Visual Studio, no menu **Arquivo**, selecione **Novo** > **Projeto**.

2. Expanda o **Visual C#** ou **Visual Basic** no painel esquerdo e, em seguida, selecione **área de trabalho do Windows**.

3. No painel central, selecione o tipo de projeto **Windows Forms aplicativo** .

4. Nomeie o projeto **SimpleControlWalkthrough** e escolha **OK**.

     O projeto **SimpleControlWalkthrough** é criado e adicionado ao **Gerenciador de Soluções**.

## <a name="add-a-user-control-to-the-project"></a>Adicionar um controle de usuário ao projeto

Este tutorial cria um controle vinculável de dados simples de um **controle de usuário**. Adicione um item de **controle de usuário** ao projeto **SimpleControlWalkthrough** :

1. No menu **Projeto**, escolha **Adicionar Controle do Usuário**.

2. Digite **PhoneNumberBox** na área Nome e clique em **Adicionar**.

     O controle **PhoneNumberBox** é adicionado ao **Gerenciador de Soluções** e abre no designer.

## <a name="design-the-phonenumberbox-control"></a>Criar o controle PhoneNumberBox

Este passo a passos se expande sobre o existente <xref:System.Windows.Forms.MaskedTextBox> para criar o controle **PhoneNumberBox** :

1. Arraste um <xref:System.Windows.Forms.MaskedTextBox> da **Caixa de Ferramentas** para a superfície de design do controle de usuário.

2. Selecione a smart tag no <xref:System.Windows.Forms.MaskedTextBox> que você acabou de arrastar e selecione **Definir Máscara**.

3. Selecione **Número do telefone** na caixa de diálogo **Máscara de Entrada** e clique em **OK** para configurar a máscara.

## <a name="add-the-required-data-binding-attribute"></a>Adicionar o atributo de associação de dados necessário

Para controles simples que dão suporte à associação de dados, implemente o <xref:System.ComponentModel.DefaultBindingPropertyAttribute>:

1. Alterne o controle **PhoneNumberBox** para o modo de exibição de código. (No menu **Exibir**, escolha **Código**.)

2. Substitua o código no **PhoneNumberBox** pelo seguinte:

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataDisplaying/CS/PhoneNumberBox.cs" id="Snippet3":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataDisplaying/VB/PhoneNumberBox.vb" id="Snippet3":::

3. No menu **Compilar** , escolha **Compilar solução**.

## <a name="create-a-data-source-from-your-database"></a>Criar uma fonte de dados do seu banco de dados

Esta etapa usa o assistente de **configuração de fonte de dados** para criar uma fonte de dados com base na `Customers` tabela no banco de dados de exemplo Northwind. É preciso ter acesso ao banco de dados de exemplo Northwind para criar a conexão. Para obter informações sobre como configurar o banco de dados de exemplo Northwind, consulte [How to: Install exemplo databases](../data-tools/installing-database-systems-tools-and-samples.md).

1. Para abrir a janela **fontes de dados** , no menu **dados** , clique em **mostrar fontes de dados**.

2. Na janela **Fontes de Dados**, selecione **Adicionar Nova Fonte de Dados** para iniciar o assistente de **Configuração de Fonte de Dados**.

3. Na página **Escolher um Tipo de Fonte de Dados**, selecione **Banco de Dados** e clique em **Avançar**.

4. Na página **Escolha a Conexão de Dados**, faça o seguinte:

    - Se uma conexão de dados com o banco de dados de exemplo Northwind estiver disponível na lista suspensa, selecione-o.

    - Selecione **Nova Conexão** para inicializar a caixa de diálogo **Adicionar/Modificar Conexão**.

5. Se o banco de dados exigir uma senha, selecione a opção para incluir dados confidenciais e, em seguida, clique em **Avançar**.

6. Na página **salvar cadeia de conexão no arquivo de configuração do aplicativo** , clique em **Avançar**.

7. Na página **escolher seus objetos de banco de dados** , expanda o nó **tabelas** .

8. Selecione a tabela `Customers` e clique em **Concluir**.

     O **NorthwindDataSet** é adicionado ao seu projeto e a `Customers` tabela é exibida na janela **Data Sources** .

## <a name="set-the-phone-column-to-use-the-phonenumberbox-control"></a>Definir a coluna de telefone para usar o controle PhoneNumberBox

Na janela **fontes de dados** , você pode definir o controle a ser criado antes de arrastar itens para o formulário:

1. Abra **Form1** no designer.

2. Expanda o nó **Clientes** na janela **Fontes de Dados**.

3. Clique na seta suspensa no nó **Clientes** e escolha **Detalhes** na lista de controle.

4. Clique na seta suspensa na coluna **Telefone** e escolha **Personalizar**.

5. Selecione **PhoneNumberBox** na lista de **Controles Associados** na caixa de diálogo **Opções de Personalização da Interface do Usuário de Dados**.

6. Clique na seta suspensa na coluna **Telefone** e escolha **PhoneNumberBox**.

## <a name="add-controls-to-the-form"></a>Adicionar controles ao formulário

É possível criar controles de associação de dados ao arrastar itens da janela **Fontes de Dados** para o formulário.

Para criar controles ligados a dados no formulário, arraste o nó **clientes** principais da janela **fontes de dados** para o formulário e verifique se o controle **PhoneNumberBox** é usado para exibir os dados na coluna **telefone** .

Os controles de associação de dados com rótulos descritivos são exibidos no formulário, juntamente com uma faixa de ferramentas (<xref:System.Windows.Forms.BindingNavigator>) para registros de navegação. Um [NorthwindDataSet](../data-tools/dataset-tools-in-visual-studio.md), CustomersTableAdapter, <xref:System.Windows.Forms.BindingSource> e <xref:System.Windows.Forms.BindingNavigator> são exibidos na bandeja de componentes.

## <a name="run-the-application"></a>Executar o aplicativo

Pressione **F5** para executar o aplicativo.

## <a name="next-steps"></a>Próximas etapas

Dependendo dos requisitos do aplicativo, existem várias etapas que você pode realizar após criar um controle com suporte a associação de dados. Algumas etapas seguintes típicas incluem:

- Colocando os controles personalizados em uma biblioteca de controles para que você possa reutilizá-los em outros aplicativos.

- Criando controles que suportam cenários de associação de dados mais complexos. Para obter mais informações, consulte [criar um Windows Forms controle de usuário que dá suporte à vinculação de dados complexa](../data-tools/create-a-windows-forms-user-control-that-supports-complex-data-binding.md) e [criar um controle de usuário de Windows Forms que dá suporte à vinculação de dados de pesquisa](../data-tools/create-a-windows-forms-user-control-that-supports-lookup-data-binding.md).

## <a name="see-also"></a>Confira também

- [Associar controles do Windows Forms a dados no Visual Studio](../data-tools/bind-windows-forms-controls-to-data-in-visual-studio.md)
- [Definir o controle a ser criado quando arrastado da janela Fontes de Dados](../data-tools/set-the-control-to-be-created-when-dragging-from-the-data-sources-window.md)
