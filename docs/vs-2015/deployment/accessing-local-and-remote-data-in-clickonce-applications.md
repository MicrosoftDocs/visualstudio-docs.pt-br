---
title: Acessando dados locais e remotos em aplicativos ClickOnce | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-deployment
ms.tgt_pltfrm: ''
ms.topic: article
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- ClickOnce deployment, data
- data access, ClickOnce applications
ms.assetid: be5cbe12-6cb6-49c9-aa59-a1624e1eef3d
caps.latest.revision: 23
author: mikejo5000
ms.author: mikejo
manager: wpickett
ms.openlocfilehash: 4fe0c0b1cd7659a5887f267181ffd6fa7bb5e8d4
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49218826"
---
# <a name="accessing-local-and-remote-data-in-clickonce-applications"></a>Acessando dados locais e remotos em aplicativos ClickOnce
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

A maioria dos aplicativos consuma nem produza dados. [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] Fornece uma variedade de opções para ler e gravar dados, tanto local quanto remotamente.  
  
## <a name="local-data"></a>Dados locais  
 Com [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)], você pode carregar e armazenar dados localmente usando qualquer um dos seguintes métodos:  
  
-   [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] Diretório de dados  
  
-   Armazenamentos isolado  
  
-   Outros arquivos locais  
  
### <a name="clickonce-data-directory"></a>Diretório de dados do ClickOnce  
 Cada [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] aplicativo instalado em um computador local tem um diretório de dados armazenado na pasta de documentos e configurações do usuário. Qualquer arquivo incluído em um [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] aplicativo e marcada como um arquivo de "dados" é copiado para esse diretório quando um aplicativo é instalado. Arquivos de dados podem ser de qualquer tipo de arquivo, usado com mais frequência que está sendo texto, XML e arquivos de banco de dados, como arquivos. mdb do Microsoft Access.  
  
 O diretório de dados destina-se a dados gerenciados de aplicativo, que são dados que o aplicativo armazena e mantém explicitamente. Todos estáticos, arquivos de nondependency não marcados como "dados" no manifesto do aplicativo em vez disso, reside no diretório do aplicativo. Esse diretório é onde residem os arquivos executáveis (.exe) e assemblies do aplicativo.  
  
> [!NOTE]
>  Quando um [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] aplicativo for desinstalado, seu diretório de dados também será removido. Nunca use o diretório de dados para armazenar dados gerenciados de final pelo usuário, como documentos.  
  
#### <a name="marking-data-files-in-a-clickonce-distribution"></a>Marcar os arquivos de dados em uma distribuição do ClickOnce  
 Para colocar um arquivo existente dentro do diretório de dados, você deve marcar o arquivo existente como um arquivo de dados no seu [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] arquivo de manifesto de aplicativo do aplicativo. Para obter mais informações, consulte [Como incluir um arquivo de dados em um aplicativo ClickOnce](../deployment/how-to-include-a-data-file-in-a-clickonce-application.md).  
  
#### <a name="reading-from-and-writing-to-the-data-directory"></a>Leitura e gravação para o diretório de dados  
 A leitura do diretório de dados requer que seu [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] solicitação do aplicativo a permissão de leitura; da mesma forma, gravar no diretório requer a permissão de gravação. Seu aplicativo terá essa permissão automaticamente se ele está configurado para ser executado com confiança total. Para obter mais informações sobre como elevar permissões para seu aplicativo usando a implantação de aplicativo confiável ou elevação de permissões, consulte [Protegendo aplicativos ClickOnce](../deployment/securing-clickonce-applications.md).  
  
> [!NOTE]
>  Se sua organização não usa implantação de aplicativos confiáveis e tenha desativado a elevação de permissões, declarando permissões irá falhar.  
  
 Depois que seu aplicativo tiver essas permissões, ele pode acessar o diretório de dados por meio de chamadas de método em classes dentro do <xref:System.IO>. Você pode obter o caminho do diretório de dados dentro de um Windows Forms [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] aplicativo usando o <xref:System.Deployment.Application.ApplicationDeployment.DataDirectory%2A> propriedade definida na <xref:System.Deployment.Application.ApplicationDeployment.CurrentDeployment%2A> propriedade do <xref:System.Deployment.Application.ApplicationDeployment>. Essa é a maneira recomendada e mais conveniente para acessar seus dados. O exemplo de código a seguir demonstra como fazer isso para um arquivo de texto chamado CSV.txt que você incluiu na implantação como um arquivo de dados.  
  
 [!code-csharp[ClickOnce.OpenDataFile#1](../snippets/csharp/VS_Snippets_Winforms/ClickOnce.OpenDataFile/CS/Form1.cs#1)]
 [!code-vb[ClickOnce.OpenDataFile#1](../snippets/visualbasic/VS_Snippets_Winforms/ClickOnce.OpenDataFile/VB/Form1.vb#1)]  
  
 Para obter mais informações sobre como marcar arquivos em sua implantação, como arquivos de dados, consulte [como: incluir um arquivo de dados em um aplicativo ClickOnce](../deployment/how-to-include-a-data-file-in-a-clickonce-application.md).  
  
 Também é possível obter o caminho do diretório de dados usando as variáveis relevantes sobre o <xref:System.Windows.Forms.Application> classe, como <xref:System.Windows.Forms.Application.LocalUserAppDataPath%2A>.  
  
 Manipular outros tipos de arquivos pode exigir permissões adicionais. Por exemplo, se você quiser usar um arquivo de banco de dados (. mdb) de acesso, seu aplicativo deve declarar confiança total para usar o relevantes <xref:System.Data> classes.  
  
#### <a name="data-directory-and-application-versions"></a>Diretório de dados e versões de aplicativos  
 Cada versão de um aplicativo tem seu próprio diretório de dados, que é isolado de outras versões. [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] cria esse diretório, independentemente se os arquivos de dados são incluídos na implantação para que o aplicativo tenha um local para criar novos arquivos de dados em tempo de execução. Quando uma nova versão de um aplicativo é instalada, [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] copiará todos os arquivos de dados existentes do diretório de dados da versão anterior para diretório a nova versão de dados — se foram incluídas na implantação original ou criados pelo aplicativo.  
  
 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] substituirá a versão mais antiga do arquivo com a versão mais recente do servidor se um arquivo de dados tem um valor de hash diferente na versão antiga do aplicativo como a nova versão. Além disso, se a versão anterior do aplicativo que criou um novo arquivo que tem o mesmo nome como um arquivo incluído na implantação da nova versão, [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] substituirá o arquivo da versão antiga com o novo arquivo. Em ambos os casos, os arquivos antigos serão incluídos em um subdiretório no diretório de dados denominado `.pre`, de modo que o aplicativo ainda pode acessar os dados antigos para fins de migração.  
  
 Se você precisar de mais refinados de migração de dados, você pode usar o [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] API de implantação para executar migração personalizado do diretório Data antigo para o novo diretório de dados. Você terá que testar um download disponível usando <xref:System.Deployment.Application.ApplicationDeployment.IsFirstRun%2A>, baixe a atualização usando <xref:System.Deployment.Application.ApplicationDeployment.Update%2A> ou <xref:System.Deployment.Application.ApplicationDeployment.UpdateAsync%2A>, e qualquer personalizados funcionam de migração de dados em seu próprio após a atualização for concluído.  
  
### <a name="isolated-storage"></a>Armazenamentos isolado  
 Armazenamento isolado fornece uma API para criar e acessar arquivos por meio de uma API simples. O local real dos arquivos armazenados é ocultado do desenvolvedor e o usuário.  
  
 Isolado funciona o armazenamento de todas as versões do [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)]. Armazenamento isolado também funciona em aplicativos parcialmente confiáveis sem a necessidade de concessões de permissão adicional. Se seu aplicativo deve ser executado em confiança parcial, mas deve manter dados específicos do aplicativo, você deve usar armazenamento isolado.  
  
 Para obter mais informações, consulte [armazenamento isolado](http://msdn.microsoft.com/library/aff939d7-9e49-46f2-a8cd-938d3020e94e).  
  
### <a name="other-local-files"></a>Outros arquivos locais  
 Se seu aplicativo deve funcionar com ou salvar dados do usuário final, como relatórios, imagens, música e assim por diante, seu aplicativo exigirá <xref:System.Security.Permissions.FileIOPermission> para ler e gravar dados no sistema de arquivos local.  
  
## <a name="remote-data"></a>Dados remotos  
 Em algum momento, seu aplicativo provavelmente terá que recuperar informações de um site remoto, como informações de dados ou mercado do cliente. Esta seção discute as técnicas mais comuns para recuperar os dados remotos.  
  
### <a name="accessing-files-by-using-http"></a>Acessando arquivos por meio de HTTP  
 Você pode acessar dados de um servidor Web usando o <xref:System.Net.WebClient> ou o <xref:System.Net.HttpWebRequest> classe no <xref:System.Net> namespace. Os dados podem ser qualquer um dos arquivos estáticos ou [!INCLUDE[vstecasp](../includes/vstecasp-md.md)] aplicativos que retornam dados XML ou texto não processado. Se os dados estiverem em formato XML, a maneira mais rápida para recuperar os dados é usando o <xref:System.Xml.XmlDocument> classe cuja <xref:System.Xml.XmlDocument.Load%2A> método usa uma URL como um argumento. Por exemplo, consulte [ler um documento XML no DOM](http://msdn.microsoft.com/library/a4fb291f-5630-49ba-a49a-5b66c3b71e49).  
  
 Você deve considerar a segurança quando o aplicativo acessa os dados remotos por meio de HTTP. Por padrão, seu [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] acesso do aplicativo aos recursos da rede pode ser restringido, dependendo de como seu aplicativo foi implantado. Essas restrições são aplicadas para impedir que programas mal-intencionados obtenham acesso a dados remotos com privilégios ou usando um computador do usuário para atacar outros computadores na rede.  
  
 A tabela a seguir lista as estratégias de implantação, que você pode usar e suas permissões de Web padrão.  
  
|Tipo de implantação|Permissões de rede padrão|  
|---------------------|---------------------------------|  
|Instalação da Web|Só pode acessar o servidor Web do qual o aplicativo foi instalado|  
|Instalação de compartilhamento de arquivo|Não é possível acessar todos os servidores da Web|  
|Instalar de CD-ROM|Pode acessar todos os servidores da Web|  
  
 Se sua [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] aplicativo não pode acessar um servidor Web devido a restrições de segurança, o aplicativo deve declarar <xref:System.Net.WebPermission> para o site da Web. Para obter mais informações sobre como aumentar permissões de segurança para um [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] aplicativo, consulte [Protegendo aplicativos ClickOnce](../deployment/securing-clickonce-applications.md).  
  
### <a name="accessing-data-through-an-xml-web-service"></a>Acessando dados através de um serviço Web XML  
 Se você expor seus dados como um serviço Web XML, você pode acessar os dados usando um proxy do serviço Web XML. O proxy é um [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] classe criará usando [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]. As operações do serviço Web XML — assim como a recuperação de clientes, pedidos de colocação e assim por diante — são expostos como métodos no proxy. Isso torna muito mais fácil de usar do que texto não processado ou arquivos XML Web services.  
  
 Se o serviço Web XML opera em HTTP, o serviço será limitado pelas mesmas restrições de segurança que o <xref:System.Net.WebClient> e <xref:System.Net.HttpWebRequest> classes.  
  
### <a name="accessing-a-database-directly"></a>Acessando um banco de dados diretamente  
 Você pode usar as classes dentro do <xref:System.Data> namespace para estabelecer conexões diretas com um servidor de banco de dados, como o SQL Server em sua rede, mas você deve considerar as questões de segurança. Ao contrário de solicitações HTTP, solicitações de conexão de banco de dados sempre são proibidas por padrão sob confiança parcial; Você só terá essa permissão por padrão se você instalar o [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] aplicativo de um CD-ROM. Assim, seu aplicativo de confiança total. Para habilitar o acesso a um banco de dados do SQL Server, seu aplicativo deve solicitar <xref:System.Data.SqlClient.SqlClientPermission> a ele; para habilitar o acesso a um banco de dados diferente do SQL Server, ele deverá solicitar <xref:System.Data.OleDb.OleDbPermission>.  
  
 Na maioria das vezes, você não precisará acessar o banco de dados diretamente, mas irá acessá-la em vez disso, por meio de um aplicativo de servidor da Web escrito em [!INCLUDE[vstecasp](../includes/vstecasp-md.md)] ou um serviço Web XML. Acessar o banco de dados dessa maneira é com frequência o melhor método se seu [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] aplicativo será implantado em um servidor Web. Você pode acessar o servidor em confiança parcial sem a elevação de permissões do seu aplicativo.  
  
## <a name="see-also"></a>Consulte também  
 [Como incluir um arquivo de dados em um aplicativo ClickOnce](../deployment/how-to-include-a-data-file-in-a-clickonce-application.md)



