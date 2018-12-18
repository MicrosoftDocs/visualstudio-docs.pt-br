---
title: Instalando sistemas de banco de dados, ferramentas e exemplos | Microsoft Docs
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
- sample databases
- databases, samples
ms.assetid: 821de34b-eaa9-40af-b9aa-b8305de16899
caps.latest.revision: 31
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: f18ace9a18eefd0758e581b83001b85c3f48a3da
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49244277"
---
# <a name="installing-database-systems-tools-and-samples"></a>Instalando sistemas de banco de dados, ferramentas e exemplos
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

  
O próprio Visual Studio não inclui quaisquer sistemas de banco de dados diferentes daqueles usados internamente. Para desenvolver um aplicativo conectado por dados no Visual Studio, você normalmente instala o sistema de banco de dados em seu computador de desenvolvimento local e, em seguida, implantar o aplicativo e o banco de dados em um ambiente de produção quando estiverem prontas. Para o sistema de banco de dados para ser acessado em aplicativos .NET e para ser visível nas janelas de ferramentas de dados do Visual Studio, ele deve ter um provedor de dados do ADO.NET. Um provedor especificamente deve oferecer suporte a Entity Framework se você planeja usar os modelos de dados de entidade em seu aplicativo .NET.     Muitos provedores são oferecidos por meio do Gerenciador de pacotes NuGet ou por meio da Galeria do Visual Studio.  
  
 Para o desenvolvimento do SQL, certifique-se de que você tenha o SQL Server Data Tools instalado no Visual Studio. Clique o **exibição** menu. Se você não vir o Pesquisador de objetos do SQL Server, vá para painel de controle e alterar o Visual Studio. No instalador, selecione **Microsoft SQL Server Data Tools**.  
  
 Se você estiver usando as APIs de armazenamento do Azure, instale os emuladores do armazenamento do Azure em seu computador local durante o desenvolvimento para evitar encargos até estar pronto para implantar em produção. Para obter mais informações, consulte [usar o emulador de armazenamento do Azure para desenvolvimento e teste](https://azure.microsoft.com/en-us/documentation/articles/storage-use-emulator/).  
  
 A lista a seguir inclui alguns dos mais populares sistemas de banco de dados que podem ser usados em projetos do Visual Studio. A lista não é exaustiva. Para obter uma lista de fornecedores de terceiros que oferecem os provedores de dados ADO.NET que permitem a integração profunda com ferramentas do Visual Studio, consulte [provedores de dados ADO.NET](https://msdn.microsoft.com/library/dd363565.aspx).  
  
### <a name="microsoft-sql-server"></a>Microsoft SQL Server  
 O banco de dados do Microsoft online do SQL Server está oferecendo. SQL Server 2016 fornece desempenho avançado, segurança avançada e rico e integrado, relatórios e análises. Ele é fornecido em várias edições que são projetadas para usos diferentes: de análise de negócios altamente escalonável e de alto desempenho, para usar em um único computador. SQL Server Express é uma edição completa do SQL Server que seja adequado para redistribuição e incorporação.  O LocalDB é uma edição simplificada do SQL Server Express que não requer nenhuma configuração e é executado no processo do seu aplicativo. Você pode baixar um ou ambos os produtos da [a página de download do SQL Server Express](https://www.microsoft.com/en-us/server-cloud/Products/sql-server-editions/sql-server-express.aspx).    Muitos dos exemplos de SQL nesta seção usam o LocalDB do SQL Server. SQL Server Management Studio (SSMS) é um aplicativo de gerenciamento de banco de dados autônomo que tenha mais funcionalidade que é fornecido no Visual Studio SQL Server Object Explorer. Você pode obter o SSMS do link anterior.  
  
### <a name="oracle"></a>Oracle  
 Você pode baixar uma edição gratuita ou paga do banco de dados Oracle do [Oracle Technology Network](http://www.oracle.com/technetwork/database/enterprise-edition/downloads/index-092322.html) página. Para obter suporte de tempo de design para o Entity Framework e os TableAdapters, será necessário o [Oracle Developer Tools para Visual Studio](http://www.oracle.com/technetwork/developer-tools/visual-studio/overview/index.html). Outros produtos oficiais do Oracle, incluindo o Oracle Instant Client, estão disponíveis por meio do Gerenciador de pacotes NuGet.  Você pode baixar esquemas de exemplo do Oracle, seguindo as instruções de [documentação Online da Oracle](http://docs.oracle.com/cd/E11882_01/server.112/e10831/toc.htm).  
  
### <a name="mysql"></a>MySQL  
 O MySQL é um sistema de banco de dados do código-fonte aberto popular que é amplamente usado em empresas e sites. Downloads para MySQL, MySQL para Visual Studio e produtos relacionados correm [MySQL no Windows](http://www.mysql.com/why-mysql/windows/).  Terceiros oferecem várias extensões do Visual Studio e aplicativos de gerenciamento autônomos para MySQL. Você pode procurar as ofertas no Gerenciador de pacotes NuGet (**ferramentas** > **Gerenciador de pacotes NuGet** > **gerenciar pacotes NuGet para solução**) .  
  
### <a name="postgresql"></a>PostgreSQL  
 PostgreSQL é um sistema de banco de dados relacional de objeto gratuito, código-fonte aberto. Para instalá-lo no Windows, você pode baixá-lo partir o [página de download do PostgreSQL](http://www.postgresql.org/download/windows/).  Você também pode criar PostgreSQL do código-fonte.  O sistema de núcleo do PostgreSQL inclui uma interface de linguagem C. Muitos terceiros fornecem pacotes do NuGet para usar PostgreSQL de aplicativos .NET.  Você pode procurar as ofertas no Gerenciador de pacotes NuGet (**ferramentas** > **Gerenciador de pacotes NuGet** > **gerenciar pacotes NuGet para solução**) . Talvez o pacote mais popular é fornecido pelo [npgsql.org](http://www.npgsql.org).  
  
### <a name="sqlite"></a>SQLite  
 O SQLite é um mecanismo de banco de dados SQL inserido que é executado no processo do aplicativo. Você pode baixá-lo do [página de download do SQLite](http://www.sqlite.org/download.html). Muitos pacotes do NuGet de terceiros para SQLite também estão disponíveis. Você pode procurar as ofertas no Gerenciador de pacotes NuGet (**ferramentas** > **Gerenciador de pacotes NuGet** > **gerenciar pacotes NuGet para solução**) .  
  
### <a name="firebird"></a>Firebird  
 Firebird é um sistema de banco de dados SQL do código-fonte aberto. Você pode baixá-lo do [página de download de Firebird](http://firebirdsql.org/en/downloads/). Um provedor de dados ADO.NET está disponível por meio do Gerenciador de pacotes NuGet.  
  
## <a name="see-also"></a>Consulte também  
 [Como determinar a versão e edição do SQL Server e seus componentes](http://support.microsoft.com/kb/321185)

