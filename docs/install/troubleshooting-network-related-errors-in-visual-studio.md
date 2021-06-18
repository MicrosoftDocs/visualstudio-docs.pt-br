---
title: Solução de erros relacionados à rede ou ao proxy
description: Encontre soluções para erros relacionados à rede ou ao proxy que você pode encontrar ao instalar ou usar o Visual Studio por trás de um firewall ou um servidor proxy.
ms.date: 10/29/2019
ms.topic: troubleshooting
helpviewer_keywords:
- network installation, Visual Studio
- administrator guide, Visual Studio
- installing Visual Studio, administrator guide
- list of domains, locations, URLs, Visual Studio
- proxy errors, Visual Studio
ms.assetid: ''
author: j-martens
ms.author: jmartens
manager: jmartens
ms.workload:
- multiple
ms.prod: visual-studio-windows
ms.technology: vs-installation
ms.openlocfilehash: 5e7d54b4e7777b3569031e96760699e7c075245f
ms.sourcegitcommit: 5fb4a67a8208707e79dc09601e8db70b16ba7192
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2021
ms.locfileid: "112306820"
---
# <a name="troubleshoot-network-related-errors-when-you-install-or-use-visual-studio"></a>Solucionar erros relacionados à rede ao instalar ou usar o Visual Studio

Temos soluções para os erros mais comuns relacionadas à rede ou ao proxy que você pode encontrar ao instalar ou usar o Visual Studio atrás de um firewall ou um servidor proxy.

## <a name="error-proxy-authorization-required"></a>Erro: “Autorização de proxy necessária”

Esse erro geralmente ocorre quando os usuários estão conectados à Internet por meio de um servidor proxy e o servidor proxy bloqueia as chamadas que o Visual Studio faz para alguns recursos de rede.

### <a name="to-fix-this-proxy-error"></a>Para corrigir esse erro de proxy

- Reinicie o Visual Studio. Uma caixa de diálogo de autenticação de proxy deverá aparecer. Insira suas credenciais na caixa de diálogo quando solicitado.

- Se reiniciar o Visual Studio não resolver o problema, talvez o servidor proxy não solicite credencias para endereços http:&#47;&#47;go.microsoft.com, mas solicite para endereços &#42;.visualStudio.microsoft.com. Para esses servidores, considere adicionar as seguintes URLs a uma lista de permissões para desbloquear todos os cenários de conexão no Visual Studio:

  - &#42;.windows.net

  - &#42;.microsoftonline.com

  - &#42;.visualstudio.microsoft.com

  - &#42;.microsoft.com

  - &#42;.live.com

- Caso contrário, você pode remover o endereço de http:&#47;&#47;go.microsoft.com da lista de permissões para que a caixa de diálogo de autenticação de proxy apareça tanto para o endereço http:&#47;&#47;go.microsoft.com quanto para os pontos de extremidade do servidor quando o Visual Studio for reiniciado.

  -OU-

- Se você quiser usar suas credenciais padrão com o proxy, poderá realizar as seguintes ações:

::: moniker range="vs-2017"

  1. Localize **devenv.exe.config** (o arquivo de configuração devenv.exe) em: **%ProgramFiles%\Microsoft Visual Studio\2017\Enterprise\Common7\IDE** ou em **%ProgramFiles(x86)%\Microsoft Visual Studio\2017\Enterprise\Common7\IDE**.

  2. No arquivo de configuração, localize o bloco `<system.net>` e adicione esse código:

      ```xml
      <defaultProxy enabled="true" useDefaultCredentials="true">
          <proxy bypassonlocal="True" proxyaddress="http://<yourproxy:port#>"/>
      </defaultProxy>
      ```

      Você deve inserir o endereço de proxy correto para sua rede na `proxyaddress="<http://<yourproxy:port#>`.

     > [!NOTE]
     > Para obter mais informações, consulte as páginas de elemento [ &lt; defaultProxy &gt; (configurações de rede)](/dotnet/framework/configure-apps/file-schema/network/defaultproxy-element-network-settings/) e [ &lt; &gt; elemento proxy (configurações de rede)](/dotnet/framework/configure-apps/file-schema/network/proxy-element-network-settings) .

::: moniker-end

::: moniker range=">=vs-2019"

  1. Localize **devenv.exe.config** (o arquivo de configuração devenv.exe) em: **%ProgramFiles%\Microsoft Visual Studio\2019\Enterprise\Common7\IDE** ou em **%ProgramFiles(x86)%\Microsoft Visual Studio\2019\Enterprise\Common7\IDE**.

  2. No arquivo de configuração, localize o bloco `<system.net>` e adicione esse código:

      ```xml
      <defaultProxy enabled="true" useDefaultCredentials="true">
          <proxy bypassonlocal="True" proxyaddress="http://<yourproxy:port#>"/>
      </defaultProxy>
      ```

      Você deve inserir o endereço de proxy correto para sua rede na `proxyaddress="<http://<yourproxy:port#>`.

     > [!NOTE]
     > Para obter mais informações, consulte as páginas de elemento [ &lt; defaultProxy &gt; (configurações de rede)](/dotnet/framework/configure-apps/file-schema/network/defaultproxy-element-network-settings/) e [ &lt; &gt; elemento proxy (configurações de rede)](/dotnet/framework/configure-apps/file-schema/network/proxy-element-network-settings) .

::: moniker-end

## <a name="error-disconnected-from-visual-studio-when-attempting-to-report-a-problem"></a>Erro: "desconectado do Visual Studio" ao tentar relatar um problema

Esse erro geralmente ocorre quando um usuário está conectado à Internet por meio de um servidor proxy, e o servidor proxy bloqueia as chamadas que o Visual Studio faz para alguns recursos de rede.

### <a name="to-fix-this-proxy-error"></a>Para corrigir esse erro de proxy

1. Localize **feedback.exe.config** (o arquivo de configuração feedback.exe) em: **% ProgramFiles (x86)% \ Microsoft Visual Studio\Installer** ou **%ProgramFiles%\Microsoft Visual Studio\Installer**.

2. No arquivo de configuração, verifique se o código a seguir está presente; Se o código não estiver presente, adicione-o antes da última `</configuration>` linha.

   ```xml
   <system.net>
       <defaultProxy useDefaultCredentials="true" />
   </system.net>
   ```

## <a name="error-the-underlying-connection-was-closed"></a>Erro: “A conexão subjacente estava fechada”

Se você estiver usando o Visual Studio em uma rede privada que tem um firewall, o Visual Studio poderá não ser capaz de se conectar a alguns recursos da rede. Esses recursos podem incluir o Azure DevOps Services para conexão e licenciamento, o NuGet e os serviços do Azure. Se o Visual Studio falhar ao se conectar a um desses recursos, você deverá ver a seguinte mensagem de erro:

  **A conexão subjacente estava fechada: Ocorreu um erro inesperado no envio**

O Visual Studio usa o TLS (protocolo TLS) 1.2 para se conectar aos recursos de rede. Os dispositivos de segurança de algumas redes privadas bloqueiam determinadas conexões de servidor quando o Visual Studio usa o protocolo TLS 1.2.

### <a name="to-fix-this-connection-error"></a>Para corrigir esse erro de conexão

Habilite as conexões para as seguintes URLs:

- https:&#47;&#47;management.core.windows.net

- https:&#47;&#47;app.vssps.visualstudio.com

- https:&#47;&#47;login.microsoftonline.com

- https:&#47;&#47;login.live.com

- https:&#47;&#47;go.microsoft.com

- https:&#47;&#47;graph.windows.net

- https:&#47;&#47;app.vsspsext.visualstudio.com

- &#42;.azurewebsites.net (para conexões do Azure)

- &#42;.visualstudio.microsoft.com

- cdn.vsassets.io (hospeda conteúdo da rede de distribuição de conteúdo ou CDN)

- &#42;.gallerycdn.vsassets.io (hospeda extensões do Azure DevOps Services)

- static2.sharepointonline.com (hospeda recursos que o Visual Studio usa no kit do Office UI Fabric, como fontes)

- &#42;.nuget.org (para conexões NuGet)

  > [!NOTE]
  > As URLs de servidor NuGet privadas podem não estar incluídas nesta lista. Você pode verificar os servidores NuGet que estamos usando em %APPData%\Nuget\NuGet.Config.

## <a name="error-failed-to-parse-id-from-parent-process"></a>Erro: "falha ao analisar a ID do processo pai"

Você pode encontrar essa mensagem de erro ao usar um bootstrapper do Visual Studio e um response.jsno arquivo em uma unidade de rede. A origem do erro é o controle de conta de usuário (UAC) no Windows.

Aqui está o motivo pelo qual esse erro pode ocorrer: uma unidade de rede mapeada ou um compartilhamento [UNC](/dotnet/standard/io/file-path-formats#unc-paths) está vinculado ao token de acesso do usuário. Quando o UAC está habilitado, dois [tokens de acesso](/windows/win32/secauthz/access-tokens) de usuário são criados: um *com* acesso de administrador e outro *sem* acesso de administrador. Quando uma unidade de rede ou compartilhamento é criado, o token de acesso atual do usuário é vinculado a ele. Como o bootstrapper deve ser executado como administrador, ele não poderá acessar a unidade de rede ou compartilhar se a unidade ou o compartilhamento não estiver vinculado a um token de acesso de usuário que tenha acesso de administrador.

### <a name="to-fix-this-error"></a>Para corrigir esse erro

Você pode usar o `net use` comando ou pode alterar a configuração de política de grupo do UAC. Para obter mais informações sobre essas soluções alternativas e como implementá-las, consulte os seguintes artigos de suporte da Microsoft:

* [Unidades mapeadas não estão disponíveis em um prompt com privilégios elevados quando o UAC está configurado para "solicitar credenciais" no Windows](https://support.microsoft.com/help/3035277/mapped-drives-are-not-available-from-an-elevated-prompt-when-uac-is-co)
* [Os programas podem não conseguir acessar alguns locais de rede depois de ativar o controle de conta de usuário em sistemas operacionais Windows](https://support.microsoft.com/en-us/help/937624/programs-may-be-unable-to-access-some-network-locations-after-you-turn)

[!INCLUDE[install_get_support_md](includes/install_get_support_md.md)]

## <a name="see-also"></a>Confira também

* [Instalar e usar o Visual Studio por trás de um firewall ou servidor proxy](install-and-use-visual-studio-behind-a-firewall-or-proxy-server.md)
* [Guia do administrador do Visual Studio](visual-studio-administrator-guide.md)
* [Instalar o Visual Studio](install-visual-studio.md)
