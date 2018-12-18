---
title: Acessando dados no Visual Studio | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
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
author: gewarren
ms.author: gewarren
manager: ghogen
robots: noindex,nofollow
ms.openlocfilehash: eacf075a0ba8689ff0cb5ca822d5cc8ca2f7ad1e
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49233891"
---
# <a name="accessing-data-in-visual-studio"></a>Acessando dados no Visual Studio
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

  
No Visual Studio, você pode criar aplicativos que se conectam aos dados em praticamente qualquer produto de banco de dados ou serviço, em qualquer formato, em qualquer lugar — em um computador local, em uma rede local ou em uma nuvem pública, privada ou híbrida.  
  
 Para aplicativos em JavaScript, Python, PHP, Ruby ou C++, você se conectar a dados como faria qualquer outra coisa, obtendo bibliotecas e escrever código. Para aplicativos .NET, Visual Studio fornece ferramentas que você pode usar para explorar fontes de dados, criar modelos de objeto para armazenar e manipular os dados na memória e associar dados à interface do usuário.     Microsoft Azure fornece SDKs para .NET, Java, Node. js, PHP, Python, Ruby e aplicativos móveis e ferramentas no Visual Studio para se conectar ao armazenamento do Azure.  
  
 As listas a seguir mostram apenas alguns os muitos sistemas de banco de dados e armazenamento que podem ser usados no Visual Studio. O [Microsoft Azure](https://azure.microsoft.com/en-us/) ofertas são serviços de dados que incluem todos os provisionamento e administração de armazenamento de dados subjacente.  [Ferramentas do Azure para Visual Studio](https://www.visualstudio.com/en-us/features/azure-tools-vs.aspx) é um componente opcional que permite que você trabalhe com repositórios de dados do Azure diretamente do Visual Studio. A maioria dos outros SQL e NoSQL banco de dados produtos listados aqui pode ser hospedada em um computador local, em uma rede local ou no Microsoft Azure em uma máquina virtual. Nesse cenário, você é responsável por gerenciar o próprio banco de dados.  
  
 **Microsoft Azure**  
  
||||  
|-|-|-|  
|Banco de dados SQL|DocumentDB|Armazenamento (blobs, tabelas, filas, arquivos)|  
|SQL Data Warehouse|SQL Server Stretch Database|StorSimple|  
  
 E muito mais...  
  
 **SQL**  
  
||||  
|-|-|-|  
|SQL Server 2005 – 2016, incluindo o Express e LocalDB|Firebird|MariaDB|  
|MySQL|Oracle|PostgreSQL|  
|SQLite|||  
  
 E muito mais...  
  
 **NoSQL**  
  
||||  
|-|-|-|  
|Apache Cassandra|CouchDB|MongoDB|  
|NDatabase|OrientDB|RavenDB|  
|VelocityDB|||  
  
 E muito mais...  
  
 Muitos fornecedores de banco de dados e terceiros dão suporte à integração do Visual Studio pacotes do NuGet. Você pode explorar as ofertas em nuget.org ou por meio do Gerenciador de pacotes NuGet no Visual Studio (**ferramentas** > **Gerenciador de pacotes NuGet** > **gerenciar NuGet Pacotes para a solução**). Outros produtos de banco de dados integram ao Visual Studio como uma extensão.   Você pode procurar essas ofertas na Galeria do Visual Studio, navegando até **ferramentas** > **extensões e atualizações** e, em seguida, selecionando **Online** à esquerda painel da caixa de diálogo.  Para obter mais informações, consulte [instalando sistemas de banco de dados, ferramentas e exemplos](../data-tools/installing-database-systems-tools-and-samples.md).  
  
> [!NOTE]
>  O suporte estendido para o SQL Server 2005 terminou em 12 de abril de 2016.   Não há nenhuma garantia de que as ferramentas de dados no Visual Studio 2015 e versões posteriores continuarão funcionando com o SQL Server 2005 após essa data. Para obter mais informações, consulte o [comunicado de fim do suporte para o SQL Server 2005](https://www.microsoft.com/en-us/server-cloud/products/sql-server-2005/).  
  
### <a name="net-languages"></a>Linguagens .NET  
 Todos os acesso de dados do .NET, incluindo no .NET Core baseia-se no ADO.NET, um conjunto de classes que define uma interface para acessar qualquer tipo de fonte de dados, relacional e não relacionais. O Visual Studio tem várias ferramentas e designers que trabalham com o ADO.NET para ajudá-lo a se conectar a bancos de dados, manipular os dados e apresentá-los para o usuário. A documentação nesta seção descreve como usar essas ferramentas. Você também pode programar diretamente em relação os objetos de comando do ADO.NET. Para obter mais informações sobre como chamar as APIs do ADO.NET diretamente, consulte [ADO.NET](https://msdn.microsoft.com/library/e80y5yhx\(v=vs.110\).aspx) na biblioteca MSDN.  
  
 Para obter a documentação de acesso a dados relacionada especificamente ao ASP.NET, consulte [trabalhando com dados](http://www.asp.net/web-forms/overview/presenting-and-managing-data) no site do ASP.NET. Para obter um tutorial sobre como usar o Entity Framework com o ASP.NET MVC, consulte [Introdução ao Entity Framework 6 Code First usando MVC 5](http://www.asp.net/mvc/overview/getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application).  
  
 Aplicativos universais do Windows Platform (UWP) em c# ou Visual Basic podem usar o SDK do Microsoft Azure para .NET para acessar o armazenamento do Azure e outros serviços do Azure. A classe Windows.Web.HttpClient permite a comunicação com qualquer serviço RESTful. Para obter mais informações, consulte [como se conectar a um servidor HTTP usando o Windows](https://msdn.microsoft.com/library/windows/apps/dn469430.aspx.)  
  
 Para o armazenamento de dados no computador local, a abordagem recomendada é usar o SQLite, que é executado no mesmo processo que o aplicativo. Se uma camada de mapeamento relacional de objeto (ORM) for necessária, você pode usar o Entity Framework. Para obter mais informações, consulte [acesso a dados](https://msdn.microsoft.com/windows/uwp/data-access/index) no Centro de desenvolvedores do Windows.  
  
 Se você estiver se conectando aos serviços do Azure, certifique-se de baixar a versão mais recente [Azure SDK tools](https://azure.microsoft.com/en-us/downloads/).  
  
#### <a name="data-providers"></a>Provedores de dados  
 Para um banco de dados ser consumível no ADO.NET, ele deve ter um personalizado *provedor de dados ADO.NET* ou else deve expor uma interface ODBC ou OLE DB. A Microsoft fornece um [lista de provedores de dados ADO.NET](https://msdn.microsoft.com/data/dd363565) para produtos do SQL Server, bem como provedores de ODBC e OLE DB.  
  
#### <a name="data-modeling"></a>Modelagem de dados  
 No .NET, você tem três opções de modelagem e manipulação de dados na memória depois que você recuperou de uma fonte de dados:  
  
 Entity Framework  
 A tecnologia Microsoft ORM preferencial. Você pode usá-lo ao programa em relação aos dados relacionais como objetos de primeira classe .NET. Para novos aplicativos, ele deve ser a primeira opção padrão quando um modelo é necessário. Ele requer suporte personalizado do provedor de ADO.NET subjacente.  
  
 LINQ to SQL  
 Um mapeador relacional de objeto de gerações anteriores. Ele funciona bem para cenários menos complexos, mas não está mais em desenvolvimento ativo.  
  
 Conjuntos de dados  
 O mais antigo dos três tecnologias de modelagem. Ele é projetado principalmente para desenvolvimento rápido de aplicativos "formulários sobre dados" na qual você não é enormes quantidades de dados de processamento ou execução de consultas complexas ou transformações. Um objeto de conjunto de dados consiste em objetos DataTable e DataRow logicamente semelhantes a objetos de banco de dados do SQL muito mais do que objetos .NET. Para aplicativos relativamente simples com base em fontes de dados SQL, conjuntos de dados ainda podem ser uma boa opção.  
  
 Não há nenhum requisito para usar qualquer uma dessas tecnologias. Em alguns cenários, especialmente quando o desempenho for crítico, você pode simplesmente usar um objeto DataReader para ler do banco de dados e copie os valores que você precisa para um objeto de coleção como lista\<T >.  
  
### <a name="native-c"></a>C++ Nativo  
 Aplicativos de C++ que se conectam ao SQL Server devem usar o [SQL Server Native Client](https://msdn.microsoft.com/sqlserver/aa937733.aspx). Você pode acessar outros bancos de dados usando [ODBC](https://msdn.microsoft.com/library/ms710252\(v=vs.85\).aspx) ou drivers de OLE DB diretamente. O ODBC é a interface padrão do banco de dados atual, mas a maioria dos sistemas de banco de dados fornecer funcionalidade personalizada que não pode ser acessada por meio da interface do ODBC.  OLE DB é uma tecnologia de acesso a dados COM herdados ainda têm suporte, mas não é recomendada para novos aplicativos.  Para obter mais informações, consulte [acesso a dados](http://msdn.microsoft.com/library/a9455752-39c4-4457-b14e-197772d3df0b).  
  
 Programas do C++ que consumirem serviços REST podem usar o [C++ REST SDK](https://github.com/Microsoft/cpprestsdk).  
  
 Programas do C++ que funcionam com o armazenamento do Microsoft Azure podem usar o [cliente de armazenamento do Microsoft Azure](http://www.nuget.org/packages/wastorage).  
  
#### <a name="data-modeling"></a>Modelagem de dados  
 Visual Studio não fornece uma camada ORM para C++.  [ODB](http://www.codesynthesis.com/products/odb/) é um ORM do código-fonte aberto popular para C++.  
  
 Para obter mais informações sobre as tecnologias de acesso a dados herdadas do Visual C++, consulte [acesso a dados](http://msdn.microsoft.com/library/a9455752-39c4-4457-b14e-197772d3df0b)  
  
### <a name="javascript"></a>JavaScript  
 [JavaScript no Visual Studio](https://msdn.microsoft.com/library/hh334522.aspx) é uma linguagem de primeira classe para a criação de aplicativos de plataforma cruzada, aplicativos da UWP, serviços de nuvem, sites e aplicativos web. Você pode usar o Bower, Grunt, Gulp, npm e NuGet de dentro do Visual Studio para instalar seus produtos de banco de dados e bibliotecas JavaScript favoritas. Conectar-se ao armazenamento do Azure e serviços baixando SDKs do [site do Azure](https://azure.microsoft.com/).  Js é uma biblioteca JavaScript do lado do servidor (Node. js) conecta-se a fontes de dados do ADO.NET.  
  
### <a name="python"></a>Python  
 Instale [Python Tools para Visual Studio](http://microsoft.github.io/PTVS/) juntamente com seu framework favorito do Python para criar aplicativos CPython ou IronPython (.NET).  As ferramentas Python para o site do Visual Studio tem vários tutoriais sobre como se conectar a dados, inclusive [Django e banco de dados SQL no Azure](https://github.com/Microsoft/PTVS/wiki/Django-and-SQL-Database-on-Azure), [Django e MySQL no Azure](https://github.com/Microsoft/PTVS/wiki/Django-and-MySQL-on-Azure) e [Bottle e MongoDB no Azure](https://github.com/Microsoft/PTVS/wiki/Bottle-and-MongoDB-on-Azure).  
  
## <a name="in-this-section"></a>Nesta seção  
 [Instalando sistemas de banco de dados, ferramentas e exemplos](../data-tools/installing-database-systems-tools-and-samples.md)  
 Discute como obter produtos de banco de dados e as extensões do Visual Studio ou drivers que dão suporte a eles e onde encontrar os bancos de dados para fins de aprendizado e experimentação.  
  
 [Ferramentas de dados do Visual Studio para .NET](http://msdn.microsoft.com/en-us/6b145922-2f00-47db-befc-bf351b4809a1)  
 Descreve como usar janelas de ferramentas do Visual Studio para se conectar a fontes de dados, criar conjuntos de dados ou modelos do Entity Framework e associar os dados a controles de interface do usuário.  
  
## <a name="related-topics"></a>Tópicos relacionados  
 [Dados, dispositivos e análise](https://msdn.microsoft.com/data-and-devices)  
 Fornece uma introdução à nuvem inteligente da Microsoft, incluindo o Cortana Analytics Suite e o suporte para a Internet das coisas.  
  
 [Armazenamento do Microsoft Azure](https://azure.microCsoft.com/en-us/documentation/services/storage/)  
 Descreve como criar aplicativos usando arquivos, tabelas, filas e blobs do Azure e armazenamento do Azure.  
  
 [Banco de Dados SQL do Azure](https://azure.microsoft.com/en-us/documentation/services/sql-database/)  
 Descreve como se conectar ao banco de dados SQL, banco de dados relacional como um serviço.  
  
 [SQL Server Data Tools](https://msdn.microsoft.com/library/hh272686\(v=vs.103\).aspx)  
 Descreve as ferramentas que simplificam o design, exploração, teste e implantação de bancos de dados e aplicativos conectados a dados.  
  
 [ADO.NET](http://msdn.microsoft.com/library/5b96ed06-9759-4966-a797-a1d5f6ee50ca)  
 Descreve a arquitetura do ADO.NET e como usar as classes ADO.NET para gerenciar dados de aplicativo e interagir com fontes de dados e XML.  
  
 [Entity Framework do ADO.NET](https://msdn.microsoft.com/data/ef)  
 Descreve como criar aplicativos de dados que permitem aos desenvolvedores de programas em um modelo conceitual em vez de diretamente em um banco de dados relacional.  
  
 [WCF Data Services 4.5](http://msdn.microsoft.com/library/73d2bec3-7c92-4110-b905-11bb0462357a)  
 Descreve como usar [!INCLUDE[ssAstoria](../includes/ssastoria-md.md)] para implantar serviços de dados na web ou em uma intranet que implementam o [Open Data Protocol (OData)](http://go.microsoft.com/fwlink/?LinkID=182204).  
  
 [Dados em soluções do Office](http://msdn.microsoft.com/library/8478c095-864b-4ed3-8a70-1fc19b411c6a)  
 Contém links para tópicos que explicam como dados funcionam em soluções do Office. Isso inclui informações sobre programação orientada a esquema, caching de dados e acesso a dados do lado do servidor.  
  
 [LINQ (Consulta Integrada à Linguagem)](http://msdn.microsoft.com/library/a73c4aec-5d15-4e98-b962-1274021ea93d)  
 Descreve os recursos de consulta incorporados no c# e Visual Basic e o modelo comum para consultar bancos de dados relacionais, documentos XML, conjuntos de dados e coleções na memória.  
  
 [Ferramentas XML no Visual Studio](../xml-tools/xml-tools-in-visual-studio.md)  
 Discute a trabalhar com recursos de XML do .NET Framework de dados, depuração XSLT, XML e a arquitetura de consulta XML.  
  
 [Documentos e dados XML](http://msdn.microsoft.com/library/e695047f-3c0f-4045-8708-5baea91cc380)  
 Fornece uma visão geral sobre um conjunto abrangente e integrado de classes que funcionam com documentos e dados XML no .NET Framework.

