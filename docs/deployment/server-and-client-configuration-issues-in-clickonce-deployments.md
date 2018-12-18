---
title: Servidor e problemas de configuração de cliente em implantações do ClickOnce | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-deployment
ms.topic: conceptual
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- deploying applications, ClickOnce
- troubleshooting ClickOnce deployments
- ClickOnce deployment, troubleshooting
- Windows applications, ClickOnce deployments
ms.assetid: 929e5fcc-dd56-409c-bb57-00bd9549b20b
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 444cfa375fd4e2059ddf6458224836cdec6ff18f
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49849421"
---
# <a name="server-and-client-configuration-issues-in-clickonce-deployments"></a>Problemas de configuração de servidor e cliente em implantações do ClickOnce
Se você usar os serviços de informações da Internet (IIS) no Windows Server, e sua implantação contém um tipo de arquivo que o Windows não reconhecem, como um arquivo do Microsoft Word, o IIS se recusará a transmitir esse arquivo e sua implantação não terá êxito.  

 Além disso, alguns servidores Web e Web software de aplicativo, como [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)], contêm uma lista de arquivos e tipos de arquivos que não é possível baixar. Por exemplo, [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] impede o download de todos os *Web. config* arquivos. Esses arquivos podem conter informações confidenciais como nomes de usuário e senhas.  

 Embora essa restrição não deve causar problemas para o download de núcleo [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] arquivos como manifestos e assemblies, essa restrição pode impedir que você baixe arquivos de dados incluídos como parte do seu [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] aplicativo. No [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)], você pode resolver esse erro ao remover o manipulador que proíbe o download desses arquivos de configuração no Gerenciador do IIS. Consulte a documentação do servidor IIS para obter mais detalhes.  

 Alguns servidores Web podem bloquear os arquivos com extensões como *. dll*, *. config*, e *arquivos. mdf*. Aplicativos baseados no Windows geralmente incluem arquivos com algumas destas extensões. Se um usuário tenta executar um [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] aplicativo que acessa um arquivo bloqueado em um servidor Web, ocorrerá um erro. Em vez de todas as extensões de arquivo, o desbloqueio [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] publica todos os arquivos de aplicativo com um *Deploy* extensão de arquivo por padrão. Portanto, o administrador precisa apenas configurar o servidor Web para desbloquear as seguintes extensões de arquivo de três:  

- *. Application*  

- *. manifest*  

- *. Deploy* 

  No entanto, você poderá desabilitar essa opção desmarcando os **usar a extensão de arquivo. Deploy"** opção a [caixa de diálogo Opções de publicação](/previous-versions/visualstudio/visual-studio-2010/7z83t16a(v=vs.100)), nesse caso, você deve configurar o servidor Web para desbloquear todas as extensões de arquivo usado no aplicativo.  

  Você terá que configurar *. manifest*, *. Application*, e *Deploy*, por exemplo, se você estiver usando o IIS em que você não tiver instalado o [!INCLUDE[dnprdnshort](../code-quality/includes/dnprdnshort_md.md)], ou se você estiver usando outro servidor Web (por exemplo, Apache).  

## <a name="clickonce-and-secure-sockets-layer-ssl"></a>ClickOnce e Secure Sockets Layer (SSL)  
 Um [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] aplicativo funcionará bem por SSL, exceto quando o Internet Explorer gera um aviso sobre o certificado SSL. O prompt pode ser gerado quando há algo errado com o certificado, tais como quando os nomes de site não coincidem ou o certificado expirou. Para tornar [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] trabalha em uma conexão SSL, certifique-se de que o certificado esteja atualizado e que os dados do certificado coincide com os dados do site.  

## <a name="clickonce-and-proxy-authentication"></a>Autenticação de proxy e ClickOnce  
 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] fornece suporte para a autenticação integrada do Windows do proxy a partir do .NET Framework 3.5. Não há diretivas específicas Machine. config são necessárias. [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] não oferece suporte para outros protocolos de autenticação como Basic ou Digest.  

 Você também pode aplicar um hotfix para .NET Framework 2.0 para habilitar esse recurso. Para obter mais informações, consulte http://go.microsoft.com/fwlink/?LinkId=158730.  

 Para obter mais informações, consulte [ \<defaultProxy > (configurações de rede)](/dotnet/framework/configure-apps/file-schema/network/defaultproxy-element-network-settings).  

## <a name="clickonce-and-web-browser-compatibility"></a>Compatibilidade de navegadores da Web e de ClickOnce  
 Atualmente, [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] instalações iniciará somente se a URL para o manifesto de implantação é aberta usando o Internet Explorer. Uma implantação cuja URL é iniciado a partir de outro aplicativo, como o Microsoft Office Outlook, será iniciado com êxito apenas se o Internet Explorer está definido como o navegador da Web padrão.  

> [!NOTE]
>  Mozilla Firefox é suportado se o provedor de implantação não está em branco ou a extensão do Assistente do Microsoft .NET Framework está instalada. Essa extensão é empacotada com o .NET Framework 3.5 SP1. Para obter suporte XBAP, o plug-in de NPWPF é ativado quando necessário.  

## <a name="activate-clickonce-applications-through-browser-scripting"></a>Ativar aplicativos ClickOnce por meio de scripts de navegador  
 Se você tiver desenvolvido uma página da Web personalizada que inicia um [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] aplicativo usando o script ativo, você pode achar que o aplicativo não será iniciado em alguns computadores. Internet Explorer contém uma configuração chamada **aviso automático para downloads de arquivo**, que afeta esse comportamento. Essa configuração está disponível na **segurança** guia no seu **opções** menu que afeta esse comportamento. Ele é chamado **aviso automático para downloads de arquivo**, e ele é listado sob os **Downloads** categoria. A propriedade é definida como **habilitar** por padrão para páginas da Web de intranet e para **desabilitar** por padrão para páginas da Web da Internet. Quando essa configuração é definida como **desabilitar**, qualquer tentativa de ativar um [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] aplicativo por meio de programação (por exemplo, atribuindo sua URL para o `document.location` propriedade) serão bloqueados. Nestas circunstâncias, os usuários podem iniciar aplicativos por meio de um download iniciado pelo usuário, por exemplo, ao clicar em um hiperlink definido como a URL do aplicativo.  

## <a name="additional-server-configuration-issues"></a>Problemas de configuração de servidor adicionais  

##### <a name="administrator-permissions-required"></a>Permissões de administrador necessárias  
 Você deve ter permissões de administrador no servidor de destino, se você estiver publicando com HTTP. IIS exige esse nível de permissões. Se você não estiver publicando usando HTTP, você só precisa de permissão de gravação no caminho de destino.  

##### <a name="server-authentication-issues"></a>Problemas de autenticação de servidor  
 Quando você publica em um servidor remoto que tem "Acesso anônimo" desativado, você receberá o seguinte aviso:  

```  
"The files could not be downloaded from http://<remoteserver>/<myapplication>/.  The remote server returned an error: (401) Unauthorized."  
```  

> [!NOTE]
>  Você pode fazer com que a autenticação NTLM (NT desafio-resposta) funcionará se o site solicita as credenciais que não seja de suas credenciais padrão e, na caixa de diálogo de segurança, clique em **Okey** quando for perguntado se você quiser salvar fornecido credenciais para sessões futuras. No entanto, essa solução alternativa não funcionará para a autenticação básica.  

## <a name="use-third-party-web-servers"></a>Usar servidores de Web de terceiros  
 Se você estiver implantando um [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] aplicativo de um servidor Web que não seja o IIS, você poderá ter um problema se o servidor está retornando o tipo de conteúdo incorreto para a chave [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] arquivos, como o manifesto de implantação e o manifesto do aplicativo. Para resolver esse problema, consulte a Ajuda da seu servidor Web documentação sobre como adicionar novos tipos de conteúdo para o servidor e certifique-se de que todos os mapeamentos de extensão de nome arquivo listado na tabela a seguir estão em vigor.  

|Extensão de nome de arquivo|Tipo de conteúdo|  
|-------------------------|------------------|  
|`.application`|`application/x-ms-application`|  
|`.manifest`|`application/x-ms-manifest`|  
|`.deploy`|`application/octet-stream`|  
|`.msu`|`application/octet-stream`|  
|`.msp`|`application/octet-stream`|  

## <a name="clickonce-and-mapped-drives"></a>ClickOnce e unidades mapeadas  
 Se você usar o Visual Studio para publicar um aplicativo ClickOnce, é possível especificar uma unidade mapeada como o local de instalação. No entanto, você pode modificar o aplicativo ClickOnce para instalar de uma unidade mapeada, usando o Editor (Mage.exe e MageUI.exe) e o gerador de manifesto. Para obter mais informações, consulte [Mage.exe (Manifest Generation and Editing Tool)](/dotnet/framework/tools/mage-exe-manifest-generation-and-editing-tool) e [MageUI.exe (Manifest Generation and Editing Tool, cliente gráfico)](/dotnet/framework/tools/mageui-exe-manifest-generation-and-editing-tool-graphical-client).  

## <a name="ftp-protocol-not-supported-for-installing-applications"></a>Protocolo FTP não tem suportado para a instalação de aplicativos  
 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] dá suporte à instalação de aplicativos de qualquer servidor da Web HTTP 1.1 ou o servidor de arquivos. Não há suporte para FTP, o protocolo de transferência de arquivo, para instalar aplicativos. Você pode usar o FTP para publicar aplicativos somente. A tabela a seguir resume essas diferenças:  


| Tipo de URL | Descrição |
|----------| - |
| FTP: / / | Você pode publicar um [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] aplicativo usando esse protocolo. |
| http:// | Você pode instalar um [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] aplicativo usando esse protocolo. |
| https:// | Você pode instalar um [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] aplicativo usando esse protocolo. |
| file:// | Você pode instalar um [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] aplicativo usando esse protocolo. |

## <a name="windows-xp-sp2-windows-firewall"></a>Windows XP SP2: Firewall de Windows  
 Por padrão, o Windows XP SP2 habilita o Firewall do Windows. Se você estiver desenvolvendo seu aplicativo em um computador com Windows XP instalado, é ainda possível publicar e executar [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] aplicativos do servidor local que está executando o IIS. No entanto, você não pode acessar o servidor que está executando o IIS de outro computador, a menos que você abrir o Firewall do Windows. Consulte a Ajuda do Windows para obter instruções sobre como gerenciar o Firewall do Windows.  

## <a name="windows-server-enable-frontpage-server-extensions"></a>Windows Server: Habilitar extensões FrontPage server extensions  
 Extensões de servidor do FrontPage da Microsoft é necessária para publicar aplicativos para um servidor Web do Windows que usa o HTTP.  

 Por padrão, o Windows Server não tem instalado extensões FrontPage Server Extensions. Se você quiser usar [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] para publicar em um servidor Web do Windows Server que usa HTTP com o FrontPage Server Extensions, você deve instalar extensões FrontPage Server Extensions primeiro. Você pode executar a instalação usando a ferramenta de administração de gerenciar o servidor no Windows Server.  

## <a name="windows-server-locked-down-content-types"></a>Windows Server: Tipos de conteúdo de bloqueada  
 IIS no [!INCLUDE[WinXPSvr](../debugger/includes/winxpsvr_md.md)] bloqueará todos os tipos de arquivo, exceto para determinados tipos de conteúdo conhecidos (por exemplo, *. htm*, *. HTML*, *. txt*e assim por diante). Para habilitar a implantação do [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] aplicativos que usam esse servidor, você precisa alterar as configurações do IIS para permitir o download de arquivos do tipo *. Application*, *. manifest*e outros tipos de arquivo personalizado usado pelo seu aplicativo.  

 Se você implantar usando um servidor IIS, execute *inetmgr.exe* e adicionar novos tipos de arquivo da página da Web padrão:  

- Para o *. Application* e *. manifest* extensões, o tipo de MIME deve ser "application/x-ms-application." Para outros tipos de arquivo, o tipo MIME deve ser "application/octet-stream".  

- Se você criar um tipo de MIME com a extensão "<em>" e o tipo MIME "application/octet-stream", ele permitirá arquivos desbloqueado do tipo de arquivo a ser baixado. (No entanto, bloqueados tipos de arquivo como *. aspx</em> e *asmx* não pode ser baixado.)  

  Para obter instruções específicas sobre como configurar tipos de MIME no Windows Server, consulte o artigo da Base de Conhecimento Microsoft KB326965, "IIS 6.0 não atender os tipos de MIME desconhecidos" na [ http://support.microsoft.com/default.aspx?scid=kb; en-us; 326965](http://support.microsoft.com/default.aspx?scid=kb;en-us;326965).  

## <a name="content-type-mappings"></a>Mapeamentos de tipo de conteúdo  
 Ao publicar por meio de HTTP, o tipo de conteúdo (também conhecido como o tipo MIME) para o *. Application* arquivo deve ser "application/x-ms-application." Se você tiver [!INCLUDE[dnprdnlong](../code-quality/includes/dnprdnlong_md.md)] instalado no servidor, isso será definido para você automaticamente. Se isso não estiver instalado, você precisa criar uma associação de tipo MIME para o [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] vroot do aplicativo (ou todo o servidor).  

 Se você implantar usando um servidor IIS, execute <em>inetmgr.</em> exe e adicione um novo tipo de conteúdo de "application/x-ms-application" para o *. Application* extensão.  

## <a name="http-compression-issues"></a>Problemas de compactação HTTP  
 Com [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)], você pode executar downloads que usam a compactação HTTP, uma tecnologia de servidor da Web que usa o algoritmo GZIP para compactar um fluxo de dados antes de enviar o fluxo para o cliente. O cliente — nesse caso, [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)]— descompacta o fluxo antes de ler os arquivos.  

 Se você estiver usando o IIS, você pode facilmente habilitar a compactação HTTP. No entanto, quando você habilita a compactação HTTP, ele é apenas habilitado para determinados tipos de arquivo — ou seja, arquivos HTML e texto. Para habilitar a compactação para assemblies (*. dll*), XML (*. XML*), manifestos de implantação (*Application*) e os manifestos de aplicativo (*. manifest*), você deve adicionar esses tipos à lista de tipos para o IIS compactar de arquivos. Até que você adicione os tipos de arquivo para sua implantação, apenas arquivos de texto e HTML serão compactados.  

 Para obter instruções detalhadas para o IIS, consulte [como especificar tipos de documento adicionais para a compactação HTTP](http://go.microsoft.com/fwlink/?LinkId=178459).  

## <a name="see-also"></a>Consulte também  
 [Solucionar problemas de implantações do ClickOnce](../deployment/troubleshooting-clickonce-deployments.md)   
 [Escolher uma estratégia de implantação do ClickOnce](../deployment/choosing-a-clickonce-deployment-strategy.md)   
 [Pré-requisitos de implantação do aplicativo](../deployment/application-deployment-prerequisites.md)