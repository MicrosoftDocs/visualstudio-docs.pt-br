---
title: 'Erro: Não é possível iniciar a depuração no servidor Web | Microsoft Docs'
ms.custom: ''
ms.date: 05/23/2017
ms.technology: vs-ide-debug
ms.topic: troubleshooting
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
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: e58f8152d5c927271161bbf9615b1dfe3944e6dd
ms.sourcegitcommit: 3d10b93eb5b326639f3e5c19b9e6a8d1ba078de1
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/18/2018
ms.locfileid: "31478246"
---
# <a name="error-unable-to-start-debugging-on-the-web-server"></a>Erro: não foi possível iniciar a depuração no servidor Web

Quando você tentar depurar um aplicativo ASP.NET em execução em um servidor Web, você pode receber essa mensagem de erro: `Unable to start debugging on the Web server`.

Geralmente, esse erro ocorre porque ocorreu uma erro ou alteração de configuração que requer uma atualização para os Pools de aplicativos, uma redefinição de IIS ou ambos. Você pode redefinir o IIS abrindo um prompt de comando e digitando `iisreset`. 

## <a name="specificerrors"></a>O que é a mensagem de erro detalhadas?

O `Unable to start debugging on the Web server` mensagem é genérica. Normalmente, uma mensagem mais específica está incluída na cadeia de caracteres de erro e que podem ajudá-lo a identificar a causa do problema ou pesquise uma correção mais exata. Aqui estão algumas das mensagens de erro mais comuns que são anexadas à mensagem de erro principal:

- [O IIS não lista um site que coincide com a inicialização url](#IISlist)
- [O servidor web não está configurado corretamente](#web_server_config)
- [Não é possível se conectar ao servidor da Web](#unabletoconnect)
- [O servidor web não respondeu em tempo adequado](#webservertimeout)
- [O microsoft visual studio remote debugging monitor(msvsmon.exe) parece não estar em execução no computador remoto](#msvsmon)
- [O servidor remoto retornou um erro](#server_error)
- [Não foi possível iniciar a depuração do ASP.NET](#aspnet)
- [O depurador não pode se conectar ao computador remoto](#cannot_connect)
- [Consulte a Ajuda para erros comuns de configuração. Executando a página da Web fora do depurador pode fornecer mais informações.](#see_help)

## <a name="IISlist"></a> O IIS não lista um site que coincide com a inicialização url

- Reinicie o Visual Studio como administrador e repita a depuração. (Alguns cenários de depuração do ASP.NET requerem privilégios elevados.)

    Você pode configurar o Visual Studio para sempre executar como administrador clicando com o ícone de atalho do Visual Studio, escolha **Propriedades > Avançado**e, em seguida, escolhendo para sempre executar como administrador.

## <a name="web_server_config"></a> O servidor web não está configurado corretamente

- Consulte [erro: O servidor web não está configurado corretamente](../debugger/error-the-web-server-is-not-configured-correctly.md).

## <a name="unabletoconnect"></a> Não é possível se conectar ao servidor da Web

- Tem executando o Visual Studio e o servidor Web no mesmo computador e a depuração usando **F5** (em vez de **anexar ao processo**)? Abra as propriedades do projeto e certifique-se de que o projeto está configurado para se conectar ao servidor da Web correto e iniciar a URL. (Abra **Propriedades > Web > servidores** ou **Propriedades > Depurar** dependendo do tipo de projeto. Para um projeto de formulários da Web, abra **páginas de propriedade > Iniciar Opções > servidor**.)

- Caso contrário, reinicie o Pool de aplicativos e, em seguida, reinicie o IIS. Para obter mais informações, consulte [Verifique a configuração do IIS](#vxtbshttpservererrorsthingstocheck).

## <a name="webservertimeout"></a> O servidor web não respondeu em tempo adequado

- Redefina o IIS e repita a depuração. Várias instâncias do depurador podem ser anexadas ao processo IIS; uma redefinição encerra-los. Para obter mais informações, consulte [Verifique a configuração do IIS](#vxtbshttpservererrorsthingstocheck).

## <a name="msvsmon"></a> O microsoft visual studio remote debugging monitor(msvsmon.exe) parece não estar em execução no computador remoto

- Se você estiver depurando em um computador remoto, verifique se você tem [instalado e estiver executando o depurador remoto](../debugger/remote-debugging.md). Se a mensagem mencionar um firewall, verifique se o [corrigir portas no firewall](../debugger/remote-debugger-port-assignments.md) estão abertos, especialmente se você estiver usando um firewall de terceiros.
- Se você estiver usando um arquivo de HOSTS, verifique se que ele está configurado corretamente. Por exemplo, se a depuração usando **F5** (em vez de **anexar ao processo**), precisa incluir a mesma URL de projeto como suas propriedades de projeto do arquivo HOSTS **Propriedades > Web > servidores**  ou **Propriedades > Depurar**, dependendo de seu tipo de projeto.

## <a name="server_error"></a> O servidor remoto retornou um erro

Verifique seu [arquivo de log do IIS](https://support.microsoft.com/help/943891/the-http-status-code-in-iis-7-0--iis-7-5--and-iis-8-0) para subcódigos de erro e informações adicionais e esta IIS 7 [postagem de blog](https://blogs.iis.net/tomkmvp/troubleshoot-a-403).

Além disso, aqui estão alguns dos códigos de erro comuns e algumas sugestões.
- Proibido (403). Há muitas causas possíveis para esse erro, portanto, verifique o arquivo de log e as configurações de segurança do IIS para o site da web. Certifique-se Web. config do servidor inclui `debug=true` no elemento de compilação. Certifique-se de que sua pasta de aplicativo Web tem as permissões corretas e se a configuração do Pool de aplicativos está correta (uma senha pode ter sido alterado). Consulte [Verifique a configuração do IIS](#vxtbshttpservererrorsthingstocheck). Se essas configurações já estão corretas e você estiver depurando localmente, verifique também se você está se conectando para o tipo de servidor correto e a URL (em **Propriedades > Web > servidores** ou **Propriedades > Depurar**, Dependendo de seu tipo de projeto).
- Servidor (503) não está disponível. O Pool de aplicativos pode ter parado devido a uma erro ou alteração de configuração. Reinicie o Pool de aplicativos.
- (404) não encontrado. Certifique-se de que o Pool de aplicativos está configurado para a versão correta do ASP.NET.

## <a name="aspnet"></a> Não foi possível iniciar a depuração do ASP.NET

- Reinicie o Pool de aplicativos e reinicie o IIS. Para obter mais informações, consulte [Verifique a configuração do IIS](#vxtbshttpservererrorsthingstocheck).
- Se você estiver fazendo URL regrava, um Web. config básico com regravações nenhuma URL de teste. Consulte o **Observação** sobre a URL de reconfiguração de módulo em [Verifique a configuração do IIS](#vxtbshttpservererrorsthingstocheck).

## <a name="cannot_connect"></a> O depurador não pode se conectar ao computador remoto

Se você estiver depurando localmente, esse erro pode ocorrer porque o Visual Studio é um aplicativo de 32 bits, portanto, ele usa a versão de 64 bits do depurador remoto para depurar aplicativos de 64 bits. Abra as propriedades do projeto e certifique-se de que o projeto está configurado para conectar-se para o servidor Web e a URL correta. (Abra **Propriedades > Web > servidores** ou **Propriedades > Depurar** dependendo do tipo de projeto.)

Além disso, se você estiver usando um arquivo de HOSTS, verifique se que ele está configurado corretamente. Por exemplo, os HOSTS do arquivo precisa incluir a mesma URL de projeto como suas propriedades de projeto, **Propriedades > Web > servidores** ou **Propriedades > Depurar**, dependendo de seu tipo de projeto.

## <a name="see_help"></a> Consulte a Ajuda para erros comuns de configuração. Executando a página da Web fora do depurador pode fornecer mais informações.

- Você está executando o Visual Studio e o servidor Web no mesmo computador? Abra as propriedades do projeto e certifique-se de que o projeto está configurado para se conectar ao servidor da Web correto e iniciar a URL. (Abra **Propriedades > Web > servidores** ou **Propriedades > Depurar** dependendo do tipo de projeto.)

- Se isso não funcionar ou se você estiver depurando remotamente, siga as etapas [Verifique a configuração do IIS](#vxtbshttpservererrorsthingstocheck).

##  <a name="vxtbshttpservererrorsthingstocheck"></a> Verifique a configuração do IIS

Depois de fazer as etapas descritas aqui para resolver o problema e antes de tentar novamente depurar, você talvez precise redefinir o IIS. Você pode fazer isso abrindo um prompt de comando e digitando `iisreset`. 

* Parar e reiniciar os Pools de aplicativos do IIS e repita. 

    O Pool de aplicativos pode ter interrompido como resultado de um erro. Ou então, outra alteração de configuração que você fez pode exigir que você parar e reiniciar o Pool de aplicativos.
    
    > [!NOTE]
    > Se o Pool de aplicativos mantém parando, você precisará desinstalar o módulo de reescrita de URL do painel de controle. Você pode reinstalá-lo usando o Web Platform Installer (WebPI). Esse problema pode ocorrer após uma atualização do sistema significativos.

* Verifique a configuração do Pool de aplicativos, corrigi-lo se necessário e, em seguida, tente novamente.

    O Pool de aplicativos pode ser configurado para uma versão do ASP.NET que não coincide com o projeto do Visual Studio. Atualize a versão do ASP.NET no Pool de aplicativos e reiniciá-lo. Para obter informações detalhadas, consulte [IIS 8.0 usando ASP.NET 3.5 e o ASP.NET 4.5](/iis/get-started/whats-new-in-iis-8/iis-80-using-aspnet-35-and-aspnet-45).

    Além disso, se as credenciais de senha foi alterado, você precisará atualizá-los em seu Pool de aplicativos ou site da Web.  No Pool de aplicativos, atualize as credenciais no **configurações avançadas > modelo de processo > identidade**. Para o site da Web, atualize as credenciais no **configurações básicas > Conecte-se como...** . Reinicie o Pool de aplicativos.
    
* Verifique se a pasta de aplicativo Web tem as permissões corretas.

    Certifique-se de que você fornecer IIS_IUSRS, IUSR, ou o usuário específico associado a [Pool de aplicativos](/iis/manage/configuring-security/application-pool-identities) de leitura e execução de direitos para a pasta de aplicativo da Web. Corrija o problema e reinicie o Pool de aplicativos.

* Certifique-se de que a versão correta do ASP.NET é instalada no IIS.

    Versões incompatíveis do ASP.NET no IIS e no projeto do Visual Studio podem causar esse problema. Talvez seja necessário definir a versão do framework no Web. config. Para instalar o ASP.NET no IIS, use o [Web Platform Installer (WebPI)](https://www.microsoft.com/web/downloads/platform.aspx). Além disso, consulte [IIS 8.0 usando ASP.NET 3.5 e o ASP.NET 4.5](/iis/get-started/whats-new-in-iis-8/iis-80-using-aspnet-35-and-aspnet-45) ou, para o ASP.NET Core [Host no Windows com o IIS](https://docs.asp.net/en/latest/publishing/iis.html).
  
* Resolver erros de autenticação, se você estiver usando apenas o endereço IP

     Por padrão, os endereços IP devem fazer parte da Internet e a autenticação NTLM não é feita pela Internet. Se seu site estiver configurado no IIS para exigir autenticação, essa autenticação falha. Para corrigir esse problema, você pode especificar o nome do computador remoto em vez do endereço IP.
     
## <a name="other-causes"></a>Outras causas

Se a configuração do IIS não está causando o problema, tente estas etapas:

- Reinicie o Visual Studio com privilégios de administrador e tente novamente.

    Alguns cenários de depuração de ASP.NET como o uso de implantação da Web exigem privilégios elevados para o Visual Studio.
    
- Se estiver executando várias instâncias do Visual Studio, abra seu projeto em uma instância do Visual Studio (com privilégios de administrador) e tente novamente.

- Se você estiver usando um arquivo de HOSTS com endereços locais, tente usar o endereço de loopback em vez do endereço IP do computador.

    Se você não estiver usando endereços locais, verifique se o arquivo de HOSTS inclui a mesma URL de projeto como suas propriedades de projeto, **Propriedades > Web > servidores** ou **Propriedades > Depurar**, dependendo de sua tipo de projeto.

## <a name="more-troubleshooting-steps"></a>Mais etapas de solução de problemas

* Abra a página de localhost no navegador do servidor.

     Se o IIS não está instalado corretamente, você deve receber erros quando você digita `http://localhost` em um navegador.
     
     Para obter mais informações sobre como implantar o IIS, consulte [IIS 8.0 usando ASP.NET 3.5 e o ASP.NET 4.5](/iis/get-started/whats-new-in-iis-8/iis-80-using-aspnet-35-and-aspnet-45) e, para o ASP.NET Core [Host no Windows com o IIS](https://docs.asp.net/en/latest/publishing/iis.html).

* Criar um aplicativo básico ASP.NET no servidor (ou usar um arquivo Web. config básico).

    Se você não pode obter seu aplicativo para trabalhar com o depurador, tente criar um aplicativo ASP.NET básico localmente no servidor e tentar depurar o aplicativo básico. (Você talvez queira usar o modelo do ASP.NET MVC padrão.) Se você pode depurar um aplicativo básico, que pode ajudá-lo a identificar qual é a diferença entre as duas configurações. Procure as diferenças nas configurações no arquivo Web. config, como regras de reescrita de URL.

## <a name="see-also"></a>Consulte também  
 [Depurando aplicativos Web: erros e solução de problemas](../debugger/debugging-web-applications-errors-and-troubleshooting.md)