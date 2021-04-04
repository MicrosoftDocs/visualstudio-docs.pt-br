---
title: Acessar dados remotos do & local (aplicativos ClickOnce)
description: Saiba mais sobre a variedade de opções que o ClickOnce fornece para ler e gravar dados, tanto localmente quanto remotamente.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- ClickOnce deployment, data
- data access, ClickOnce applications
ms.assetid: be5cbe12-6cb6-49c9-aa59-a1624e1eef3d
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: cbffa062e1115264f9496081cdcf63d17d2a36c7
ms.sourcegitcommit: 80fc9a72e9a1aba2d417dbfee997fab013fc36ac
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/02/2021
ms.locfileid: "106217483"
---
# <a name="access-local-and-remote-data-in-clickonce-applications"></a>Acesso a dados locais e remotos em aplicativos ClickOnce
A maioria dos aplicativos consome ou gera dados. [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] oferece uma variedade de opções para ler e gravar dados, tanto localmente quanto remotamente.

## <a name="local-data"></a>Dados locais
 Com [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] o, você pode carregar e armazenar dados localmente usando qualquer um dos seguintes métodos:

- Diretório de dados de [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)]

- Armazenamentos isolado

- Outros arquivos locais

### <a name="clickonce-data-directory"></a>Diretório de dados do ClickOnce
 Cada [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] aplicativo instalado em um computador local tem um diretório de dados, armazenado na pasta Documents and Settings do usuário. Qualquer arquivo incluído em um [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] aplicativo e marcado como um arquivo de "dados" é copiado para esse diretório quando um aplicativo é instalado. Os arquivos de dados podem ser de qualquer tipo de arquivo, usados com mais frequência são arquivos de texto, XML e de banco de dado, como arquivos. mdb do Microsoft Access.

 O diretório de dados destina-se a dados gerenciados por aplicativo, que são dados que o aplicativo armazena e mantém explicitamente. Todos os arquivos estáticos e não de dependência não marcados como "dados" no manifesto do aplicativo residirão no diretório do aplicativo. Esse diretório é onde residem os arquivos e assemblies do executável (*. exe*) do aplicativo.

> [!NOTE]
> Quando um [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] aplicativo é desinstalado, seu diretório de dados também é removido. Nunca use o diretório de dados para armazenar dados gerenciados pelo usuário final, como documentos.

#### <a name="mark-data-files-in-a-clickonce-distribution"></a>Marcar arquivos de dados em uma distribuição do ClickOnce
 Para colocar um arquivo existente dentro do diretório de dados, você deve marcar o arquivo existente como um arquivo de dados no [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] arquivo de manifesto do aplicativo do aplicativo. Para obter mais informações, consulte [Como incluir um arquivo de dados em um aplicativo ClickOnce](../deployment/how-to-include-a-data-file-in-a-clickonce-application.md).

#### <a name="read-from-and-write-to-the-data-directory"></a>Ler e gravar no diretório de dados
 A leitura do diretório de dados requer que sua [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] permissão de leitura de solicitação de aplicativo; de maneira semelhante, gravar no diretório requer permissão de gravação. Seu aplicativo terá essa permissão automaticamente se estiver configurado para ser executado com confiança total. Para obter mais informações sobre como elevar permissões para seu aplicativo usando a elevação de permissão ou a implantação de aplicativo confiável, consulte [proteger aplicativos ClickOnce](../deployment/securing-clickonce-applications.md).

> [!NOTE]
> Se sua organização não usar a implantação de aplicativos confiáveis e tiver desativado a elevação da permissão, ocorrerá uma falha na declaração das permissões.

 Depois que o aplicativo tiver essas permissões, ele poderá acessar o diretório de dados usando chamadas de método em classes dentro do <xref:System.IO> . Você pode obter o caminho do diretório de dados em um [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] aplicativo Windows Forms usando a <xref:System.Deployment.Application.ApplicationDeployment.DataDirectory%2A> propriedade definida na <xref:System.Deployment.Application.ApplicationDeployment.CurrentDeployment%2A> propriedade de <xref:System.Deployment.Application.ApplicationDeployment> . Essa é a maneira mais conveniente e recomendada para acessar seus dados. O exemplo de código a seguir demonstra como fazer isso para um arquivo de texto chamado *CSV.txt* que você incluiu em sua implantação como um arquivo de dados.

 :::code language="csharp" source="../snippets/csharp/VS_Snippets_Winforms/ClickOnce.OpenDataFile/CS/Form1.cs" id="Snippet1":::
 :::code language="vb" source="../snippets/visualbasic/VS_Snippets_Winforms/ClickOnce.OpenDataFile/VB/Form1.vb" id="Snippet1":::

 Para obter mais informações sobre como marcar arquivos em sua implantação como arquivos de dados, consulte [como: incluir um arquivo de dados em um aplicativo ClickOnce](../deployment/how-to-include-a-data-file-in-a-clickonce-application.md).

 Você também pode obter o caminho do diretório de dados usando as variáveis relevantes na <xref:System.Windows.Forms.Application> classe, como <xref:System.Windows.Forms.Application.LocalUserAppDataPath%2A> .

 A manipulação de outros tipos de arquivos pode exigir permissões adicionais. Por exemplo, se você quiser usar um arquivo de banco de dados do Access (*. mdb*), seu aplicativo deverá declarar confiança total para usar as \<xref:System.Data> classes relevantes.

#### <a name="data-directory-and-application-versions"></a>Versões do aplicativo e do diretório de dados
 Cada versão de um aplicativo tem seu próprio diretório de dados, que é isolado de outras versões. [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] cria esse diretório independentemente de os arquivos de dados serem incluídos na implantação, de forma que o aplicativo tenha um local para criar novos arquivos de dados em tempo de execução. Quando uma nova versão de um aplicativo for instalada, o [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] copiará todos os arquivos de dados existentes do diretório de dados da versão anterior para o diretório de dados da nova versão, independentemente de eles terem sido incluídos na implantação original ou criados pelo aplicativo.

 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] substituirá a versão mais antiga do arquivo pela versão mais recente do servidor se um arquivo de dados tiver um valor de hash diferente na versão antiga do aplicativo como na nova versão. Além disso, se a versão anterior do aplicativo criou um novo arquivo com o mesmo nome de um arquivo incluído na implantação da nova versão, [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] o substituirá o arquivo da versão antiga pelo novo arquivo. Em ambos os casos, os arquivos antigos serão incluídos em um subdiretório dentro do diretório de dados chamado `.pre` , para que o aplicativo ainda possa acessar os dados antigos para fins de migração.

 Se precisar de uma migração de dados refinada, você poderá usar a [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] API de implantação para executar a migração personalizada do diretório de dados antigos para o novo diretório de dados. Você precisará testar um download disponível usando <xref:System.Deployment.Application.ApplicationDeployment.IsFirstRun%2A> o, baixar a atualização usando o <xref:System.Deployment.Application.ApplicationDeployment.Update%2A> ou <xref:System.Deployment.Application.ApplicationDeployment.UpdateAsync%2A> o, e fazer qualquer trabalho de migração de dados personalizado por conta própria após a conclusão da atualização.

### <a name="isolated-storage"></a>Armazenamento isolado
 O armazenamento isolado fornece uma API para criar e acessar arquivos usando uma API simples. O local real dos arquivos armazenados fica oculto do desenvolvedor e do usuário.

 O armazenamento isolado funciona em todas as versões do .NET Framework. O armazenamento isolado também funciona em aplicativos parcialmente confiáveis sem a necessidade de concessões de permissão adicional. Você deve usar o armazenamento isolado se seu aplicativo deve ser executado com confiança parcial, mas deve manter dados específicos do aplicativo.

 Para obter mais informações, consulte [armazenamento isolado](/dotnet/standard/io/isolated-storage).

### <a name="other-local-files"></a>Outros arquivos locais
 Se seu aplicativo precisar trabalhar com ou salvar dados do usuário final, como relatórios, imagens, música e assim por diante, seu aplicativo precisará <xref:System.Security.Permissions.FileIOPermission> ler e gravar dados no sistema de arquivos local.

## <a name="remote-data"></a>Dados remotos
 Em algum momento, seu aplicativo provavelmente terá que recuperar informações de um site remoto, como dados do cliente ou informações do mercado. Esta seção aborda as técnicas mais comuns para recuperar dados remotos.

### <a name="access-files-with-http"></a>Acessar arquivos com HTTP
 Você pode acessar dados de um servidor Web usando o <xref:System.Net.WebClient> ou a <xref:System.Net.HttpWebRequest> classe no <xref:System.Net> namespace. Os dados podem ser arquivos estáticos ou [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] aplicativos que retornam texto bruto ou dados XML. Se os dados estiverem em formato XML, a maneira mais rápida de recuperar os dados é usando a <xref:System.Xml.XmlDocument> classe, cujo <xref:System.Xml.XmlDocument.Load%2A> método usa uma URL como um argumento. Para obter um exemplo, consulte [ler um documento XML no dom](/dotnet/standard/data/xml/reading-an-xml-document-into-the-dom).

 Você precisa considerar a segurança quando seu aplicativo acessa dados remotos via HTTP. Por padrão, o [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] acesso do seu aplicativo aos recursos de rede pode ser restrito, dependendo de como seu aplicativo foi implantado. Essas restrições são aplicadas para impedir que programas mal-intencionados obtenham acesso a dados remotos privilegiados ou usando um computador do usuário para atacar outros computadores na rede.

 A tabela a seguir lista as estratégias de implantação que você pode usar e suas permissões da Web padrão.

|Tipo de implantação|Permissões de rede padrão|
|---------------------|---------------------------------|
|Instalação na Web|Só é possível acessar o servidor Web do qual o aplicativo foi instalado|
|Instalação do compartilhamento de arquivos|Não é possível acessar nenhum servidor Web|
|Instalação do CD-ROM|Pode acessar qualquer servidor Web|

 Se seu [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] aplicativo não puder acessar um servidor Web devido a restrições de segurança, o aplicativo deverá declarar <xref:System.Net.WebPermission> para esse site. Para obter mais informações sobre como aumentar as permissões de segurança para um [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] aplicativo, consulte [proteger aplicativos ClickOnce](../deployment/securing-clickonce-applications.md).

### <a name="access-data-through-an-xml-web-service"></a>Acessar dados por meio de um serviço Web XML
 Se você expor seus dados como um serviço Web XML, poderá acessar os dados usando um proxy de serviço Web XML. O proxy é uma classe .NET Framework que você cria usando qualquer um deles [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] . As operações do serviço Web XML, como recuperação de clientes, colocação de pedidos e assim por diante, são expostas como métodos no proxy. Isso torna os serviços Web muito mais fáceis de usar do que os arquivos XML ou de texto bruto.

 Se o serviço Web XML operar por HTTP, o serviço será associado pelas mesmas restrições de segurança das <xref:System.Net.WebClient> <xref:System.Net.HttpWebRequest> classes e.

### <a name="access-a-database-directly"></a>Acessar um banco de dados diretamente
 Você pode usar as classes dentro do <xref:System.Data> namespace para estabelecer conexões diretas com um servidor de banco de dados, como SQL Server em sua rede, mas você deve considerar os problemas de segurança. Diferentemente das solicitações HTTP, as solicitações de conexão de banco de dados são sempre proibidas por padrão sob confiança parcial; Você só terá essa permissão por padrão se instalar o [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] aplicativo de um CD-ROM. Isso dá ao seu aplicativo confiança total. Para habilitar o acesso a um banco de dados SQL Server específico, seu aplicativo deve solicitar <xref:System.Data.SqlClient.SqlClientPermission> a ele; para habilitar o acesso a um banco de dados que não seja SQL Server, ele deve solicitar <xref:System.Data.OleDb.OleDbPermission> .

 Na maioria das vezes, você não precisará acessar o banco de dados diretamente, mas o acessará, em vez disso, por meio de um aplicativo de servidor Web escrito em um [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] serviço Web XML. O acesso ao banco de dados dessa maneira costuma ser o melhor método se seu [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] aplicativo for implantado de um servidor Web. Você pode acessar o servidor em confiança parcial sem elevar as permissões do aplicativo.

## <a name="see-also"></a>Confira também

- [Como: incluir um arquivo de dados em um aplicativo ClickOnce](../deployment/how-to-include-a-data-file-in-a-clickonce-application.md)