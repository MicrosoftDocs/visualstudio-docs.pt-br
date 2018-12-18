---
title: Criando aplicativos de dados | Microsoft Docs
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
- data access [Visual Studio], creating applications
- applications [Visual Studio], data
- data [Visual Studio]
- data [Visual Studio], creating applications
ms.assetid: ab334d5f-4f49-4346-bce0-3325d6130b3e
caps.latest.revision: 41
author: gewarren
ms.author: gewarren
manager: ghogen
robots: noindex,nofollow
ms.openlocfilehash: 4e5354d167dd6d3a1bef9beeb3dcaaaf24871bab
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49291293"
---
# <a name="creating-data-applications"></a>Criando aplicativos de dados
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Visual Studio fornece várias ferramentas de tempo de design para ajudá-lo a criar aplicativos que acessam dados. Esta introdução apresenta uma visão geral sobre os processos básicos envolvidos na criação de aplicativos que funcionam com dados. As informações aqui deliberadamente ignoram muitos detalhes e foi projetadas como uma fonte de informações gerais e um ponto de partida para as muitas outras páginas da Ajuda associadas à criação de um aplicativo de dados.  
  
 À medida que desenvolve aplicativos que acessam dados em [!INCLUDE[vsprvs](../includes/vsprvs-md.md)], você terá requisitos diferentes. Em alguns casos, você pode simplesmente querer exibir dados em um formulário. Em outros casos, talvez você precise planejar uma forma de compartilhar informações com outros aplicativos ou processos.  
  
 Não importa o que fazer com os dados, existem certos conceitos fundamentais que você deve compreender. Você talvez nunca precise conhecer alguns dos detalhes da manipulação de dados — por exemplo, você talvez nunca precise criar programaticamente um banco de dados — mas é muito útil para entender os conceitos básicos de dados, bem como as ferramentas de dados (assistentes e designers) disponíveis no [!INCLUDE[vsprvs](../includes/vsprvs-md.md)].  
  
 Um aplicativo de dados típico usa a maior parte dos processos ilustrados no diagrama a seguir:  
  
 ![Gráfico de ciclo de dados](../data-tools/media/datacyclegraphicinfo.gif "datacyclegraphicinfo")  
O ciclo de dados  
  
 Conforme você cria seu aplicativo, pense na tarefa que você está tentando realizar. Use as seções a seguir para ajudar a localizar o [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] ferramentas e os objetos que estão disponíveis para você.  
  
> [!NOTE]
>  [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] fornece assistentes para simplificar vários processos mostrados no diagrama anterior. Por exemplo, executando o **Data Source Configuration Wizard** fornece a seu aplicativo informações suficientes para se conectar aos dados, criar um dataset tipado para receber os dados e trazer os dados para seu aplicativo.  
  
 Para ver rapidamente como [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] ajuda no desenvolvimento de aplicativos de dados, consulte [passo a passo: Criando um aplicativo de dados simples](http://msdn.microsoft.com/library/c5d0968c-d86f-4ae9-a2e1-871f208a3bb3).  
  
## <a name="connecting-to-data"></a>Conectando-se a Dados  
 Para transferir dados para seu aplicativo (e enviar alterações de volta para a fonte de dados), algum tipo de comunicação bidirecional precisará ser estabelecida. Essa comunicação bidirecional é geralmente tratada por objetos no seu modelo de dados.  
  
 Por exemplo, uma `TableAdapter` conecta os aplicativos que usam conjuntos de dados para um banco de dados e <xref:System.Data.Objects.ObjectContext> conecta entidades no Entity Framework para um banco de dados. [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] fornece várias ferramentas para auxiliar na criação de conexões que podem ser usadas pelo seu aplicativo. Para obter mais informações sobre como conectar seu aplicativo a dados, consulte [conectando-se a dados no Visual Studio](../data-tools/connecting-to-data-in-visual-studio.md).  
  
 Para saber como usar conjuntos de dados para conectar seu aplicativo a dados em um banco de dados, consulte [instruções passo a passo: conectando a dados em um banco de dados (Windows Forms)](http://msdn.microsoft.com/library/02d39aa6-8993-4602-be13-a13536af3d1c).  
  
## <a name="preparing-your-application-to-receive-data"></a>Preparando o aplicativo para receber dados  
 Se seu aplicativo usa um modelo de dados desconectado, que você precisa armazenar temporariamente os dados em seu aplicativo enquanto você trabalha com ele. O Visual Studio fornece ferramentas que ajudam a criar os objetos que seu aplicativo usa para armazenar dados temporariamente: conjuntos de dados, entidades, e [!INCLUDE[vbtecdlinq](../includes/vbtecdlinq-md.md)] objetos.  
  
> [!NOTE]
>  Um aplicativo que usa um modelo de dados desconectado geralmente se conecta a um banco de dados, executar uma consulta trazendo dados para o aplicativo, desconecte o banco de dados e, em seguida, manipular os dados offline antes de reconectar-se e atualizar o banco de dados.  
  
 Para obter mais informações sobre como criar datasets tipados no seu aplicativo, consulte [Preparing Your Application to Receive Data](http://msdn.microsoft.com/library/c17bdb7e-c234-4f2f-9582-5e55c27356ad). Para obter informações adicionais sobre como usar conjuntos de dados em aplicativos de n camadas, consulte [separar conjuntos de dados e TableAdapters em diferentes projetos](../data-tools/separate-datasets-and-tableadapters-into-different-projects.md).  
  
 Para saber como criar um conjunto de dados, conclua os procedimentos [instruções passo a passo: Criando um conjunto de dados com o Designer de conjunto de dados](../data-tools/walkthrough-creating-a-dataset-with-the-dataset-designer.md).  
  
 Para aprender a criar [!INCLUDE[vbtecdlinq](../includes/vbtecdlinq-md.md)] objetos, conclua os procedimentos [passo a passo: Criando Classes LINQ to SQL (Object Relational Designer)](http://msdn.microsoft.com/library/35aad4a4-2e8a-46e2-ae09-5fbfd333c233).  
  
## <a name="fetching-data-into-your-application"></a>Buscando dados no aplicativo  
 Se seu aplicativo usa um modelo de dados desconectado ou não, você precisa ser capaz de buscar dados no seu aplicativo. Transferir dados para seu aplicativo executando consultas ou procedimentos armazenados em um banco de dados. Aplicativos que armazenam dados em conjuntos de dados executam consultas e procedimentos armazenados usando `TableAdapter`s, enquanto os aplicativos que armazenam dados em entidades executam consultas usando [LINQ to Entities](http://msdn.microsoft.com/library/641f9b68-9046-47a1-abb0-1c8eaeda0e2d) ou conectando entidades diretamente para os procedimentos armazenados. Para obter mais informações sobre como criar e editar as consultas que usam TableAdapters, consulte [como: criar consultas do TableAdapter](../data-tools/how-to-create-tableadapter-queries.md) e [como: editar consultas do TableAdapter](../data-tools/how-to-edit-tableadapter-queries.md).  
  
 Para obter mais informações sobre como carregar dados em conjuntos de dados e sobre como executar consultas e procedimentos armazenados, consulte [buscando dados em seu aplicativo](../data-tools/fetching-data-into-your-application.md).  
  
 Para saber como carregar dados em um conjunto de dados, conclua os procedimentos [instruções passo a passo: exibindo dados em um formulário do Windows](../data-tools/walkthrough-displaying-data-on-a-windows-form.md) e examine o código no manipulador de eventos de carregamento de formulário.  
  
 Para saber como carregar dados no [!INCLUDE[vbtecdlinq](../includes/vbtecdlinq-md.md)] objetos, conclua os procedimentos [passo a passo: Criando Classes LINQ to SQL (Object Relational Designer)](http://msdn.microsoft.com/library/35aad4a4-2e8a-46e2-ae09-5fbfd333c233).  
  
 Para saber como criar e executar uma consulta SQL, consulte [como: criar e executar uma instrução SQL que retorna linhas](http://msdn.microsoft.com/library/14637fc5-d42a-4cca-97ac-54c181ec3eed).  
  
 Para saber como executar um procedimento armazenado, consulte [como: executar um procedimento armazenado que retorna linhas](http://msdn.microsoft.com/library/db3d7021-d3ef-4db8-b12a-b6146570355d).  
  
## <a name="displaying-data-on-forms"></a>Exibindo dados em formulários  
 Depois de inserir os dados em seu aplicativo, você normalmente irá exibi-lo em um formulário para que os usuários exibir ou modificar. [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] fornece o [janela fontes de dados](http://msdn.microsoft.com/library/0d20f699-cc95-45b3-8ecb-c7edf1f67992), onde você pode arrastar itens para formulários para criar automaticamente os controles ligados a dados que exibem dados. Para obter mais informações sobre vinculação de dados e exibição de dados para os usuários, consulte [associar controles a dados no Visual Studio](../data-tools/bind-controls-to-data-in-visual-studio.md).  
  
 Para saber como apresentar dados aos usuários, conclua os procedimentos nas instruções a seguir (prestando atenção especial ao processo de arrastar itens dos **fontes de dados** janela):  
  
-   [Passo a passo: Exibindo dados em um formulário do Windows](../data-tools/walkthrough-displaying-data-on-a-windows-form.md).  
  
-   [Associar controles WPF a um WCF Data Service](../data-tools/bind-wpf-controls-to-a-wcf-data-service.md)  
  
-   [Passo a passo: Associando controles Silverlight a um WCF Data Service](http://msdn.microsoft.com/library/f3f08661-7d91-4185-8ed6-912d524d4c6b)  
  
## <a name="editing-data-in-your-application"></a>Editando dados no aplicativo  
 Depois que os usuários serem apresentados aos dados, provavelmente eles modificá-lo adicionando novos registros e editando e excluindo registros antes de enviar os dados de volta para o banco de dados.  
  
 Para obter mais informações sobre como trabalhar com os dados depois que ele é carregado em seu conjunto de dados, consulte [editando dados em seu aplicativo](../data-tools/editing-data-in-your-application.md).  
  
## <a name="validating-data"></a>Validando dados  
 Ao fazer alterações aos dados, você geralmente deseja verificar as alterações antes de permitir que os valores sejam aceitos de volta para o conjunto de dados ou gravados no banco de dados. *Validação* é o nome do processo para verificar se esses novos valores são aceitáveis para os requisitos do seu aplicativo. Você pode adicionar lógica para verificar valores em seu aplicativo conforme mudam. Visual Studio fornece ferramentas que ajudam na adição de código que valida os dados durante alterações de coluna e linha. Para obter mais informações, consulte [Validando dados](http://msdn.microsoft.com/library/b3a9ee4e-5d4d-4411-9c56-c811f2b4ee7e).  
  
 Para saber como adicionar validação de dados ao seu aplicativo, consulte [instruções passo a passo: adicionando validação a um conjunto de dados](http://msdn.microsoft.com/library/09351fab-d670-45e3-b53a-a944eff717e7).  
  
 Para saber como adicionar validação a um conjunto de dados que é separado em um aplicativo de n camadas, consulte [adicionar validação a um conjunto de dados de n camadas](../data-tools/add-validation-to-an-n-tier-dataset.md).  
  
## <a name="saving-data"></a>Salvar Dados  
 Depois de fazer alterações em seu aplicativo (e validar essas alterações), você geralmente deseja enviar que as alterações de volta para o banco de dados. Aplicativos que armazenam dados em conjuntos de dados geralmente usam um TableAdapterManager para salvar dados. Para obter mais informações, consulte [visão geral de TableAdapterManager](http://msdn.microsoft.com/library/33076d42-6b41-491a-ac11-6c6339aea650). Aplicativos do Entity Framework usam o <xref:System.Data.Objects.ObjectContext.SaveChanges%2A> método para salvar dados.  
  
 Para obter mais informações sobre como enviar dados atualizados para um banco de dados, consulte [salvando dados](../data-tools/saving-data.md).  
  
 Para saber como enviar dados atualizados de um conjunto de dados para um banco de dados, conclua os procedimentos [instruções passo a passo: salvando dados de tabelas de dados relacionados (atualização hierárquica)](http://msdn.microsoft.com/library/50601bd7-a488-480c-9910-3c6570fa3a1b).  
  
## <a name="related-topics"></a>Tópicos relacionados  
 [Visão geral de aplicativos de dados no Visual Studio](../data-tools/overview-of-data-applications-in-visual-studio.md)  
 Fornece links para tópicos que abordam como criar aplicativos que funcionam com dados.  
  
 [Conectando-se a dados no Visual Studio](../data-tools/connecting-to-data-in-visual-studio.md)  
 Fornece links para tópicos sobre como usar [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] para conectar seu aplicativo a dados e criar fontes de dados para seus aplicativos.  
  
 [Preparando seu aplicativo para receber dados](http://msdn.microsoft.com/library/c17bdb7e-c234-4f2f-9582-5e55c27356ad)  
 Fornece links para tópicos que explicam como trabalhar com modelos de dados em seu aplicativo, incluindo conjuntos de dados e modelos de dados de entidade.  
  
 [Buscando dados no aplicativo](../data-tools/fetching-data-into-your-application.md)  
 Fornece links para tópicos que descrevem como carregar dados em seu aplicativo.  
  
 [Associar controles a dados no Visual Studio](../data-tools/bind-controls-to-data-in-visual-studio.md)  
 Fornece links para tópicos que explicam como a associação de formulários do Windows controles, controles do WPF e controles do Silverlight a fontes de dados.  
  
 [Editando dados no aplicativo](../data-tools/editing-data-in-your-application.md)  
 Fornece links para tópicos que descrevem como alterar dados em seu aplicativo.  
  
 [Validando dados](http://msdn.microsoft.com/library/b3a9ee4e-5d4d-4411-9c56-c811f2b4ee7e)  
 Fornece links para tópicos que descrevem como adicionar validação para alterações de dados.  
  
 [Salvando dados](../data-tools/saving-data.md)  
 Fornece links para tópicos que explicam como enviar dados atualizados do seu aplicativo para um banco de dados, ou como salvá-lo em outros formatos como XML.  
  
 [Ferramentas para trabalhar com fontes de dados no Visual Studio](http://msdn.microsoft.com/library/1e584c75-900a-49a0-a82a-d19172ef2eb3)  
 Fornece links para tópicos sobre as ferramentas que você pode usar para trabalhar com fontes de dados no Visual Studio, como o **fontes de dados** janela e o ADO.NET Entity Data Model Designer.