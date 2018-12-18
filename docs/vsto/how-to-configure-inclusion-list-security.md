---
title: 'Como: configurar a segurança da lista de inclusões'
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- permissions [Office development in Visual Studio
- inclusion lists [Office development in Visual Studio]
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: 6e5bd1794b76485d60588b94d3ca139a314f9723
ms.sourcegitcommit: 34f7d23ce3bd140dcae875b602d5719bb4363ed1
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/11/2018
ms.locfileid: "35255831"
---
# <a name="how-to-configure-inclusion-list-security"></a>Como: configurar a segurança da lista de inclusões
  Se você tiver permissões de administrador, você pode configurar o [!INCLUDE[ndptecclick](../vsto/includes/ndptecclick-md.md)] prompt confiável para controlar se os usuários finais recebem a opção de instalação de soluções do Office, salvando uma decisão de confiança para a lista de inclusão. Para obter informações sobre listas de inclusão, consulte [soluções do Office de confiança usando listas de inclusão](../vsto/trusting-office-solutions-by-using-inclusion-lists.md).  
  
 [!INCLUDE[appliesto_all](../vsto/includes/appliesto-all-md.md)]  
  
 Para soluções que estão em cada um dos cinco zonas, você pode definir as seguintes opções:  
  
-   Habilitar o [!INCLUDE[ndptecclick](../vsto/includes/ndptecclick-md.md)] chave Prompt de confiança e a lista de inclusão. Você pode permitir que os usuários finais conceder confiança a soluções do Office que são assinados com um certificado.  
  
-   Restringir o [!INCLUDE[ndptecclick](../vsto/includes/ndptecclick-md.md)] chave Prompt de confiança e a lista de inclusão. Você pode permitir que os usuários finais instalarem soluções do Office que são assinadas com um certificado que identifica o Editor, mas que ainda não for confiável.  
  
-   Desabilitar o [!INCLUDE[ndptecclick](../vsto/includes/ndptecclick-md.md)] chave Prompt de confiança e a lista de inclusão. Você pode impedir que os usuários finais instalando qualquer solução do Office que não está assinada com um certificado confiável explicitamente.  
  
## <a name="enable-the-inclusion-list"></a>Habilitar a lista de inclusão  
 Habilite a lista de inclusão de uma zona quando desejar que os usuários finais a ser apresentada com a opção de instalar e executar qualquer solução do Office que vem a partir dessa zona.  
  
### <a name="to-enable-the-inclusion-list-by-using-the-registry-editor"></a>Para habilitar a lista de inclusão, usando o editor do registro  
  
1.  Abra o editor do registro:  
  
    1.  Clique em **inicie**e, em seguida, clique em **executar**.  
  
    2.  No **aberto** , digite **regedt32.exe**e, em seguida, clique em **Okey**.  
  
2.  Localize a seguinte chave do registro:  
  
     **\HKEY_LOCAL_MACHINE\SOFTWARE\MICROSOFT\\. NETFramework\Security\TrustManager\PromptingLevel**  
  
     Se a chave não existir, crie-o.  
  
3.  Adicione as seguintes subchaves como **valor de cadeia de caracteres**, se ainda não existirem, com os valores associados.  
  
    |Subchave do valor de cadeia de caracteres|Valor|  
    |-------------------------|-----------|  
    |**Internet**|**AuthenticodeRequired**|  
    |**UntrustedSites**|**Desabilitado**|  
    |**Meu computador**|**Habilitado**|  
    |**LocalIntranet**|**Habilitado**|  
    |**TrustedSites**|**Habilitado**|  
  
     Por padrão, **Internet** tem o valor **AuthenticodeRequired** e **UntrustedSites** tem o valor **desabilitado**.  
  
### <a name="to-enable-the-inclusion-list-programmatically"></a>Para habilitar a lista de inclusão de forma programática  
  
1.  Crie um aplicativo de console do Visual Basic ou Visual c#.  
  
2.  Abra o *Program. vb* ou *Program.cs* arquivo para edição e adicione o código a seguir.  
  
    ```vb  
    Dim key As Microsoft.Win32.RegistryKey  
    key = Microsoft.Win32.Registry.LocalMachine.CreateSubKey("SOFTWARE\MICROSOFT\.NETFramework\Security\TrustManager\PromptingLevel")  
    key.SetValue("MyComputer", "Enabled")  
    key.SetValue("LocalIntranet", "Enabled")  
    key.SetValue("Internet", "AuthenticodeRequired")  
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
  
## <a name="restrict-the-inclusion-list"></a>Restringir a lista de inclusão  
 Restringir a lista de inclusão para que as soluções devem ser assinadas com certificados Authenticode que têm conhecidos identidade antes que os usuários são solicitados para uma decisão de confiança.  
  
### <a name="to-restrict-the-inclusion-list"></a>Para restringir a lista de inclusão  
  
1.  Abra o editor do registro:  
  
    1.  Clique em **inicie**e, em seguida, clique em **executar**.  
  
    2.  No **aberto** , digite **regedt32.exe**e, em seguida, clique em **Okey**.  
  
2.  Localize a seguinte chave do registro:  
  
     **\HKEY_LOCAL_MACHINE\SOFTWARE\MICROSOFT\\. NETFramework\Security\TrustManager\PromptingLevel**  
  
     Se a chave não existir, crie-o.  
  
3.  Adicione as seguintes subchaves como **valor de cadeia de caracteres**, se ainda não existirem, com os valores associados.  
  
    |Subchave do valor de cadeia de caracteres|Valor|  
    |-------------------------|-----------|  
    |**UntrustedSites**|**Desabilitado**|  
    |**Internet**|**AuthenticodeRequired**|  
    |**Meu computador**|**AuthenticodeRequired**|  
    |**LocalIntranet**|**AuthenticodeRequired**|  
    |**TrustedSites**|**AuthenticodeRequired**|  
  
     Por padrão, **Internet** tem o valor **AuthenticodeRequired** e **UntrustedSites** tem o valor **desabilitado**.  
  
### <a name="to-restrict-the-inclusion-list-programmatically"></a>Para restringir a lista de inclusão programaticamente  
  
1.  Crie um aplicativo de console do Visual Basic ou Visual c#.  
  
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
  
## <a name="disable-the-inclusion-list"></a>Desabilitar a lista de inclusão  
 Você pode desativar a lista de inclusão para que os usuários finais só pode instalar as soluções que são assinadas com um certificado confiável e conhecido.  
  
### <a name="to-disable-the-inclusion-list"></a>Para desabilitar a lista de inclusão  
  
1.  Abra o editor do registro:  
  
    1.  Clique em **inicie**e, em seguida, clique em **executar**.  
  
    2.  No **aberto** , digite **regedt32.exe**e, em seguida, clique em **Okey**.  
  
2.  Se isso ainda não existir, crie a seguinte chave do registro:  
  
     **\HKEY_LOCAL_MACHINE\SOFTWARE\MICROSOFT\\. NETFramework\Security\TrustManager\PromptingLevel**  
  
3.  Adicione as seguintes subchaves como **valor de cadeia de caracteres**, se ainda não existirem, com os valores associados.  
  
    |Subchave do valor de cadeia de caracteres|Valor|  
    |-------------------------|-----------|  
    |**UntrustedSites**|**Desabilitado**|  
    |**Internet**|**Desabilitado**|  
    |**Meu computador**|**Desabilitado**|  
    |**LocalIntranet**|**Desabilitado**|  
    |**TrustedSites**|**Desabilitado**|  
  
### <a name="to-disable-the-inclusion-list-programmatically"></a>Para desabilitar a lista de inclusão programaticamente  
  
1.  Crie um aplicativo de console do Visual Basic ou Visual c#.  
  
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
 [Confiar em soluções do Office usando listas de inclusão](../vsto/trusting-office-solutions-by-using-inclusion-lists.md)   
 [Proteger as soluções do Office](../vsto/securing-office-solutions.md)  
  
  