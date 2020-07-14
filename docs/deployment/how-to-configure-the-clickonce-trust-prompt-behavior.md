---
title: Como configurar o comportamento do prompt de confiança do ClickOnce | Microsoft Docs
ms.date: 11/04/2016
ms.topic: how-to
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- ClickOnce deployment, install without prompting
- deploying applications [ClickOnce], trust prompt
- ClickOnce applications, install without prompting
- ClickOnce applications, trust prompt
- ClickOnce deployment, trust prompt
ms.assetid: cc04fa75-012b-47c9-9347-f4216be23cf2
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 7417f9cdce21dc09aeaf306b55834ad7d3a125a6
ms.sourcegitcommit: 3f491903e0c10db9a3f3fc0940f7b587fcbf9530
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/26/2020
ms.locfileid: "85382543"
---
# <a name="how-to-configure-the-clickonce-trust-prompt-behavior"></a>Como configurar o comportamento do prompt confiável do ClickOnce
Você pode configurar o prompt de confiança do ClickOnce para controlar se os usuários finais recebem a opção de instalar aplicativos ClickOnce, como Windows Forms aplicativos, Windows Presentation Foundation aplicativos, aplicativos de console, aplicativos de navegador WPF e soluções do Office. Configure o prompt de confiança definindo chaves do registro no computador de cada usuário final.

 A tabela a seguir mostra as opções de configuração que podem ser aplicadas a cada uma das cinco zonas (Internet, UntrustedSites, MyComputer, LocalIntranet e TrustedSites).

|Opção|Valor de configuração do registro|Descrição|
|------------|----------------------------|-----------------|
|Habilite o prompt de confiança.|`Enabled`|O prompt de confiança do ClickOnce é exibido para que os usuários finais possam conceder confiança a aplicativos ClickOnce.|
|Restrinja o prompt de confiança.|`AuthenticodeRequired`|O prompt de confiança do ClickOnce só será exibido se os aplicativos ClickOnce forem assinados com um certificado que identifica o Publicador.|
|Desabilite o prompt de confiança.|`Disabled`|O prompt de confiança do ClickOnce não é exibido para nenhum aplicativo ClickOnce que não esteja assinado com um certificado explicitamente confiável.|

 A tabela a seguir mostra o comportamento padrão para cada zona. A coluna aplicativos refere-se a Windows Forms aplicativos, Windows Presentation Foundation aplicativos, aplicativos de navegador WPF e aplicativos de console.

|Zona|Aplicativos|Soluções do Office|
|----------|------------------|----------------------|
|`MyComputer`|`Enabled`|`Enabled`|
|`LocalIntranet`|`Enabled`|`Enabled`|
|`TrustedSites`|`Enabled`|`Enabled`|
|`Internet`|`Enabled`|`AuthenticodeRequired`|
|`UntrustedSites`|`Disabled`|`Disabled`|

 Você pode substituir essas configurações habilitando, restringindo ou desabilitando o prompt de confiança do ClickOnce.

## <a name="enable-the-clickonce-trust-prompt"></a>Habilitar o prompt de confiança do ClickOnce
 Habilite o prompt de confiança para uma zona quando desejar que os usuários finais sejam apresentados com a opção de instalar e executar qualquer aplicativo ClickOnce proveniente dessa zona.

#### <a name="to-enable-the-clickonce-trust-prompt-by-using-the-registry-editor"></a>Para habilitar o prompt de confiança do ClickOnce usando o editor do registro

1. Abra o Editor do Registro:

    1. Clique em **Iniciar**e em **Executar**.

    2. Na caixa **abrir** , digite `regedit` e clique em **OK**.

2. Localize a seguinte chave do registro:

     **\HKEY_LOCAL_MACHINE\SOFTWARE\MICROSOFT\\.NETFramework\Security\TrustManager\PromptingLevel**

     Se a chave não existir, crie-a.

3. Adicione as seguintes subchaves como **valor de cadeia de caracteres**, se elas ainda não existirem, com os valores associados mostrados na tabela a seguir.

    |Subchave de valor da cadeia de caracteres|Valor|
    |-------------------------|-----------|
    |`Internet`|`Enabled`|
    |`UntrustedSites`|`Disabled`|
    |`MyComputer`|`Enabled`|
    |`LocalIntranet`|`Enabled`|
    |`TrustedSites`|`Enabled`|

     Para soluções do Office, `Internet` tem o valor padrão `AuthenticodeRequired` e `UntrustedSites` tem o valor `Disabled` . Para todos os outros, `Internet` tem o valor padrão `Enabled` .

#### <a name="to-enable-the-clickonce-trust-prompt-programmatically"></a>Para habilitar o prompt de confiança do ClickOnce programaticamente

1. Crie um aplicativo de console Visual Basic ou Visual C# no Visual Studio.

2. Abra o arquivo *Program. vb* ou *Program.cs* para edição e adicione o código a seguir.

    ```vb
    Dim key As Microsoft.Win32.RegistryKey
    key = Microsoft.Win32.Registry.LocalMachine.CreateSubKey("SOFTWARE\MICROSOFT\.NETFramework\Security\TrustManager\PromptingLevel")
    key.SetValue("MyComputer", "Enabled")
    key.SetValue("LocalIntranet", "Enabled")
    key.SetValue("Internet", "Enabled")
    key.SetValue("TrustedSites", "Enabled")
    key.SetValue("UntrustedSites", "Disabled")
    key.Close()
    ```

    ```csharp
    Microsoft.Win32.RegistryKey key;
    key = Microsoft.Win32.Registry.LocalMachine.CreateSubKey("SOFTWARE\\MICROSOFT\\.NETFramework\\Security\\TrustManager\\PromptingLevel");
    key.SetValue("MyComputer", "Enabled");
    key.SetValue("LocalIntranet", "Enabled");
    key.SetValue("Internet", "AuthenticodeRequired");
    key.SetValue("TrustedSites", "Enabled");
    key.SetValue("UntrustedSites", "Disabled");
    key.Close();
    ```

3. Criar e executar o aplicativo.

## <a name="restrict-the-clickonce-trust-prompt"></a>Restringir o prompt de confiança do ClickOnce
 Restrinja o prompt de confiança para que as soluções devam ser assinadas com certificados Authenticode com identidade conhecida antes que os usuários sejam solicitados a fornecer uma decisão de confiança.

#### <a name="to-restrict-the-clickonce-trust-prompt-by-using-the-registry-editor"></a>Para restringir o prompt de confiança do ClickOnce usando o editor do registro

1. Abra o Editor do Registro:

    1. Clique em **Iniciar**e em **Executar**.

    2. Na caixa **abrir** , digite `regedit` e clique em **OK**.

2. Localize a seguinte chave do registro:

     **\HKEY_LOCAL_MACHINE\SOFTWARE\MICROSOFT\\.NETFramework\Security\TrustManager\PromptingLevel**

     Se a chave não existir, crie-a.

3. Adicione as seguintes subchaves como **valor de cadeia de caracteres**, se elas ainda não existirem, com os valores associados mostrados na tabela a seguir.

    |Subchave de valor da cadeia de caracteres|Valor|
    |-------------------------|-----------|
    |`UntrustedSites`|`Disabled`|
    |`Internet`|`AuthenticodeRequired`|
    |`MyComputer`|`AuthenticodeRequired`|
    |`LocalIntranet`|`AuthenticodeRequired`|
    |`TrustedSites`|`AuthenticodeRequired`|

#### <a name="to-restrict-the-clickonce-trust-prompt-programmatically"></a>Para restringir o prompt de confiança do ClickOnce programaticamente

1. Crie um aplicativo de console Visual Basic ou Visual C# no Visual Studio.

2. Abra o arquivo *Program. vb* ou *Program.cs* para edição e adicione o código a seguir.

    ```vb
    Dim key As Microsoft.Win32.RegistryKey
    key = Microsoft.Win32.Registry.LocalMachine.CreateSubKey("SOFTWARE\MICROSOFT\.NETFramework\Security\TrustManager\PromptingLevel")
    key.SetValue("MyComputer", "AuthenticodeRequired")
    key.SetValue("LocalIntranet", "AuthenticodeRequired")
    key.SetValue("Internet", "AuthenticodeRequired")
    key.SetValue("TrustedSites", "AuthenticodeRequired")
    key.SetValue("UntrustedSites", "Disabled")
    key.Close()
    ```

    ```csharp
    Microsoft.Win32.RegistryKey key;
    key = Microsoft.Win32.Registry.LocalMachine.CreateSubKey("SOFTWARE\\MICROSOFT\\.NETFramework\\Security\\TrustManager\\PromptingLevel");
    key.SetValue("MyComputer", "AuthenticodeRequired");
    key.SetValue("LocalIntranet", "AuthenticodeRequired");
    key.SetValue("Internet", "AuthenticodeRequired");
    key.SetValue("TrustedSites", "AuthenticodeRequired");
    key.SetValue("UntrustedSites", "Disabled");
    key.Close();
    ```

3. Criar e executar o aplicativo.

## <a name="disable-the-clickonce-trust-prompt"></a>Desabilitar o prompt de confiança do ClickOnce
 Você pode desabilitar o prompt de confiança para que os usuários finais não tenham a opção de instalar soluções que ainda não são confiáveis em sua política de segurança.

#### <a name="to-disable-the-clickonce-trust-prompt-by-using-the-registry-editor"></a>Para desabilitar o prompt de confiança do ClickOnce usando o editor do registro

1. Abra o Editor do Registro:

    1. Clique em **Iniciar**e em **Executar**.

    2. Na caixa **abrir** , digite `regedit` e clique em **OK**.

2. Localize a seguinte chave do registro:

     **\HKEY_LOCAL_MACHINE\SOFTWARE\MICROSOFT\\.NETFramework\Security\TrustManager\PromptingLevel**

     Se a chave não existir, crie-a.

3. Adicione as seguintes subchaves como **valor de cadeia de caracteres**, se elas ainda não existirem, com os valores associados mostrados na tabela a seguir.

    |Subchave de valor da cadeia de caracteres|Valor|
    |-------------------------|-----------|
    |`UntrustedSites`|`Disabled`|
    |`Internet`|`Disabled`|
    |`MyComputer`|`Disabled`|
    |`LocalIntranet`|`Disabled`|
    |`TrustedSites`|`Disabled`|

#### <a name="to-disable-the-clickonce-trust-prompt-programmatically"></a>Para desabilitar o prompt de confiança do ClickOnce programaticamente

1. Crie um aplicativo de console Visual Basic ou Visual C# no Visual Studio.

2. Abra o arquivo *Program. vb* ou *Program.cs* para edição e adicione o código a seguir.

    ```vb
    Dim key As Microsoft.Win32.RegistryKey
    key = Microsoft.Win32.Registry.LocalMachine.CreateSubKey("SOFTWARE\MICROSOFT\.NETFramework\Security\TrustManager\PromptingLevel")
    key.SetValue("MyComputer", "Disabled")
    key.SetValue("LocalIntranet", "Disabled")
    key.SetValue("Internet", "Disabled")
    key.SetValue("TrustedSites", "Disabled")
    key.SetValue("UntrustedSites", "Disabled")
    key.Close()
    ```

    ```csharp
    Microsoft.Win32.RegistryKey key;
    key = Microsoft.Win32.Registry.LocalMachine.CreateSubKey("SOFTWARE\\MICROSOFT\\.NETFramework\\Security\\TrustManager\\PromptingLevel");
    key.SetValue("MyComputer", "Disabled");
    key.SetValue("LocalIntranet", "Disabled");
    key.SetValue("Internet", "Disabled");
    key.SetValue("TrustedSites", "Disabled");
    key.SetValue("UntrustedSites", "Disabled");
    key.Close();

    ```

3. Criar e executar o aplicativo.

## <a name="see-also"></a>Veja também
- [Proteger aplicativos ClickOnce](../deployment/securing-clickonce-applications.md)
- [Segurança de acesso do código para aplicativos ClickOnce](../deployment/code-access-security-for-clickonce-applications.md)
- [ClickOnce e Authenticode](../deployment/clickonce-and-authenticode.md)
- [Visão geral da implantação de aplicativos confiáveis](../deployment/trusted-application-deployment-overview.md)
- [Como habilitar as configurações de segurança do ClickOnce](../deployment/how-to-enable-clickonce-security-settings.md)
- [Como definir uma zona de segurança em um aplicativo ClickOnce](../deployment/how-to-set-a-security-zone-for-a-clickonce-application.md)
- [Como definir permissões personalizadas em um aplicativo ClickOnce](../deployment/how-to-set-custom-permissions-for-a-clickonce-application.md)
- [Como depurar um aplicativo ClickOnce com permissões restritas](securing-clickonce-applications.md)
- [Como adicionar um fornecedor confiável a um computador cliente em aplicativos ClickOnce](../deployment/how-to-add-a-trusted-publisher-to-a-client-computer-for-clickonce-applications.md)
- [Como reassinar manifestos do aplicativo e de implantação](../deployment/how-to-re-sign-application-and-deployment-manifests.md)
