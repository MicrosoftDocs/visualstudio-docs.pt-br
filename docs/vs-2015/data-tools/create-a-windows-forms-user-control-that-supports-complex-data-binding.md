---
title: Criar um controle de usuário do Windows Forms que dá suporte à vinculação de dados complexos | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
dev_langs:
- VB
- CSharp
- C++
- aspx
helpviewer_keywords:
- data binding, user controls
- data binding, complex
- user controls [Visual Studio], complex data binding
ms.assetid: c8f29c2b-b49b-4618-88aa-33b6105880b5
caps.latest.revision: 16
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: de22f93c6fd04f89360fdaf8a2f5d83bd373d93d
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49284252"
---
# <a name="create-a-windows-forms-user-control-that-supports-complex-data-binding"></a>Criar um controle de usuário do Windows Forms que dá suporte à vinculação de dados complexos
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

  
Ao exibir dados em formulários em aplicativos do Windows, você pode escolher os controles existentes dos **caixa de ferramentas**, ou você pode criar controles personalizados se seu aplicativo requer funcionalidade que não está disponível nos controles padrão. Este passo a passo mostra como criar um controle que implementa o <xref:System.ComponentModel.ComplexBindingPropertiesAttribute>. Os controles que implementam o <xref:System.ComponentModel.ComplexBindingPropertiesAttribute> contêm uma propriedade de `DataSource` e `DataMember` que pode ser associada a dados. Tais controles são semelhantes a um <xref:System.Windows.Forms.DataGridView> ou <xref:System.Windows.Forms.ListBox>.  
  
 Para obter mais informações sobre criação de controle, consulte [desenvolvendo controles dos Windows Forms em tempo de Design](http://msdn.microsoft.com/library/e5a8e088-7ec8-4fd9-bcb3-9078fd134829).  
  
 Ao criar controles para uso em cenários de vinculação de dados, você precisa implementar um dos seguintes atributos de associação de dados:  
  
|Uso do atributo de associação de dados|  
|-----------------------------------|  
|Implemente o <xref:System.ComponentModel.DefaultBindingPropertyAttribute> em controles simples, como um <xref:System.Windows.Forms.TextBox>, que exibe uma única coluna (ou propriedade) de dados. Para obter mais informações, consulte [criar um controle de usuário do Windows Forms que dá suporte à vinculação de dados simples](../data-tools/create-a-windows-forms-user-control-that-supports-simple-data-binding.md).|  
|Implemente o <xref:System.ComponentModel.ComplexBindingPropertiesAttribute> nos controles, como um <xref:System.Windows.Forms.DataGridView> que exibe listas (ou tabelas) de dados. (Esse processo é descrito nesta página de passo a passo.)|  
|Implemente o <xref:System.ComponentModel.LookupBindingPropertiesAttribute> nos controles, como um <xref:System.Windows.Forms.ComboBox>que exibe listas (ou tabelas) de dados, mas também precisa apresentar uma única coluna ou propriedade. Para obter mais informações, consulte [criar um controle de usuário do Windows Forms que dá suporte à vinculação de dados de pesquisa](../data-tools/create-a-windows-forms-user-control-that-supports-lookup-data-binding.md).|  
  
 Este passo a passo cria um controle complexo que exibe linhas de dados de uma tabela. Este exemplo usa a tabela `Customers` do banco de dados de exemplo Northwind. O controle de usuário complexo exibirá a tabela de clientes em uma <xref:System.Windows.Forms.DataGridView> no controle personalizado.  
  
 Durante este passo a passo, você aprenderá a:  
  
-   Criar um novo **aplicativo do Windows**.  
  
-   Adicione um novo **controle de usuário** ao seu projeto.  
  
-   Projetar visualmente o controle do usuário.  
  
-   Implementar o atributo `ComplexBindingProperty`.  
  
-   Criar um conjunto de dados com o [Data Source Configuration Wizard](http://msdn.microsoft.com/library/c4df7de5-5da0-4064-940c-761dd6d9e28f).  
  
-   Defina as **clientes** na tabela a [janela fontes de dados](http://msdn.microsoft.com/library/0d20f699-cc95-45b3-8ecb-c7edf1f67992) para usar o novo controle complexo.  
  
-   Adicione o novo controle, arrastando-o do **janela fontes de dados** até **Form1**.  
  
## <a name="prerequisites"></a>Pré-requisitos  
 Para concluir este passo a passo, você precisará de:  
  
-   Acesso ao banco de dados de exemplo Northwind. Para obter mais informações, consulte [como: instalar os bancos de dados de exemplo](../data-tools/how-to-install-sample-databases.md).  
  
## <a name="create-a-windows-application"></a>Criar um aplicativo do Windows  
 A primeira etapa é criar uma **aplicativo do Windows**.  
  
#### <a name="to-create-the-new-windows-project"></a>Para criar o novo projeto do Windows  
  
1.  No Visual Studio, do **arquivo** menu, crie uma nova **projeto**.  
  
2.  Nomeie o projeto **ComplexControlWalkthrough**.  
  
3.  Selecione **aplicativo do Windows**e clique em **Okey**. Para obter mais informações, consulte [aplicativos cliente](http://msdn.microsoft.com/library/2dfb50b7-5af2-4e12-9bbb-c5ade0e39a68).  
  
     O **ComplexControlWalkthrough** projeto é criado e adicionado ao **Gerenciador de soluções**.  
  
## <a name="add-a-user-control-to-the-project"></a>Adicionar um controle de usuário ao projeto  
 Porque este passo a passo cria um controle associável a dados complexo de um **controle de usuário**, você deve adicionar uma **controle de usuário** item ao projeto.  
  
#### <a name="to-add-a-user-control-to-the-project"></a>Para adicionar um controle de usuário ao projeto  
  
1.  Dos **Project** menu, escolha **adicionar controle de usuário**.  
  
2.  Tipo de **ComplexDataGridView** na **nome** área e clique **adicionar**.  
  
     O **ComplexDataGridView** controle é adicionado à **Gerenciador de soluções**e o abre no designer.  
  
## <a name="design-the-complexdatagridview-control"></a>Criar o controle ComplexDataGridView  
 Esta etapa adiciona um <xref:System.Windows.Forms.DataGridView> ao controle de usuário.  
  
#### <a name="to-design-the-complexdatagridview-control"></a>Para projetar o controle ComplexDataGridView  
  
-   Arraste uma <xref:System.Windows.Forms.DataGridView> do **caixa de ferramentas** na superfície de design do controle de usuário.  
  
## <a name="add-the-required-data-binding-attribute"></a>Adicione o atributo obrigatório de associação de dados  
 Para controles complexos que suportam associação de dados, você pode implementar o <xref:System.ComponentModel.ComplexBindingPropertiesAttribute>.  
  
#### <a name="to-implement-the-complexbindingproperties-attribute"></a>Para implementar o atributo ComplexBindingProperties  
  
1.  Opção de **ComplexDataGridView** controle a exibição de código. (Sobre o **modo de exibição** menu, selecione **código**.)  
  
2.  Substitua o código no `ComplexDataGridView` pelo seguinte:  
  
     [!code-csharp[VbRaddataDisplaying#4](../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataDisplaying/CS/ComplexDataGridView.cs#4)]
     [!code-vb[VbRaddataDisplaying#4](../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataDisplaying/VB/ComplexDataGridView.vb#4)]  
  
3.  No menu **Compilação**, escolha **Compilar Solução**.  
  
## <a name="creating-a-data-source-from-your-database"></a>Criando uma fonte de dados do banco de dados  
 Esta etapa usa a **Data Source Configuration** Assistente para criar uma fonte de dados com base no `Customers` tabela no banco de dados de exemplo Northwind. É preciso ter acesso ao banco de dados de exemplo Northwind para criar a conexão. Para obter informações sobre como configurar o banco de dados de exemplo Northwind, consulte [bancos de dados de exemplo de instalar o SQL Server](../data-tools/install-sql-server-sample-databases.md).  
  
#### <a name="to-create-the-data-source"></a>Para criar a fonte de dados  
  
1.  Sobre o **dados** menu, clique em **Show Data Sources**.  
  
2.  No **fontes de dados** janela, selecione **Add New Data Source** para iniciar o **configuração de fonte de dados** assistente.  
  
3.  Selecione **banco de dados** sobre o **escolher um tipo de fonte de dados** página e, em seguida, clique em **próxima**.  
  
4.  Sobre o **escolha sua Conexão de dados** página faça o seguinte:  
  
    -   Se uma conexão de dados com o banco de dados de exemplo Northwind estiver disponível na lista suspensa, selecione-o.  
  
    -   Selecione **nova Conexão** para iniciar o **Adicionar/Modificar Conexão** caixa de diálogo.  
  
5.  Se seu banco de dados exigir uma senha, selecione a opção para incluir dados confidenciais e, em seguida, clique em **próxima**.  
  
6.  Sobre o **salvar a cadeia de caracteres de conexão para o arquivo de configuração de aplicativo** , clique em **próxima**.  
  
7.  Sobre o **Choose your Database Objects** página, expanda o **tabelas** nó.  
  
8.  Selecione o `Customers` de tabela e, em seguida, clique em **concluir**.  
  
     O **NorthwindDataSet** é adicionado ao seu projeto e o `Customers` tabela aparece no **fontes de dados** janela.  
  
## <a name="set-the-customers-table-to-use-the-complexdatagridview-control"></a>Definir a tabela de clientes para usar o controle ComplexDataGridView  
 Dentro de **fontes de dados** janela, você pode definir o controle a ser criado antes de arrastar itens para seu formulário.  
  
#### <a name="to-set-the-customers-table-to-bind-to-the-complexdatagridview-control"></a>Para configurar a coluna Clientes para se associar ao controle ComplexDataGridView  
  
1.  Abra **Form1** no designer.  
  
2.  Expanda o **clientes** nó na **fontes de dados** janela.  
  
3.  Clique na seta suspensa na **clientes** nó e escolha **personalizar**.  
  
4.  Selecione o **ComplexDataGridView** na lista de **controles associados** no **opções de personalização da interface do usuário de dados** caixa de diálogo.  
  
5.  Clique na seta suspensa na `Customers` da tabela e escolha **ComplexDataGridView** na lista de controle.  
  
## <a name="addcontrols-to-the-form"></a>Addcontrols ao formulário  
 Você pode criar os controles ligados a dados arrastando itens dos **fontes de dados** window para seu formulário.  
  
#### <a name="to-create-data-bound-controls-on-the-form"></a>Para criar controles de associação de dados no formulário  
  
-   Arraste principal **clientes** nó a partir do **fontes de dados** janela para o formulário. Verifique se que o **ComplexDataGridView** controle é usado para exibir os dados da tabela.  
  
## <a name="running-the-application"></a>Executando o aplicativo  
  
#### <a name="to-run-the-application"></a>Para executar o aplicativo  
  
-   Pressione F5 para executar o aplicativo.  
  
## <a name="next-steps"></a>Próximas etapas  
 Dependendo dos requisitos do aplicativo, existem várias etapas que você pode realizar após criar um controle com suporte a associação de dados. Algumas etapas seguintes típicas incluem:  
  
-   Colocando os controles personalizados em uma biblioteca de controles para que você possa reutilizá-los em outros aplicativos.  
  
-   Criando controles que suportam cenários de pesquisa. Para obter mais informações, consulte [criar um controle de usuário do Windows Forms que dá suporte à vinculação de dados de pesquisa](../data-tools/create-a-windows-forms-user-control-that-supports-lookup-data-binding.md).  
  
## <a name="see-also"></a>Consulte também  
 [Associar controles do Windows Forms a dados no Visual Studio](../data-tools/bind-windows-forms-controls-to-data-in-visual-studio.md)   
 [Definir o controle a ser criado quando arrastado da janela fontes de dados](../data-tools/set-the-control-to-be-created-when-dragging-from-the-data-sources-window.md)   
 [Controles dos Windows Forms](http://msdn.microsoft.com/library/f050de8f-4ebd-4042-94b8-edf9a1dbd52a)

