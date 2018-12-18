---
title: Criar um controle de usuário do Windows Forms que dá suporte à vinculação de dados simples | Microsoft Docs
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
- custom controls [Visual Studio], Data Sources Window
- Data Sources Window, controls
ms.assetid: b1488366-6dfb-454e-9751-f42fd3f3ddfb
caps.latest.revision: 17
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: 607c324e11591211593522957dcd08747d230279
ms.sourcegitcommit: d462dd10746624ad139f1db04edd501e7737d51e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/29/2018
ms.locfileid: "50219816"
---
# <a name="create-a-windows-forms-user-control-that-supports-simple-data-binding"></a>Criar um controle de usuário do Windows Forms que dá suporte à vinculação de dados simples
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

  
Ao exibir dados em formulários em aplicativos do Windows, você pode escolher os controles existentes dos **caixa de ferramentas**, ou você pode criar controles personalizados se seu aplicativo requer funcionalidade que não está disponível nos controles padrão. Este passo a passo mostra como criar um controle que implementa o <xref:System.ComponentModel.DefaultBindingPropertyAttribute>. Os controles que implementam o <xref:System.ComponentModel.DefaultBindingPropertyAttribute> contêm uma propriedade que pode ser associada a dados. Tais controles são semelhantes a um <xref:System.Windows.Forms.TextBox> ou <xref:System.Windows.Forms.CheckBox>.  
  
 Para obter mais informações sobre criação de controle, consulte [desenvolvendo controles dos Windows Forms em tempo de Design](http://msdn.microsoft.com/library/e5a8e088-7ec8-4fd9-bcb3-9078fd134829).  
  
 Ao criar controles para uso em cenários de vinculação de dados, você deve implementar um dos seguintes atributos de associação de dados:  
  
|Uso do atributo de associação de dados|  
|-----------------------------------|  
|Implemente o <xref:System.ComponentModel.DefaultBindingPropertyAttribute> em controles simples, como um <xref:System.Windows.Forms.TextBox>, que exibe uma única coluna (ou propriedade) de dados. (Esse processo é descrito nesta página de passo a passo.)|  
|Implemente o <xref:System.ComponentModel.ComplexBindingPropertiesAttribute> nos controles, como um <xref:System.Windows.Forms.DataGridView> que exibe listas (ou tabelas) de dados. Para obter mais informações, consulte [criar um controle de usuário do Windows Forms que dá suporte à vinculação de dados complexos](../data-tools/create-a-windows-forms-user-control-that-supports-complex-data-binding.md).|  
|Implemente o <xref:System.ComponentModel.LookupBindingPropertiesAttribute> nos controles, como um <xref:System.Windows.Forms.ComboBox>que exibe listas (ou tabelas) de dados, mas também precisa apresentar uma única coluna ou propriedade. Para obter mais informações, consulte [criar um controle de usuário do Windows Forms que dá suporte à vinculação de dados de pesquisa](../data-tools/create-a-windows-forms-user-control-that-supports-lookup-data-binding.md).|  
  
 Este passo a passo cria um controle simples que exibe dados de uma única coluna em uma tabela. Este exemplo usa a coluna `Phone` da tabela `Customers` do banco de dados de exemplo Northwind. O controle de usuário simples exibirá números de telefone dos clientes em um formato de número de telefone padrão, usando um <xref:System.Windows.Forms.MaskedTextBox> e definindo a máscara para um número de telefone.  
  
 Durante este passo a passo, você aprenderá a:  
  
-   Criar um novo **aplicativo do Windows**.  
  
-   Adicione um novo **controle de usuário** ao seu projeto.  
  
-   Projetar visualmente o controle do usuário.  
  
-   Implementar o atributo `DefaultBindingProperty`.  
  
-   Criar um conjunto de dados com o **configuração de fonte de dados** assistente.  
  
-   Definir o **telefone** coluna o **fontes de dados** janela para usar o novo controle.  
  
-   Criar um formulário para exibir dados no novo controle.  
  
## <a name="prerequisites"></a>Pré-requisitos  
 Para concluir este passo a passo, você precisará de:  
  
-   Acesso ao banco de dados de exemplo Northwind. Para obter mais informações, consulte [como: instalar os bancos de dados de exemplo](../data-tools/how-to-install-sample-databases.md).  
  
## <a name="create-a-windows-application"></a>Criar um aplicativo do Windows  
 A primeira etapa é criar uma **aplicativo do Windows**.  
  
#### <a name="to-create-the-new-windows-project"></a>Para criar o novo projeto do Windows  
  
1.  No Visual Studio, do **arquivo** menu, crie uma nova **projeto**.  
  
2.  Nomeie o projeto **SimpleControlWalkthrough**.  
  
3.  Selecione **aplicativo do Windows** e clique em **Okey**. Para obter mais informações, consulte [aplicativos cliente](http://msdn.microsoft.com/library/2dfb50b7-5af2-4e12-9bbb-c5ade0e39a68).  
  
     O **SimpleControlWalkthrough** projeto é criado e adicionado ao **Gerenciador de soluções**.  
  
## <a name="add-a-user-control-to-the-project"></a>Adicionar um controle de usuário ao projeto  
 Este passo a passo cria um simples controle associável a dados de um **controle de usuário**, então, adicione um **controle de usuário** de item para o **SimpleControlWalkthrough** projeto.  
  
#### <a name="to-add-a-user-control-to-the-project"></a>Para adicionar um controle de usuário ao projeto  
  
1.  Dos **Project** menu, escolha **adicionar controle de usuário**.  
  
2.  Tipo de `PhoneNumberBox` na área nome e clique **Add**.  
  
     O **PhoneNumberBox** controle é adicionado à **Gerenciador de soluções**e o abre no designer.  
  
## <a name="design-the-phonenumberbox-control"></a>Projetar o controle PhoneNumberBox  
 Este passo a passo expande o <xref:System.Windows.Forms.MaskedTextBox> existente para criar o controle `PhoneNumberBox`.  
  
#### <a name="to-design-the-phonenumberbox-control"></a>Para projetar o controle PhoneNumberBox  
  
1.  Arraste uma <xref:System.Windows.Forms.MaskedTextBox> do **caixa de ferramentas** na superfície de design do controle de usuário.  
  
2.  Selecione a marca inteligente sobre o <xref:System.Windows.Forms.MaskedTextBox> você acabou de arrastar e escolha **definir máscara**.  
  
3.  Selecione **número de telefone** na **máscara de entrada** caixa de diálogo e clique em **Okey** para configurar a máscara.  
  
## <a name="add-the-required-data-binding-attribute"></a>Adicione o atributo obrigatório de associação de dados  
 Para controles simples que suportam associação de dados, implemente o <xref:System.ComponentModel.DefaultBindingPropertyAttribute>.  
  
#### <a name="to-implement-the-defaultbindingproperty-attribute"></a>Para implementar o atributo DefaultBindingProperty  
  
1.  Alterne o controle `PhoneNumberBox` para exibição de código. (Sobre o **modo de exibição** menu, escolha **código**.)  
  
2.  Substitua o código no `PhoneNumberBox` pelo seguinte:  
  
     [!code-csharp[VbRaddataDisplaying#3](../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataDisplaying/CS/PhoneNumberBox.cs#3)]
     [!code-vb[VbRaddataDisplaying#3](../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataDisplaying/VB/PhoneNumberBox.vb#3)]  
  
3.  No menu **Compilação**, escolha **Compilar Solução**.  
  
## <a name="create-a-data-source-from-your-database"></a>Criar uma fonte de dados do banco de dados  
 Esta etapa usa a **Data Source Configuration** Assistente para criar uma fonte de dados com base no `Customers` tabela no banco de dados de exemplo Northwind. É preciso ter acesso ao banco de dados de exemplo Northwind para criar a conexão. Para obter informações sobre como configurar o banco de dados de exemplo Northwind, consulte [como: instalar os bancos de dados de exemplo](../data-tools/how-to-install-sample-databases.md).  
  
#### <a name="to-create-the-data-source"></a>Para criar a fonte de dados  
  
1.  Sobre o **dados** menu, clique em **Show Data Sources**.  
  
2.  No **fontes de dados** janela, selecione **Add New Data Source** para iniciar o **configuração de fonte de dados** assistente.  
  
3.  Sobre o **escolher um tipo de fonte de dados** página, selecione **banco de dados**e, em seguida, clique em **próxima**.  
  
4.  Sobre o **escolha sua Conexão de dados** página, faça o seguinte:  
  
    -   Se uma conexão de dados com o banco de dados de exemplo Northwind estiver disponível na lista suspensa, selecione-o.  
  
    -   Selecione **nova Conexão** para iniciar o **Adicionar/Modificar Conexão** caixa de diálogo.  
  
5.  Se seu banco de dados exigir uma senha, selecione a opção para incluir dados confidenciais e, em seguida, clique em **próxima**.  
  
6.  Sobre o **salvar a cadeia de caracteres de conexão para o arquivo de configuração de aplicativo** , clique em **próxima**.  
  
7.  Sobre o **Choose your Database Objects** página, expanda o **tabelas** nó.  
  
8.  Selecione o `Customers` de tabela e, em seguida, clique em **concluir**.  
  
     O **NorthwindDataSet** é adicionado ao seu projeto e o `Customers` tabela aparece no **fontes de dados** janela.  
  
## <a name="set-the-phone-column-to-use-the-phonenumberbox-control"></a>Definir a coluna telefone para usar o controle PhoneNumberBox  
 Dentro de **fontes de dados** janela, você pode definir o controle a ser criado antes de arrastar itens para seu formulário.  
  
#### <a name="to-set-the-phone-column-to-bind-to-the-phonenumberbox-control"></a>Para definir a coluna telefone para se associar ao controle PhoneNumberBox  
  
1.  Abra **Form1** no designer.  
  
2.  Expanda o **clientes** nó na **fontes de dados** janela.  
  
3.  Clique na seta suspensa na **clientes** nó e escolha **detalhes** na lista de controle.  
  
4.  Clique na seta suspensa na **Phone** coluna e escolha **personalizar**.  
  
5.  Selecione o **PhoneNumberBox** na lista de **controles associados** no **opções de personalização da interface do usuário de dados** caixa de diálogo.  
  
6.  Clique na seta suspensa na **Phone** coluna e escolha **PhoneNumberBox**.  
  
## <a name="addcontrols-to-the-form"></a>Addcontrols ao formulário  
 Você pode criar os controles ligados a dados arrastando itens dos **fontes de dados** janela para o formulário.  
  
#### <a name="to-create-data-bound-controls-on-the-form"></a>Para criar controles de associação de dados no formulário  
  
-   Arraste principal **clientes** nó a partir o **fontes de dados** janela para o formulário e verificar se o `PhoneNumberBox` controle é usado para exibir os dados no `Phone` coluna.  
  
     Os controles de associação de dados com rótulos descritivos são exibidos no formulário, juntamente com uma faixa de ferramentas (<xref:System.Windows.Forms.BindingNavigator>) para registros de navegação. Um [NorthwindDataSet](../data-tools/dataset-tools-in-visual-studio.md), [CustomersTableAdapter](../data-tools/tableadapter-overview.md), <xref:System.Windows.Forms.BindingSource>, e <xref:System.Windows.Forms.BindingNavigator> aparecem na bandeja de componentes.  
  
## <a name="run-the-application"></a>Executar o aplicativo  
  
#### <a name="to-run-the-application"></a>Para executar o aplicativo  
  
-   Pressione F5 para executar o aplicativo.  
  
## <a name="next-steps"></a>Próximas etapas  
 Dependendo dos requisitos do aplicativo, existem várias etapas que você pode realizar após criar um controle com suporte a associação de dados. Algumas etapas seguintes típicas incluem:  
  
-   Colocando os controles personalizados em uma biblioteca de controles para que você possa reutilizá-los em outros aplicativos.  
  
-   Criando controles que suportam cenários de associação de dados mais complexos. Para obter mais informações, consulte [criar um controle de usuário do Windows Forms que dá suporte à vinculação de dados complexos](../data-tools/create-a-windows-forms-user-control-that-supports-complex-data-binding.md) e [criar um controle de usuário do Windows Forms que dá suporte à vinculação de dados de pesquisa](../data-tools/create-a-windows-forms-user-control-that-supports-lookup-data-binding.md).  
  
## <a name="see-also"></a>Consulte também  
 [Associar controles do Windows Forms a dados no Visual Studio](../data-tools/bind-windows-forms-controls-to-data-in-visual-studio.md)   
 [Definir o controle a ser criado quando arrastado da janela Fontes de Dados](../data-tools/set-the-control-to-be-created-when-dragging-from-the-data-sources-window.md)

