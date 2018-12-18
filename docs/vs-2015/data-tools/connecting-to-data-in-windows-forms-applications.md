---
title: Connecting to Data in Windows Forms de aplicativos | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- System.Data.SqlClient.SqlConnection
- System.Data.Odbc.OdbcConnection
- System.Data.OleDb.OleDbConnection
- System.Data.OracleClient.OracleConnection
dev_langs:
- VB
- CSharp
- C++
- aspx
helpviewer_keywords:
- connection objects, tools for working with
- OleDbConnection class, ADO.NET connection objects
- databases [Visual Studio], connecting to
- data adapters, connections
- connection pooling, ADO.NET connections
- connection strings [Visual Studio], ADO.NET
- connection objects, types of
- dynamic properties, ADO.NET connections
- connections, about connections
- data [Visual Studio], connecting
- design-time connections
- connections, design-time
- TableAdapters, connections
- connection objects
- SqlConnection class, ADO.NET connection objects
- connecting to databases, ADO.NET connections
- transactions, ADO.NET
- database connections [Visual Studio], ADO.NET
ms.assetid: 184cbd0d-3b26-418d-a11c-f9f8f004fbff
caps.latest.revision: 31
author: gewarren
ms.author: gewarren
manager: ghogen
robots: noindex,nofollow
ms.openlocfilehash: d8da35b32f3dd25bd7ed47b25f722c6b0aa21ac7
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49208943"
---
# <a name="connecting-to-data-in-windows-forms-applications"></a>Conectando a dados em aplicativos dos Windows Forms
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

O [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] fornece ferramentas para conectar seu aplicativo a dados de várias fontes diferentes, como bancos de dados, serviços Web e objetos. Se você estiver usando as ferramentas de design de dados no [!INCLUDE[vsprvs](../includes/vsprvs-md.md)], normalmente você não precisa criar explicitamente um objeto de conexão para o formulário ou componente. O objeto de conexão geralmente é criado depois que você preenche um dos assistentes de dados ou arrasta objetos de dados para o seu formulário. Para conectar seu aplicativo a dados em um banco de dados, serviço web ou objeto, execute as [Data Source Configuration Wizard](http://msdn.microsoft.com/library/c4df7de5-5da0-4064-940c-761dd6d9e28f) selecionando **Add New Data Source** do [janela fontes de dados](http://msdn.microsoft.com/library/0d20f699-cc95-45b3-8ecb-c7edf1f67992).  
  
 O diagrama a seguir mostra o fluxo normal das operações durante a conexão aos dados, executando uma consulta TableAdapter para buscar dados e exibi-lo em um formulário em um aplicativo do Windows.  
  
 ![Fluxo de dados em um aplicativo cliente](../data-tools/media/clientdatadiagram.gif "ClientDataDiagram")  
  
 Em algumas situações, é conveniente criar um objeto de conexão sem o auxílio de ferramentas de design de dados. Para obter informações sobre como criar conexões programaticamente, consulte [conectando a uma fonte de dados](http://msdn.microsoft.com/library/9abc3f92-1be3-4e1a-b360-762dc689650e).  
  
> [!NOTE]
>  Para obter informações sobre como conectar aplicativos web aos dados, consulte [mapa de conteúdo de acesso do ASP.NET dados](http://msdn.microsoft.com/en-us/f9219396-a0fa-481f-894d-e3d9c67d64f2).  
  
## <a name="walkthroughs-for-connecting-windows-forms-applications-to-data"></a>Passo a passo para conectar aplicativos do Windows Forms a dados  
 O passo a passo a seguir fornece procedimentos relacionados à conexão a dados em aplicativos do Windows Forms:  
  
-   [Passo a passo: Conectando a dados em um banco de dados (Windows Forms)](http://msdn.microsoft.com/library/02d39aa6-8993-4602-be13-a13536af3d1c)  
  
-   [Passo a passo: conectando a dados em um arquivo de banco de dados local (Windows Forms)](../data-tools/walkthrough-connecting-to-data-in-a-local-database-file-windows-forms.md)  
  
-   [Passo a passo: Conectando a dados em um serviço Web (Windows Forms)](http://msdn.microsoft.com/library/079fb9b0-c733-40c1-acd1-d0d68834354d)  
  
-   [Passo a passo: Conectando a dados em objetos (Windows Forms)](http://msdn.microsoft.com/library/21a7fba2-b38b-4726-8cbe-d22154b75a05)  
  
-   [Conectar-se a dados em um banco de dados do Access (Windows Forms)](../data-tools/connect-to-data-in-an-access-database-windows-forms.md)  
  
## <a name="creating-connections"></a>Criando conexões  
 Na [!INCLUDE[vsprvs](../includes/vsprvs-md.md)], as conexões são configuradas usando o **Adicionar/Modificar Conexão** caixa de diálogo. O **Adicionar Conexão** caixa de diálogo aparece quando você está editando ou criando conexões dentro de um dos assistentes de dados ou [Server Explorer/Database Explorer](http://msdn.microsoft.com/library/4ea29b3b-bbb2-45e4-9082-eaf635c41c4d) ou quando você está editando propriedades de conexão no o **propriedades** janela.  
  
 As conexões de dados são configuradas automaticamente quando você executa uma das seguintes ações.  
  
|Ação|Descrição|  
|------------|-----------------|  
|Execute o [Assistente de configuração de fonte de dados](http://msdn.microsoft.com/library/c4df7de5-5da0-4064-940c-761dd6d9e28f).|As conexões são configuradas quando o caminho do banco de dados é escolhido na **Data Source Configuration Wizard**. Para obter mais informações, consulte [como: conectar a dados em um banco de dados](../data-tools/how-to-connect-to-data-in-a-database.md).|  
|Execute o [Assistente de configuração TableAdapter](http://msdn.microsoft.com/library/3a373dd9-7b34-4d3c-a48b-69414512bac8).|As conexões são criadas dentro de **Assistente de configuração TableAdapter**. Para obter mais informações, consulte [criar e configurar TableAdapters](../data-tools/create-and-configure-tableadapters.md).|  
|Execute o [editando TableAdapters](../data-tools/editing-tableadapters.md).|As conexões são criadas dentro de **Assistente de configuração de consulta do TableAdapter**. Para obter mais informações, consulte [como: criar consultas do TableAdapter](../data-tools/how-to-create-tableadapter-queries.md).|  
|Arraste itens dos [janela fontes de dados](http://msdn.microsoft.com/library/0d20f699-cc95-45b3-8ecb-c7edf1f67992) em um formulário ou o [Component Designer](http://msdn.microsoft.com/library/61a3a450-5b15-465e-bd9a-72a6c8c2b282).|Objetos de Conexão são criados quando você arrasta itens dos **fontes de dados** janela para o **Designer de formulários do Windows** ou **Component Designer**. Para obter mais informações, consulte [associar controles a dados no Visual Studio](../data-tools/bind-controls-to-data-in-visual-studio.md).|  
|Adicionar novas conexões de dados para [Server Explorer/Database Explorer](http://msdn.microsoft.com/library/4ea29b3b-bbb2-45e4-9082-eaf635c41c4d).|Conexões de dados **Server Explorer/Database Explorer** aparecem na lista de conexões disponíveis dentro dos assistentes de dados|  
  
## <a name="connection-strings"></a>Cadeias de caracteres de conexão  
 As cadeias de caracteres de conexão podem ser armazenadas dentro do seu aplicativo compilado ou no arquivo de configuração do aplicativo. Para obter mais informações, consulte [como: salvar e editar cadeias de caracteres de Conexão](~/E:/Repos/visualstudio-docs-pr/docs/data-tools/how-to-save-and-edit-connection-strings.md).  
  
## <a name="connection-information-and-security"></a>Informações e segurança de conexão  
 Como abrir uma conexão envolve a obtenção de acesso a um importante recurso, que é um banco de dados, muitas vezes há questões de segurança envolvidas na configuração e trabalho com uma conexão.  
  
 Como você protege o aplicativo e o acesso dele à fonte de dados depende da arquitetura do seu sistema. Em um aplicativo baseado na Web, por exemplo, os usuários normalmente têm acesso anônimo ao IIS (Internet Information Services) e, portanto, não fornecem credenciais de segurança. Nesse caso, o aplicativo mantém e usa suas próprias informações de logon, em vez de quaisquer informações específicas do usuário, para abrir a conexão e acessar o banco de dados.  
  
> [!IMPORTANT]
>  O armazenamento de detalhes da cadeia de caracteres de conexão, como uma senha, pode afetar a segurança do aplicativo. O uso da segurança integrada do Windows é uma maneira mais segura de controlar o acesso a um banco de dados. Para obter mais informações, consulte [Protegendo informações de conexão](http://msdn.microsoft.com/library/1471f580-bcd4-4046-bdaf-d2541ecda2f4).  
  
 Em aplicativos de intranet ou de várias camadas, você pode usar a opção de segurança integrada fornecida pelo Windows, IIS e SQL Server. Nesse modelo, as credenciais de autenticação do usuário para a rede local também são usadas para acessar recursos de banco de dados e nenhum nome de usuário ou senha explícita é usada na cadeia de caracteres de conexão. Normalmente, as permissões são estabelecidas no computador do servidor de banco de dados por meio de grupos, para que você não precise estabelecer permissões individuais para cada usuário que acesse o banco de dados. Neste modelo, você não precisa armazenar nenhuma informação de logon para a conexão e não precisa realizar outras ações para proteger as informações da cadeia de caracteres de conexão.  
  
 Para obter mais informações sobre segurança, consulte os seguintes tópicos:  
  
-   [Securing ADO.NET Applications](http://msdn.microsoft.com/library/005a1d43-6ee5-471e-ad98-1d30a44d49d5) (Protegendo aplicativos ADO.NET)  
  
-   [Acesso mais seguro a arquivos e a dados nos Windows Forms](http://msdn.microsoft.com/library/3cd3e55b-2f5e-40dd-835d-f50f7ce08967)  
  
## <a name="design-time-connections-in-server-explorerdatabase-explorer"></a>Conexões de tempo de design no Gerenciador de Servidores/Navegador de Banco de Dados  
 **Gerenciador de banco de dados/Gerenciador de servidores** fornece uma maneira de criar conexões de tempo de design para fontes de dados. Isso permite que você: navegue fontes de dados disponíveis, exiba informações sobre as tabelas, colunas e outros elementos que elas contêm e edite e crie elementos de banco de dados.  
  
 Seu aplicativo não usa diretamente as conexões disponíveis no **Server Explorer/Database Explorer**. Essas conexões são usadas pelo [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] para trabalhar com seu banco de dados em tempo de design. Para obter mais informações, consulte [Visual Database Tools](http://msdn.microsoft.com/en-us/6b145922-2f00-47db-befc-bf351b4809a1).  
  
 Por exemplo, no tempo de design você pode usar **Server Explorer/Database Explorer** para criar uma conexão para um banco de dados. Posteriormente, ao criar um formulário, você pode procurar o banco de dados, selecionar colunas de uma tabela e arrastá-las para o [Dataset Designer](../data-tools/creating-and-editing-typed-datasets.md). Isso cria uma [TableAdapter](../data-tools/tableadapter-overview.md) no conjunto de dados. Ele também cria um novo objeto de conexão, que é parte do TableAdapter recém-criado.  
  
 As informações sobre conexões de tempo de design são armazenadas no seu computador local, independentemente de um projeto ou solução específicos. Portanto, depois de estabelecer uma conexão de tempo de design enquanto trabalha em um aplicativo, ele aparece no **Gerenciador de banco de dados/Gerenciador de servidores** sempre que você trabalha em [!INCLUDE[vsprvs](../includes/vsprvs-md.md)], desde que o servidor ao qual a conexão pontos está disponível. Para obter mais informações, consulte [como: conectar-se ao banco de dados do Gerenciador de servidores](http://msdn.microsoft.com/en-us/7c1c3067-0d77-471b-872b-639f9f50db74).  
  
 [!INCLUDE[SQLObjectExplorer](../includes/sqlobjectexplorer-md.md)]  
  
## <a name="see-also"></a>Consulte também  
 [Conectando-se a dados no Visual Studio](../data-tools/connecting-to-data-in-visual-studio.md)   
 [Como conectar-se a dados em um banco de dados](../data-tools/how-to-connect-to-data-in-a-database.md)   
 [Passo a passo: Conectando a dados em um banco de dados (Windows Forms)](http://msdn.microsoft.com/library/02d39aa6-8993-4602-be13-a13536af3d1c)   
 [Mapa de conteúdo de acesso de dados do ASP.NET](http://msdn.microsoft.com/en-us/f9219396-a0fa-481f-894d-e3d9c67d64f2)   
 [Preparando o aplicativo para receber dados](http://msdn.microsoft.com/library/c17bdb7e-c234-4f2f-9582-5e55c27356ad)   
 [Buscando dados no aplicativo](../data-tools/fetching-data-into-your-application.md)   
 [Associar controles a dados no Visual Studio](../data-tools/bind-controls-to-data-in-visual-studio.md)   
 [Editando dados no aplicativo](../data-tools/editing-data-in-your-application.md)   
 [Validando dados](http://msdn.microsoft.com/library/b3a9ee4e-5d4d-4411-9c56-c811f2b4ee7e)   
 [Salvando dados](../data-tools/saving-data.md)