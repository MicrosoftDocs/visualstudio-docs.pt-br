---
title: '&lt;dependência&gt; elemento (implantação do ClickOnce) | Microsoft Docs'
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-deployment
ms.topic: reference
f1_keywords:
- urn:schemas-microsoft-com:asm.v2#osVersionInfo
- urn:schemas-microsoft-com:asm.v2#os
- http://www.w3.org/2000/09/xmldsig#Transform
- urn:schemas-microsoft-com:asm.v2#dependency
- http://www.w3.org/2000/09/xmldsig#DigestValue
- urn:schemas-microsoft-com:asm.v2#assemblyIdentity
- http://www.w3.org/2000/09/xmldsig#DigestMethod
- http://www.w3.org/2000/09/xmldsig#Transforms
- urn:schemas-microsoft-com:asm.v2#hash
- urn:schemas-microsoft-com:asm.v2#dependentAssembly
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- <dependency> element [ClickOnce deployment manifest]
ms.assetid: 9b4d2082-0347-4922-ac70-85f11b913039
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 33e210b0787c3325a009bc54505812f22c44da84
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49916888"
---
# <a name="ltdependencygt-element-clickonce-deployment"></a>&lt;dependência&gt; elemento (implantação do ClickOnce)
Identifica a versão do aplicativo para instalar e o local do manifesto do aplicativo.  

## <a name="syntax"></a>Sintaxe  

```xml  

      <dependency>   
   <dependentAssembly  
      preRequisite  
      visible  
      dependencyType  
      codeBase  
      size  
   >   
      <assemblyIdentity   
         name   
         version   
         publicKeyToken   
         processorArchitecture   
         language  
         type  
      />   
      <hash>  
         <dsig:Transforms>  
            <dsig:Transform  
                Algorithm  
            />  
         </dsig:Transforms>  
         <dsig:DigestMethod />  
         <dsig:DigestValue>  
         </dsig:DigestValue>  
      </hash>  

   </dependentAssembly>   
</dependency>  
```  

## <a name="elements-and-attributes"></a>Elementos e atributos  
 O `dependency` elemento é necessário. Ele não tem atributos. Um manifesto de implantação pode ter vários `dependency` elementos.  

 O `dependency` elemento geralmente expressa as dependências para o aplicativo principal em assemblies contidos dentro de um [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] aplicativo. Se seu aplicativo Main.exe consome um assembly chamado DotNetAssembly.dll, esse assembly deve estar listado em uma seção de dependência. Dependência, no entanto, pode também expressar outros tipos de dependências, como dependências em uma versão específica do common language runtime, em um assembly no cache de assembly global (GAC), ou em um objeto COM. Porque é uma tecnologia de implantação no-touch, [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] não é possível iniciar download e instalação desses tipos de dependências, mas impede que a execução do aplicativo se uma ou mais das dependências especificadas não existe.  

## <a name="dependentassembly"></a>dependentAssembly  
 Necessário. Esse elemento contém o `assemblyIdentity` elemento. A tabela a seguir mostra os atributos de `dependentAssembly` dá suporte.  


| Atributo | Descrição |
|------------------| - |
| `preRequisite` | Opcional. Especifica que esse assembly já deve existir no GAC. Os valores válidos são `true` e `false`. Se `true`e o assembly especificado não existe no GAC, o aplicativo falhar ser executado. |
| `visible` | Opcional. Identifica a identidade do aplicativo de nível superior, incluindo suas dependências. Usado internamente pelo [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] para gerenciar o armazenamento de aplicativos e a ativação. |
| `dependencyType` | Necessário. A relação entre essa dependência e o aplicativo. Os valores válidos são:<br /><br /> -   `install`. Componente representa uma instalação separada do aplicativo atual.<br />-   `preRequisite`. Componente é exigido pelo aplicativo atual. |
| `codebase` | Opcional. O caminho completo para o manifesto do aplicativo. |
| `size` | Opcional. O tamanho do manifesto do aplicativo, em bytes. |

## <a name="assemblyidentity"></a>assemblyIdentity  
 Necessário. Esse elemento é um filho de `dependentAssembly` elemento. O conteúdo do `assemblyIdentity` deve ser o mesmo descrito o [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] manifesto do aplicativo. A tabela a seguir mostra os atributos do `assemblyIdentity` elemento.  

|Atributo|Descrição|  
|---------------|-----------------|  
|`Name`|Necessário. Identifica o nome do aplicativo.|  
|`Version`|Necessário. Especifica o número de versão do aplicativo, no seguinte formato: `major.minor.build.revision`|  
|`publicKeyToken`|Necessário. Especifica uma cadeia hexadecimal de 16 caracteres que representa os últimos 8 bytes do hash SHA-1 da chave pública sob a qual o aplicativo ou assembly é assinado. A chave pública usada para assinar deve ser de 2048 bits ou superior.|  
|`processorArchitecture`|Necessário. Especifica o microprocessador. Os valores válidos são `x86` para Windows de 32 bits e `IA64` para Windows de 64 bits.|  
|`Language`|Opcional. Identifica os códigos de idioma de duas partes do assembly. Por exemplo, EN-US, que significa para inglês (EUA). O padrão é `neutral`. Elemento o `asmv2` namespace.|  
|`type`|Opcional. Para compatibilidade com Windows lado a lado com versões anteriores instale o tecnologia. O único valor permitido é `win32`.|  

## <a name="hash"></a>hash  
 O `hash` elemento é um filho opcional de `file` elemento. O `hash` elemento não tem atributos.  

 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] usa um algoritmo hash de todos os arquivos em um aplicativo como uma verificação de segurança para garantir que nenhum dos arquivos foram alterados após a implantação. Se o `hash` elemento não for incluído, essa verificação não será executada. Portanto, omitindo o `hash` elemento não é recomendado.  

## <a name="dsigtransforms"></a>DSIG:Transforms  
 O `dsig:Transforms` elemento é um filho necessário do `hash` elemento. O `dsig:Transforms` elemento não tem atributos.  

## <a name="dsigtransform"></a>DSIG:Transform  
 O `dsig:Transform` elemento é um filho necessário do `dsig:Transforms` elemento. A tabela a seguir mostra os atributos do `dsig:Transform` elemento.  


| Atributo | Descrição |
|-------------| - |
| `Algorithm` | O algoritmo usado para calcular o resumo para este arquivo. Atualmente, o único valor usado pelo [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] é `urn:schemas-microsoft-com:HashTransforms.Identity`. |

## <a name="dsigdigestmethod"></a>DSIG:DigestMethod  
 O `dsig:DigestMethod` elemento é um filho necessário do `hash` elemento. A tabela a seguir mostra os atributos do `dsig:DigestMethod` elemento.  


| Atributo | Descrição |
|-------------| - |
| `Algorithm` | O algoritmo usado para calcular o resumo para este arquivo. Atualmente, o único valor usado pelo [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] é `http://www.w3.org/2000/09/xmldsig#sha1`. |

## <a name="dsigdigestvalue"></a>DSIG:DigestValue  
 O `dsig:DigestValue` elemento é um filho necessário do `hash` elemento. O `dsig:DigestValue` elemento não tem atributos. Seu valor de texto é o hash calculado para o arquivo especificado.  

## <a name="remarks"></a>Comentários  
 Manifestos de implantação normalmente têm um único `assemblyIdentity` elemento que identifica o nome e versão do manifesto do aplicativo.  

## <a name="example"></a>Exemplo  
 O seguinte exemplo de código mostra uma `dependency` elemento em um [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] manifesto de implantação.  

```xml  
<!-- Identify the assembly dependencies -->  
<dependency>  
  <dependentAssembly dependencyType="install" allowDelayedBinding="true" codebase="MyApplication.exe" size="16384">  
    <assemblyIdentity name="MyApplication" version="0.0.0.0" cultural="neutral" processorArchitecture="msil" />  
    <hash>  
      <dsig:Transforms>  
        <dsig:Transform Algorithm="urn:schemas-microsoft-com:HashTransforms.Identity" />  
      </dsig:Transforms>  
      <dsig:DigestMethod Algorithm="http://www.w3.org/2000/09/xmldsig#sha1" />  
       <dsig:DigestValue>YzXYZJAvj9pgAG3y8jXUjC7AtHg=</dsig:DigestValue>  
    </hash>  
  </dependentAssembly>  
</dependency>  
```  

## <a name="example"></a>Exemplo  
 O exemplo de código a seguir especifica uma dependência em um assembly já instalado no GAC.  

```xml  
<dependency>  
  <dependentAssembly dependencyType="preRequisite" allowDelayedBinding="true">  
    <assemblyIdentity name="GACAssembly" version="1.0.0.0" language="neutral" processorArchitecture="msil" />  
  </dependentAssembly>  
</dependency>  
```  

## <a name="example"></a>Exemplo  
 O exemplo de código a seguir especifica uma dependência em uma versão específica do common language runtime.  

```xml  
<dependency>  
  <dependentAssembly dependencyType="preRequisite" allowDelayedBinding="true">  
    <assemblyIdentity name="Microsoft.Windows.CommonLanguageRuntime" version="2.0.50215.0" />  
  </dependentAssembly>  
</dependency>  
```  

## <a name="example"></a>Exemplo  
 O exemplo de código a seguir especifica uma dependência do sistema operacional.  

```xml  
<dependency>  
   <dependentOS supportUrl="http://www.microsoft.com" description="Microsoft Windows Operating System">  
      <osVersionInfo>  
         <os majorVersion="4" minorVersion="10" />  
      </osVersionInfo>  
   </dependentOS>  
</dependency>  
```  

## <a name="see-also"></a>Consulte também  
 [Manifesto de implantação do ClickOnce](../deployment/clickonce-deployment-manifest.md)   
 [\<dependência > elemento](../deployment/dependency-element-clickonce-application.md)