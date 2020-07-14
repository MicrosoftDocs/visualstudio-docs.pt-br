---
title: Erro-não é possível iniciar a depuração no servidor Web | Microsoft Docs
ms.date: 05/23/2018
ms.topic: error-reference
f1_keywords:
- vs.debug.error.http
- vwd.nonadmin.error.
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- IIS, debugging DLLs
- debugger, Web application errors
- unable to start debugging error
- security [debugger], Web applications
- debugging [Visual Studio], errors
- HTTP servers, debugging error
- security settings, checking for default Web sites
- errors [debugger], unable to start debugging
- debugging ASP.NET Web applications, unable to start debugging error
- remote debugging, errors
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 00d27dafd5e44b058cff05b3c478322e45242b3c
ms.sourcegitcommit: 66f31cc4ce1236e638ab58d2f70d3646206386fa
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85460033"
---
# <a name="error-unable-to-start-debugging-on-the-web-server"></a>Erro: não foi possível iniciar a depuração no servidor Web

Ao tentar depurar um aplicativo ASP.NET em execução em um servidor Web, você poderá receber essa mensagem de erro: `Unable to start debugging on the Web server` .

Geralmente, esse erro ocorre devido a uma alteração de erro ou configuração que requer uma atualização para seus pools de aplicativos, uma redefinição do IIS ou ambos. Você pode redefinir o IIS abrindo um prompt de comandos com privilégios elevados e digitando `iisreset` .

## <a name="what-is-the-detailed-error-message"></a><a name="specificerrors"></a>Qual é a mensagem de erro detalhada?

A `Unable to start debugging on the Web server` mensagem é genérica. Normalmente, uma mensagem mais específica é incluída na cadeia de caracteres de erro e pode ajudar a identificar a causa do problema ou pesquisar uma correção mais exata. Aqui estão algumas das mensagens de erro mais comuns que são acrescentadas à mensagem de erro principal:

- [O IIS não lista um site que corresponda à URL de inicialização](#IISlist)
- [O servidor Web não foi configurado corretamente](#web_server_config)
- [Não é possível conectar ao servidor](#unabletoconnect)
- [O servidor Web não respondeu oportunamente](#webservertimeout)
- [O Monitor de Depuração Remota do Microsoft Visual Studio (MSVSMON.EXE) parece não estar sendo executado no computador remoto](#msvsmon)
- [O servidor remoto retornou um erro](#server_error)
- [Não foi possível iniciar a depuração de ASP.NET](#aspnet)
- [O depurador não pode se conectar ao computador remoto](#cannot_connect)
- [Consulte a ajuda para obter os erros de configuração comuns. Executando a página da Web fora do depurador pode fornecer mais informações.](#see_help)
- [Operação sem suporte. Erro desconhecido: *ErrorNumber*](#operation_not_supported)

## <a name="iis-does-not-list-a-website-that-matches-the-launch-url"></a><a name="IISlist"></a>O IIS não lista um site que corresponda à URL de inicialização

- Reinicie o Visual Studio como administrador e tente depurar novamente. (Alguns cenários de depuração ASP.NET exigem privilégios elevados.)

    Você pode configurar o Visual Studio para sempre executar como administrador clicando com o botão direito do mouse no ícone de atalho do Visual Studio, escolhendo **propriedades > avançado**e, em seguida, escolhendo sempre executar como administrador.

## <a name="the-web-server-is-not-configured-correctly"></a><a name="web_server_config"></a>O servidor Web não está configurado corretamente

- Consulte [o erro: o servidor Web não está configurado corretamente](../debugger/error-the-web-server-is-not-configured-correctly.md).

## <a name="unable-to-connect-to-the-webserver"></a><a name="unabletoconnect"></a>Não é possível conectar ao servidor

- Você está executando o Visual Studio e o servidor Web no mesmo computador e Depurando usando **F5** (em vez de **anexar ao processo**)? Abra as propriedades do projeto e verifique se o projeto está configurado para se conectar ao servidor Web correto e à URL de inicialização. (Abra **propriedades > servidores ou propriedades de > da Web** **> depurar** , dependendo do tipo de projeto. Para um projeto Web Forms, abra **páginas de propriedades > opções de início > servidor**.)

- Caso contrário, reinicie o pool de aplicativos e redefina o IIS. Para obter mais informações, consulte [verificar a configuração do IIS](#vxtbshttpservererrorsthingstocheck).

## <a name="the-web-server-did-not-respond-in-a-timely-manner"></a><a name="webservertimeout"></a>O servidor Web não respondeu oportunamente

- Redefina o IIS e tente depurar novamente. Várias instâncias do depurador podem ser anexadas ao processo do IIS; uma redefinição as encerra. Para obter mais informações, consulte [verificar a configuração do IIS](#vxtbshttpservererrorsthingstocheck).

## <a name="the-microsoft-visual-studio-remote-debugging-monitormsvsmonexe-does-not-appear-to-be-running-on-the-remote-computer"></a><a name="msvsmon"></a>O monitor de depuração remota do Microsoft Visual Studio (msvsmon.exe) não parece estar em execução no computador remoto

- Se você estiver Depurando em um computador remoto, verifique se você [instalou e está executando o depurador remoto](../debugger/remote-debugging.md). Se a mensagem mencionar um firewall, verifique se as [portas corretas no firewall](../debugger/remote-debugger-port-assignments.md) estão abertas, especialmente se você estiver usando um firewall de terceiros.
- Se você estiver usando um arquivo de HOSTs, verifique se ele está configurado corretamente. Por exemplo, se estiver Depurando usando **F5** (em vez de **anexar ao processo**), o arquivo hosts precisará incluir a mesma URL do projeto que nas propriedades do projeto, **Propriedades > servidores ou propriedades de > da Web** **> depurar**, dependendo do tipo de projeto.

## <a name="the-remote-server-returned-an-error"></a><a name="server_error"></a>O servidor remoto retornou um erro

Verifique o [arquivo de log do IIS](https://support.microsoft.com/help/943891/the-http-status-code-in-iis-7-0--iis-7-5--and-iis-8-0) para obter os subcódigos de erro e informações adicionais e esta [postagem no blog](https://blogs.iis.net/tomkmvp/troubleshoot-a-403)do IIS 7.

Além disso, aqui estão alguns dos códigos de erro comuns e algumas sugestões.
- (403) Proibido. Há muitas causas possíveis para esse erro, portanto, verifique o arquivo de log e as configurações de segurança do IIS para o site. Verifique se o web.config do servidor inclui `debug=true` no elemento Compilation. Verifique se a pasta do aplicativo Web tem as permissões corretas e se a configuração do pool de aplicativos está correta (uma senha pode ter sido alterada). Consulte [verificar a configuração do IIS](#vxtbshttpservererrorsthingstocheck). Se essas configurações já estiverem corretas e você estiver Depurando localmente, verifique também se está se conectando ao tipo de servidor e à URL corretos (em **propriedades > servidores > Web** ou **Propriedades > depurar**, dependendo do tipo de projeto).
- (503) Servidor não disponível. O pool de aplicativos pode ter sido interrompido devido a um erro ou alteração de configuração. Reinicie o pool de aplicativos.
- (404) Não encontrado. Verifique se o pool de aplicativos está configurado para a versão correta do ASP.NET.

## <a name="could-not-start-aspnet-debugging"></a><a name="aspnet"></a>Não foi possível iniciar a depuração de ASP.NET

- Reinicie o pool de aplicativos e redefina o IIS. Para obter mais informações, consulte [verificar a configuração do IIS](#vxtbshttpservererrorsthingstocheck).
- Se você estiver fazendo regravações de URL, teste um web.config básico sem regravações de URL. Consulte a **Observação** sobre o módulo de reescrita de URL em [verificar a configuração do IIS](#vxtbshttpservererrorsthingstocheck).

## <a name="the-debugger-cannot-connect-to-the-remote-computer"></a><a name="cannot_connect"></a>O depurador não pode se conectar ao computador remoto

Se você estiver Depurando localmente, abra as propriedades do projeto no Visual Studio e verifique se o projeto está configurado para se conectar ao servidor Web e à URL corretos. (Abra **propriedades > servidores ou propriedades de > da Web** **> depurar** , dependendo do tipo de projeto.)

Esse erro pode ocorrer durante a depuração local porque o Visual Studio é um aplicativo de 32 bits, portanto, ele usa a versão de 64 bits do depurador remoto para depurar aplicativos de 64 bits. Verifique seu pool de aplicativos no IIS para certificar-se de que **habilitar aplicativos de 32 bits** está definido como `true` , reinicie o IIS e tente novamente.

Além disso, se você estiver usando um arquivo de HOSTs, verifique se ele está configurado corretamente. Por exemplo, o arquivo HOSTs precisa incluir a mesma URL de projeto das propriedades do projeto, **propriedades > servidores ou propriedades de > da Web** **> depurar**, dependendo do tipo de projeto.

## <a name="see-help-for-common-configuration-errors-running-the-webpage-outside-of-the-debugger-may-provide-further-information"></a><a name="see_help"></a> Confira a ajuda para obter os erros de configuração comuns. A execução da página da Web fora do depurador pode fornecer mais informações.

- Você está executando o Visual Studio e o servidor Web no mesmo computador? Abra as propriedades do projeto e verifique se o projeto está configurado para se conectar ao servidor Web correto e à URL de inicialização. (Abra **propriedades > servidores ou propriedades de > da Web** **> depurar** , dependendo do tipo de projeto.)

- Se isso não funcionar ou se você estiver depurando remotamente, siga as etapas em [verificar a configuração do IIS](#vxtbshttpservererrorsthingstocheck).

## <a name="operation-not-supported-unknown-error-errornumber"></a><a name="operation_not_supported"></a>Operação sem suporte. Erro desconhecido: *ErrorNumber*

Se você estiver fazendo regravações de URL, teste um web.config básico sem regravações de URL. Consulte a **Observação** sobre o módulo de reescrita de URL em [verificar a configuração do IIS](#vxtbshttpservererrorsthingstocheck).

## <a name="check-your-iis-configuration"></a><a name="vxtbshttpservererrorsthingstocheck"></a>Verifique a configuração do IIS

Depois de executar as etapas detalhadas aqui para resolver o problema e antes de tentar depurar novamente, talvez você também precise redefinir o IIS. Você pode fazer isso abrindo um prompt de comandos com privilégios elevados e digitando `iisreset` .

* Pare e reinicie os pools de aplicativos do IIS e tente novamente.

    O pool de aplicativos pode ter sido interrompido como resultado de um erro. Ou então, outra alteração de configuração que você fez pode exigir que você pare e reinicie o pool de aplicativos.

    > [!NOTE]
    > Se o pool de aplicativos continuar a parar, talvez seja necessário desinstalar o módulo de reescrita de URL no painel de controle. Você pode reinstalá-lo usando o Web Platform Installer (WebPI). Esse problema pode ocorrer após uma atualização significativa do sistema.

* Verifique a configuração do pool de aplicativos, corrija-o se necessário e tente novamente.

    O pool de aplicativos pode ser configurado para uma versão do ASP.NET que não corresponde ao seu projeto do Visual Studio. Atualize a versão ASP.NET no pool de aplicativos e reinicie-a. Para obter informações detalhadas, consulte [IIS 8,0 usando ASP.NET 3,5 e ASP.NET 4,5](/iis/get-started/whats-new-in-iis-8/iis-80-using-aspnet-35-and-aspnet-45).

    Além disso, se as credenciais de senha forem alteradas, talvez seja necessário atualizá-las no seu pool de aplicativos ou site.  No pool de aplicativos, atualize as credenciais em **Configurações avançadas > modelo de processo > identidade**. Para o site, atualize as credenciais nas **configurações básicas > conectar como...**. Reinicie o pool de aplicativos.

* Verifique se a pasta do aplicativo Web tem as permissões corretas.

    Certifique-se de fornecer IIS_IUSRS, IUSR ou o usuário específico associado ao pool de [aplicativos](/iis/manage/configuring-security/application-pool-identities) direitos de leitura e execução para a pasta do aplicativo Web. Corrija o problema e reinicie o pool de aplicativos.

* Verifique se a versão correta do ASP.NET está instalada no IIS.

    As versões incompatíveis do ASP.NET no IIS e no seu projeto do Visual Studio podem causar esse problema. Talvez seja necessário definir a versão do Framework no web.config. Para instalar o ASP.NET no IIS, use o [Web Platform Installer (WebPI)](https://www.microsoft.com/web/downloads/platform.aspx). Além disso, consulte [iis 8,0 usando ASP.NET 3,5 e ASP.NET 4,5](/iis/get-started/whats-new-in-iis-8/iis-80-using-aspnet-35-and-aspnet-45) ou, para ASP.NET Core, [host no Windows com IIS](https://docs.asp.net/en/latest/publishing/iis.html).

* Resolver erros de autenticação se você estiver usando apenas o endereço IP

     Por padrão, os endereços IP devem fazer parte da Internet e a autenticação NTLM não é feita pela Internet. Se o seu site estiver configurado no IIS para exigir autenticação, essa autenticação falhará. Para corrigir esse problema, você pode especificar o nome do computador remoto em vez do endereço IP.

## <a name="other-causes"></a>Outras causas

Se a configuração do IIS não estiver causando o problema, tente estas etapas:

- Reinicie o Visual Studio com privilégios de administrador e tente novamente.

    Alguns cenários de depuração ASP.NET, como o uso de Implantação da Web exigem privilégios elevados para o Visual Studio.

- Se várias instâncias do Visual Studio estiverem em execução, reabra o projeto em uma instância do Visual Studio (com privilégios de administrador) e tente novamente.

- Se você estiver usando um arquivo de HOSTs com endereços locais, tente usar o endereço de loopback em vez do endereço IP da máquina.

    Se você não estiver usando endereços locais, verifique se o arquivo de HOSTs inclui a mesma URL de projeto das propriedades do projeto, **propriedades > servidores ou propriedades de > da Web** **> depurar**, dependendo do tipo de projeto.

## <a name="more-troubleshooting-steps"></a>Mais etapas de solução de problemas

* Ative a página localhost no navegador no servidor.

     Se o IIS não estiver instalado corretamente, você deverá obter erros ao digitar `http://localhost` um navegador.

     Para obter mais informações sobre como implantar no IIS, consulte [iis 8,0 usando ASP.NET 3,5 e ASP.NET 4,5](/iis/get-started/whats-new-in-iis-8/iis-80-using-aspnet-35-and-aspnet-45) e, para ASP.NET Core, [host no Windows com o IIS](https://docs.asp.net/en/latest/publishing/iis.html).

* Crie um aplicativo ASP.NET básico no servidor (ou use um arquivo web.config básico).

    Se você não puder fazer com que seu aplicativo funcione com o depurador, tente criar um aplicativo ASP.NET básico localmente no servidor e tente depurar o aplicativo básico. (Talvez você queira usar o modelo ASP.NET MVC padrão.) Se você puder depurar um aplicativo básico, isso poderá ajudá-lo a identificar o que há de diferente entre as duas configurações. Procure diferenças nas configurações no arquivo de web.config, como regras de reescrita de URL.

## <a name="see-also"></a>Veja também
- [Depurando aplicativos Web: erros e solução de problemas](../debugger/debugging-web-applications-errors-and-troubleshooting.md)