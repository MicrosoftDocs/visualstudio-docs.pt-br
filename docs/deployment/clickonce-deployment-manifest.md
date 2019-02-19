---
title: Manifesto de implantação do ClickOnce | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- ClickOnce, deployment manifests
- deployment manifests [ClickOnce]
ms.assetid: 8457e615-e3b6-4990-8dcf-11bc590e4e9b
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: e62fb21f33658c07a5c7b60885c0cc83310e15f4
ms.sourcegitcommit: 2193323efc608118e0ce6f6b2ff532f158245d56
ms.translationtype: MTE95
ms.contentlocale: pt-BR
ms.lasthandoff: 01/25/2019
ms.locfileid: "54927789"
---
# <a name="clickonce-deployment-manifest"></a>Manifesto de implantação do ClickOnce
Um manifesto de implantação é um arquivo XML que descreve uma [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] implantação, incluindo a identificação do atual [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] versão do aplicativo para implantar.  

 Manifestos de implantação têm os seguintes elementos e atributos.  


| Elemento | Descrição | Atributos |
| - | - | - |
| [Elemento \<assembly>](../deployment/assembly-element-clickonce-deployment.md) | Necessário. Elemento de nível superior. | `manifestVersion` |
| [Elemento \<assemblyIdentity>](../deployment/assemblyidentity-element-clickonce-deployment.md) | Necessário. Identifica o manifesto do aplicativo para o [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] aplicativo. | `name`<br /><br /> `version`<br /><br /> `publicKeyToken`<br /><br /> `processorArchitecture`<br /><br /> `culture` |
| [\<Descrição > elemento](../deployment/description-element-clickonce-deployment.md) | Necessário. Identifica as informações do aplicativo usadas para criar uma presença de shell e o **adicionar ou remover programas** item no painel de controle. | `publisher`<br /><br /> `product`<br /><br /> `supportUrl` |
| [\<implantação > elemento](../deployment/deployment-element-clickonce-deployment.md) | Opcional. Identifica os atributos usados para a implantação de atualizações e exposição ao sistema. | `install`<br /><br /> `minimumRequiredVersion`<br /><br /> `mapFileExtensions`<br /><br /> `disallowUrlActivation`<br /><br /> `trustUrlParameters` |
| [\<compatibleFrameworks > elemento](../deployment/compatibleframeworks-element-clickonce-deployment.md) | Necessário. Identifica as versões do .NET Framework em que este aplicativo pode instalar e executar. | `SupportUrl` |
| [\<dependência > elemento](../deployment/dependency-element-clickonce-deployment.md) | Necessário. Identifica a versão do aplicativo para instalar a implantação e o local do manifesto do aplicativo. | `preRequisite`<br /><br /> `visible`<br /><br /> `dependencyType`<br /><br /> `codebase`<br /><br /> `size` |
| [Elemento \<publisherIdentity>](../deployment/publisheridentity-element-clickonce-deployment.md) | Necessário para manifestos assinados. Contém informações sobre o editor que assinou o manifesto de implantação. | `Name`<br /><br /> `issuerKeyHash` |
| [\<Assinatura > elemento](../deployment/signature-element-clickonce-deployment.md) | Opcional. Contém as informações necessárias para assinar digitalmente o manifesto de implantação. | Nenhuma |
| [\<customErrorReporting > elemento](../deployment/customerrorreporting-element-clickonce-deployment.md) | Opcional. Especifica um URI para mostrar quando ocorre um erro. | URI |

## <a name="remarks"></a>Comentários  
 Identifica o arquivo de manifesto de implantação uma [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] implantação de aplicativo, incluindo a versão atual e outras configurações de implantação. Ele referencia o manifesto do aplicativo, que descreve a versão atual do aplicativo e todos os arquivos contidos dentro da implantação.  

 Para obter mais informações, consulte [Segurança e implantação do ClickOnce](../deployment/clickonce-security-and-deployment.md).  

## <a name="file-location"></a>Local do arquivo  
 O arquivo de manifesto de implantação referencia o manifesto do aplicativo correta para a versão atual do aplicativo. Quando você faz uma nova versão de uma implantação de aplicativo disponível, você deve atualizar o manifesto de implantação para se referir a novo manifesto do aplicativo.  

 O arquivo de manifesto de implantação deve ser fortemente nomeado e também pode conter certificados para validação do publicador.  

## <a name="file-name-syntax"></a>Sintaxe de nome de arquivo  
 O nome de um arquivo de manifesto de implantação deve terminar com o *. Application* extensão.  

## <a name="examples"></a>Exemplos  
 O exemplo de código a seguir ilustra um manifesto de implantação.  

```xml
<?xml version="1.0" encoding="utf-8"?>  
<asmv1:assembly xsi:schemaLocation="urn:schemas-microsoft-com:asm.v1 assembly.adaptive.xsd"  
  manifestVersion="1.0"  
  xmlns:asmv3="urn:schemas-microsoft-com:asm.v3"  
  xmlns:dsig=http://www.w3.org/2000/09/xmldsig#  
  xmlns:co.v1="urn:schemas-microsoft-com:clickonce.v1"  
  xmlns:co.v2="urn:schemas-microsoft-com:clickonce.v2"  
  xmlns="urn:schemas-microsoft-com:asm.v2"  
  xmlns:asmv1="urn:schemas-microsoft-com:asm.v1"  
  xmlns:asmv2="urn:schemas-microsoft-com:asm.v2"  
  xmlns:xrml="urn:mpeg:mpeg21:2003:01-REL-R-NS"  
  xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">  
  <assemblyIdentity   
    name="My Application Deployment.app"  
    version="1.0.0.0"  
    publicKeyToken="43cb1e8e7a352766"  
    language="neutral"  
    processorArchitecture="x86"  
    xmlns="urn:schemas-microsoft-com:asm.v1" />  
  <description  
    asmv2:publisher="My Company Name"  
    asmv2:product="My Application"  
    xmlns="urn:schemas-microsoft-com:asm.v1" />  
  <deployment install="true">  
    <subscription>  
      <update>  
        <expiration maximumAge="0" unit="days" />  
      </update>  
    </subscription>  
    <deploymentProvider codebase="\\myServer\sampleDeployment\MyApplicationDeployment.application" />  
  </deployment>  
  <compatibleFrameworks xmlns="urn:schemas-microsoft-com:clickonce.v2">  
    <framework targetVersion="4.0" profile="Full" supportedRuntime="4.0.20506" />  
    <framework targetVersion="4.0" profile="Client" supportedRuntime="4.0.20506" />  
  </compatibleFrameworks>  
  <dependency>  
    <dependentAssembly  
      dependencyType="install"  
      codebase="1.0.0.0\My Application Deployment.exe.manifest"  
      size="6756">  
      <assemblyIdentity  
        name="My Application Deployment.exe"  
        version="1.0.0.0"  
        publicKeyToken="43cb1e8e7a352766"  
        language="neutral"  
        processorArchitecture="x86"  
        type="win32" />  
      <hash>  
        <dsig:Transforms>  
          <dsig:Transform Algorithm="urn:schemas-microsoft-com:HashTransforms.Identity" />  
        </dsig:Transforms>  
        <dsig:DigestMethod Algorithm="http://www.w3.org/2000/09/xmldsig#sha1" />  
        <dsig:DigestValue>E506x9FwNauks7UjQywmzgtd3FE=</dsig:DigestValue>  
      </hash>  
    </dependentAssembly>  
  </dependency>  
<publisherIdentity name="CN=DOMAIN\MyUsername" issuerKeyHash="18312a18a21b215ecf4cdb20f5a0e0b0dd263c08" /><Signature Id="StrongNameSignature" xmlns="http://www.w3.org/2000/09/xmldsig#">  
...  
</Signature></asmv1:assembly>  
```  

## <a name="see-also"></a>Consulte também  
 [Publicar aplicativos ClickOnce](../deployment/publishing-clickonce-applications.md)