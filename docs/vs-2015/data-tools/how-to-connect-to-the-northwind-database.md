---
title: 'Como: conectar-se ao banco de dados Northwind | Microsoft Docs'
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
- connections [Visual Studio], Northwind database
- Northwind sample database
ms.assetid: cc6cb79f-d035-41f8-b398-8d4a45922bfb
caps.latest.revision: 29
author: gewarren
ms.author: gewarren
manager: ghogen
robots: noindex,nofollow
ms.openlocfilehash: 3f64fa378029546f7a3126b324c282f6a91d7231
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49897622"
---
# <a name="how-to-connect-to-the-northwind-database"></a>Como se conectar ao banco de dados Northwind
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

À medida que aprender a criar aplicativos de banco de dados usando o Visual Studio, você precisará se conectar ao banco de dados Northwind para seguir vários dos exemplos na documentação desse produto. Dependendo do exemplo seguido, você se conectará ao banco de dados no SQL Server ou em um arquivo de banco de dados, tal como o Microsoft Access ou o SQL Server.  
  
## <a name="creating-data-connections-to-the-northwind-database"></a>Criando conexões de dados com o banco de dados Northwind  
 [!INCLUDE[note_settings_general](../includes/note-settings-general-md.md)]  
  
#### <a name="to-create-a-data-connection-to-the-northwind-database-sql-server"></a>Para criar uma conexão de dados com o banco de dados Northwind (SQL Server)  
  
1. Sobre o **exibição** menu, escolha **Gerenciador de servidores**/**Database Explorer**.  
  
2. Na **Gerenciador de servidores**/**Database Explorer**, abra o menu de atalho **conexões de dados** e escolha **Adicionar Conexão**.  
  
    Depois de escolher **Adicionar Conexão**, o **Escolher fonte de dados** caixa de diálogo ou o **Adicionar Conexão** caixa de diálogo será exibida.  
  
3. Se o **Choose Data Source** caixa de diálogo for exibida, selecione **Microsoft SQL Server**e, em seguida, escolha **Okey**.  
  
    Se o **Adicionar Conexão** caixa de diálogo aparece e o **fonte de dados** não é **Microsoft SQL Server (SqlClient)**, escolha o **alteração** Para abrir o **fonte de dados de alteração** caixa de diálogo, selecione **Microsoft SQL Server**e, em seguida, escolha o **Okey** botão.  
  
4. No **nome do servidor** lista, especifique o nome do servidor no qual o banco de dados Northwind está localizado.  
  
5. Dependendo dos requisitos da sua versão do SQL Server e banco de dados Northwind, escolha **usar autenticação do Windows** ou escolha **usar a autenticação do SQL Server** e insira um nome de usuário e senha para fazer logon no computador que executa o SQL Server.  
  
6. Escolha o banco de dados Northwind a **selecione ou insira um nome de banco de dados** lista.  
  
7. Escolher **Conexão de teste** para verificar a conectividade ao banco de dados Northwind.  
  
8. Escolha **OK**.  
  
    Uma conexão de dados no banco de dados Northwind é adicionada à **Gerenciador de servidores**/**Gerenciador de banco de dados**.  
  
   Além de conectar a uma instância remota de um banco de dados do SQL Server, também é possível se conectar diretamente aos arquivos reais que contêm o banco de dados. Isso permite que você adicione os arquivos de banco de dados diretamente em um projeto em que eles possam ser implantados como parte do aplicativo. Atualmente, há suporte para os seguintes arquivos de banco de dados local: arquivos de banco de dados do SQL Server Compact (. sdf), [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] e arquivos de banco de dados SQL Server Express (. mdf) e arquivos de banco de dados do Microsoft Access (. mdb ou. accdb).  
  
#### <a name="to-create-a-data-connection-to-the-northwind-databasesql-server-database-file-mdf"></a>Para criar uma conexão de dados com o banco de dados Northwind – arquivo de banco de dados do SQL Server (.mdf)  
  
1.  Sobre o **exibição** menu, escolha **Gerenciador de servidores**/**Database Explorer**.  
  
2.  Na **Gerenciador de servidores**/**Database Explorer**, abra o menu de atalho **conexões de dados** e escolha **Adicionar Conexão**.  
  
     Depois de escolher **Adicionar Conexão**, o **Adicionar Conexão** caixa de diálogo ou o **Escolher fonte de dados** caixa de diálogo será exibida.  
  
3.  Se o **Choose Data Source** caixa de diálogo for exibida, selecione **arquivo de banco de dados do Microsoft SQL Server**e, em seguida, escolha o **Okey**.  
  
4.  Se o **Adicionar Conexão** caixa de diálogo for exibida, verifique se que o **fonte de dados** está definido como **arquivo de banco de dados do Microsoft SQL Server (SqlClient)**. Se ele não for definido como **arquivo de banco de dados do Microsoft SQL Server (SqlClient)**, escolha **alteração** para abrir o **alterar fonte de dados** caixa de diálogo, escolha **Microsoft SQL Arquivo de banco de dados do servidor**e, em seguida, escolha o **Okey** botão.  
  
5.  Escolher **procurar** para localizar o arquivo. mdf que contém o banco de dados Northwind.  
  
6.  Dependendo dos requisitos da sua versão do banco de dados Northwind, escolha **usar autenticação do Windows** ou escolha **autenticação do SQL Server** e insira um nome de usuário e senha para fazer logon na computador executando o SQL Server.  
  
7.  Escolha o botão **OK**.  
  
     Uma conexão de dados no banco de dados Northwind é adicionada à **Gerenciador de servidores**/**Gerenciador de banco de dados**.  
  
> [!NOTE]
>  [!INCLUDE[vs_dev11_long](../includes/vs-dev11-long-md.md)] possui alterações que se aplicam ao arquivo de banco de dados Northwind (.mdf). Para obter informações, consulte [como: instalar os bancos de dados de exemplo](../data-tools/how-to-install-sample-databases.md).  
  
#### <a name="to-create-a-data-connection-to-the-northwind-databaseaccess-database-file-mdb-or-accdb"></a>Para criar uma conexão de dados com o banco de dados Northwind – arquivo de banco de dados do Access (.mdb ou .accdb)  
  
1.  Sobre o **exibição** menu, escolha **Gerenciador de servidores**/**Database Explorer**.  
  
2.  Na **Gerenciador de servidores**/**Database Explorer**, abra o menu de atalho **conexões de dados** e escolha **Adicionar Conexão**.  
  
     Depois de escolher **Adicionar Conexão**, o **Adicionar Conexão** caixa de diálogo ou o **Escolher fonte de dados** caixa de diálogo será exibida.  
  
3.  Se o **Choose Data Source** caixa de diálogo for exibida, selecione **arquivo de banco de dados do Microsoft Access**e, em seguida, escolha **Okey**.  
  
4.  Se o **Adicionar Conexão** caixa de diálogo for exibida, verifique se que o **fonte de dados** está definido como **arquivo de banco de dados do Microsoft Access**. Se ele não for definido como **arquivo de banco de dados do Microsoft Access**, escolha **alteração** para abrir o **alterar fonte de dados** caixa de diálogo, escolha **banco de dados do Microsoft Access Arquivo**e, em seguida, escolha o **Okey** botão.  
  
5.  Escolher **procurar** para localizar o arquivo. mdb ou. accdb que contém o banco de dados Northwind.  
  
6.  Insira um nome de usuário e uma senha caso sua versão do banco de dados Northwind exija.  
  
7.  Escolha **OK**.  
  
     Uma conexão de dados no banco de dados Northwind é adicionada à **Gerenciador de servidores**/**Gerenciador de banco de dados**.  
  
## <a name="see-also"></a>Consulte também  
 [Como instalar bancos de dados de exemplo](../data-tools/how-to-install-sample-databases.md)   
 [Programação de dados com o Microsoft Access 2010](http://msdn.microsoft.com/library/office/ff965871.aspx)   
 [Instruções passo a passo de dados](http://msdn.microsoft.com/library/15a88fb8-3bee-4962-914d-7a1f8bd40ec4)