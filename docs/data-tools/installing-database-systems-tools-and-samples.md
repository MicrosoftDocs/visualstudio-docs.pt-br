---
title: Compatibilidade de banco de dados
ms.date: 09/06/2017
ms.topic: conceptual
helpviewer_keywords:
- database systems
- database compatibility
- databases for Visual Studio
ms.assetid: 821de34b-eaa9-40af-b9aa-b8305de16899
author: gewarren
ms.author: gewarren
manager: douge
ms.prod: visual-studio-dev15
ms.technology: vs-data-tools
ms.workload:
- data-storage
ms.openlocfilehash: ddb950fd916df6ff514e13435765b118e1e579dd
ms.sourcegitcommit: 708f77071c73c95d212645b00fa943d45d35361b
ms.translationtype: MTE95
ms.contentlocale: pt-BR
ms.lasthandoff: 12/07/2018
ms.locfileid: "53049554"
---
# <a name="compatible-database-systems-for-visual-studio"></a>Sistemas de banco de dados compatíveis para Visual Studio

Para desenvolver um aplicativo conectado por dados no Visual Studio, você normalmente instala o sistema de banco de dados em seu computador de desenvolvimento local e, em seguida, implantar o aplicativo e o banco de dados em um ambiente de produção quando estiverem prontas. O Visual Studio instala o SQL Server Express LocalDB em seu computador como parte do **armazenamento de dados e processamento** carga de trabalho. Esta instância de LocalDB é útil para desenvolvimento de aplicativos de dados conectados rápida e facilmente.

Para um sistema de banco de dados para ser acessado em aplicativos .NET e para ser visível nas janelas de ferramentas de dados do Visual Studio, ele deve ter um provedor de dados do ADO.NET. Um provedor especificamente deve oferecer suporte a Entity Framework se você planeja usar os modelos de dados de entidade em seu aplicativo .NET. Muitos provedores são oferecidos por meio do Gerenciador de pacotes NuGet ou por meio do Visual Studio Marketplace.

Se você estiver usando as APIs de armazenamento do Azure, instale os emuladores do armazenamento do Azure em seu computador local durante o desenvolvimento para evitar encargos até estar pronto para implantar em produção. Para obter mais informações, consulte [usar o emulador de armazenamento do Azure para desenvolvimento e teste](/azure/storage/common/storage-use-emulator).

A lista a seguir inclui alguns dos mais populares sistemas de banco de dados que podem ser usados em projetos do Visual Studio. A lista não é exaustiva. Para obter uma lista de fornecedores de terceiros que oferecem os provedores de dados ADO.NET que permitem a integração profunda com ferramentas do Visual Studio, consulte [provedores de dados ADO.NET](/dotnet/framework/data/adonet/data-providers).

## <a name="microsoft-sql-server"></a>Microsoft SQL Server

O banco de dados do Microsoft online do SQL Server está oferecendo. SQL Server 2016 fornece desempenho avançado, segurança avançada e rico e integrado, relatórios e análises. Ele é fornecido em várias edições que são projetadas para usos diferentes: de análise de negócios altamente escalonável e de alto desempenho, para usar em um único computador. SQL Server Express é uma edição completa do SQL Server que seja adequado para redistribuição e incorporação.  O LocalDB é uma edição simplificada do SQL Server Express que não requer nenhuma configuração e é executado no processo do seu aplicativo. Você pode baixar um ou ambos os produtos da [página de download do SQL Server Express](https://www.microsoft.com/sql-server/sql-server-editions-express). Muitos dos exemplos de SQL nesta seção usam o LocalDB do SQL Server. SQL Server Management Studio (SSMS) é um aplicativo de gerenciamento de banco de dados autônomo que tenha mais funcionalidade que é fornecido no Visual Studio SQL Server Object Explorer. Você pode obter o SSMS do link anterior.

## <a name="oracle"></a>Oracle

Você pode baixar uma edição gratuita ou paga do banco de dados Oracle do [rede de tecnologia do Oracle](http://www.oracle.com/technetwork/database/enterprise-edition/downloads/index-092322.html) página. Para obter suporte de tempo de design para o Entity Framework e os TableAdapters, será necessário o [ferramentas de desenvolvedor do Oracle para Visual Studio](http://www.oracle.com/technetwork/developer-tools/visual-studio/overview/index.html). Outros produtos oficiais do Oracle, incluindo o Oracle Instant Client, estão disponíveis por meio do Gerenciador de pacotes NuGet. Você pode baixar esquemas de exemplo do Oracle, seguindo as instruções de [documentação online da Oracle](http://docs.oracle.com/cd/E11882_01/server.112/e10831/toc.htm).

## <a name="mysql"></a>MySQL

O MySQL é um sistema de banco de dados do código-fonte aberto popular que é amplamente usado em empresas e sites. Downloads para MySQL, MySQL para Visual Studio e produtos relacionados correm [MySQL no Windows](http://www.mysql.com/why-mysql/windows/). Terceiros oferecem várias extensões do Visual Studio e aplicativos de gerenciamento autônomos para MySQL. Você pode procurar as ofertas no Gerenciador de pacotes NuGet (**ferramentas** > **Gerenciador de pacotes NuGet** > **gerenciar pacotes NuGet para solução**) .

## <a name="postgresql"></a>PostgreSQL

PostgreSQL é um sistema de banco de dados relacional de objeto gratuito, código-fonte aberto. Para instalá-lo no Windows, você pode baixá-lo partir o [página de download do PostgreSQL](http://www.postgresql.org/download/windows/). Você também pode criar PostgreSQL do código-fonte. O sistema de núcleo do PostgreSQL inclui uma interface de linguagem C. Muitos terceiros fornecem pacotes do NuGet para usar PostgreSQL de aplicativos .NET. Você pode procurar as ofertas no Gerenciador de pacotes NuGet (**ferramentas** > **Gerenciador de pacotes NuGet** > **gerenciar pacotes NuGet para solução**) . Talvez, o pacote mais popular é fornecido pelo [npgsql.org](http://www.npgsql.org).

## <a name="sqlite"></a>SQLite

O SQLite é um mecanismo de banco de dados SQL inserido que é executado no processo do aplicativo. Você pode baixá-lo do [página de download do SQLite](http://www.sqlite.org/download.html). Muitos pacotes do NuGet de terceiros para SQLite também estão disponíveis. Você pode procurar as ofertas no Gerenciador de pacotes NuGet (**ferramentas** > **Gerenciador de pacotes NuGet** > **gerenciar pacotes NuGet para solução**) .

## <a name="firebird"></a>Firebird

Firebird é um sistema de banco de dados SQL do código-fonte aberto. Você pode baixá-lo do [página de download de Firebird](http://firebirdsql.org/en/downloads/). Um provedor de dados ADO.NET está disponível por meio do Gerenciador de pacotes NuGet.

## <a name="see-also"></a>Consulte também

- [Acessando dados no Visual Studio](../data-tools/accessing-data-in-visual-studio.md)
- [Como determinar a versão e edição do SQL Server e seus componentes](http://support.microsoft.com/kb/321185)