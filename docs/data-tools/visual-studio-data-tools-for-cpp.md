---
title: Ferramentas de dados para C++
ms.date: 11/04/2016
ms.topic: overview
dev_langs:
- CPP
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- data-storage
- cplusplus
ms.openlocfilehash: 063efeebff92698b8e5db66880360713c73fe150
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/23/2020
ms.locfileid: "85281091"
---
# <a name="visual-studio-data-tools-for-c"></a>Ferramentas de dados do Visual Studio para C++

O C++ nativo geralmente pode fornecer o desempenho mais rápido quando você está acessando fontes de dados. No entanto, as ferramentas de dados para aplicativos C++ no Visual Studio não são tão ricas quanto para aplicativos .NET. Por exemplo, a janela **fontes de dados** não pode ser usada para arrastar e soltar fontes de dados em uma superfície de design do C++. Se você precisar de uma camada relacional de objeto, precisará escrever sua própria conta ou usar um produto de terceiros. O mesmo é verdadeiro para a funcionalidade de vinculação de dados, embora os aplicativos que usam a biblioteca Microsoft Foundation Class possam usar algumas classes de banco de dado, junto com documentos e exibições, para armazenar dados na memória e exibi-los para o usuário. Para obter mais informações, consulte [acesso a dados em Visual C++](/cpp/data/data-access-in-cpp).

Para se conectar a bancos de dados SQL, os aplicativos C++ nativos podem usar os drivers ODBC e OLE DB e o provedor ADO que estão incluídos no Windows. Eles podem se conectar a qualquer banco de dados que dê suporte a essas interfaces. O driver ODBC é o padrão. OLE DB é fornecida para compatibilidade com versões anteriores. Para obter mais informações sobre essas tecnologias de dados, consulte [componentes de acesso a dados do Windows](/previous-versions/windows/desktop/ms692897(v=vs.85)).

Para aproveitar a funcionalidade personalizada no SQL Server 2005 e posterior, use o [cliente SQL Server Native](/sql/relational-databases/native-client/sql-server-native-client). O Native Client também contém o SQL Server driver ODBC e o provedor de OLE DB de SQL Server em uma DLL (biblioteca de vínculo dinâmico) nativa. Esses aplicativos dão suporte ao uso de APIs de código nativo (ODBC, OLE DB e ADO) para Microsoft SQL Server. O SQL Server Native Client é instalado com SQL Server Data Tools. O guia de programação está aqui: [SQL Server programação de cliente nativo](/sql/relational-databases/native-client/sql-server-native-client-programming).

## <a name="to-connect-to-localdb-through-odbc-and-sql-native-client-from-a-c-application"></a>Para se conectar ao localDB por meio de ODBC e SQL Native Client de um aplicativo C++

1. Instale o SQL Server Data Tools.

2. Se você precisar de um banco de dados SQL de exemplo para se conectar, baixe o banco de dados Northwind e descompacte-o em um novo local.

3. Use SQL Server Management Studio para anexar o arquivo *Northwind. MDF* descompactado ao localDB. Quando SQL Server Management Studio for iniciado, conecte-se a (LocalDB) \MSSQLLocalDB.

   ![Caixa de diálogo do SSMS Connect](../data-tools/media/raddata-ssms-connect-dialog.png)

   Em seguida, clique com o botão direito do mouse no nó LocalDB no painel esquerdo e escolha **anexar**.

   ![Banco de dados do SSMS Attach](../data-tools/media/raddata-ssms-attach-database.png)

4. Baixe o exemplo de SDK do Windows ODBC e descompacte-o em um novo local. Este exemplo mostra os comandos ODBC básicos que são usados para se conectar a um banco de dados e emitir consultas e comandos. Você pode saber mais sobre essas funções no [ODBC (Microsoft Open Database Connectivity)](/sql/odbc/microsoft-open-database-connectivity-odbc). Quando você carrega a solução pela primeira vez (ela está na pasta C++), o Visual Studio oferecerá para atualizar a solução para a versão atual do Visual Studio. Clique em **Sim**.

5. Para usar o cliente nativo, você precisa do arquivo de *cabeçalho* e do arquivo *lib* . Esses arquivos contêm funções e definições específicas para SQL Server, além das funções ODBC definidas em SQL. h. Em Propriedades do **projeto**  >  **Properties**  >  ,**diretórios vc + +**, adicione o seguinte diretório de inclusão:

   **%ProgramFiles%\Microsoft SQL Server\110\SDK\Include**

   E este diretório de biblioteca:

   **%ProgramFiles%\Microsoft SQL Server\110\SDK\Lib**

6. Adicione essas linhas em *odbcsql. cpp*. A #define impede que as definições de OLE DB irrelevantes sejam compiladas.

   ```cpp
   #define _SQLNCLI_ODBC_
   #include <sqlncli.h>
   ```

    Observe que o exemplo não usa realmente nenhuma funcionalidade de cliente nativo, portanto, as etapas anteriores não são necessárias para compilar e executar. Mas o projeto agora está configurado para você usar essa funcionalidade. Para obter mais informações, consulte [SQL Server Native Client Programming](/sql/relational-databases/native-client/sql-server-native-client).

7. Especifique qual driver usar no subsistema ODBC. O exemplo passa o atributo de cadeia de conexão do DRIVER no como um argumento de linha de comando. Em depuração de propriedades do **projeto**  >  **Properties**  >  **Debugging**, adicione este argumento de comando:

   ```cpp
   DRIVER="SQL Server Native Client 11.0"
   ```

8. Pressione **F5** para compilar e executar o aplicativo. Você deve ver uma caixa de diálogo do driver que solicita que você insira um banco de dados. Insira `(localdb)\MSSQLLocalDB` e marque **usar conexão confiável**. Pressione **OK**. Você deve ver um console com mensagens que indicam uma conexão bem-sucedida. Você também deve ver um prompt de comando onde é possível digitar uma instrução SQL. A tela a seguir mostra um exemplo de consulta e os resultados:

   ![Saída de consulta de exemplo ODBC](../data-tools/media/raddata-odbc-sample-query-output.png)

## <a name="see-also"></a>Veja também

- [Acessando dados no Visual Studio](../data-tools/accessing-data-in-visual-studio.md)
