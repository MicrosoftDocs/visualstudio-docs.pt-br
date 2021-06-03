---
title: Problemas de configuração do servidor/cliente (ClickOnce)
description: Saiba mais sobre problemas de configuração de servidor e cliente que podem afetar a implantação do seu aplicativo ClickOnce.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
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
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 9f0361816d0621f52e9f95f4159dd0d46f4f5951
ms.sourcegitcommit: f50bbdb15c4f9fca0fa245ca765183c378960cc5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/03/2021
ms.locfileid: "111352001"
---
# <a name="server-and-client-configuration-issues-in-clickonce-deployments"></a>Problemas de configuração de servidor e cliente em implantações do ClickOnce
Se você usar o Serviços de Informações da Internet (IIS) no Windows Server e sua implantação contiver um tipo de arquivo que o Windows não reconhece, como um arquivo do Microsoft Word, o IIS se recusará a transmitir esse arquivo e sua implantação não terá sucesso.

 Além disso, alguns servidores Web e software de aplicativos Web, como [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] , contêm uma lista de arquivos e tipos de arquivos que você não pode baixar. Por exemplo, [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] impede o download de todos os arquivos de *Web.config* . Esses arquivos podem conter informações confidenciais, como nomes de usuário e senhas.

 Embora essa restrição não possa causar problemas de download de arquivos de núcleo, como [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] manifestos e assemblies, essa restrição pode impedi-lo de baixar arquivos de dados incluídos como parte do seu [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] aplicativo. No [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] , você pode resolver esse erro removendo o manipulador que proíbe o download desses arquivos do Gerenciador de configurações do IIS. Consulte a documentação do servidor IIS para obter detalhes adicionais.

 Alguns servidores Web podem bloquear arquivos com extensões como *.dll*, *.config* e *. MDF*. Aplicativos baseados em Windows normalmente incluem arquivos com algumas dessas extensões. Se um usuário tentar executar um [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] aplicativo que acessa um arquivo bloqueado em um servidor Web, ocorrerá um erro. Em vez de desbloquear todas as extensões de arquivo, [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] o publica cada arquivo de aplicativo com uma extensão de arquivo *. Deploy* por padrão. Portanto, o administrador só precisa configurar o servidor Web para desbloquear as três extensões de arquivo a seguir:

- *. aplicativo*

- *. manifest*

- *. implantar*

  No entanto, você pode desabilitar essa opção desmarcando a opção de **extensão de arquivo use ". Deploy"** na [caixa de diálogo opções de publicação](/previous-versions/visualstudio/visual-studio-2010/7z83t16a(v=vs.100)). nesse caso, você deve configurar o servidor Web para desbloquear todas as extensões de arquivo usadas no aplicativo.

  Você precisará configurar o *. manifest*, o *. Application* e o *. Deploy*, por exemplo, se você estiver usando o IIS em que você não instalou o .NET Framework, ou se estiver usando outro servidor Web (por exemplo, Apache).

## <a name="clickonce-and-secure-sockets-layer-ssl"></a>ClickOnce e protocolo SSL (SSL)
 Um [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] aplicativo funcionará bem em SSL, exceto quando o Internet Explorer emitir um prompt sobre o certificado SSL. O prompt pode ser gerado quando há algo errado com o certificado, como quando os nomes de site não coincidem ou o certificado expirou. Para fazer [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] o trabalho em uma conexão SSL, verifique se o certificado está atualizado e se os dados do certificado correspondem aos dados do site.

## <a name="clickonce-and-proxy-authentication"></a>Autenticação de proxy e ClickOnce
 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] fornece suporte para autenticação de proxy integrado do Windows a partir do .NET Framework 3,5. Nenhuma diretivas de machine.config específicas são necessárias. [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] o não fornece suporte para outros protocolos de autenticação, como Basic ou Digest.

 Você também pode aplicar um hotfix para .NET Framework 2,0 para habilitar esse recurso. Para obter mais informações, consulte [corrigir: mensagem de erro ao tentar instalar um aplicativo ClickOnce criado no .NET Framework 2,0 em um computador cliente configurado para usar um servidor proxy: "autenticação de proxy necessária"](https://support.microsoft.com/help/917952/fix-error-message-when-you-try-to-install-a-clickonce-application-that).

 Para obter mais informações, consulte [ \<defaultProxy> elemento (configurações de rede)](/dotnet/framework/configure-apps/file-schema/network/defaultproxy-element-network-settings).

## <a name="clickonce-and-web-browser-compatibility"></a>Compatibilidade de navegador da Web e ClickOnce
 Atualmente, as [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] instalações serão iniciadas somente se a URL para o manifesto de implantação for aberta usando o Internet Explorer. Uma implantação cuja URL é iniciada de outro aplicativo, como Microsoft Office Outlook, será iniciada com êxito somente se o Internet Explorer estiver definido como o navegador da Web padrão.

> [!NOTE]
> O Mozilla Firefox terá suporte se o provedor de implantação não estiver em branco ou se a extensão do assistente do Microsoft .NET Framework estiver instalada. Essa extensão é empacotada com .NET Framework 3,5 SP1. Para suporte a XBAP, o plug-in NPWPF é ativado quando necessário.

## <a name="activate-clickonce-applications-through-browser-scripting"></a>Ativar aplicativos ClickOnce por meio de scripts de navegador
 Se você tiver desenvolvido uma página da Web personalizada que inicia um [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] aplicativo usando o script ativo, talvez você ache que o aplicativo não será iniciado em alguns computadores. O Internet Explorer contém uma configuração chamada **solicitação automática para downloads de arquivos**, que afeta esse comportamento. Essa configuração está disponível na guia **segurança** no menu de **Opções** que afeta esse comportamento. Ele é chamado de **solicitação automática de downloads de arquivos** e é listado abaixo da categoria de **downloads** . A propriedade é definida como **habilitar** por padrão para páginas da Web da intranet e para **desabilitar** por padrão para páginas da Web da Internet. Quando essa configuração é definida como **desabilitar**, qualquer tentativa de ativar um [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] aplicativo programaticamente (por exemplo, atribuindo sua URL à `document.location` Propriedade) será bloqueada. Sob essa circunstância, os usuários podem iniciar aplicativos somente por meio de um download iniciado pelo usuário, por exemplo, clicando em um hiperlink definido para a URL do aplicativo.

## <a name="additional-server-configuration-issues"></a>Problemas de configuração de servidor adicionais

##### <a name="administrator-permissions-required"></a>Permissões de administrador necessárias
 Você deve ter permissões de administrador no servidor de destino se estiver publicando com HTTP. O IIS requer esse nível de permissões. Se você não estiver publicando usando HTTP, precisará apenas da permissão de gravação no caminho de destino.

##### <a name="server-authentication-issues"></a>Problemas de autenticação do servidor
 Quando você publicar em um servidor remoto que tem "acesso anônimo" desativado, receberá o seguinte aviso:

```
"The files could not be downloaded from http://<remoteserver>/<myapplication>/.  The remote server returned an error: (401) Unauthorized."
```

> [!NOTE]
> Você pode fazer com que a autenticação NTLM (NT Challenge-Response) funcione se o site solicitar credenciais que não sejam suas credenciais padrão e, na caixa de diálogo Segurança, você clicar em **OK** quando for solicitado se quiser salvar as credenciais fornecidas para futuras sessões. No entanto, essa solução alternativa não funcionará para a autenticação básica.

## <a name="use-third-party-web-servers"></a>Usar servidores Web de terceiros
 Se você estiver implantando um [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] aplicativo de um servidor Web que não seja o IIS, poderá ocorrer um problema se o servidor estiver retornando o tipo de conteúdo incorreto para arquivos de chave [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] , como o manifesto de implantação e o manifesto do aplicativo. Para resolver esse problema, consulte a documentação da ajuda do seu servidor Web sobre como adicionar novos tipos de conteúdo ao servidor e verifique se todos os mapeamentos de extensão de nome de arquivo listados na tabela a seguir estão em vigor.

|Extensão de nome de arquivo|Tipo de conteúdo|
|-------------------------|------------------|
|`.application`|`application/x-ms-application`|
|`.manifest`|`application/x-ms-manifest`|
|`.deploy`|`application/octet-stream`|
|`.msu`|`application/octet-stream`|
|`.msp`|`application/octet-stream`|

## <a name="clickonce-and-mapped-drives"></a>ClickOnce e unidades mapeadas
 Se você usar o Visual Studio para publicar um aplicativo ClickOnce, não poderá especificar uma unidade mapeada como o local de instalação. No entanto, você pode modificar o aplicativo ClickOnce para instalar a partir de uma unidade mapeada usando o gerador e o editor de manifesto (Mage.exe e MageUI.exe). Para obter mais informações, consulte [Mage.exe (manifest Generation and Editing Tool)](/dotnet/framework/tools/mage-exe-manifest-generation-and-editing-tool) e [MageUI.exe (manifest Generation and Editing Tool, cliente gráfico)](/dotnet/framework/tools/mageui-exe-manifest-generation-and-editing-tool-graphical-client).

## <a name="ftp-protocol-not-supported-for-installing-applications"></a>Protocolo FTP sem suporte para instalar aplicativos
 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] oferece suporte à instalação de aplicativos de qualquer servidor Web HTTP 1,1 ou servidor de arquivos. O FTP, o protocolo FTP, não tem suporte para instalar aplicativos. Você pode usar o FTP para publicar somente aplicativos. A tabela a seguir resume essas diferenças:

| Tipo de URL | Descrição |
|----------| - |
| ftp:// | Você pode publicar um [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] aplicativo usando esse protocolo. |
| http:// | Você pode instalar um [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] aplicativo usando esse protocolo. |
| https:// | Você pode instalar um [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] aplicativo usando esse protocolo. |
| file:// | Você pode instalar um [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] aplicativo usando esse protocolo. |

## <a name="windows-xp-sp2-windows-firewall"></a>Windows XP SP2: Firewall do Windows
 Por padrão, o Windows XP SP2 habilita o Firewall do Windows. Se você estiver desenvolvendo seu aplicativo em um computador com o Windows XP instalado, ainda poderá publicar e executar [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] aplicativos do servidor local que está executando o IIS. No entanto, você não pode acessar esse servidor que está executando o IIS de outro computador, a menos que você abra o Firewall do Windows. Consulte a ajuda do Windows para obter instruções sobre como gerenciar o Firewall do Windows.

## <a name="windows-server-enable-frontpage-server-extensions"></a>Windows Server: habilitar extensões de servidor do FrontPage
 As extensões de servidor do FrontPage da Microsoft são necessárias para publicar aplicativos em um servidor Web do Windows que usa HTTP.

 Por padrão, o Windows Server não tem as extensões de servidor do FrontPage instaladas. Se você quiser usar [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] o para publicar em um servidor Web do Windows Server que usa http com extensões de servidor do FrontPage, deverá instalar primeiro as extensões de servidor do FrontPage. Você pode executar a instalação usando a ferramenta gerenciar sua administração de servidor no Windows Server.

## <a name="windows-server-locked-down-content-types"></a>Windows Server: tipos de conteúdo bloqueados
 O IIS em [!INCLUDE[WinXPSvr](../debugger/includes/winxpsvr_md.md)] bloqueia todos os tipos de arquivo, exceto para determinados tipos de conteúdo conhecidos (por exemplo, *.htm*, *.html*, *.txt* e assim por diante). Para habilitar a implantação de [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] aplicativos usando esse servidor, você precisa alterar as configurações do IIS para permitir o download de arquivos do tipo *. Application*, *. manifest* e de qualquer outro tipo de arquivo personalizado usado pelo seu aplicativo.

 Se você implantar usando um servidor IIS, execute *inetmgr.exe* e adicione novos tipos de arquivo para a página da Web padrão:

- Para as extensões *. Application* e *. manifest* , o tipo MIME deve ser "application/x-MS-Application". Para outros tipos de arquivo, o tipo MIME deve ser "application/octet-stream".

- Se você criar um tipo MIME com a extensão " \<em> " e o tipo MIME "application/octet-stream", ele permitirá que os arquivos de tipo de arquivo desbloqueado sejam baixados. (No entanto, os tipos de arquivo bloqueados, como *\* . aspx* e *\* . asmx* , não podem ser baixados.)

  Para obter instruções específicas sobre como configurar tipos MIME no Windows Server, consulte [como adicionar um tipo de MIME a um site ou aplicativo da Web](/iis/configuration/system.webserver/staticcontent/mimemap#how-to-add-a-mime-type-to-a-web-site-or-application).

## <a name="content-type-mappings"></a>Mapeamentos de tipo de conteúdo
 Ao publicar por HTTP, o tipo de conteúdo (também conhecido como tipo MIME) para o arquivo *. Application* deve ser "application/x-MS-Application". Se você tiver .NET Framework 2,0 instalado no servidor, isso será definido para você automaticamente. Se não estiver instalado, você precisará criar uma associação de tipo MIME para o [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] aplicativo vroot (ou servidor inteiro).

 Se você implantar usando um servidor IIS, execute <em>inetmgr.</em> exe e adicione um novo tipo de conteúdo de "application/x-MS-Application" para a extensão *. Application* .

## <a name="http-compression-issues"></a>Problemas de compactação de HTTP
 Com [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] o, você pode executar downloads que usam a compactação HTTP, uma tecnologia de servidor Web que usa o algoritmo gzip para compactar um fluxo de dados antes de enviar o fluxo para o cliente. O cliente — nesse caso, [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] — descompacta o fluxo antes de ler os arquivos.

 Se você estiver usando o IIS, poderá habilitar facilmente a compactação HTTP. No entanto, quando você habilita a compactação HTTP, ela só é habilitada para determinados tipos de arquivo, ou seja, HTML e arquivos de texto. Para habilitar a compactação para assemblies (*.dll*), XML (*.xml*), manifestos de implantação (*. Application*) e manifestos de aplicativo (*. manifest*), você deve adicionar esses tipos de arquivo à lista de tipos para que o IIS seja compactado. Até que você adicione os tipos de arquivo à sua implantação, somente arquivos de texto e HTML serão compactados.

 Para obter instruções detalhadas sobre o IIS, consulte [como especificar tipos de documento adicionais para a compactação http](/troubleshoot/iis/content-types-http-compression).

## <a name="see-also"></a>Confira também
- [Solucionar problemas de implantações do ClickOnce](../deployment/troubleshooting-clickonce-deployments.md)
- [Escolher uma estratégia de implantação do ClickOnce](../deployment/choosing-a-clickonce-deployment-strategy.md)
- [Pré-requisitos de implantação do aplicativo](../deployment/application-deployment-prerequisites.md)
