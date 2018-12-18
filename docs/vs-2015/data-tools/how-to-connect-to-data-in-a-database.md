---
title: 'Como: conectar a dados em um banco de dados | Microsoft Docs'
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
- databases, connecting to
- data sources, databases
- data [Visual Studio], connecting to databases
- data sources, creating
- database connections
ms.assetid: 6c56e54e-8834-4297-85aa-cc1a443ba556
caps.latest.revision: 55
author: gewarren
ms.author: gewarren
manager: ghogen
robots: noindex,nofollow
ms.openlocfilehash: e75de3c81270449da6fe6bb504b476b912f51583
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49273800"
---
# <a name="how-to-connect-to-data-in-a-database"></a>Como conectar a dados em um banco de dados
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

É possível usar o Visual Studio para conectar o aplicativo a um banco de dados. Após criar a conexão de dados, o Visual Studio gera um modelo de dados que o aplicativo usa para interagir com os dados no banco de dados. Os objetos no modelo de dados aparecem na [janela fontes de dados](http://msdn.microsoft.com/library/0d20f699-cc95-45b3-8ecb-c7edf1f67992). Em seguida, você pode criar controles associados a dados arrastando itens dos **janela fontes de dados** para uma superfície de design. Para obter mais informações, consulte [associar controles a dados no Visual Studio](../data-tools/bind-controls-to-data-in-visual-studio.md).  
  
 Este tópico fornece instruções para conectar a um banco de dados e criar os seguintes tipos de modelos de dados:  
  
-   Conjunto de dados  
  
-   Modelo de Dados de Entidade (EDM)  
  
> [!NOTE]
>  Também é possível usar o Visual Studio para criar classes LINQ to SQL a partir de um banco de dados. No entanto, classes LINQ to SQL não aparecem na **fontes de dados** janela e, portanto, não pode ser arrastada diretamente para um designer para criar controles associados a dados. Para obter mais informações sobre como criar o LINQ para classes SQL de um banco de dados, consulte [como: criar classes LINQ to SQL mapeadas para tabelas e exibições (Designer relacional de objetos)](../data-tools/how-to-create-linq-to-sql-classes-mapped-to-tables-and-views-o-r-designer.md).  
  
 [!INCLUDE[note_settings_general](../includes/note-settings-general-md.md)]  
  
##  <a name="dataset"></a> Conectar-se a um banco de dados e criar um conjunto de dados  
 Ao criar um conjunto de dados que é baseado em um banco de dados, o Visual Studio cria um conjunto de classes que representa uma visão programável dos dados. A classe principal é chamada uma *conjunto de dados digitados*. O conjunto de dados digitados contém objetos de tabela de dados que representam tabelas no banco de dados. Para obter mais informações sobre conjuntos de dados tipados, consulte [ferramentas de conjunto de dados no Visual Studio](../data-tools/dataset-tools-in-visual-studio.md).  
  
 Após criar um conjunto de dados, é possível criar controles WPF ou Windows Forms associados a dados arrastando objetos de conjunto de dados da janela Fontes de Dados para o designer de WPF ou Windows Forms.  
  
#### <a name="to-connect-your-application-to-a-database-and-create-a-dataset"></a>Conectar o aplicativo a um banco de dados e criar um conjunto de dados  
  
1.  Abra um projeto existente no Visual Studio ou crie um novo projeto.  
  
2.  Sobre o **dados** menu, clique em **Add New Data Source**.  
  
     O **Data Source Configuration Wizard** é aberta.  
  
3.  Sobre o **escolher um tipo de fonte de dados** página, selecione **banco de dados**e, em seguida, clique em **próxima**.  
  
4.  Sobre o **escolha um modelo de banco de dados** página, selecione **Dataset**e, em seguida, clique em **próxima**.  
  
5.  Sobre o **escolha sua Conexão de dados** , selecione uma conexão de dados da lista de conexões disponíveis e, em seguida, clique em **próxima**.  
  
     Se sua conexão de dados desejada não estiver disponível, crie uma nova conexão seguindo as etapas em [criando uma nova Conexão de banco de dados](#CreatingDataConnection).  
  
6.  Sobre o **salvar a cadeia de Conexão para o arquivo de configuração de aplicativo** página, opcionalmente, desmarque a **Sim, salvar a conexão como** caixa de seleção se você quiser salvar a cadeia de conexão diretamente no compilado aplicativo. Por padrão, a conexão é salva no arquivo de configuração do aplicativo. Para obter mais informações, consulte [como: salvar e editar cadeias de caracteres de Conexão](~/E:/Repos/visualstudio-docs-pr/docs/data-tools/how-to-save-and-edit-connection-strings.md).  
  
7.  Sobre o **Choose Your Database Objects** , selecione os objetos de banco de dados que você usará em seu aplicativo. Você também tem a opção de substituir o padrão **nome do conjunto de dados**.  
  
8.  Clique em **Finalizar**. O conjunto de dados que você acabou de criar agora está disponível na **fontes de dados** janela.  
  
    > [!NOTE]
    >  Se o **fontes de dados** janela não estiver aberta, clique em **Show Data Sources** sobre o **dados** menu para abrir a janela.  
  
9. Agora você pode arrastar itens dos **fontes de dados** janela para o WPF designer, o designer de formulários do Windows, ou o [Component Designer](http://msdn.microsoft.com/library/61a3a450-5b15-465e-bd9a-72a6c8c2b282) para criar controles associados a dados. Para obter mais informações, consulte [associar controles a dados no Visual Studio](../data-tools/bind-controls-to-data-in-visual-studio.md).  
  
##  <a name="edm"></a> Conectar-se ao banco de dados e criando um modelo de dados de entidade  
 Ao criar um Modelo de Dados de Entidade que é baseado em um banco de dados, o Visual Studio cria um conjunto de classes que representa uma visão programável dos dados. Para obter mais informações sobre modelos de dados de entidade e o ADO.NET Entity Framework, consulte [visão geral do Entity Framework](http://msdn.microsoft.com/library/a2166b3d-d8ba-4a0a-8552-6ba1e3eaaee0).  
  
 Após criar um Modelo de Dados de Entidade, é possível criar controles WPF associados a dados arrastando objetos de entidade da janela Fontes de Dados para o designer de WPF.  
  
#### <a name="to-connect-your-application-to-a-database-and-create-an-entity-data-model"></a>Conectar o aplicativo a um banco de dados e criar um Modelo de Dados de Entidade  
  
1.  Abra um projeto existente no Visual Studio ou crie um novo projeto.  
  
2.  Siga as etapas a **Assistente de modelo de dados de entidade** para se conectar a um banco de dados e especificar o conteúdo do modelo. Para obter mais informações, consulte [como: criar um novo. do EDMX arquivo](http://msdn.microsoft.com/en-us/beb8189e-e51c-4051-839c-9902c224abf2).  
  
3.  Depois de concluir a **Assistente de modelo de dados de entidade**, o modelo de dados de entidade criado é aberto no Designer de modelo de dados de entidade e os objetos de dados agora estão disponíveis na **fontes de dados** janela.  
  
    > [!NOTE]
    >  Se o **fontes de dados** janela não estiver aberta, clique em **Show Data Sources** sobre o **dados** menu para abrir a janela.  
  
4.  Se o WPF designer estiver aberto, agora você pode arrastar itens dos **fontes de dados** janela para o designer para criar controles associados ao modelo de dados de entidade. Para obter mais informações, consulte [WPF associar controles a dados no Visual Studio](../data-tools/bind-wpf-controls-to-data-in-visual-studio2.md).  
  
     Se o designer de formulários do Windows estiver aberto, você não pode arrastar itens dos **fontes de dados** ao designer. Para criar controles associados ao Modelo de Dados de Entidade, é necessário compilar o projeto, incluir uma nova fonte de dados de objeto que é baseado no Modelo de Dados de Entidade e arrastar esses objetos para o designer.  
  
##  <a name="CreatingDataConnection"></a> Criando uma nova Conexão de banco de dados  
 Quando você usa o **Data Source Configuration Wizard**ou o **Assistente de modelo de dados de entidade**, você deve especificar uma conexão ao banco de dados que você deseja usar. Se a conexão com o banco de dados ainda não existir, realize as etapas a seguir para criar a conexão.  
  
 Essas instruções pressupõem que você já tiver começado a **Data Source Configuration Wizard** ou o **Assistente de modelo de dados de entidade** conforme descrito em [conectando-se ao banco de dados e criando um conjunto de dados ](#dataset) e [conectar-se ao banco de dados e criando um modelo de dados de entidade](#edm).  
  
#### <a name="to-create-a-new-database-connection"></a>Para criar uma nova conexão de banco de dados  
  
1.  No **escolha sua Conexão de dados** página do **Data Source Configuration Wizard** ou o **Assistente de modelo de dados de entidade**, clique em **nova Conexão**.  
  
     Ocorrerá uma das seguintes ações:  
  
    -   Se você já tiver criado uma conexão de dados no Visual Studio, o **Adicionar Conexão** caixa de diálogo é aberta.  
  
    -   Se esta for a primeira conexão de dados você tiver criado no Visual Studio, o **Choose Data Source** exibe a caixa de diálogo. Selecione o tipo de banco de dados que você deseja se conectar a e, em seguida, clique em **Okey** para exibir o **Adicionar Conexão** caixa de diálogo.  
  
2.  No **Adicionar Conexão** caixa de diálogo, digite as informações solicitadas. O **Adicionar Conexão** caixa de diálogo é diferente para cada tipo de provedor de dados.  
  
    > [!NOTE]
    >  Se selecionado **fonte de dados** na **Adicionar Conexão** caixa de diálogo não é a fonte de dados que você deseja conectar, clique em **alteração** para abrir o **dados de alteração Origem** caixa de diálogo caixa e, em seguida, escolha uma fonte de dados diferentes.  
  
3.  No **Adicionar Conexão** caixa de diálogo, clique em **Okey**.  
  
     Retornar para o **escolha sua Conexão de dados** página do **Data Source Configuration Wizard** ou o **Assistente de modelo de dados de entidade**.  
  
4.  Sobre o **escolha sua Conexão de dados** página, certifique-se de que a nova conexão de dados está selecionado e, em seguida, clique em **próxima**.  
  
5.  Conclua as etapas restantes **Data Source Configuration Wizard** ou o **Assistente de modelo de dados de entidade**.  
  
## <a name="net-framework-security"></a>Segurança do .NET Framework  
 O armazenamento das informações confidenciais (como uma senha) pode afetar a segurança do aplicativo. O uso da Autenticação do Windows (também conhecida como segurança integrada) é uma maneira mais segura de controlar o acesso a um banco de dados. Para obter mais informações, consulte [Protegendo informações de conexão](http://msdn.microsoft.com/library/1471f580-bcd4-4046-bdaf-d2541ecda2f4).  
  
## <a name="see-also"></a>Consulte também  
 [Adicionar novas fontes de dados](../data-tools/add-new-data-sources.md)   
 [Instruções passo a passo de dados](http://msdn.microsoft.com/library/15a88fb8-3bee-4962-914d-7a1f8bd40ec4)   
 [Associar controles do Windows Forms a dados no Visual Studio](../data-tools/bind-windows-forms-controls-to-data-in-visual-studio.md)   
 [Conectando-se a dados no Visual Studio](../data-tools/connecting-to-data-in-visual-studio.md)   
 [Conectando a uma fonte de dados](http://msdn.microsoft.com/library/9abc3f92-1be3-4e1a-b360-762dc689650e)