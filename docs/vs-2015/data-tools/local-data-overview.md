---
title: Visão geral de dados local | Microsoft Docs
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
- SQL Server Express
- local data
- SQL Server LocalDB
- LocalDB
- SQLEXPRESS
- SQL Server, local data
- SQL Express
- SQL Server Compact
- data access [Visual Studio], troubleshooting
- Access, .mdb files in Visual Studio
- data [Visual Studio], local
ms.assetid: d6afa5ac-2bb8-49f2-a50e-f71f611ed506
caps.latest.revision: 71
author: gewarren
ms.author: gewarren
manager: ghogen
robots: noindex,nofollow
ms.openlocfilehash: 94b3f066a66a380875609b4f6485d56a19ebde3e
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49885571"
---
# <a name="local-data-overview"></a>Visão geral de dados local
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Ao desenvolver aplicativos de dados, é melhor usar uma cópia local de um banco de dados, para que você não introduzir erros em dados de produção. Até mesmo compartilhar um banco de dados de teste com outros desenvolvedores cria problemas em potencial se dois desenvolvedores introduzem erros que interagem de maneiras difíceis de detectar. Você pode evitar todas essas armadilhas usando seus próprios dados de teste no computador local. A maioria se nem todos os sistemas de banco de dados permite criar arquivos de dados locais. Para projetos do .NET, o Visual Studio fornece suporte especial para os arquivos de banco de dados locais do SQL Server (. mdf) e arquivos de banco de dados do Microsoft Access (. mdb).  
  
 Visual Studio dá suporte a estes cenários:  
  
1.  
  
2.  
  
- 
  
- 
  
- Criar um projeto de banco de dados do SQL Server clicando no nó da solução no Gerenciador de soluções e escolhendo **adicionar &#124; novo projeto**.  No painel esquerdo, escolha **SQL Server &#124; banco de dados** do projeto e clique em Okey. No Gerenciador de soluções, clique com botão direito no nó do projeto de banco de dados para importar um arquivo de banco de dados local e, em seguida, desenvolver o aplicativo que se conecta ao banco de dados produzido pelo projeto. BOM quando você estiver desenvolvendo e modificar o esquema de banco de dados ao mesmo tempo que você está desenvolvendo o aplicativo.  
  
   ![Importar banco de dados para o projeto de banco de dados](../data-tools/media/raddata-import-database-into-database-project.png "raddata importar banco de dados no projeto de banco de dados")  
  
- Se você estiver criando um novo banco de dados, primeiro adicione uma **arquivo de banco de dados baseado em serviço** ao seu projeto (**projeto &#124; Adicionar Novo Item)**. Isso cria um novo arquivo. mdf que está anexado à instância padrão do SQL Server no computador local, que é \MSSQLocalDB (localdb) por padrão. O banco de dados deve aparecer no Gerenciador de servidores. Expanda o nó e o botão direito do mouse em nós para adicionar novos objetos de banco de dados como tabelas, exibições, funções e assim por diante.  
  
  Para obter mais informações sobre o SQL Server Express LocalDB, consulte [Introdução ao LocalDB, um SQL Express aprimorado](http://go.microsoft.com/fwlink/?LinkId=234375) e [LocalDB: onde está meu banco de dados?](http://go.microsoft.com/fwlink/?LinkId=234376) no site da Microsoft.  
  
  A tabela a seguir fornece links para tópicos que descrevem como conectar seu aplicativo a dados locais:  
  
|Tópico|Descrição|  
|-----------|-----------------|  
|[Criar um banco de dados SQL usando um designer](../data-tools/create-a-sql-database-by-using-a-designer.md)|Fornece instruções passo a passo para a criação de um arquivo de banco de dados local que você pode usar para testar recursos de dados e criar aplicativos.|  
|[Passo a passo: conectando a dados em um arquivo de banco de dados local (Windows Forms)](../data-tools/walkthrough-connecting-to-data-in-a-local-database-file-windows-forms.md)|Fornece instruções passo a passo para se conectar a um banco de dados do SQL Server Express LocalDB durante a criação de um aplicativo simples do Windows.|  
|[Conectar-se a dados em um banco de dados do Access (Windows Forms)](../data-tools/connect-to-data-in-an-access-database-windows-forms.md)|Fornece instruções passo a passo para se conectar a um banco de dados do Microsoft Access.|  
|[Como se conectar ao banco de dados Northwind](../data-tools/how-to-connect-to-the-northwind-database.md)|Fornece instruções para conectar ao banco de dados de exemplo Northwind no [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], o SQL Server Compact, SQL Server Express e Access.|  
  
## <a name="use-the-connection-string"></a>Use a cadeia de conexão  
 Isso é a abordagem mais simples e é uma boa opção quando o aplicativo lê apenas do banco de dados e ao usar bancos de dados de terceiros. O arquivo de banco de dados pode ser localizado em qualquer lugar no computador local que o aplicativo tem permissão para acessar e que o sistema de banco de dados oferece suporte.  
  
1.  (Opcional) Crie uma nova conexão, conforme descrito em [adicionar novas conexões](../data-tools/add-new-connections.md). Para bancos de dados de terceiros e os arquivos. mdf para o qual você já sabe a cadeia de caracteres de conexão e não será fazendo a ligação de dados ou usar uma fonte de dados, como classes de estrutura de entidades ou conjuntos de dados, esta etapa não é necessária. Basta use a cadeia de caracteres de conexão para conectar-se para o arquivo local. Para arquivos. mdf, consulte [atualizar arquivos. mdf](../data-tools/upgrade-dot-mdf-files.md) e [estabelecendo a Conexão](https://msdn.microsoft.com/en-us/library/ms254507.aspx).  
  
2.  (Opcional) Se você estiver usando conjuntos de dados, o Entity Framework ou LINQ to SQL, em seguida, crie a fonte de dados usando o Assistente de configuração de fonte de dados. Para obter mais informações, consulte [Adicionar novas fontes de dados](../data-tools/add-new-data-sources.md).  
  
## <a name="add-an-existing-mdf-to-your-project"></a>Adicionar. mdf existente ao seu projeto  
 Se seu aplicativo será inserindo, excluindo ou atualizando dados e você deseja manter uma cópia do arquivo original disponível, considere adicionar o arquivo ao seu projeto. Quando você fizer isso, você pode definir a propriedade de item-la para **Copy to Output Directory** à **copiar sempre** ou **copiar se mais recente**e desenvolver o aplicativo. Sempre que você compilar o aplicativo, o banco de dados original é copiado para a pasta de saída e alterações do seu aplicativo são executadas na cópia. Dessa forma, você sempre tem uma cópia limpa dos dados originais.  
  
1.  Use **Explorador de arquivos do Windows** para arrastar e soltar o arquivo. mdf do seu local atual para o nó do projeto no Gerenciador de soluções no Visual Studio.  Se o arquivo já está anexado a uma instância de localDB, você deve desanexá-lo pela primeira vez. Depois que você pode removê-lo para o projeto, o Visual Studio será reanexá-lo automaticamente na instância de localDB padrão.  
  
2.  Clique com botão direito no nó do banco de dados novo e escolha Propriedades. Selecione o comportamento de cópia, ou **Copy Always** ou **copiar se mais recente**.  
  
## <a name="create-a-sql-server-database-project-and-import-your-database"></a>Criar um projeto de banco de dados do SQL Server e importar seu banco de dados  
 Isso é uma boa opção quando você desenvolverá o banco de dados em si, talvez adicionando colunas ou tabelas, ou alterar os tipos de dados.  
  
## <a name="each-project-contains-two-copies-of-the-database"></a>Cada projeto contém duas cópias do banco de dados  
 Quando você compila um projeto, o arquivo de banco de dados pode ser copiado da pasta raiz do projeto para a saída **bin**, pasta. Esse comportamento depende de **Copy to Output Directory** propriedade do arquivo e o valor padrão dessa propriedade dependem do tipo de arquivo de banco de dados que você está usando.  
  
 Para exibir o **bin** pasta **Gerenciador de soluções**, escolha o **Mostrar todos os arquivos** na barra de ferramentas.  
  
> [!NOTE]
>  O **Copy to Output Directory** propriedade não se aplica a web ou projetos C++.  
  
 O arquivo de banco de dados na pasta raiz do projeto é alterado ao editar o esquema de banco de dados ou dados usando **Gerenciador de servidores**/**Database Explorer** ou outros [Visual Ferramentas de banco de dados](http://msdn.microsoft.com/en-us/6b145922-2f00-47db-befc-bf351b4809a1).  
  
 Como alterar dados durante o desenvolvimento de aplicativo, você está alterando o banco de dados do **bin** pasta. Por exemplo, quando você escolhe a tecla F5 para depurar seu aplicativo, você está conectado ao banco de dados nessa pasta.  
  
|Valor de **Copy to Output Directory** propriedade|Comportamento|  
|----------------------------------------------------|--------------|  
|**Copiar se mais recente** (valor padrão para arquivos. sdf)|O arquivo de banco de dados é copiado do diretório do projeto para o **bin** na primeira vez que você compila o projeto. O **data de modificação** propriedade dos arquivos, em seguida, é comparada sempre que você compilar o projeto novamente. Se o arquivo na pasta do projeto for mais recente, ele é copiado para o **bin** pasta, substituindo o arquivo anterior. Caso contrário, nenhum arquivo será copiado. **Cuidado:** não recomendamos esse valor para arquivos. mdb ou. mdf. O arquivo de banco de dados pode alterar, mesmo se os dados não mudam. O arquivo pode ser marcado como mais recente, se você simplesmente abrir uma conexão (por exemplo, expanda o **tabelas** nó no **Gerenciador de servidores**).|  
|**Copiar sempre** (valor padrão para arquivos. mdf e. mdb)|O arquivo de banco de dados é copiado do diretório do projeto para o **bin** sempre que você criar seu aplicativo. Todas as alterações feitas ao arquivo de dados na pasta de saída são substituídas na próxima vez que você executar o aplicativo.|  
|**Não copiar**|O sistema nunca sobrescreve o arquivo na **bin** directory. Seu aplicativo cria uma cadeia de caracteres de conexão dinâmica que aponta para o arquivo de banco de dados no diretório de saída. Portanto, você deve copiar manualmente o arquivo para o diretório de saída se você deseja que os dados no diretório de saída para corresponder os dados no diretório do projeto.|  
  
## <a name="common-issues-with-local-data"></a>Problemas comuns com dados locais  
 A tabela a seguir explica os problemas comuns que você pode encontrar ao trabalhar com arquivos de dados locais.  
  
|Problema|Explicação|  
|-----------|-----------------|  
|Sempre que eu testar meu aplicativo e modificar dados, minhas alterações são perdidas na próxima vez que eu executar o aplicativo.|O valor de **Copy to Output Directory** é de propriedade **copiar se mais recente** ou **copiar sempre**. O banco de dados na sua pasta de saída (o banco de dados que está sendo modificado ao testar seu aplicativo) é substituído sempre que você compila seu projeto. Para obter mais informações, consulte [como: gerenciar arquivos de dados locais em seu projeto](../data-tools/how-to-manage-local-data-files-in-your-project.md).|  
|Será exibida uma mensagem dizendo que o arquivo de dados está bloqueado.|Acesso (arquivos. mdb): verificar que o arquivo não está aberto em outro programa, como o acesso.<br /><br /> SQL Server Express (arquivos. mdf): SQL Express bloqueia o arquivo de dados se você tentar copiar, mover ou renomeá-lo fora do IDE do Visual Studio.|  
|Acesso negado quando mais de um usuário tenta acessar o mesmo banco de dados ao mesmo tempo.|Visual Studio aproveita *instâncias de usuário*, que é um recurso do SQL Server Express que cria uma instância separada do SQL Server para cada usuário. Depois que um usuário acessa o arquivo, quaisquer usuários subsequentes não podem se conectar. Esse problema pode ocorrer se, por exemplo, você tentar executar um aplicativo web no ASP.NET Development Server e serviços de informações da Internet (IIS), ao mesmo tempo, porque o IIS geralmente executa em uma conta diferente.|  
  
## <a name="see-also"></a>Consulte também  
 [Passo a passo: Conectando a dados em um arquivo de banco de dados Local (Windows Forms)](../data-tools/walkthrough-connecting-to-data-in-a-local-database-file-windows-forms.md)   
 [Conectar-se a dados em um banco de dados do Access (Windows Forms)](../data-tools/connect-to-data-in-an-access-database-windows-forms.md)