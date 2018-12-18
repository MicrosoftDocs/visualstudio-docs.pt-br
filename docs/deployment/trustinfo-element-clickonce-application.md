---
title: '&lt;trustInfo&gt; elemento (aplicativo ClickOnce) | Microsoft Docs'
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-deployment
ms.topic: reference
f1_keywords:
- urn:schemas-microsoft-com:asm.v2#IPermission
- urn:schemas-microsoft-com:asm.v2#PermissionSet
- urn:schemas-microsoft-com:asm.v2#assemblyRequest
- urn:schemas-microsoft-com:asm.v2#trustInfo
- urn:schemas-microsoft-com:asm.v2#defaultAssemblyRequest
- urn:schemas-microsoft-com:asm.v2#security
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- manifests [ClickOnce], trustInfo element
- <trustInfo> element [ClickOnce application manifest]
ms.assetid: 8a813a74-e158-4308-be78-565937f6af83
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: d6d6f7955cb010d981b62e2b9fcdc70a092d76ef
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49941212"
---
# <a name="lttrustinfogt-element-clickonce-application"></a>&lt;trustInfo&gt; elemento (aplicativo ClickOnce)
Descreve as permissões de segurança mínima necessárias para o aplicativo seja executado no computador cliente.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml
  
      <trustInfo>  
   <security>  
      <applicationRequestMinimum>  
         <PermissionSet  
            ID  
            Unrestricted>  
            <IPermission  
               class  
               version  
               Unrestricted  
            />  
         </PermissionSet>  
         <defaultAssemblyRequest  
            permissionSetReference  
         />  
         <assemblyRequest  
            name  
            permissionSetReference  
         />  
      </applicationRequestMinimum>  
      <requestedPrivileges>  
         <requestedExecutionLevel  
            level  
            uiAccess  
         />  
      </requestedPrivileges>  
   </security>  
</trustInfo>  
```  
  
## <a name="elements-and-attributes"></a>Elementos e atributos  
 O `trustInfo` elemento é necessário e está no `asm.v2` namespace. Ele não tem atributos e contém os seguintes elementos.  
  
## <a name="security"></a>segurança  
 Necessário. Esse elemento é um filho de `trustInfo` elemento. Ele contém o `applicationRequestMinimum` elemento e não tem atributos.  
  
## <a name="applicationrequestminimum"></a>applicationRequestMinimum  
 Necessário. Esse elemento é um filho de `security` elemento e contém o `PermissionSet`, `assemblyRequest`, e `defaultAssemblyRequest`elementos. Esse elemento não tem atributos.  
  
## <a name="permissionset"></a>PermissionSet  
 Necessário. Esse elemento é um filho de `applicationRequestMinimum` elemento e contém o `IPermission` elemento. Este elemento tem os seguintes atributos.  
  
-   `ID`  
  
     Necessário. Identifica o conjunto de permissões. Esse atributo pode ser qualquer valor. A ID é referenciada na `defaultAssemblyRequest` e `assemblyRequest` atributos.  
  
-   `version`  
  
     Necessário. Identifica a versão da permissão. Normalmente, esse valor é `1`.  
  
## <a name="ipermission"></a>IPermission  
 Opcional. Esse elemento é um filho de `PermissionSet` elemento. O `IPermission` elemento totalmente identifica uma classe de permissão no [!INCLUDE[dnprdnshort](../code-quality/includes/dnprdnshort_md.md)]. O `IPermission` elemento tem os seguintes atributos, mas pode ter atributos adicionais que correspondem às propriedades da classe de permissão. Para descobrir a sintaxe para uma permissão específica, consulte os exemplos listados no arquivo config.  
  
-   `class`  
  
     Necessário. Identifica a classe de permissão por nome forte. Por exemplo, o código a seguir identifica o `FileDialogPermission` tipo.  
  
     `System.Security.Permissions.FileDialogPermission, mscorlib, Version=1.2.3300.0, Culture=neutral, PublicKeyToken=b77a5c561934e089`  
  
-   `version`  
  
     Necessário. Identifica a versão da permissão. Normalmente, esse valor é `1`.  
  
-   `Unrestricted`  
  
     Necessário. Identifica se o aplicativo precisa de uma concessão irrestrita dessa permissão. Se `true`, a concessão de permissão é incondicional. Se `false`, ou se esse atributo for indefinido, ele é restrito de acordo com os atributos de permissão específica definidos no `IPermission` marca. Execute as seguintes permissões:  
  
    ```xml  
    <IPermission  
      class="System.Security.Permissions.EnvironmentPermission, mscorlib, Version=1.2.3300.0, Culture=neutral, PublicKeyToken=b77a5c561934e089"   
      version="1"   
      Read="USERNAME" />  
    <IPermission  
      class="System.Security.Permissions.FileDialogPermission, mscorlib, Version=1.2.3300.0, Culture=neutral, PublicKeyToken=b77a5c561934e089"   
      version="1"   
      Unrestricted="true" />  
    ```  
  
     Neste exemplo, a declaração <xref:System.Security.Permissions.EnvironmentPermission> restringe o aplicativo a ler apenas a nome de usuário, da variável de ambiente, enquanto a declaração <xref:System.Security.Permissions.FileDialogPermission> fornece o uso do aplicativo irrestrito de todas as <xref:System.Windows.Forms.FileDialog> classes.  
  
## <a name="defaultassemblyrequest"></a>defaultAssemblyRequest  
 Opcional. Identifica o conjunto de permissões concedidas a todos os assemblies. Esse elemento é um filho de `applicationRequestMinimum` elemento e tem o seguinte atributo.  
  
-   `permissionSetReference`  
  
     Necessário. Identifica a ID do conjunto de permissões que é a permissão padrão. O conjunto de permissões é declarado no `PermissionSet` elemento.  
  
## <a name="assemblyrequest"></a>assemblyRequest  
 Opcional. Identifica as permissões para um assembly específico. Esse elemento é um filho de `applicationRequestMinimum` elemento e tem os seguintes atributos.  
  
-   `Name`  
  
     Necessário. Identifica o nome do assembly.  
  
-   `permissionSetReference`  
  
     Necessário. Identifica a ID do conjunto de permissões que requer esse assembly. O conjunto de permissões é declarado no `PermissionSet` elemento.  
  
## <a name="requestedprivileges"></a>requestedPrivileges  
 Opcional. Esse elemento é um filho de `security` elemento e contém o `requestedExecutionLevel` elemento. Esse elemento não tem atributos.  
  
## <a name="requestedexecutionlevel"></a>requestedExecutionLevel  
 Opcional. Identifica o nível de segurança no qual o aplicativo solicita a ser executado. Esse elemento não tem filhos e tem os seguintes atributos.  
  
- `Level`  
  
   Necessário. Indica que o nível de segurança do aplicativo está solicitando. Os possíveis valores são:  
  
   `asInvoker`, não solicitando nenhuma permissão adicional. Este nível exige que não solicita nenhuma confiança adicional.  
  
   `highestAvailable`, solicitando as permissões mais altas disponíveis para o processo pai.  
  
   `requireAdministrator`, solicitando permissões de administrador completo.  
  
   [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] aplicativos instalará apenas com um valor de `asInvoker`. Instalação com qualquer outro valor falhará.  
  
- `uiAccess`  
  
   Opcional. Indica se o aplicativo requer acesso aos elementos de interface do usuário protegido. Os valores são `true` ou `false`, e o padrão é false. Somente os aplicativos assinados devem ter um valor true.  
  
## <a name="remarks"></a>Comentários  
 Se um [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] aplicativo pede mais permissões do que o computador cliente, será concedido por padrão, o common language Gerenciador do runtime de confiança solicitará ao usuário se ela deseja conceder ao aplicativo nesse alto nível de confiança. Se ela disser não, o aplicativo não será executado; Caso contrário, ele será executado com as permissões solicitadas.  
  
 Todas as permissões solicitadas usando `defaultAssemblyRequest` e `assemblyRequest` será concedido sem nenhum aviso ao usuário se o manifesto de implantação tiver uma licença de confiança válida.  
  
 Para obter mais informações sobre a elevação de permissões, consulte [Protegendo aplicativos ClickOnce](../deployment/securing-clickonce-applications.md). Para obter mais informações sobre a implantação de política, consulte [Trusted Application Deployment Overview](../deployment/trusted-application-deployment-overview.md).  
  
## <a name="examples"></a>Exemplos  
 Os exemplos de código de três a seguir ilustram `trustInfo` elementos para o padrão chamado zonas de segurança — Internet, intranet local e FullTrust — para uso em um [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] manifesto do aplicativo da implantação.  
  
 O primeiro exemplo ilustra o `trustInfo` elemento para as permissões padrão disponíveis na zona de segurança da Internet.  
  
```xml  
<trustInfo>  
    <security>  
      <applicationRequestMinimum>  
        <PermissionSet ID="Internet">  
          <IPermission  
            class="System.Security.Permissions.FileDialogPermission, mscorlib, Version=1.2.3300.0, Culture=neutral, PublicKeyToken=b77a5c561934e089"  
            version="1"   
            Access="Open" />  
          <IPermission  
           class="System.Security.Permissions.IsolatedStorageFilePermission, mscorlib, Version=1.2.3300.0, Culture=neutral, PublicKeyToken=b77a5c561934e089"   
            version="1"  
            Allowed="DomainIsolationByUser"  
            UserQuota="10240" />  
          <IPermission  
            class="System.Security.Permissions.SecurityPermission, mscorlib, Version=1.2.3300.0, Culture=neutral, PublicKeyToken=b77a5c561934e089"  
            version="1"   
            Flags="Execution" />  
          <IPermission   
            class="System.Security.Permissions.UIPermission, mscorlib, Version=1.2.3300.0, Culture=neutral, PublicKeyToken=b77a5c561934e089"   
            version="1"   
            Window="SafeTopLevelWindows"  
            Clipboard="OwnClipboard" />  
          <IPermission  
            class="System.Drawing.Printing.PrintingPermission, System.Drawing, Version=1.2.3300.0, Culture=neutral, PublicKeyToken=b03f5f7f11d50a3a"  
            version="1"   
            Level="SafePrinting" />  
        </PermissionSet>  
        <defaultAssemblyRequest permissionSetReference="Internet" />  
      </applicationRequestMinimum>  
    </security>  
  </trustInfo>  
```  
  
 O segundo exemplo ilustra o `trustInfo` elemento para as permissões padrão disponíveis na zona de segurança LocalIntranet.  
  
```xml  
<trustInfo>  
    <security>  
      <applicationRequestMinimum>  
        <PermissionSet ID="LocalIntranet">  
          <IPermission  
            class="System.Security.Permissions.EnvironmentPermission, mscorlib, Version=1.2.3300.0, Culture=neutral, PublicKeyToken=b77a5c561934e089"   
            version="1"   
            Read="USERNAME" />  
          <IPermission  
            class="System.Security.Permissions.FileDialogPermission, mscorlib, Version=1.2.3300.0, Culture=neutral, PublicKeyToken=b77a5c561934e089"   
            version="1"   
            Unrestricted="true" />  
          <IPermission  
            class="System.Security.Permissions.IsolatedStorageFilePermission, mscorlib, Version=1.2.3300.0, Culture=neutral, PublicKeyToken=b77a5c561934e089"   
            version="1"   
            Allowed="AssemblyIsolationByUser"  
            UserQuota="9223372036854775807"  
            Expiry="9223372036854775807"  
            Permanent="True" />  
          <IPermission  
            class="System.Security.Permissions.ReflectionPermission, mscorlib, Version=1.2.3300.0, Culture=neutral, PublicKeyToken=b77a5c561934e089"   
            version="1"   
            Flags="ReflectionEmit" />  
          <IPermission  
            class="System.Security.Permissions.SecurityPermission, mscorlib, Version=1.2.3300.0, Culture=neutral, PublicKeyToken=b77a5c561934e089"   
            version="1"   
            Flags="Assertion, Execution" />  
          <IPermission   
            class="System.Security.Permissions.UIPermission, mscorlib, Version=1.2.3300.0, Culture=neutral, PublicKeyToken=b77a5c561934e089"  
            version="1"   
            Unrestricted="true" />  
          <IPermission  
            class="System.Net.DnsPermission, System, Version=1.2.3300.0, Culture=neutral, PublicKeyToken=b77a5c561934e089"  
            version="1"   
            Unrestricted="true" />  
          <IPermission  
            class="System.Drawing.Printing.PrintingPermission, System.Drawing, Version=1.2.3300.0, Culture=neutral, PublicKeyToken=b03f5f7f11d50a3a"  
            version="1"  
            Level="DefaultPrinting" />  
          <IPermission  
            class="System.Diagnostics.EventLogPermission, System, Version=1.2.3300.0, Culture=neutral, PublicKeyToken=b77a5c561934e089"  
            version="1" />  
        </PermissionSet>  
        <defaultAssemblyRequest permissionSetReference="LocalIntranet" />  
      </applicationRequestMinimum>  
    </security>  
</trustInfo>  
```  
  
 O terceiro exemplo ilustra o `trustInfo` elemento para as permissões padrão disponíveis na zona de segurança FullTrust.  
  
```xml  
<trustInfo>  
  <security>  
    <applicationRequestMinimum>  
      <PermissionSet ID="FullTrust" Unrestricted="true" />  
      <defaultAssemblyRequest permissionSetReference="FullTrust" />  
    </applicationRequestMinimum>  
  </security>  
</trustInfo>  
```  
  
## <a name="see-also"></a>Consulte também  
 [Visão geral de implantação de aplicativos confiável](../deployment/trusted-application-deployment-overview.md)   
 [Manifesto do aplicativo ClickOnce](../deployment/clickonce-application-manifest.md)