---
title: Ferramentas de dados do Visual Studio para .NET | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: c3175080-1dfb-4ab8-a460-92dadbb844b4
caps.latest.revision: 22
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: 841311af90ddf4bedfb9d055e5764068cdc71632
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49859701"
---
# <a name="visual-studio-data-tools-for-net"></a>Ferramentas de dados do Visual Studio para .NET
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Visual Studio e o .NET Framework juntos fornecem API abrangente e suporte a ferramentas para conectar-se aos bancos de dados, modelagem de dados na memória e exibir os dados na interface do usuário.  As classes do .NET Framework que fornecem funcionalidade de acesso a dados são conhecidas como [ADO.NET](https://msdn.microsoft.com/library/e80y5yhx\(v=vs.110\).aspx). ADO.NET, juntamente com os dados de ferramentas no Visual Studio, foi originalmente projetado principalmente para dar suporte a bancos de dados relacionais e XML. Hoje em dia, muitos fornecedores de banco de dados NoSQL, ou por terceiros, oferecem provedores ADO.NET.  
  
 Visual Studio 2015 atualização 2 inclui as atualizações mais recentes do [SQL Server Data Tools](https://msdn.microsoft.com/library/hh272686\(v=vs.103\).aspx), que permitem que o suporte para os recursos mais recentes do Azure [banco de dados SQL](https://azure.microsoft.com/en-us/services/sql-database/) e [SQL Server 2016](https://www.microsoft.com/en-us/server-cloud/products/sql-server-2016/). [.NET core](https://www.dotnetfoundation.org/netcore) dá suporte ao ADO.NET, exceto para conjuntos de dados e tipos relacionados. Se você estiver direcionando o .NET Core e exige uma camada de mapeamento relacional de objeto (ORM), use [Entity Framework Core](https://msdn.microsoft.com/data/ef.aspx).  
  
 O diagrama a seguir mostra uma exibição simplificada da arquitetura básica:  
  
 ![Arquitetura do ADO.NET](../data-tools/media/raddata-ado-net-architecture-diagram.png "raddata diagrama da arquitetura do ADO.NET")  
  
 O fluxo de trabalho típico é o seguinte:  
  
1. Instale um desenvolvimento ou teste de banco de dados em seu computador local. Ver [instalando sistemas de banco de dados, ferramentas e exemplos](../data-tools/installing-database-systems-tools-and-samples.md). Se você estiver usando um serviço de dados do Azure, essa etapa não é necessária.  
  
2. Teste a conexão ao banco de dados (ou serviço ou arquivo local) no Visual Studio. Ver [adicionar novas conexões](../data-tools/add-new-connections.md).  
  
3. (Opcional) Use as ferramentas para gerar e configurar um novo modelo. Modelos com base no Entity Framework são a recomendação padrão para novos aplicativos. O modelo, seja qual for o que você utiliza, é a fonte de dados que o aplicativo interage com. O modelo logicamente fica entre o banco de dados ou serviço e o aplicativo.  Ver [adicionar novas fontes de dados](../data-tools/add-new-data-sources.md).  
  
4. Arraste a fonte de dados do **fontes de dados** janela na superfície de design do Windows Forms, ASP.NET ou Windows Presentation Foundation para gerar o código de associação de dados que exibirá os dados para o usuário da maneira que você especificar. Ver [associar controles a dados no Visual Studio](../data-tools/bind-controls-to-data-in-visual-studio.md).  
  
5. Adicione código personalizado para coisas como as regras de negócio, pesquisa e validação de dados, ou para tirar proveito da funcionalidade personalizada que expõe o banco de dados subjacente.  
  
   Você pode ignorar a etapa 3 e programar um aplicativo .NET para emitir comandos diretamente para um banco de dados, em vez de usar um modelo. Nesse caso, você encontrará a documentação relevante aqui: [ADO.NET](https://msdn.microsoft.com/library/e80y5yhx\(v=vs.110\).aspx). Observe que você ainda pode usar o Assistente de configuração de fonte de dados e designers para gerar o código de associação de dados ao popular seus próprios objetos na memória e, em seguida, vincular dados em controles de interface do usuário a esses objetos.  
  
## <a name="in-this-section"></a>Nesta seção  
  
-   [Criar um aplicativo de dados simples usando o ADO.NET](../data-tools/create-a-simple-data-application-by-using-adonet.md)  
  
-   [Adicionar novas conexões](../data-tools/add-new-connections.md)  
  
-   [Adicionar novas fontes de dados](../data-tools/add-new-data-sources.md)  
  
-   [Ferramentas do Modelo de Dados de Entidade no Visual Studio](../data-tools/entity-data-model-tools-in-visual-studio.md)  
  
-   [Ferramentas de conjunto de dados no Visual Studio](../data-tools/dataset-tools-in-visual-studio.md)  
  
-   [Ferramentas LINQ to SQL no Visual Studio](../data-tools/linq-to-sql-tools-in-visual-studio2.md)  
  
-   [Associar controles a dados no Visual Studio](../data-tools/bind-controls-to-data-in-visual-studio.md)  
  
-   [Recursos adicionais para solucionar problemas de erros de acesso a dados](../data-tools/additional-resources-for-troubleshooting-data-access-errors.md)  
  
-   [Serviços do Windows Communication Foundation e WCF Data Services no Visual Studio](../data-tools/windows-communication-foundation-services-and-wcf-data-services-in-visual-studio.md)  
  
-   [Criando e gerenciando bancos de dados e aplicativos da camada de dados no Visual Studio](../data-tools/creating-and-managing-databases-and-data-tier-applications-in-visual-studio.md)  
  
-   [Recursos adicionais para solucionar problemas de erros de acesso a dados](../data-tools/additional-resources-for-troubleshooting-data-access-errors.md)  
  
## <a name="see-also"></a>Consulte também  
 [Acessando dados no Visual Studio](../data-tools/accessing-data-in-visual-studio.md)







