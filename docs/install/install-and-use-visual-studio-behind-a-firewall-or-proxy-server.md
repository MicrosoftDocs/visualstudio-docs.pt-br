---
title: Instalar e usar o Visual Studio e os Serviços do Azure atrás de um firewall ou servidor proxy | Microsoft Docs
description: Examine as URLs de domínio, as portas e os protocolos que você pode querer adicionar à lista de permissões ou abrir se sua organização usar um firewall ou um servidor proxy
ms.custom: ''
ms.date: 07/10/2018
ms.technology: vs-acquisition
ms.prod: visual-studio-dev15
ms.topic: conceptual
helpviewer_keywords:
- network installation, Visual Studio
- administrator guide, Visual Studio
- installing Visual Studio, administrator guide
- list of domains, locations, URLs
ms.assetid: ''
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 2636bed20da5af32e011b39cf262349d42ddda55
ms.sourcegitcommit: bc43970c000f07c9cc2051f1264a9742943a9755
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2018
ms.locfileid: "51349563"
---
# <a name="install-and-use-visual-studio-and-azure-services-behind-a-firewall-or-proxy-server"></a>Instalar e usar o Visual Studio e os Serviços do Azure atrás de um firewall ou servidor proxy

Se você ou sua organização usa medidas de segurança como um firewall ou um servidor proxy, há URLs de domínio que você talvez queira adicionar à "lista de permissões" e portas e protocolos que talvez você queira abrir para que tenha a melhor experiência ao instalar e usar o Visual Studio e os Serviços do Azure.

* **[Instalar o Visual Studio](#install-visual-studio)**: essas tabelas incluem as URLs de domínio na lista de permissões para que você tenha acesso a todos os componentes e cargas de trabalho desejados.

* **[Usar o Visual Studio e Serviços do Azure](#use-visual-studio-and-azure-services)**: essa tabela inclui as URLs de domínio na lista de permissões e as portas e protocolos a serem abertos para que você tenha acesso a todos os recursos e serviços desejados.

> [!NOTE]
> Este artigo foi escrito para o Visual Studio no Windows, mas determinadas informações também são aplicáveis à [instalação do Visual Studio para Mac](/visualstudio/mac/install-behind-a-firewall-or-proxy-server) por trás de um firewall ou de um servidor proxy.

## <a name="install-visual-studio"></a>Instalar o Visual Studio

### <a name="urls-to-whitelist"></a>URLs a serem adicionadas à lista de permissões

Como o Instalador do Visual Studio baixa arquivos de vários domínios e seus servidores de download, aqui estão as URLs que talvez você deseje adicionar à lista de permissões como confiáveis na interface do usuário ou em seus scripts de implantação.

#### <a name="microsoft-domains"></a>Domínios da Microsoft

| Domain | Finalidade |
| - | - |
| go.microsoft.com | Resolução da URL de instalação |
| aka.ms | Resolução da URL de instalação |
| download.visualstudio.microsoft.com | Local de download de pacotes de instalação |
| download.microsoft.com | Local de download de pacotes de instalação |
| download.visualstudio.com | Local de download de pacotes de instalação |
| dl.xamarin.com | Local de download de pacotes de instalação |
| marketplace.visualstudio.com | Local de download de extensões do Visual Studio |
| visualstudio.microsoft.com | Local da documentação |
| docs.microsoft.com | Local da documentação |
| msdn.microsoft.com | Local da documentação |
| www.microsoft.com | Local da documentação |
| \*.windows.net | Local de conexão |
| \*.microsoftonline.com | Local de conexão |
| \*.live.com | Local de conexão |
| | |

#### <a name="non-microsoft-domains"></a>Domínios que não são da Microsoft

| Domain | Instala essas cargas de trabalho |
| - | - |
| archive.apache.org | Desenvolvimento móvel com JavaScript (Cordova) |
| cocos2d-x.org | Desenvolvimento de jogos com C++ (Cocos) |
| download.epicgames.com | Desenvolvimento de jogos com C++ (Unreal Engine) |
| download.oracle.com | Desenvolvimento móvel com JavaScript (SDK do Java) <br /><br />Desenvolvimento móvel com .NET (SDK do Java) |
| download.unity3d.com | Desenvolvimento de jogos com Unity (Unity) |
| netstorage.unity3d.com | Desenvolvimento de jogos com Unity (Unity) |
| dl.google.com | Desenvolvimento móvel com JavaScript (NDK e SDK do Android, Emulador) <br /><br />Desenvolvimento móvel com .NET (NDK e SDK do Android, Emulador) |
| www.incredibuild.com | Desenvolvimento de jogos com C++ (IncrediBuild) |
| incredibuildvs2017i.azureedge.net | Desenvolvimento de jogos com C++ (IncrediBuild) |
| www.python.org | Desenvolvimento do Python (Python) <br /><br />Ciência de dados e aplicativos analíticos (Python) |
| | |

## <a name="use-visual-studio-and-azure-services"></a>Usar o Visual Studio e Serviços do Azure

### <a name="urls-to-whitelist-and-ports-and-protocols-to-open"></a>URLs a serem adicionadas à lista de permissões e portas e protocolos a serem abertos

Para certificar-se de que você tem acesso a tudo o que é necessário ao usar o Visual Studio ou Serviços do Azure por trás de um firewall ou servidor proxy, aqui estão as URLs que devem ser adicionadas à lista de permissões e as portas e protocolos que talvez você deseje abrir.

| Cenário ou serviço | Ponto de extremidade DNS | Protocolo | Porta | Descrição |
| - | - | - | - | - |
| URL<br>resolução | go.microsoft.com<br><br>aka.ms | | | Usada para reduzir as URLs, que, em seguida, resolvem em URLs mais longas |
| Start Page | vsstartpage.blob.core.windows.net | | 443 | Usada para exibir as Novidades do Desenvolvedor mostradas na página inicial no Visual Studio |
| Destino<br> Notificação <br>Serviço | targetednotifications.azurewebsites.net <br><br>www.research.net | | 80<br><br>443 | Usada para filtrar uma lista global de notificações para uma lista aplicável somente a tipos específicos de cenários de uso/computadores |
| Extensão <br>verificação de atualização | marketplace.visualstudio.com<br><br>&#42;.windows.net <br>&#42;.microsoftonline.com <br>&#42;.live.com | | 443 | Usada para fornecer notificações quando uma extensão instalada tem uma atualização disponível <br><br> Usada como um local de conexão |
| Projeto do AI <br>Integração | az861674.vo.msecnd.net | | 443<br> | Usada para configurar novos projetos para enviar dados de uso para sua conta do Application Insights registrada |
| CodeLens | codelensprodscus1su0.app.<br>codelens.visualstudio.com | | 443 | Usada para fornecer informações no editor sobre quando um arquivo foi atualizado pela última, a linha do tempo de alterações, os itens de trabalho aos quais as alterações estão associadas, os autores e muito mais |
| Habilitação <br>de recurso experimental | visualstudio-devdiv-c2s.msedge.net | | 80 | Usada para ativar novos recursos experimentais ou alterações de recurso |
| “Notificação” de identidade <br>(nome de usuário e avatar)<br>e <br>Configurações de roaming | app.vssps.visualstudio.com <br><br>app.vsspsext.visualstudio.com<br><br>app.vssps.visualstudio.com<br><br> ns-sb2-prod-ch1-002.cloudapp.net <br><br>az700632.vo.msecnd.net | | 443 | Usada para exibir o nome do usuário e o avatar no IDE <br><br> Usada para garantir que as alterações de configuração atravessem de um computador para outro |
| Configurações Remotas | az700632.vo.msecnd.net | | 443 | Usada para desativar extensões que são conhecidas por causar problemas no Visual Studio |
| Ferramentas do Windows | developer.microsoft.com <br><br>dev.windows.com  <br><br>appdev.microsoft.com | HTTPS | 443 | Usada para cenários de armazenamento de aplicativos do Windows |
| JSON Schema <br>Descoberta <br><br>JSON Schema <br>Definição<br><br>JSON Schema <br>Suporte para <br>Recursos do Azure | json.schemastore.org <br>schemastoreorg.azurewebsites.net<br><br>json-schema.org<br><br>schema.management.azure.com | HTTP<br>HTTPS<br><br>HTTP<br><br>HTTPS | 80<br>443 <br><br> 443<br><br>443 | Usada para descobrir e baixar os esquemas JSON que o usuário pode usar durante a edição de documentos JSON <br><br>Usada para obter o esquema de metavalidação para JSON<br><br>Usada para obter o esquema atual para modelos de implantação do Azure Resource Manager |
| Pacote NPM <br>descoberta | Skimdb.npmjs.com <br><br>Registry.npmjs.org <br><br>Api.npms.io | HTTPS<br><br>http/s<br><br>HTTPS | 443<br><br>80/443<br><br>443 | Necessária para pesquisar pacotes NPM e usada para a instalação do pacote de script do lado do cliente em projetos da Web |
| Pacote de Bower<br> ícones<br><br>Pacote de Bower <br>search | Bower.io <br><br>bowercache.azurewebsites.net <br>go.microsoft.com <br>Registry.bower.io | HTTP<br><br>HTTPS<br>HTTP<br>HTTPS | 80<br><br>443<br>80<br>443 | Fornece o ícone padrão do pacote de Bower  <br><br>Fornece a capacidade de pesquisar pacotes de Bower |
| NuGet<br><br>Pacote NuGet<br> descoberta | Api.nuget.org <br>www.nuget.org <br>Nuget.org<br><br>crl3.digicert.com <br>crl4.digicert.com <br>ocsp.digicert.com <br>cacerts.digicert.com | HTTPS<br><br>http/s | 443<br><br>80/443<br> | Usada para verificar pacotes NuGet assinados.<br><br>Necessária para pesquisar versões e pacotes NuGet |
| Informações do repositório GitHub | api.github.com | HTTPS | 443 | Necessária para obter informações adicionais sobre pacotes de Bower |
| Linters da Web | Eslint.org<br><br>www.Bing.com <br><br>www.coffeelint.org | HTTP | 80 | |
| Criação do projeto do<br>Explorador do Cookiecutter<br>descoberta <br><br>Criação do projeto do <br>Explorador do Cookiecutter<br> criação  | api.github.com <br>raw.githubusercontent.com <br>go.microsoft.com<br><br>pypi.org <br> pypi.python.org | HTTPS | 443<br> | Usada para descobrir modelos online de nosso feed recomendado em repositórios github <br><br>Usada para criar um projeto de um modelo de cookiecutter que requer uma instalação sob demanda única de um pacote do Python de cookiecutter do PyPI (índice de pacote do Python) |
| Pacote do Python <br>descoberta<br><br>Pacote do Python <br>gerenciamento<br><br>Python <br>Novo Projeto <br>modelos | pypi.org<br> <br>pypi.python.org <br>bootstrap.pypa.io<br><br>go.microsoft.com | HTTPS | 443 | Fornece a capacidade de pesquisar pacotes de pip<br><br>Usada para instalar o pip automaticamente se ele estiver ausente <br><br> Usada para criar o <br><br>Usada para resolver os seguintes modelos de projeto do Python na caixa de diálogo Novo Projeto para URLs de modelo do cookiecutter:<br> – Projeto de classificador<br>– Projeto de clustering <br> – Projeto de regressão <br> – PyGame usando PyKinect <br> – Projeto Pyvot |
| Web do Office <br>add-in <br> Manifest <br>Verificação <br>Serviço | verificationservice.osi.office.net | HTTPS | 443 | Usada para validar os manifestos de suplementos de Web do Office |
| Suplementos do SharePoint <br>e do Office | sharepoint.com | HTTPS | 443 | Usada para publicar e testar o SharePoint e os Suplementos do Office para o SharePoint Online |
| Serviço de teste do <br>Gerenciador de Fluxo de Trabalho<br> Host | | HTTP | 12292 | Uma regra de firewall que é criada automaticamente para testar suplementos do SharePoint com fluxos de trabalho |
| Estatísticas de confiabilidade <br>coletadas automaticamente <br>e outros <br>CEIP (Programas de Aperfeiçoamento da <br>Experiência do Usuário)<br> para o SDK do Azure <br>para Ferramentas do SQL <br><br> | vortex.data.microsoft.com<br> <br>dc.services.visualstudio.com | HTTPS | 443 | Usada para enviar as estatísticas de confiabilidade (dados de travamento ou falha) do usuário à Microsoft. Os despejos de travamento/falha reais ainda serão carregados se o Relatório de Erros do Windows estiver habilitado, apenas informações estatísticas serão suprimidas; <br>Usada para revelar padrões de uso anônimos para a extensão do SDK de Ferramentas do Azure para o Visual Studio e para padrões de uso para ferramentas do SQL para Visual Studio |
| Visual Studio <br> CEIP (Programa de Aperfeiçoamento da <br>Experiência do Usuário) <br><br>PerfWatson.exe | vortex.data.microsoft.com<br>dc.services.visualstudio.com<br>visualstudio-devdiv-c2s.msedge.net<br>az667904.vo.msecnd.net <br>scus-breeziest-in.cloudapp.net<br> | HTTPS | 443 | Usada para coletar logs de erro e padrões de uso anônimos <br><br>Usada para rastrear problemas de congelamento da interface do usuário |
| Criação e<br>Gerenciamento de <br>Recursos do Azure | management.azure.com <br>management.core.windows.net | HTTPS | 443 | Usada para criar sites do Azure ou outros recursos para dar suporte à publicação de aplicativos Web, Azure Functions ou WebJobs |
| Recomendações de <br>extensão e verificações de <br>ferramentas de publicação da Web atualizadas | marketplace.visualstudio.com | HTTPS | 443 | Usada para verificar a disponibilidade de ferramentas de publicação atualizadas. Se desabilitada, uma potencial extensão recomendada para publicação Web poderá não ser mostrada |
| Informações de ponto de extremidade de criação <br>de Recurso do Azure atualizadas | \*.blob.core.windows.net | HTTPS | 443 | Usada para atualizar os pontos de extremidade usados para a criação de Recursos do Azure para determinados Serviços do Azure. Se desabilitada, as últimas localizações de ponto de extremidade baixadas ou inseridas são usadas |
| Depuração remota e <br>Criação de perfil remota de <br>Sites do Azure | &#42;.cloudapp.net <br> &#42;.azurewebsites.net | | 4022 | Usada para anexar o depurador remoto a sites do Azure. Se desabilitada, a anexação do depurador remoto a sites do Azure não funcionará |
| Active Directory <br>Graph | graph.windows.net | HTTPS | 443 | Usada para provisionar novos aplicativos do Azure Active Directory. Também usado pelo provedor de serviço conectado MSGraph do Office 365 |
| Verificação de <br>Atualização de CLI do <br>Azure Functions | functionscdn.azureedge.net | HTTPS | 443 | Usada para verificar as versões atualizadas da CLI do Azure Functions. Se desabilitada, uma cópia armazenada em cache (ou a cópia carregada pelo componente do Azure Functions) da CLI será usada |
| Cordova | npmjs.org<br>gradle.org | http/s | 80/443 | O HTTP é usado para downloads de Gradle durante o build. O HTTPS é usado para incluir plug-ins do Cordova nos projetos |
| Explorador de nuvem | 1. &#60;ponto de extremidade do cluster&#62; <br>Service Fabric <br>2. &#60;ponto de extremidade de gerenciamento&#62;<br>General Cloud Exp <br>3. &#60;ponto de extremidade do grafo&#62;<br>General Cloud Exp<br>4. &#60;ponto de extremidade da conta de armazenamento&#62;<br>Nós de Armazenamento <br>5. &#60;Azure portal URLs&#62;<br>Exp. de nuvem geral <br>6. &#60;pontos de extremidade do key vault&#62; <br>Nós de VM do Azure Resource Manager<br>7. &#60;Endereço de IP pública do cluster&#62;<br>Depuração remota do Service Fabric e Rastreamentos de ETW | <br>1. https<br>2. https<br>3. https<br>4. https<br>5. https<br>6. https<br>7: tcp | 1. 19080<br>2. 443 <br>3. 443 <br>4. 443 <br>5. 443 <br>6. 443 <br>7. dinâmica | 1. Exemplo: test12.eastus.cloudapp.com<br>2. Recupera as assinaturas e recupera/gerencia recursos do Azure<br>3. Recupera assinaturas do Azure Stack<br>4. Gerencia recursos de armazenamento (exemplo: mystorageaccount.blob.core.windows.net)<br>5. Opção do menu de contexto “Abrir no Portal” (Abre um recurso no Portal do Azure)<br>6. Cria e usa cofres de chaves para a depuração de VM (exemplo: myvault.vault.azure.net) <br><br>7. Aloca dinamicamente o bloco de portas com base no número de nós no cluster e as portas disponíveis. <br><br>Um bloco de portas tentará obter três vezes o número dos nós com um mínimo de 10 portas.<br><br>Para rastreamentos de Streaming, é feita uma tentativa para obter o bloco de portas de 810. Se qualquer um dos blocos de portas já estiver em uso, será feita uma tentativa de obter o próximo bloco e assim por diante. (O balanceador de carga está vazio, então as portas de 810 provavelmente serão usadas) <br><br>Da mesma forma para depuração, quatro conjuntos de blocos de portas são reservados: <br>- connectorPort: 30398, <br>- forwarderPort: 31398, <br>- forwarderPortx86: 31399,<br>- fileUploadPort: 32398<br> |
| Serviços de Nuvem | 1. RDP<br><br>2. core.windows.net <br><br>3. management.azure.com<br> management.core.windows.net <br><br>4. &#42;.blob.core.windows.net <br>&#42;.queue.core.windows.net<br>&#42;.table.core.windows.net <br><br>5. portal.azure.com <br><br>6. &#60;serviço de nuvem do usuário&#62;.cloudapp.net <br> &#60;VM do usuário&#62;.&#60;região&#62;.azure.com | 1. rdp <br><br> 2. https <br><br> 3. https <br><br> 4. https <br><br> 5. https <br><br>6. tcp | 1. 3389 <br><br> 2. 443 <br><br> 3. 443 <br><br>4. 443 <br><br>5. 443 <br><br> 6. a) 30398 <br> 6. b) 30400 <br> 6. c) 31398 <br> 6. d) 31400 <br> 6. e) 32398 <br> 6. f) 32400 | 1.  Área de Trabalho Remota com VM de Serviços de Nuvem <br><br> 2.  Componente de conta de armazenamento da configuração de diagnóstico privada <br><br> 3.  Portal do Azure <br><br> 4. Gerenciador de Servidores – Armazenamento do Azure &#42; é a conta de armazenamento nomeada do usuário  <br><br> 5.  Links para abrir o portal &#47; Baixar o certificado de assinatura &#47; Publicar arquivos de configurações <br><br>6. a) Porta local do conector para depuração remota para serviço de nuvem e VM<br> 6. b) Porta pública do conector para depuração remota para serviço de nuvem e VM <br> 6. c) Porta local do encaminhador para depuração remota para serviço de nuvem e VM <br> 6. d) Porta pública do encaminhador para depuração remota para serviço de nuvem e VM  <br> 6. e) Porta local do carregador de arquivos para depuração remota para serviço de nuvem e VM <br> 6. f) Porta pública do carregador de arquivos para depuração remota para serviço de nuvem e VM |
| Service Fabric | 1. <br>ocs.Microsoft.com<br>aka.ms <br>go.microsoft.com <br><br>2. <br>vssftools.blob.core.windows.net <br>Vault.azure.com <br>Portal.azure.com <br><br> 3. &#42; vault.azure.net<br><br> 4. <br>app.vsaex.visualstudio.com<br>&#42; .vsspsext.visualstudio.com<br>clouds.vsrm.visualstudio.com <br>clouds.visualstudio.com<br>app.vssps.visualstudio.com <br>&#42; .visualstudio.com | HTTPS | 443 | 1. Documentação <br><br> 2. Criar o recurso de cluster <br><br>3. O &#42; é o nome do Azure Key Vault (Exemplo: test11220180112110108.vault.azure.net  <br><br>  4. O &#42; é dinâmico (Exemplo: vsspsextprodch1su1.vsspsext.visualstudio.com) |
| Instantâneo <br>Depurador | 1. go.microsoft.com <br>2. management.azure.com <br> 3. &#42;azurewebsites.net <br> 4. &#42;scm.azurewebsites.net<br>5. api.nuget.org/v3/index.json <br>6. msvsmon | 1. https <br>2. https  <br>3. http <br>4. https <br>5. https <br>6. Concord <br> | 1. 443<br> 2. 443<br>3. 80  <br>4. 443<br> 5. 443<br> 6. 4022 (dependente da versão do Visual Studio) | 1. Consultar arquivo .json para o tamanho do SKU do serviço de aplicativo <br>2. Várias chamadas do RM do Azure <br>3. Chamada de aquecimento do site por meio de  <br>4. Ponto de extremidade Kudu do Serviço de Aplicativo de destino do cliente <br>5. Consultar versão da Extensão de Site publicada em nuget.org <br>6. Canal de depuração remota |
| Azure Stream Analytics <br><br>HDInsight | Management.azure.com | HTTPS | 443 | Usada para exibir, enviar, executar e gerenciar trabalhos ASA <br><br> Usada para navegar em clusters HDI e enviar, diagnosticar e depurar trabalhos HDI |
| Azure Data Lake | &#42;.azuredatalakestore.net <br>&#42;.azuredatalakeanalytics.net | HTTPS | 443 | Usada para compilar, enviar, exibir, diagnosticar e depurar os trabalhos, usada para navegar em arquivos ADLS, usada para carregar e baixar arquivos |
| Empacotar serviço | [conta].visualstudio.com <br/> [conta].\*.visualstudio.com <br/> \*.blob.core.windows.net <br/> registry.npmjs.org </br> nodejs.org <br/> dist.nuget.org <br/> nuget.org | HTTPS | 443 | \*.npmjs.org, \*.nuget.org e \*.nodejs.org são necessários somente para determinados cenários de tarefas de build (por exemplo: instalador de ferramentas do NuGet, instalador de ferramenta de nós) ou se você desejar usar upstreams públicos com os Feeds. Os outros três domínios são necessários para a funcionalidade principal do serviço de empacotamento. |
| Azure DevOps Services | \*.vsassets.io <br/> static2.sharepointonline.com | | | Usado para conectar-se ao Azure DevOps Services |
| | | | | |

## <a name="troubleshoot-network-related-errors"></a>Solucionar problemas de erros relacionados à rede

Às vezes, você pode encontrar erros relacionados à rede ou ao proxy ao instalar ou usar o Visual Studio atrás de um firewall ou servidor proxy. Para obter mais informações sobre as soluções para essas mensagens de erro, consulte a página [Solução de erros relacionados à rede ao instalar ou usar o Visual Studio](troubleshooting-network-related-errors-in-visual-studio.md).

## <a name="get-support"></a>Obter suporte

Oferecemos uma opção de suporte por [**chat ao vivo**](https://visualstudio.microsoft.com/vs/support/#talktous) (somente em inglês) para problemas relacionados à instalação.

Aqui estão algumas outras opções de suporte:

* Relate problemas do produto para nós por meio da ferramenta [Relatar um Problema](../ide/how-to-report-a-problem-with-visual-studio-2017.md), exibida no Instalador do Visual Studio e no IDE do Visual Studio.
* Sugira um recurso, acompanhe os problemas do produto e encontre respostas na [Comunidade de Desenvolvedores do Visual Studio](https://developercommunity.visualstudio.com/).
* Use sua conta do [GitHub](https://github.com/) para falar conosco e com outros desenvolvedores do Visual Studio nas [conversas sobre o Visual Studio na comunidade do Gitter](https://gitter.im/Microsoft/VisualStudio).

## <a name="see-also"></a>Consulte também

* [Criar uma instalação de rede do Visual Studio](create-a-network-installation-of-visual-studio.md)
* [Solução de erros relacionados à rede no Visual Studio](troubleshooting-network-related-errors-in-visual-studio.md)
* [Guia do administrador do Visual Studio](visual-studio-administrator-guide.md)
* [Instalar por trás de um firewall ou de um servidor proxy (Visual Studio para Mac)](/visualstudio/mac/install-behind-a-firewall-or-proxy-server)