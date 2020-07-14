---
title: 'Como: configurar a segurança da lista de inclusão'
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- permissions [Office development in Visual Studio
- inclusion lists [Office development in Visual Studio]
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 459cf3f33197939a916a5f11a94bbaf09e8142e3
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85541629"
---
# <a name="how-to-configure-inclusion-list-security"></a>Como: configurar a segurança da lista de inclusão
  Se você tiver permissões de administrador, poderá configurar o [!INCLUDE[ndptecclick](../vsto/includes/ndptecclick-md.md)] prompt de confiança para controlar se os usuários finais recebem a opção de instalar soluções do Office, salvando uma decisão de confiança na lista de inclusão. Para obter informações sobre listas de inclusão, consulte [confiar em soluções do Office usando listas de inclusão](../vsto/trusting-office-solutions-by-using-inclusion-lists.md).

 [!INCLUDE[appliesto_all](../vsto/includes/appliesto-all-md.md)]

 Para soluções que estão em cada uma das cinco zonas, você pode definir as seguintes opções:

- Habilite a [!INCLUDE[ndptecclick](../vsto/includes/ndptecclick-md.md)] chave de prompt de confiança e a lista de inclusão. Você pode permitir que os usuários finais ascedam confiança às soluções do Office que são assinadas com qualquer certificado.

- Restrinja a [!INCLUDE[ndptecclick](../vsto/includes/ndptecclick-md.md)] chave de solicitação de confiança e a lista de inclusão. Você pode permitir que os usuários finais instalem soluções do Office que são assinadas com um certificado que identifica o Publicador, mas que ainda não é confiável.

- Desabilite a [!INCLUDE[ndptecclick](../vsto/includes/ndptecclick-md.md)] chave de solicitação de confiança e a lista de inclusão. Você pode impedir que os usuários finais instalem qualquer solução do Office que não esteja assinada com um certificado explicitamente confiável.

## <a name="enable-the-inclusion-list"></a>Habilitar a lista de inclusão
 Habilite a lista de inclusão para uma zona quando desejar que os usuários finais sejam apresentados com a opção de instalar e executar qualquer solução do Office que venha dessa zona.

### <a name="to-enable-the-inclusion-list-by-using-the-registry-editor"></a>Para habilitar a lista de inclusão usando o editor do registro

1. Abra o Editor do Registro:

    1. Clique em **Iniciar**e em **Executar**.

    2. Na caixa **abrir** , digite **regedt32.exe**e clique em **OK**.

2. Localize a seguinte chave do registro:

     **\HKEY_LOCAL_MACHINE\SOFTWARE\MICROSOFT\\.NETFramework\Security\TrustManager\PromptingLevel**

     Se a chave não existir, crie-a.

3. Adicione as seguintes subchaves como **valor de cadeia de caracteres**, se elas ainda não existirem, com os valores associados.

    |Subchave de valor da cadeia de caracteres|Valor|
    |-------------------------|-----------|
    |**Internet**|**AuthenticodeRequired**|
    |**UntrustedSites**|**Desabilitado**|
    |**Meu**|**Habilitado**|
    |**Intranet Local**|**Habilitado**|
    |**TrustedSites**|**Habilitado**|

     Por padrão, a **Internet** tem o valor **AuthenticodeRequired** e **UntrustedSites** tem o valor **desabilitado**.

### <a name="to-enable-the-inclusion-list-programmatically"></a>Para habilitar a lista de inclusão programaticamente

1. Crie um aplicativo de console do Visual Basic ou do Visual C#.

2. Abra o arquivo *Program. vb* ou *Program.cs* para edição e adicione o código a seguir.

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

3. Criar e executar o aplicativo.

## <a name="restrict-the-inclusion-list"></a>Restringir a lista de inclusão
 Restrinja a lista de inclusão para que as soluções devam ser assinadas com certificados Authenticode com identidade conhecida antes que os usuários sejam solicitados a fornecer uma decisão de confiança.

### <a name="to-restrict-the-inclusion-list"></a>Para restringir a lista de inclusão

1. Abra o Editor do Registro:

    1. Clique em **Iniciar**e em **Executar**.

    2. Na caixa **abrir** , digite **regedt32.exe**e clique em **OK**.

2. Localize a seguinte chave do registro:

     **\HKEY_LOCAL_MACHINE\SOFTWARE\MICROSOFT\\.NETFramework\Security\TrustManager\PromptingLevel**

     Se a chave não existir, crie-a.

3. Adicione as seguintes subchaves como **valor de cadeia de caracteres**, se elas ainda não existirem, com os valores associados.

    |Subchave de valor da cadeia de caracteres|Valor|
    |-------------------------|-----------|
    |**UntrustedSites**|**Desabilitado**|
    |**Internet**|**AuthenticodeRequired**|
    |**Meu**|**AuthenticodeRequired**|
    |**Intranet Local**|**AuthenticodeRequired**|
    |**TrustedSites**|**AuthenticodeRequired**|

     Por padrão, a **Internet** tem o valor **AuthenticodeRequired** e **UntrustedSites** tem o valor **desabilitado**.

### <a name="to-restrict-the-inclusion-list-programmatically"></a>Para restringir a lista de inclusão programaticamente

1. Crie um aplicativo de console do Visual Basic ou do Visual C#.

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

## <a name="disable-the-inclusion-list"></a>Desabilitar a lista de inclusão
 Você pode desabilitar a lista de inclusão para que os usuários finais possam instalar apenas soluções assinadas com um certificado confiável e conhecido.

### <a name="to-disable-the-inclusion-list"></a>Para desabilitar a lista de inclusão

1. Abra o Editor do Registro:

    1. Clique em **Iniciar**e em **Executar**.

    2. Na caixa **abrir** , digite **regedt32.exe**e clique em **OK**.

2. Crie a seguinte chave do registro se ela ainda não existir:

     **\HKEY_LOCAL_MACHINE\SOFTWARE\MICROSOFT\\.NETFramework\Security\TrustManager\PromptingLevel**

3. Adicione as seguintes subchaves como **valor de cadeia de caracteres**, se elas ainda não existirem, com os valores associados.

    |Subchave de valor da cadeia de caracteres|Valor|
    |-------------------------|-----------|
    |**UntrustedSites**|**Desabilitado**|
    |**Internet**|**Desabilitado**|
    |**Meu**|**Desabilitado**|
    |**Intranet Local**|**Desabilitado**|
    |**TrustedSites**|**Desabilitado**|

### <a name="to-disable-the-inclusion-list-programmatically"></a>Para desabilitar a lista de inclusão programaticamente

1. Crie um aplicativo de console do Visual Basic ou do Visual C#.

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

## <a name="see-also"></a>Consulte também
- [Confiar em soluções do Office usando listas de inclusão](../vsto/trusting-office-solutions-by-using-inclusion-lists.md)
- [Proteger soluções do Office](../vsto/securing-office-solutions.md)
