---
title: Manifesto de aplicativo ClickOnce | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-deployment
ms.topic: reference
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- application manifests [ClickOnce]
- ClickOnce, application manifests
ms.assetid: 29570cec-4e53-4660-a850-abc4fa150243
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 5326f71ba7a075cc6ca3e321318de89624c56894
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49872884"
---
# <a name="clickonce-application-manifest"></a>Manifesto do aplicativo ClickOnce
Um [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] manifesto do aplicativo é um arquivo XML que descreve um aplicativo que é implantado usando [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)].  

[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] manifestos de aplicativo têm os seguintes elementos e atributos.  


| Elemento | Descrição | Atributos |
| - | - | - |
| [\<assembly > elemento](../deployment/assembly-element-clickonce-application.md) | Necessário. Elemento de nível superior. | `manifestVersion` |
| [\<assemblyIdentity > elemento](../deployment/assemblyidentity-element-clickonce-application.md) | Necessário. Identifica o assembly principal da [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] aplicativo. | `name`<br /><br /> `version`<br /><br /> `publicKeyToken`<br /><br /> `processorArchitecture`<br /><br /> `language` |
| [\<trustInfo > elemento](../deployment/trustinfo-element-clickonce-application.md) | Identifica os requisitos de segurança do aplicativo. | Nenhum |
| [\<entryPoint > elemento](../deployment/entrypoint-element-clickonce-application.md) | Necessário. Identifica o ponto de entrada de código do aplicativo. | `name` |
| [\<dependência > elemento](../deployment/dependency-element-clickonce-application.md) | Necessário. Identifica cada dependência necessária para a execução do aplicativo. Opcionalmente, identifica os assemblies que precisam ser pré-instalado. | Nenhum |
| [\<Elemento file>](../deployment/file-element-clickonce-application.md) | Opcional. Identifica cada arquivo nonassembly que é usado pelo aplicativo. Pode incluir dados de isolamento (COM Component Object Model) associados ao arquivo. | `name`<br /><br /> `size`<br /><br /> `group`<br /><br /> `optional`<br /><br /> `writeableType` |
| [\<fileAssociation > elemento](../deployment/fileassociation-element-clickonce-application.md) | Opcional. Identifica uma extensão de arquivo a ser associado com o aplicativo. | `extension`<br /><br /> `description`<br /><br /> `progid`<br /><br /> `defaultIcon` |

## <a name="remarks"></a>Comentários  
 O [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] arquivo de manifesto do aplicativo identifica um aplicativo implantado usando [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)]. Para obter mais informações sobre o [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)], consulte [Segurança e implantação do ClickOnce](../deployment/clickonce-security-and-deployment.md).  

## <a name="file-location"></a>Local do arquivo  
 Um [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] manifesto do aplicativo é específico para uma única versão de uma implantação. Por esse motivo, eles devem ser armazenados separadamente dos manifestos de implantação. A convenção comum é colocá-los em um subdiretório chamado depois que a versão associada.  

 O manifesto do aplicativo sempre deve ser assinado antes da implantação. Se você alterar manualmente um manifesto de aplicativo, você deve usar *mage.exe* para assinar novamente o manifesto do aplicativo, atualize o manifesto de implantação e, em seguida, assinar novamente o manifesto de implantação. Para obter mais informações, consulte [instruções passo a passo: implantar manualmente um aplicativo ClickOnce](../deployment/walkthrough-manually-deploying-a-clickonce-application.md).  

## <a name="file-name-syntax"></a>Sintaxe de nome de arquivo  
 O nome de um [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] arquivo de manifesto do aplicativo deve ser o nome completo e a extensão do aplicativo, conforme identificado na `assemblyIdentity` elemento, seguido pela extensão *. manifest*. Por exemplo, um manifesto de aplicativo refere-se para o *Example.exe* aplicativo usaria a seguinte sintaxe de nome de arquivo.  

 `example.exe.manifest`  

## <a name="example"></a>Exemplo  
 O exemplo de código a seguir mostra um manifesto de aplicativo para um [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] aplicativo.  

```xml
<?xml version="1.0" encoding="utf-8"?>  
<asmv1:assembly xsi:schemaLocation="urn:schemas-microsoft-com:asm.v1 assembly.adaptive.xsd" manifestVersion="1.0" xmlns:asmv3="urn:schemas-microsoft-com:asm.v3" xmlns:dsig="http://www.w3.org/2000/09/xmldsig#" xmlns:co.v2="urn:schemas-microsoft-com:clickonce.v2" xmlns="urn:schemas-microsoft-com:asm.v2" xmlns:asmv1="urn:schemas-microsoft-com:asm.v1" xmlns:asmv2="urn:schemas-microsoft-com:asm.v2" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:co.v1="urn:schemas-microsoft-com:clickonce.v1">  
  <asmv1:assemblyIdentity name="My Application Deployment.exe" version="1.0.0.0" publicKeyToken="43cb1e8e7a352766" language="neutral" processorArchitecture="x86" type="win32" />  
  <application />  
  <entryPoint>  
    <assemblyIdentity name="MyApplication" version="1.0.0.0" language="neutral" processorArchitecture="x86" />  
    <commandLine file="MyApplication.exe" parameters="" />  
  </entryPoint>  
  <trustInfo>  
    <security>  
      <applicationRequestMinimum>  
        <PermissionSet Unrestricted="true" ID="Custom" SameSite="site" />  
        <defaultAssemblyRequest permissionSetReference="Custom" />  
      </applicationRequestMinimum>  
      <requestedPrivileges xmlns="urn:schemas-microsoft-com:asm.v3">  
        <!--  
          UAC Manifest Options  
          If you want to change the Windows User Account Control level replace the   
          requestedExecutionLevel node with one of the following.  

        <requestedExecutionLevel  level="asInvoker" uiAccess="false" />  
        <requestedExecutionLevel  level="requireAdministrator" uiAccess="false" />  
        <requestedExecutionLevel  level="highestAvailable" uiAccess="false" />  

         If you want to utilize File and Registry Virtualization for backward   
         compatibility then delete the requestedExecutionLevel node.  
    -->  
        <requestedExecutionLevel level="asInvoker" uiAccess="false" />  
      </requestedPrivileges>  
    </security>  
  </trustInfo>  
  <dependency>  
    <dependentOS>  
      <osVersionInfo>  
        <os majorVersion="4" minorVersion="10" buildNumber="0" servicePackMajor="0" />  
      </osVersionInfo>  
    </dependentOS>  
  </dependency>  
  <dependency>  
    <dependentAssembly dependencyType="preRequisite" allowDelayedBinding="true">  
      <assemblyIdentity name="Microsoft.Windows.CommonLanguageRuntime" version="4.0.20506.0" />  
    </dependentAssembly>  
  </dependency>  
  <dependency>  
    <dependentAssembly dependencyType="install" allowDelayedBinding="true" codebase="MyApplication.exe" size="4096">  
      <assemblyIdentity name="MyApplication" version="1.0.0.0" language="neutral" processorArchitecture="x86" />  
      <hash>  
        <dsig:Transforms>  
          <dsig:Transform Algorithm="urn:schemas-microsoft-com:HashTransforms.Identity" />  
        </dsig:Transforms>  
        <dsig:DigestMethod Algorithm="http://www.w3.org/2000/09/xmldsig#sha1" />  
        <dsig:DigestValue>DpTW7RzS9IeT/RBSLj54vfTEzNg=</dsig:DigestValue>  
      </hash>  
    </dependentAssembly>  
  </dependency>  
<publisherIdentity name="CN=DOMAINCONTROLLER\UserMe" issuerKeyHash="18312a18a21b215ecf4cdb20f5a0e0b0dd263c08" /><Signature Id="StrongNameSignature" xmlns="http://www.w3.org/2000/09/xmldsig#">  
...  
</Signature></r:issuer></r:license></msrel:RelData></KeyInfo></Signature></asmv1:assembly>  
```  

## <a name="see-also"></a>Consulte também  
 [Publicar aplicativos ClickOnce](../deployment/publishing-clickonce-applications.md)