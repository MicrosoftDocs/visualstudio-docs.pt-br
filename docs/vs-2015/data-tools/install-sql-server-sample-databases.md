---
title: Instalar bancos de dados de exemplo do SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 38840167-c3f8-4cb3-8d15-8af04a0a20a1
caps.latest.revision: 14
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: f6cd9260f29d8e46f66e54fec8cb24ae6857eb05
ms.sourcegitcommit: d462dd10746624ad139f1db04edd501e7737d51e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/29/2018
ms.locfileid: "50217857"
---
# <a name="install-sql-server-sample-databases"></a>Instalar bancos de dados de exemplo do SQL Server
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

  
Os bancos de dados são úteis para experimentar consultas SQL e LINQ, vinculação de dados, modelagem de Entity Framework e assim por diante.  Cada produto de banco de dados tem seus próprios bancos de dados de exemplo. Northwind e AdventureWorks são dois populares do SQL Server os bancos de dados.  
  
 **AdventureWorks** é o atual banco de dados de exemplo fornecido para produtos do SQL Server. Você pode baixá-lo como um arquivo. mdf a partir de [página do AdventureWorks no Codeplex](http://msftdbprodsamples.codeplex.com/). Há versões de (LT) regulares e leves do banco de dados disponíveis aqui. Na maioria dos cenários, a versão de longo prazo é preferencial porque é menos complexo.  
  
 **Northwind** é um banco de dados do SQL Server relativamente simple que foi usado por muitos anos. Você pode baixá-lo como um arquivo. bak do [página de banco de dados Northwind no CodePlex](https://northwinddatabase.codeplex.com/). Para evitar problemas de permissões, descompacte o arquivo em uma nova pasta que não está sob sua pasta de usuário.  
  
#### <a name="to-restore-a-database-from-a-bak-file-in-visual-studio"></a>Para restaurar um banco de dados de um arquivo. bak no Visual Studio  
  
1.  Quando você faz backup de um banco de dados do Microsoft SQL Server, o resultado é um arquivo. bak. Para tornar o. bak arquivo utilizável novamente como um arquivo de banco de dados, ele deve ser *restaurado*. No menu principal, selecione **modo de exibição** > **SQL Server Object Explorer**. Se você não estiver visível, talvez você precise instalá-lo. Vá para **painel de controle** > **programas e recursos**, localize o Microsoft Visual Studio 2015 e clique o **alteração** botão. Quando a lista dos componentes instalados é exibida na janela do instalador, selecione a **Pesquisador de objetos do SQL Server** caixa de seleção e, em seguida, continue com a instalação.  
  
2.  No Pesquisador de objetos do SQL Server, clique em qualquer mecanismo de banco de dados do SQL Server (por exemplo, o localdb) e selecione**nova consulta**.  
  
     ![SQL Server objeto Explorer nova consulta](../data-tools/media/raddata-sql-server-object-explorer-new-query.png "raddata SQL Server objeto Gerenciador de nova consulta")  
  
3.  Primeiro, você precisa que os nomes lógicos dos arquivos de log e banco de dados dentro do arquivo. bak. Para fazer isso, insira esta consulta no Editor de consultas SQL e, em seguida, selecionar o verde **executar** botão na parte superior da janela. Modifique o caminho do arquivo se necessário, para apontar para o arquivo. bak.  
  
    ```  
    RESTORE FILELISTONLY  
    FROM DISK = 'C:\nw\northwind.bak'  
    GO  
    ```  
  
     Anote os nomes lógicos que aparecem na janela de resultados.  Para o banco de dados Northwind, os dois nomes lógicos são Northwind e Northwind_log.  
  
4.  Agora, execute esta consulta para criar o banco de dados. Substitua seus próprios caminhos de origem e de destino, nomes de banco de dados lógicos e nomes de arquivo físico para a Northwind conforme apropriado. Manter os arquivos. mdf e. ldf de extensões de arquivo.  
  
    ```  
    RESTORE DATABASE Northwind  
    FROM DISK = 'c:\nw\northwind.bak'  
    WITH MOVE 'Northwind' TO 'c:\nw\northwind.mdf',  
    MOVE 'Northwind_log' TO 'c:\nw\northwind.ldf'  
    ```  
  
5.  No Pesquisador de objetos do SQL Server, clique com botão direito no **bancos de dados** nó e você verá o nó de banco de dados Northwind. Se não, em seguida, clique com botão direito em bancos de dados e selecione **adicionar novo banco de dados**. Insira o nome e o local do arquivo. mdf que você acabou de criar.  
  
6.  O banco de dados agora está pronto para uso como uma fonte de dados no Visual Studio.  
  
#### <a name="to-restore-a-database-from-a-bak-file-in-sql-server-management-studio"></a>Para restaurar um banco de dados de um arquivo. bak no SQL Server Management Studio  
  
1.  Baixe o SQL Server Management Studio no site de download.  
  
2.  No SSMS **Pesquisador de objetos** janela, clique com botão direito do **bancos de dados** nó, selecione**restaurar banco de dados**e fornecer o local do arquivo. bak.  
  
     ![Restaurar banco de dados SSMS](../data-tools/media/raddata-ssms-restore-database.png "raddata SSMS restaurar banco de dados")

