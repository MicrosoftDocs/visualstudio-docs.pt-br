---
title: 'Como: configurar o comportamento do Prompt confiável do ClickOnce | Microsoft Docs'
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-deployment
ms.topic: conceptual
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
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 103fcd8b47e423aaa8d66c3df96afe3598818de2
ms.sourcegitcommit: 6944ceb7193d410a2a913ecee6f40c6e87e8a54b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/05/2018
ms.locfileid: "43774801"
---
# <a name="how-to-configure-the-clickonce-trust-prompt-behavior"></a>Como: configurar o comportamento do prompt confiável do ClickOnce
Você pode configurar o prompt de confiança do ClickOnce para controlar se os usuários finais recebem a opção de instalação de aplicativos do ClickOnce, como aplicativos do Windows Forms, aplicativos do Windows Presentation Foundation, aplicativos de console, navegador do WPF os aplicativos e soluções do Office. Configurar o prompt de confiança, definindo as chaves do registro no computador de cada usuário final.  
  
 A tabela a seguir mostra as opções de configuração que podem ser aplicadas a cada uma das cinco zonas (Internet, UntrustedSites, MyComputer, LocalIntranet e TrustedSites).  
  
|Opção|Valor da configuração do registro|Descrição|  
|------------|----------------------------|-----------------|  
|Habilite o prompt de confiança.|`Enabled`|O prompt de confiança do ClickOnce é a exibição para que os usuários finais possam conceder confiança aos aplicativos ClickOnce.|  
|Restringir o prompt de confiança.|`AuthenticodeRequired`|O prompt de confiança do ClickOnce é exibido somente se os aplicativos ClickOnce são assinados com um certificado que identifica o Editor.|  
|Desabilite o prompt de confiança.|`Disabled`|O prompt de confiança do ClickOnce não é exibido para todos os aplicativos ClickOnce que não são assinados com um certificado confiável explicitamente.|  
  
 A tabela a seguir mostra o comportamento padrão para cada zona. A coluna de aplicativos se refere a aplicativos do Windows Forms, aplicativos do Windows Presentation Foundation, aplicativos de navegador WPF e aplicativos de console.  
  
|Zona|Aplicativos|Soluções do Office|  
|----------|------------------|----------------------|  
|`MyComputer`|`Enabled`|`Enabled`|  
|`LocalIntranet`|`Enabled`|`Enabled`|  
|`TrustedSites`|`Enabled`|`Enabled`|  
|`Internet`|`Enabled`|`AuthenticodeRequired`|  
|`UntrustedSites`|`Disabled`|`Disabled`|  
  
 Você pode substituir essas configurações, habilitar, restringir ou desabilitar o prompt de confiança do ClickOnce.  
  
## <a name="enable-the-clickonce-trust-prompt"></a>Habilitar o prompt de confiança do ClickOnce  
 Habilite o prompt de confiança para uma zona quando desejar que os usuários finais a ser apresentada com a opção de instalar e executar qualquer aplicativo ClickOnce que vem a partir dessa zona.  
  
#### <a name="to-enable-the-clickonce-trust-prompt-by-using-the-registry-editor"></a>Para habilitar o prompt de confiança do ClickOnce usando o editor do registro  
  
1.  Abra o editor do registro:  
  
    1.  Clique em **inicie**e, em seguida, clique em **executar**.  
  
    2.  No **aberto** , digite `regedit`e, em seguida, clique em **Okey**.  
  
2.  Localize a seguinte chave do registro:  
  
     **\HKEY_LOCAL_MACHINE\SOFTWARE\MICROSOFT\\. NETFramework\Security\TrustManager\PromptingLevel**  
  
     Se a chave não existir, crie-o.  
  
3.  Adicione as seguintes subchaves como **valor de cadeia de caracteres**, se ainda não existirem, com os valores associados, mostrados na tabela a seguir.  
  
    |Subchave do valor de cadeia de caracteres|Valor|  
    |-------------------------|-----------|  
    |`Internet`|`Enabled`|  
    |`UntrustedSites`|`Disabled`|  
    |`MyComputer`|`Enabled`|  
    |`LocalIntranet`|`Enabled`|  
    |`TrustedSites`|`Enabled`|  
  
     Para soluções do Office `Internet` tem o valor padrão `AuthenticodeRequired` e `UntrustedSites` tem o valor `Disabled`. Para todas as outras, `Internet` tem o valor padrão `Enabled`.  
  
#### <a name="to-enable-the-clickonce-trust-prompt-programmatically"></a>Para habilitar o prompt de confiança do ClickOnce por meio de programação  
  
1.  Crie um aplicativo de console do Visual Basic ou Visual c# no Visual Studio.  
  
2.  Abra o *Program. vb* ou *Program.cs* arquivo para edição e adicione o código a seguir.  
  
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
  
3.  Crie e execute o aplicativo.  
  
## <a name="restrict-the-clickonce-trust-prompt"></a>Restringir o prompt de confiança do ClickOnce  
 Restringir o prompt de confiança para que as soluções devem ser assinadas com certificados Authenticode que têm conhecidos identidade antes que os usuários são solicitados para uma decisão de confiança.  
  
#### <a name="to-restrict-the-clickonce-trust-prompt-by-using-the-registry-editor"></a>Para restringir o prompt de confiança do ClickOnce usando o editor do registro  
  
1.  Abra o editor do registro:  
  
    1.  Clique em **inicie**e, em seguida, clique em **executar**.  
  
    2.  No **aberto** , digite `regedit`e, em seguida, clique em **Okey**.  
  
2.  Localize a seguinte chave do registro:  
  
     **\HKEY_LOCAL_MACHINE\SOFTWARE\MICROSOFT\\. NETFramework\Security\TrustManager\PromptingLevel** 
  
     Se a chave não existir, crie-o.  
  
3.  Adicione as seguintes subchaves como **valor de cadeia de caracteres**, se ainda não existirem, com os valores associados, mostrados na tabela a seguir.  
  
    |Subchave do valor de cadeia de caracteres|Valor|  
    |-------------------------|-----------|  
    |`UntrustedSites`|`Disabled`|  
    |`Internet`|`AuthenticodeRequired`|  
    |`MyComputer`|`AuthenticodeRequired`|  
    |`LocalIntranet`|`AuthenticodeRequired`|  
    |`TrustedSites`|`AuthenticodeRequired`|  
  
#### <a name="to-restrict-the-clickonce-trust-prompt-programmatically"></a>Para restringir o prompt de confiança do ClickOnce por meio de programação  
  
1.  Crie um aplicativo de console do Visual Basic ou Visual c# no Visual Studio.  
  
2.  Abra o *Program. vb* ou *Program.cs* arquivo para edição e adicione o código a seguir.  
  
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
  
3.  Crie e execute o aplicativo.  
  
## <a name="disable-the-clickonce-trust-prompt"></a>Desabilitar o prompt de confiança do ClickOnce  
 Você pode desabilitar o prompt de confiança para que os usuários finais não recebem a opção de instalar as soluções que já não são confiáveis na sua política de segurança.  
  
#### <a name="to-disable-the-clickonce-trust-prompt-by-using-the-registry-editor"></a>Para desabilitar o prompt de confiança do ClickOnce usando o editor do registro  
  
1.  Abra o editor do registro:  
  
    1.  Clique em **inicie**e, em seguida, clique em **executar**.  
  
    2.  No **aberto** , digite `regedit`e, em seguida, clique em **Okey**.  
  
2.  Localize a seguinte chave do registro:  
  
     **\HKEY_LOCAL_MACHINE\SOFTWARE\MICROSOFT\\. NETFramework\Security\TrustManager\PromptingLevel**  
  
     Se a chave não existir, crie-o.  
  
3.  Adicione as seguintes subchaves como **valor de cadeia de caracteres**, se ainda não existirem, com os valores associados, mostrados na tabela a seguir.  
  
    |Subchave do valor de cadeia de caracteres|Valor|  
    |-------------------------|-----------|  
    |`UntrustedSites`|`Disabled`|  
    |`Internet`|`Disabled`|  
    |`MyComputer`|`Disabled`|  
    |`LocalIntranet`|`Disabled`|  
    |`TrustedSites`|`Disabled`|  
  
#### <a name="to-disable-the-clickonce-trust-prompt-programmatically"></a>Para desabilitar o prompt de confiança do ClickOnce por meio de programação  
  
1.  Crie um aplicativo de console do Visual Basic ou Visual c# no Visual Studio.  
  
2.  Abra o *Program. vb* ou *Program.cs* arquivo para edição e adicione o código a seguir.  
  
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
  
3.  Crie e execute o aplicativo.  
  
## <a name="see-also"></a>Consulte também  
 [Proteger aplicativos ClickOnce](../deployment/securing-clickonce-applications.md)   
 [Segurança de acesso do código para aplicativos ClickOnce](../deployment/code-access-security-for-clickonce-applications.md)   
 [ClickOnce e Authenticode](../deployment/clickonce-and-authenticode.md)   
 [Visão geral da implantação de aplicativo confiável](../deployment/trusted-application-deployment-overview.md)   
 [Como: Habilitar configurações de segurança do ClickOnce](../deployment/how-to-enable-clickonce-security-settings.md)   
 [Como: definir uma zona de segurança para um aplicativo ClickOnce](../deployment/how-to-set-a-security-zone-for-a-clickonce-application.md)   
 [Como: definir permissões personalizadas para um aplicativo ClickOnce](../deployment/how-to-set-custom-permissions-for-a-clickonce-application.md)   
 [Como: depurar um aplicativo ClickOnce com permissões restritas](../deployment/how-to-debug-a-clickonce-application-with-restricted-permissions.md)   
 [Como: adicionar um fornecedor confiável a um computador cliente para aplicativos ClickOnce](../deployment/how-to-add-a-trusted-publisher-to-a-client-computer-for-clickonce-applications.md)   
 [Como: assinar novamente os manifestos de aplicativo e implantação](../deployment/how-to-re-sign-application-and-deployment-manifests.md)
