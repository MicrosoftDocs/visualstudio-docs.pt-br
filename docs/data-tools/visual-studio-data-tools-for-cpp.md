---
title: Ferramentas de dados para C++
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- CPP
author: gewarren
ms.author: gewarren
manager: douge
ms.prod: visual-studio-dev15
ms.technology: vs-data-tools
ms.workload:
- data-storage
- cplusplus
ms.openlocfilehash: 4c247d693da287581b8ab163880e9cecf4aeb17c
ms.sourcegitcommit: 81e9d90843ead658bc73b30c869f25921d99e116
ms.translationtype: MTE95
ms.contentlocale: pt-BR
ms.lasthandoff: 11/26/2018
ms.locfileid: "52304906"
---
# <a name="visual-studio-data-tools-for-c"></a>Ferramentas de dados do Visual Studio para C++

C++ nativo geralmente fornecem o melhor desempenho quando você está acessando fontes de dados. No entanto, os dados de ferramentas para aplicativos do C++ no Visual Studio não são tão rico quanto vale para aplicativos .NET. Por exemplo, o **fontes de dados** janela não pode ser usada para arrastar e soltar fontes de dados em uma superfície de design de C++. Se você precisar de uma camada relacional de objeto, você precisará escrever sua própria ou usar um produto de terceiros. O mesmo é verdadeiro para a funcionalidade de associação de dados, embora os aplicativos que usam a biblioteca Microsoft Foundation Class podem usar algumas classes de banco de dados, junto com os documentos e exibições, para armazenar dados na memória e exibi-lo ao usuário. Para obter mais informações, consulte [acesso a dados no Visual C++](/cpp/data/data-access-in-cpp).

Para se conectar aos bancos de dados SQL, os aplicativos nativos do C++ podem usar os drivers ODBC e OLE DB e o provedor ADO que estão incluídos com o Windows. Eles podem se conectar a qualquer banco de dados que dá suporte a essas interfaces. O driver ODBC é o padrão. OLE DB é fornecido para compatibilidade com versões anteriores. Para obter mais informações sobre essas tecnologias de dados, consulte [Windows Data Access Components](/previous-versions/windows/desktop/ms692897(v=vs.85)).

Para tirar proveito da funcionalidade personalizada no SQL Server 2005 e posterior, use o [SQL Server native client](/sql/relational-databases/native-client/sql-server-native-client). O native client também contém o driver ODBC do SQL Server e o provedor OLE DB do SQL Server em uma biblioteca de vínculo dinâmico (DLL). Suporte a aplicativos que usam APIs de código nativo (ODBC, OLE DB e ADO) para o Microsoft SQL Server. SQL Server Native Client é instalado com o SQL Server Data Tools. O guia de programação está aqui: [SQL Server native client de programação](/sql/relational-databases/native-client/sql-server-native-client-programming).

## <a name="to-connect-to-localdb-through-odbc-and-sql-native-client-from-a-c-application"></a>Para conectar-se ao localDB por meio de ODBC e SQL Native Client de um aplicativo C++

1. Instalar o SQL Server Data Tools

2. Se você precisar de um banco de dados SQL de exemplo para se conectar ao, baixe o banco de dados Northwind e descompacte-o em um novo local.

3. Usar o SQL Server Management Studio para anexar o descompactado *mdf* arquivo para o localDB. Quando o SQL Server Management Studio é iniciado, conecte-se ao (localdb) \MSSQLLocalDB.

   ![Caixa de diálogo de conexão do SSMS](../data-tools/media/raddata-ssms-connect-dialog.png)

   Em seguida, clique com botão direito no nó de localdb no painel esquerdo e escolha **Attach**.

   ![SSMS anexar o banco de dados](../data-tools/media/raddata-ssms-attach-database.png)

4. Baixe o exemplo de SDK do Windows ODBC e descompacte-o em um novo local. Este exemplo mostra os comandos básicos do ODBC que são usados para se conectar a um banco de dados e emitir consultas e comandos. Você pode aprender mais sobre essas funções na [conectividade de banco de dados aberto (ODBC) Microsoft](/sql/odbc/microsoft-open-database-connectivity-odbc). Quando você primeiro carrega a solução (está na pasta C++), o Visual Studio oferecerá para atualizar a solução para a versão atual do Visual Studio. Clique em **Sim**.

5. Para usar o cliente nativo, você precisa de sua *cabeçalho* arquivo e *lib* arquivo. Esses arquivos contêm funções e definições específicas para o SQL Server, além de funções ODBC definidas no SQL. Na **Project** > **as propriedades** > **diretórios VC + +**, adicione o seguinte diretório de inclusão:

   **%ProgramFiles%\Microsoft SQL Server\110\SDK\Include**

   E esse diretório de biblioteca:

   **%ProgramFiles%\Microsoft SQL Server\110\SDK\Lib**

6. Adicione estas linhas em *odbcsql.cpp*. O #define impede irrelevantes definições de OLE DB de que está sendo compilado.

   ```cpp
   #define _SQLNCLI_ODBC_
   #include <sqlncli.h>
   ```

    Observe que o exemplo não, na verdade, usar a funcionalidade de cliente nativo, portanto, as etapas anteriores não são necessárias compilar e executar. Mas o projeto agora está configurado para usar essa funcionalidade. Para obter mais informações, consulte [Programação do SQL Server Native Client](/sql/relational-databases/native-client/sql-server-native-client)

7. Especifique qual driver a ser usado no subsistema do ODBC. O exemplo passa o atributo de cadeia de caracteres de conexão do DRIVER no como um argumento de linha de comando. Na **Project** > **as propriedades** > **depuração**, adicione este argumento de comando:

   ```cpp
   DRIVER="SQL Server Native Client 11.0"
   ```

8. Pressione **F5** para compilar e executar o aplicativo. Você deve ver uma caixa de diálogo do driver que solicita que você insira um banco de dados. Insira `(localdb)\MSSQLLocalDB`e marque **Conexão confiável do uso**. Clique em OK **. Você deve ver um console com as mensagens que indicam uma conexão bem-sucedida. Você também verá um prompt de comando onde você pode digitar em uma instrução SQL. A tela a seguir mostra um exemplo de consulta e os resultados:

   ![Saída de consulta de exemplo do ODBC](../data-tools/media/raddata-odbc-sample-query-output.png)

## <a name="see-also"></a>Consulte também

- [Acessando dados no Visual Studio](../data-tools/accessing-data-in-visual-studio.md)