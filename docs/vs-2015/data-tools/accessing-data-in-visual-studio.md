---
title: Accessing data
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-data-tools
ms.topic: conceptual
f1_keywords:
- "80025080"
dev_langs:
- VB
- CSharp
- C++
- aspx
helpviewer_keywords:
- data [Visual Studio]
- data access [Visual Studio]
- data [C#]
- ADO.NET, data access
ms.assetid: 9812a6d5-23d2-4427-8b98-70a2abfec3bc
caps.latest.revision: 103
author: jillre
ms.author: jillfra
manager: jillfra
robots: noindex,nofollow
ms.openlocfilehash: 78d950b777d866835ef516c4910180b21de295e9
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85544996"
---
# <a name="accessing-data-in-visual-studio"></a>Acessando dados no Visual Studio
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

No Visual Studio, você pode criar aplicativos que se conectam a dados em praticamente qualquer produto ou serviço de banco de dado, em qualquer formato, em qualquer lugar — em um computador local, em uma rede local ou em uma nuvem pública, privada ou híbrida.

 Para aplicativos em JavaScript, Python, PHP, Ruby ou C++, você se conecta a dados como faz qualquer outra coisa, obtendo bibliotecas e escrevendo código. Para aplicativos .NET, o Visual Studio fornece ferramentas que você pode usar para explorar fontes de dados, criar modelos de objeto para armazenar e manipular dados na memória e associar dados à interface do usuário.     O Microsoft Azure fornece SDKs para .NET, Java, Node.js, PHP, Python, Ruby e aplicativos móveis e ferramentas no Visual Studio para se conectar ao armazenamento do Azure.

 As listas a seguir mostram apenas alguns dos vários sistemas de banco de dados e de armazenamento que podem ser usados no Visual Studio. As ofertas de [Microsoft Azure](https://azure.microsoft.com/) são serviços de dados que incluem todo o provisionamento e a administração do armazenamento de dados subjacente.  As [Ferramentas do Azure para Visual Studio](https://www.visualstudio.com/features/azure-tools-vs.aspx) são um componente opcional que permite que você trabalhe com armazenamentos de dados do Azure diretamente do Visual Studio. A maioria dos outros produtos de banco de dados SQL e NoSQL listados aqui pode ser hospedada em um computador local, em uma rede local ou em Microsoft Azure em uma máquina virtual. Nesse cenário, você é responsável pelo gerenciamento do próprio banco de dados.

 **Microsoft Azure**

- Banco de Dados SQL

- DocumentDB

-Armazenamento (BLOBs, tabelas, filas, arquivos)

- SQL Data Warehouse

- SQL Server Stretch Database

- StorSimple

 E muito mais…

 **SQL**

- SQL Server 2005 – 2016, incluindo Express e LocalDB
- Firebird
- MariaDB
- MySQL
- Oracle
- PostgreSQL
- SQLite

 E muito mais…

 **NoSQL**

- Apache Cassandra
- CouchDB
- MongoDB
- NDatabase
- OrientDB
- RavenDB
- VelocityDB

 E muito mais…

 Muitos fornecedores de banco de dados e terceiros dão suporte à integração do Visual Studio por pacotes NuGet. Você pode explorar as ofertas em NuGet.org ou por meio do Gerenciador de pacotes NuGet no Visual Studio (**ferramentas**  >  **Gerenciador de pacotes NuGet**  >  **gerenciar pacotes NuGet para solução**). Outros produtos de banco de dados se integram com o Visual Studio como uma extensão.   Você pode procurar essas ofertas na galeria do Visual Studio navegando até **ferramentas**  >  **extensões e atualizações** e, em seguida, selecionando **online** no painel esquerdo da caixa de diálogo.  Para obter mais informações, consulte [instalando sistemas de banco de dados, ferramentas e exemplos](../data-tools/installing-database-systems-tools-and-samples.md).

> [!NOTE]
> O suporte estendido para o SQL Server 2005 terminou em 12 de abril de 2016.   Não há nenhuma garantia de que as ferramentas de dados no Visual Studio 2015 e posteriores continuarão a funcionar com o SQL Server 2005 após essa data. Para obter mais informações, consulte o [anúncio do fim do suporte para o SQL Server 2005](https://www.microsoft.com/sql-server/sql-server-2005).

### <a name="net-languages"></a>Linguagens .NET
 Todo o acesso a dados do .NET, incluindo o .NET Core, é baseado em ADO.NET, um conjunto de classes que define uma interface para acessar qualquer tipo de fonte de dados, relacional e não relacional. O Visual Studio tem várias ferramentas e designers que funcionam com o ADO.NET para ajudá-lo a se conectar a bancos de dados, manipular e apresentar os dados para o usuário. A documentação nesta seção descreve como usar essas ferramentas. Você também pode programar diretamente em relação aos objetos de comando ADO.NET. Para obter mais informações sobre como chamar as APIs ADO.NET diretamente, consulte [ADO.net](https://msdn.microsoft.com/library/e80y5yhx\(v=vs.110\).aspx) na biblioteca MSDN.

 Para obter a documentação de acesso a dados especificamente relacionada ao ASP.NET, consulte [trabalhando com dados](/aspnet/web-forms/overview/presenting-and-managing-data/) no site do ASP.net. Para obter um tutorial sobre como usar Entity Framework com o ASP.NET MVC, confira [introdução com Entity Framework 6 Code First usando o MVC 5](/aspnet/mvc/overview/getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application).

 Os aplicativos Plataforma Universal do Windows (UWP) em C# ou Visual Basic podem usar o SDK do Microsoft Azure para .NET para acessar o armazenamento do Azure e outros serviços do Azure. A classe Windows. Web. HttpClient permite a comunicação com qualquer serviço RESTful. Para obter mais informações, consulte [como se conectar a um servidor http usando Windows. Web. http](https://msdn.microsoft.com/library/windows/apps/dn469430.aspx).

 Para o armazenamento de dados no computador local, a abordagem recomendada é usar o SQLite, que é executado no mesmo processo que o aplicativo. Se uma camada de ORM (mapeamento relacional de objeto) for necessária, você poderá usar Entity Framework. Para obter mais informações, consulte [acesso a dados](https://msdn.microsoft.com/windows/uwp/data-access/index) no Windows Developer Center.

 Se você estiver se conectando aos serviços do Azure, certifique-se de baixar as ferramentas mais recentes do [SDK do Azure](https://azure.microsoft.com/downloads/).

#### <a name="data-providers"></a>Provedores de dados
 Para que um banco de dados seja consumível em ADO.NET, ele deve ter um provedor personalizado de *ADO.net* ou mais deve expor uma interface ODBC ou OLE DB. A Microsoft fornece uma [lista de provedores de dados ADO.net](https://msdn.microsoft.com/data/dd363565) para produtos SQL Server, bem como provedores de OLE DB e ODBC.

#### <a name="data-modeling"></a>Modelagem de dados
 No .NET, você tem três opções para modelar e manipular dados na memória depois de recuperá-los de uma fonte de dados:

 Entity Framework a tecnologia de ORM da Microsoft preferida. Você pode usá-lo para programar em dados relacionais como objetos do .NET de primeira classe. Para novos aplicativos, deve ser a primeira opção padrão quando um modelo é necessário. Ele requer suporte personalizado do provedor de ADO.NET subjacente.

 LINQ to SQL um mapeador relacional de objeto de geração anterior. Ele funciona bem para cenários menos complexos, mas não está mais no desenvolvimento ativo.

 DataSets é o mais antigo das três tecnologias de modelagem. Ele foi projetado principalmente para o desenvolvimento rápido de aplicativos de "formulários em dados" nos quais você não está processando grandes quantidades de dados ou realizando consultas ou transformações complexas. Um objeto DataSet consiste em objetos DataTable e DataRow que se assemelham logicamente a objetos do banco de dados SQL muito mais do que objetos .NET. Para aplicativos relativamente simples com base em fontes de dados SQL, os DataSets ainda podem ser uma boa opção.

 Não há nenhum requisito para usar nenhuma dessas tecnologias. Em alguns cenários, especialmente onde o desempenho é crítico, você pode simplesmente usar um objeto DataReader para ler do banco de dados e copiar os valores necessários para um objeto de coleção, como List \<T> .

### <a name="native-c"></a>C++ nativo
 Os aplicativos C++ que se conectam ao SQL Server devem usar o [SQL Server Native Client](https://msdn.microsoft.com/sqlserver/aa937733.aspx). Você pode acessar outros bancos de dados usando os drivers [ODBC](https://msdn.microsoft.com/library/ms710252\(v=vs.85\).aspx) ou OLE DB diretamente. O ODBC é a interface de banco de dados padrão atual, mas a maioria dos sistemas de banco de dados fornece uma funcionalidade personalizada que não pode ser acessada pela interface ODBC.  OLE DB é uma tecnologia de acesso a dados COM herdada que ainda é suportada, mas não é recomendada para novos aplicativos.  Para obter mais informações, consulte [acesso a dados](https://msdn.microsoft.com/library/a9455752-39c4-4457-b14e-197772d3df0b).

 Os programas C++ que consomem serviços REST podem usar o [C++ REST SDK](https://github.com/Microsoft/cpprestsdk).

 Programas C++ que funcionam com Armazenamento do Microsoft Azure podem usar o [cliente armazenamento do Microsoft Azure](https://www.nuget.org/packages/wastorage).

#### <a name="data-modeling"></a>Modelagem de dados
 O Visual Studio não fornece uma camada de ORM para C++.  O [ODB](https://www.codesynthesis.com/products/odb/) é um popular ORM de código-fonte aberto para C++.

 Para obter mais informações sobre as tecnologias de acesso a dados herdadas Visual C++, consulte [acesso a dados](https://msdn.microsoft.com/library/a9455752-39c4-4457-b14e-197772d3df0b)

### <a name="javascript"></a>JavaScript
 O [JavaScript no Visual Studio](https://msdn.microsoft.com/library/hh334522.aspx) é uma linguagem de primeira classe para a criação de aplicativos de plataforma cruzada, aplicativos UWP, serviços de nuvem, sites e aplicativos Web. Você pode usar Bower, grunt, Gulp, NPM e NuGet de dentro do Visual Studio para instalar suas bibliotecas JavaScript favoritas e seus produtos de banco de dados. Conecte-se ao armazenamento do Azure e aos serviços baixando SDKs do [site do Azure](https://azure.microsoft.com/).  Edge.js é uma biblioteca que conecta JavaScript do lado do servidor (Node.js) a fontes de dados ADO.NET.

### <a name="python"></a>Python
 Instale [ferramentas Python para Visual Studio](http://microsoft.github.io/PTVS/) junto com sua estrutura de Python favorita para criar aplicativos CPython ou IronPython (.net).  O site Ferramentas Python para Visual Studio tem vários tutoriais sobre como se conectar a dados, incluindo [Django e banco de dados SQL no Azure](https://github.com/Microsoft/PTVS/wiki/Django-and-SQL-Database-on-Azure), [Django e MySQL no Azure](https://github.com/Microsoft/PTVS/wiki/Django-and-MySQL-on-Azure) e [garrafa e MongoDB no Azure](https://github.com/Microsoft/PTVS/wiki/Bottle-and-MongoDB-on-Azure).

## <a name="in-this-section"></a>Nesta seção
 [Instalando sistemas de banco de dados, ferramentas e exemplos](../data-tools/installing-database-systems-tools-and-samples.md) Discute como obter produtos de banco de dados e as extensões ou os drivers do Visual Studio que dão suporte a eles e onde encontrar bancos de dados de exemplo para fins de experimentação e aprendizado.

 [Ferramentas de dados do Visual Studio para .net](https://msdn.microsoft.com/6b145922-2f00-47db-befc-bf351b4809a1) Descreve como usar as janelas de ferramentas do Visual Studio para se conectar a fontes de dados, criar conjuntos ou Entity Framework modelos e associar os dados aos controles da interface do usuário.

## <a name="related-topics"></a>Tópicos relacionados
 [Dados, dispositivos e análises](https://msdn.microsoft.com/data-and-devices) Fornece uma introdução à nuvem inteligente da Microsoft, incluindo o Cortana Analytics Suite e suporte para Internet das Coisas.

 [Armazenamento do Microsoft Azure](/azure/storage/) Descreve o armazenamento do Azure e como criar aplicativos usando BLOBs, tabelas, filas e arquivos do Azure.

 [Banco de dados SQL do Azure](https://azure.microsoft.com/documentation/services/sql-database/) Descreve como se conectar ao banco de dados SQL do Azure, um banco de dados relacional como um serviço.

 [SQL Server Data Tools](https://msdn.microsoft.com/library/hh272686\(v=vs.103\).aspx) Descreve as ferramentas que simplificam o design, a exploração, o teste e a implantação de aplicativos e bancos de dados conectados a data.

 [ADO.net](https://msdn.microsoft.com/library/5b96ed06-9759-4966-a797-a1d5f6ee50ca) Descreve a arquitetura ADO.NET e como usar as classes ADO.NET para gerenciar dados de aplicativos e interagir com fontes de dados e XML.

 [Entity Framework ADO.net](https://msdn.microsoft.com/data/ef) Descreve como criar aplicativos de dados que permitem aos desenvolvedores programar em um modelo conceitual em vez de diretamente em relação a um banco de dados relacional.

 [WCF Data Services 4,5](https://msdn.microsoft.com/library/73d2bec3-7c92-4110-b905-11bb0462357a) Descreve como usar [!INCLUDE[ssAstoria](../includes/ssastoria-md.md)] o para implantar serviços de dados na Web ou em uma intranet que implementam o [protocolo Open Data (OData)](https://www.odata.org/).

 [Dados em soluções do Office](https://msdn.microsoft.com/library/8478c095-864b-4ed3-8a70-1fc19b411c6a) Contém links para tópicos que explicam como os dados funcionam em soluções do Office. Isso inclui informações sobre programação orientada a esquema, cache de dados e acesso a dados no servidor.

 [LINQ (consulta integrada à linguagem)](https://msdn.microsoft.com/library/a73c4aec-5d15-4e98-b962-1274021ea93d) Descreve os recursos de consulta incorporados ao C# e Visual Basic, e o modelo comum para consultar bancos de dados relacionais, documentos XML, DataSets e coleções na memória.

 [Ferramentas XML no Visual Studio](../xml-tools/xml-tools-in-visual-studio.md) Discute o trabalho com dados XML, a depuração de XSLT, .NET Framework recursos XML e a arquitetura da consulta XML.

 [Documentos e dados XML](https://msdn.microsoft.com/library/e695047f-3c0f-4045-8708-5baea91cc380) Fornece uma visão geral de um conjunto abrangente e integrado de classes que funcionam com documentos e dados XML no .NET Framework.
