---
title: Acesso a dados e ferramentas
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- "80025080"
helpviewer_keywords:
- data [Visual Studio]
- data access [Visual Studio]
- data [C#]
- ADO.NET, data access
author: gewarren
ms.author: gewarren
manager: douge
ms.prod: visual-studio-dev15
ms.technology: vs-data-tools
ms.workload:
- data-storage
ms.openlocfilehash: e31eeaf3061968cfa916d2ec5a0d0e522b9f6ebb
ms.sourcegitcommit: 0cdd8e8a53fb4fd5e869f07c35204419fa12783d
ms.translationtype: MTE95
ms.contentlocale: pt-BR
ms.lasthandoff: 12/10/2018
ms.locfileid: "53159523"
---
# <a name="access-data-in-visual-studio"></a>Acessar dados no Visual Studio

No Visual Studio, você pode criar aplicativos que se conectam aos dados em praticamente qualquer produto de banco de dados ou serviço, em qualquer formato, em qualquer lugar — em um computador local, em uma rede local ou em uma nuvem pública, privada ou híbrida.

Para aplicativos em JavaScript, Python, PHP, Ruby ou C++, você se conectar a dados como faria qualquer outra coisa, obtendo bibliotecas e escrever código. Para aplicativos .NET, Visual Studio fornece ferramentas que você pode usar para explorar fontes de dados, criar modelos de objeto para armazenar e manipular os dados na memória e associar dados à interface do usuário. Microsoft Azure fornece SDKs para .NET, Java, Node. js, PHP, Python, Ruby e aplicativos móveis e ferramentas no Visual Studio para se conectar ao armazenamento do Azure.

As listas a seguir mostram apenas alguns os muitos sistemas de banco de dados e armazenamento que podem ser usados no Visual Studio. O [Microsoft Azure](https://azure.microsoft.com/) ofertas são serviços de dados que incluem todos os provisionamento e administração de armazenamento de dados subjacente. O **desenvolvimento do Azure** carga de trabalho no [Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017) permite que você trabalhe com repositórios de dados do Azure diretamente do Visual Studio.

![Carga de trabalho de desenvolvimento do Azure](media/azure-development-workload.png)

A maioria dos outros SQL e NoSQL banco de dados produtos listados aqui pode ser hospedada em um computador local, em uma rede local ou no Microsoft Azure em uma máquina virtual. Se você hospedar o banco de dados em uma máquina virtual do Microsoft Azure, você é responsável por gerenciar o próprio banco de dados.

**Microsoft Azure**

- Banco de Dados SQL
- Azure Cosmos DB
- Armazenamento (blobs, tabelas, filas, arquivos)
- SQL Data Warehouse
- SQL Server Stretch Database
- StorSimple
- E muito mais...

**SQL**

- SQL Server 2005-2016 (inclui o Express e LocalDB)
- Firebird
- MariaDB
- MySQL
- Oracle
- PostgreSQL
- SQLite
- E muito mais...

**NoSQL**

- Apache Cassandra
- CouchDB
- MongoDB
- NDatabase
- OrientDB |
- RavenDB
- VelocityDB
- E muito mais...

Muitos fornecedores de banco de dados e terceiros dão suporte à integração do Visual Studio pacotes do NuGet. Você pode explorar as ofertas em nuget.org ou por meio do Gerenciador de pacotes NuGet no Visual Studio (**ferramentas** > **Gerenciador de pacotes NuGet** > **gerenciar NuGet Pacotes para a solução**). Outros produtos de banco de dados integram ao Visual Studio como uma extensão. Você pode procurar essas ofertas do Visual Studio Marketplace, navegando até **ferramentas**, **extensões e atualizações** e, em seguida, selecionando **Online** no painel esquerdo das caixa de diálogo. Para obter mais informações, consulte [sistemas de banco de dados compatível para o Visual Studio](../data-tools/installing-database-systems-tools-and-samples.md).

> [!NOTE]
> O suporte estendido para o SQL Server 2005 terminou em 12 de abril de 2016. Não há nenhuma garantia de que as ferramentas de dados no Visual Studio 2015 e versões posteriores continuarão funcionando com o SQL Server 2005 após essa data. Para obter mais informações, consulte o [comunicado de fim do suporte para o SQL Server 2005](https://www.microsoft.com/sql-server/sql-server-2005).

## <a name="net-languages"></a>Linguagens .NET

Todos os acesso de dados do .NET, incluindo no .NET Core baseia-se no ADO.NET, um conjunto de classes que define uma interface para acessar qualquer tipo de fonte de dados, relacional e não relacionais. O Visual Studio tem várias ferramentas e designers que trabalham com o ADO.NET para ajudá-lo a se conectar a bancos de dados, manipular os dados e apresentá-los para o usuário. A documentação nesta seção descreve como usar essas ferramentas. Você também pode programar diretamente em relação os objetos de comando do ADO.NET. Para obter mais informações sobre como chamar as APIs do ADO.NET diretamente, consulte [ADO.NET](/dotnet/framework/data/adonet/index).

Para obter a documentação de acesso a dados relacionada ao ASP.NET, consulte [trabalhando com dados](https://www.asp.net/web-forms/overview/presenting-and-managing-data) no site do ASP.NET. Para obter um tutorial sobre como usar o Entity Framework com o ASP.NET MVC, consulte [Introdução ao Entity Framework 6 Code First usando MVC 5](/aspnet/mvc/overview/getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application).

Aplicativos universais do Windows Platform (UWP) em c# ou Visual Basic podem usar o SDK do Microsoft Azure para .NET para acessar o armazenamento do Azure e outros serviços do Azure. A classe Windows.Web.HttpClient permite a comunicação com qualquer serviço RESTful. Para obter mais informações, consulte [como se conectar a um servidor HTTP usando o Windows](https://msdn.microsoft.com/library/windows/apps/dn469430.aspx).

Para o armazenamento de dados no computador local, a abordagem recomendada é usar o SQLite, que é executado no mesmo processo que o aplicativo. Se uma camada de mapeamento relacional de objeto (ORM) for necessária, você pode usar o Entity Framework. Para obter mais informações, consulte [acesso a dados](/windows/uwp/data-access/index) no Centro de desenvolvedores do Windows.

Se você estiver se conectando aos serviços do Azure, certifique-se de baixar a versão mais recente [Azure SDK tools](https://azure.microsoft.com/downloads/).

### <a name="data-providers"></a>Provedores de dados

Para um banco de dados ser consumível no ADO.NET, ele deve ter um personalizado *provedor de dados ADO.NET* ou else deve expor uma interface ODBC ou OLE DB. A Microsoft fornece um [lista de provedores de dados ADO.NET](https://docs.microsoft.com/dotnet/framework/data/adonet/ado-net-overview) para produtos do SQL Server, bem como provedores de ODBC e OLE DB.

### <a name="data-modeling"></a>Modelagem de dados

No .NET, você tem três opções de modelagem e manipulação de dados na memória depois que você recuperou de uma fonte de dados:

[Entity Framework](../data-tools/entity-data-model-tools-in-visual-studio.md) a tecnologia Microsoft ORM preferencial. Você pode usá-lo ao programa em relação aos dados relacionais como objetos de primeira classe .NET. Para novos aplicativos, ele deve ser a primeira opção padrão quando um modelo é necessário. Ele requer suporte personalizado do provedor de ADO.NET subjacente.

[O LINQ to SQL](../data-tools/linq-to-sql-tools-in-visual-studio2.md) um mapeador relacional de objetos da geração anterior. Ele funciona bem para cenários menos complexos, mas não está mais em desenvolvimento ativo.

[Conjuntos de dados](../data-tools/dataset-tools-in-visual-studio.md) o mais antigo dos três tecnologias de modelagem. Ele é projetado principalmente para desenvolvimento rápido de aplicativos "formulários sobre dados" na qual você não é enormes quantidades de dados de processamento ou execução de consultas complexas ou transformações. Um objeto de conjunto de dados consiste em objetos DataTable e DataRow logicamente semelhantes a objetos de banco de dados do SQL muito mais do que objetos .NET. Para aplicativos relativamente simples com base em fontes de dados SQL, conjuntos de dados ainda podem ser uma boa opção.

Não há nenhum requisito para usar qualquer uma dessas tecnologias. Em alguns cenários, especialmente quando o desempenho for crítico, você pode simplesmente usar um objeto DataReader para ler do banco de dados e copie os valores que você precisa para um objeto de coleção como lista\<T >.

## <a name="native-c"></a>C++ Nativo

Aplicativos de C++ que se conectam ao SQL Server devem usar o [Microsoft® ODBC Driver 13.1 para SQL Server](https://www.microsoft.com/download/details.aspx?id=53339) na maioria dos casos. Se os servidores vinculados, em seguida, o OLE DB é necessário e para que você use o [SQL Server Native Client](/sql/relational-databases/native-client/sql-server-native-client). Você pode acessar outros bancos de dados usando [ODBC](https://docs.microsoft.com/sql/odbc/microsoft-open-database-connectivity-odbc?view=sql-server-2017) ou drivers de OLE DB diretamente. O ODBC é a interface padrão do banco de dados atual, mas a maioria dos sistemas de banco de dados fornecer funcionalidade personalizada que não pode ser acessada por meio da interface do ODBC. OLE DB é uma tecnologia de acesso a dados COM herdados ainda têm suporte, mas não é recomendada para novos aplicativos. Para obter mais informações, consulte [acesso a dados no Visual C++](/cpp/data/data-access-in-cpp).

Programas do C++ que consumirem serviços REST podem usar o [C++ REST SDK](https://github.com/Microsoft/cpprestsdk).

Programas do C++ que funcionam com o armazenamento do Microsoft Azure podem usar o [cliente de armazenamento do Microsoft Azure](https://www.nuget.org/packages/Microsoft.Azure.Storage.CPP).

Modelagem de dados&mdash;Visual Studio não fornece uma camada ORM para C++. [ODB](https://www.codesynthesis.com/products/odb/) é um ORM do código-fonte aberto popular para C++.

Para saber mais sobre como conectar aos bancos de dados de aplicativos em C++, consulte [ferramentas de dados do Visual Studio para C++](../data-tools/visual-studio-data-tools-for-cpp.md). Para obter mais informações sobre as tecnologias de acesso a dados herdadas do Visual C++, consulte [acesso a dados](/cpp/data/data-access-in-cpp).

## <a name="javascript"></a>JavaScript

[JavaScript no Visual Studio](/scripting/javascript/javascript-language-reference) é uma linguagem de primeira classe para a criação de aplicativos de plataforma cruzada, aplicativos da UWP, serviços de nuvem, sites e aplicativos web. Você pode usar o Bower, Grunt, Gulp, npm e NuGet de dentro do Visual Studio para instalar seus produtos de banco de dados e bibliotecas JavaScript favoritas. Conectar-se ao armazenamento do Azure e serviços baixando SDKs do [site do Azure](https://azure.microsoft.com/). Js é uma biblioteca JavaScript do lado do servidor (Node. js) conecta-se a fontes de dados do ADO.NET.

## <a name="python"></a>Python

Instale [suporte do Python no Visual Studio](../python/overview-of-python-tools-for-visual-studio.md) para criar aplicativos Python. Documentação do Azure tem vários tutoriais sobre como se conectar a dados, incluindo o seguinte:

- [Django e banco de dados SQL no Azure](/azure/app-service/app-service-web-get-started-python)
- [Django e MySQL no Azure](/azure/app-service-web/web-sites-python-ptvs-django-mysql)
- Trabalhar com [blobs](/azure/storage/blobs/storage-quickstart-blobs-python), [arquivos](/azure/storage/files/storage-python-how-to-use-file-storage), [filas](/azure/storage/queues/storage-python-how-to-use-queue-storage), e [tabelas (banco de dados Cosmo)](/azure/cosmos-db/table-storage-how-to-use-python).

## <a name="related-topics"></a>Tópicos relacionados

[Plataforma Microsoft AI](https://azure.microsoft.com/overview/ai-platform/?v=17.42w)&mdash;fornece uma introdução à nuvem inteligente da Microsoft, incluindo o Cortana Analytics Suite e o suporte para a Internet das coisas.

[Armazenamento do Microsoft Azure](/azure/storage/)&mdash;descreve o armazenamento do Azure e como criar aplicativos usando arquivos, tabelas, filas e blobs do Azure.

[Banco de dados SQL do Azure](/azure/sql-database/)&mdash;descreve como se conectar ao banco de dados SQL, banco de dados relacional como um serviço.

[SQL Server Data Tools](/sql/ssdt/download-sql-server-data-tools-ssdt)&mdash;descreve as ferramentas que simplificam o design, exploração, teste e implantação de aplicativos conectados a dados e bancos de dados.

[ADO.NET](/dotnet/framework/data/adonet/index)&mdash;descreve a arquitetura do ADO.NET e como usar as classes ADO.NET para gerenciar dados de aplicativo e interagir com fontes de dados e XML.

[ADO.NET Entity Framework](https://docs.microsoft.com/ef/ef6/)&mdash;descreve como criar aplicativos de dados que permitem aos desenvolvedores de programas em um modelo conceitual em vez de diretamente em um banco de dados relacional.

[Serviços de dados WCF 4.5](/dotnet/framework/data/wcf/index)&mdash;descreve como usar [!INCLUDE[ssAstoria](../data-tools/includes/ssastoria_md.md)] para implantar serviços de dados na web ou em uma intranet que implementam o [Open Data Protocol (OData)](https://www.odata.org/).

[Dados em soluções do Office](../vsto/data-in-office-solutions.md)&mdash;contém links para tópicos que explicam como dados funcionam em soluções do Office. Isso inclui informações sobre programação orientada a esquema, caching de dados e acesso a dados do lado do servidor.

[LINQ (consulta integrada à linguagem)](/dotnet/csharp/linq/)&mdash;descreve os recursos de consulta incorporados no c# e Visual Basic e o modelo comum para consultar bancos de dados relacionais, documentos XML, conjuntos de dados e coleções na memória.

[Ferramentas XML no Visual Studio](../xml-tools/xml-tools-in-visual-studio.md)&mdash;aborda o trabalho com recursos de XML do .NET Framework de dados, depuração XSLT, XML e a arquitetura de consulta XML.

[Documentos e dados XML](/dotnet/standard/data/xml/index)&mdash;fornece uma visão geral para um conjunto abrangente e integrado de classes que funcionam com documentos XML e dados no .NET Framework.
