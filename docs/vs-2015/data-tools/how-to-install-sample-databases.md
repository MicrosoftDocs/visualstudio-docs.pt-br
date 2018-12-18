---
title: 'Como: instalar bancos de dados de exemplo | Microsoft Docs'
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
- sample databases, Adventure Works
- data [Visual Studio], sample databases
- sample databases, Northwind
- Northwind sample database
- Adventure Works sample database
ms.assetid: ed1291f6-604c-4972-ae22-0345c6dea12e
caps.latest.revision: 56
author: gewarren
ms.author: gewarren
manager: ghogen
robots: noindex,nofollow
ms.openlocfilehash: d3ffe88fb54da26468ca510a2f1a7ab6170d88db
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49881710"
---
# <a name="how-to-install-sample-databases"></a>Como instalar bancos de dados de exemplo
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Muitos exemplos de dados exigem a capacidade de conectar-se ao Northwind, Pubs, bancos de dados de exemplo andAdventureWorks. Você pode instalar e conectar-se a esses bancos de dados usando os procedimentos a seguir.  
  
 [!INCLUDE[note_settings_general](../includes/note-settings-general-md.md)]  
  
## <a name="installing-databases"></a>Instalando os bancos de dados  
 Muitos exemplos de dados exigem a disponibilidade dos bancos de dados de exemplo que podem ser baixados de sites da web. Os bancos de dados de exemplo incluem os bancos de dados AdventureWorks, Northwind e Pubs.  
  
#### <a name="to-install-the-northwind-and-pubs-sample-databases-for-sql-server"></a>Para instalar os bancos de dados de exemplo Northwind e Pubs para o SQL Server  
  
1.  Vá para o [Northwind e Pubs Sample Databases](http://go.microsoft.com/fwlink?linkid=64296) site da web.  
  
2.  Baixe e execute o instalador.  
  
     O instalador adiciona uma pasta **SQL Server 2000 Sample Databases** para a pasta raiz no seu computador. (Por exemplo: **C:\SQL Server 2000 Sample Databases**).  
  
3.  Localize o script SQL para o banco de dados desejado, Northwind ou Pubs.  
  
    > [!WARNING]
    >  O arquivo de banco de dados .MDF não pode ser facilmente convertido em um formato que pode ser usado nas versões atuais do SQL Server, portanto, é melhor usar o script para criar o banco de dados.  
  
4.  Na **Gerenciador de servidores**, criar uma conexão a uma instância do SQL Server em que você deseja instalar o banco de dados. Se você não tiver um SQL Server específico que você deseja usar, poderá usar o banco de dados instalado automaticamente com o Visual Studio. Para fazer isso, especifique `(localdb)\v11.0` como o nome do servidor.  
  
     Para criar a conexão, siga estas etapas.  
  
    ###### <a name="to-create-a-connection-to-an-instance-of-sql-server"></a>Para criar uma conexão com uma instância do SQL Server  
  
    1.  Na **Gerenciador de servidores**, abra o menu de atalho para o **conexões de dados** nó e escolha **Adicionar Conexão**.  
  
         O **Adicionar Conexão** caixa de diálogo é exibida.  
  
    2.  Insira o nome do SQL Server onde você deseja criar o banco de dados Northwind ou Pubs ou digite (localdb)\v11.0.  
  
    3.  Sob **selecione ou insira um nome de banco de dados**, escolha qualquer banco de dados na lista, por exemplo, tempdb.  
  
    4.  Escolha o **Conexão de teste** botão para verificar se tudo está funcionando e, em seguida, escolha o **Okey** botão.  
  
         Um novo nó de conexão aparece na **Gerenciador de servidores**.  
  
5.  No menu de atalho para o nó de conexão para seu servidor e, em seguida, escolha o **nova consulta** botão.  
  
     Uma janela do editor é aberta e mostra um arquivo de script .sql vazio.  
  
6.  Cole o conteúdo de instnwnd.sql ou instpubs.sql na janela do editor.  
  
7.  Escolha o botão executar consulta (o ícone do triângulo verde aberto na parte superior direita da janela da consulta).  
  
     Se a consulta for bem-sucedida, a mensagem **comando (s) foi concluída com êxito** é exibida. Isso significa que o banco de dados Northwind ou pubs foi criado.  
  
     Ainda será necessário adicionar uma conexão com o banco de dados de exemplo. Na **Gerenciador de servidores**, abra o menu de atalho para o **conexões de dados** nó e escolha **Adicionar Conexão**.  
  
8.  Escolha o mesmo que você escolheu antes, mas desta vez, em Selecionar servidor de banco de dados ou digite um nome de banco de dados, escolha o banco de dados Northwind ou pubs e escolha o **Okey** botão.  
  
     Um novo nó aparece em Conexões de dados para o banco de dados de exemplo.  
  
9. Feche a janela do editor e confirme que você não deseja salvar o arquivo de consulta. Não é necessário salvar o script de criação de banco de dados depois de criar o banco de dados.  
  
#### <a name="to-install-the-adventureworks-sample-databases"></a>Para instalar os bancos de dados de exemplo AdventureWorks  
  
-   Baixe os bancos de dados de exemplo AdventureWorks do [site da CodePlex](http://go.microsoft.com/fwlink/?linkid=87843).  
  
#### <a name="to-install-the-northwind-sample-database-for-microsoft-access"></a>Para instalar o banco de dados de exemplo Northwind do Microsoft Access  
  
1. No Microsoft Access 2010 ou posterior, pesquisar modelos online para a Northwind e escolha **banco de dados de exemplo Northwind 2007 da área de trabalho**.  
  
2. No Microsoft Access, salve o arquivo de banco de dados como Northwind.accdb.  
  
   A nova extensão para bancos de dados do Access .accdb. Ver [programação de dados com o Microsoft Access 2010](http://msdn.microsoft.com/library/office/ff965871.aspx). Para se conectar ao banco de dados Northwind usando o acesso, consulte [como: conectar-se ao banco de dados Northwind](../data-tools/how-to-connect-to-the-northwind-database.md).  
  
## <a name="net-framework-security"></a>Segurança do .NET Framework  
 Os bancos de dados de amostra são apenas para ilustrar e não necessariamente demonstram as práticas recomendadas de segurança.  
  
## <a name="see-also"></a>Consulte também  
 [Como determinar a versão e edição do SQL Server e seus componentes](http://support.microsoft.com/kb/321185)   
 [Criar um banco de dados SQL usando um designer](../data-tools/create-a-sql-database-by-using-a-designer.md)   
 [Como se conectar ao banco de dados Northwind](../data-tools/how-to-connect-to-the-northwind-database.md)