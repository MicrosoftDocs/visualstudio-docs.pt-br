---
title: '&lt;dependência&gt; elemento (aplicativo ClickOnce) | Microsoft Docs'
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
- manifests [ClickOnce], dependency element
- <dependency> element [ClickOnce application manifest]
ms.assetid: 09d6a1e0-60f8-4fbd-843b-8e49ee3115a3
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 4d47775f928fc52fb7ffce2e0818fea19e30dee0
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49950206"
---
# <a name="ltdependencygt-element-clickonce-application"></a>&lt;dependência&gt; elemento (aplicativo ClickOnce)
Identifica uma dependência de plataforma ou assembly que é necessária para o aplicativo.  

## <a name="syntax"></a>Sintaxe  

```xml  

      <dependency>  
   <dependentOS  
      supportURL  
      description  
   >  
      <osVersionInfo>  
         <os  
            majorVersion  
            minorVersion  
            buildNumber  
            servicePackMajor  
            servicePackMinor  
            productType  
            suiteType  
         />   
      </osVersionInfo>  
   </dependentOS>  
   <dependentAssembly  
      dependencyType  
      allowDelayedBinding  
      group  
      codeBase  
      size  
   >  
      <assemblyIdentity  
         name  
         version  
         processorArchitecture  
         language  
      >  
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

      </assemblyIdentity>  
   </dependentAssembly>  
</dependency>  
```  

## <a name="elements-and-attributes"></a>Elementos e atributos  
 O `dependency` elemento é necessário. Pode haver várias instâncias do `dependency` no manifesto do mesmo aplicativo.  

 O `dependency` elemento não tem atributos e contém os seguintes elementos filho.  

### <a name="dependentos"></a>dependentOS  
 Opcional. Contém o `osVersionInfo` elemento. O `dependentOS` e `dependentAssembly` elementos são mutuamente exclusivos: um ou outro deve existir para um `dependency` elemento, mas não ambos.  

 `dependentOS` suporta os seguintes atributos.  

|Atributo|Descrição|  
|---------------|-----------------|  
|`supportUrl`|Opcional. Especifica uma URL de suporte para a plataforma dependente. Essa URL é mostrada ao usuário se a plataforma necessária for encontrada.|  
|`description`|Opcional. Descreve, em formato legível, o sistema operacional descrito pelo `dependentOS` elemento.|  

### <a name="osversioninfo"></a>osVersionInfo  
 Necessário. Esse elemento é um filho de `dependentOS` elemento e contém o `os` elemento. Esse elemento não tem atributos.  

### <a name="os"></a>sistema operacional  
 Necessário. Esse elemento é um filho de `osVersionInfo` elemento. Este elemento tem os seguintes atributos.  

|Atributo|Descrição|  
|---------------|-----------------|  
|`majorVersion`|Necessário. Especifica o número de versão principal do sistema operacional.|  
|`minorVersion`|Necessário. Especifica o número de versão secundária do sistema operacional.|  
|`buildNumber`|Necessário. Especifica o número de compilação do sistema operacional.|  
|`servicePackMajor`|Necessário. Especifica o número principal do service pack do sistema operacional.|  
|`servicePackMinor`|Opcional. Especifica o número secundário do service pack do sistema operacional.|  
|`productType`|Opcional. Identifica o valor do tipo de produto. Os valores válidos são `server`, `workstation` e `domainController`. Por exemplo, para o Windows 2000 Professional, esse valor de atributo é `workstation`.|  
|`suiteType`|Opcional. Identifica um conjunto de produtos disponível no sistema ou o tipo de configuração do sistema. Os valores válidos são `backoffice`, `blade`, `datacenter`, `enterprise`, `home`, `professional`, `smallbusiness`, `smallbusinessRestricted`, e `terminal`. Por exemplo, para o Windows 2000 Professional, esse valor de atributo é `professional`.|  

### <a name="dependentassembly"></a>dependentAssembly  
 Opcional. Contém o `assemblyIdentity` elemento. O `dependentOS` e `dependentAssembly` elementos são mutuamente exclusivos: um ou outro deve existir para um `dependency` elemento, mas não ambos.  

 `dependentAssembly` tem os seguintes atributos.  


| Atributo | Descrição |
|-----------------------| - |
| `dependencyType` | Necessário. Especifica o tipo de dependência. Os valores válidos são `preprequisite` e `install`. Uma `install` assembly é instalado como parte do [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] aplicativo. Um `prerequisite` assembly deve estar presente no cache de assembly global (GAC) antes do [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] pode instalar o aplicativo. |
| `allowDelayedBinding` | Necessário. Especifica se o assembly pode ser carregado por meio de programação em tempo de execução. |
| `group` | Opcional. Se o `dependencyType` atributo é definido como `install`, designa um grupo nomeado de assemblies somente instalação sob demanda. Para obter mais informações, consulte [Walkthrough: Downloading Assemblies on Demand with the ClickOnce Deployment API Using the Designer](../deployment/walkthrough-downloading-assemblies-on-demand-with-the-clickonce-deployment-api-using-the-designer.md) (Instruções passo a passo: baixando assemblies sob demanda com a API de implantação do ClickOnce usando o designer).<br /><br /> Se definido como `framework` e o `dependencyType` atributo é definido como `prerequisite`, designa o assembly como parte do .NET Framework. O cache de assembly global (GAC) não é verificado para esse assembly ao instalar em [!INCLUDE[net_v40_short](../code-quality/includes/net_v40_short_md.md)] e versões posteriores. |
| `codeBase` | Necessário quando o `dependencyType` atributo é definido como `install`. O caminho para o assembly dependente. Talvez um caminho absoluto ou um caminho relativo ao código do manifesto base. Esse caminho deve ser um URI válido para o manifesto do assembly que seja válido. |
| `size` | Necessário quando o `dependencyType` atributo é definido como `install`. O tamanho do assembly dependente, em bytes. |

### <a name="assemblyidentity"></a>assemblyIdentity  
 Necessário. Esse elemento é um filho de `dependentAssembly` elemento e tem os seguintes atributos.  

|Atributo|Descrição|  
|---------------|-----------------|  
|`name`|Necessário. Identifica o nome do aplicativo.|  
|`version`|Necessário. Especifica o número de versão do aplicativo no seguinte formato: `major.minor.build.revision`|  
|`publicKeyToken`|Opcional. Especifica uma cadeia hexadecimal de 16 caracteres que representa os últimos 8 bytes do `SHA-1` valor de hash da chave pública sob a qual o aplicativo ou assembly é assinado. A chave pública usada para assinar o catálogo deve ser de 2048 bits ou mais.|  
|`processorArchitecture`|Opcional. Especifica o processador. Os valores válidos são `x86` para Windows de 32 bits e `I64` para Windows de 64 bits.|  
|`language`|Opcional. Identifica os códigos de idioma de duas partes, como EN-US do assembly.|  

### <a name="hash"></a>hash  
 O `hash` elemento é um filho opcional de `assemblyIdentity` elemento. O `hash` elemento não tem atributos.  

 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] usa um algoritmo hash de todos os arquivos em um aplicativo como uma verificação de segurança, para garantir que nenhum dos arquivos foram alterados após a implantação. Se o `hash` elemento não for incluído, essa verificação não será executada. Portanto, omitindo o `hash` elemento não é recomendado.  

### <a name="dsigtransforms"></a>DSIG:Transforms  
 O `dsig:Transforms` elemento é um filho necessário do `hash` elemento. O `dsig:Transforms` elemento não tem atributos.  

### <a name="dsigtransform"></a>DSIG:Transform  
 O `dsig:Transform` elemento é um filho necessário do `dsig:Transforms` elemento. O `dsig:Transform` elemento tem os seguintes atributos.  


| Atributo | Descrição |
|-------------| - |
| `Algorithm` | O algoritmo usado para calcular o resumo para este arquivo. Atualmente, o único valor usado pelo [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] é `urn:schemas-microsoft-com:HashTransforms.Identity`. |

### <a name="dsigdigestmethod"></a>DSIG:DigestMethod  
 O `dsig:DigestMethod` elemento é um filho necessário do `hash` elemento. O `dsig:DigestMethod` elemento tem os seguintes atributos.  


| Atributo | Descrição |
|-------------| - |
| `Algorithm` | O algoritmo usado para calcular o resumo para este arquivo. Atualmente, o único valor usado pelo [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] é `http://www.w3.org/2000/09/xmldsig#sha1`. |

### <a name="dsigdigestvalue"></a>DSIG:DigestValue  
 O `dsig:DigestValue` elemento é um filho necessário do `hash` elemento. O `dsig:DigestValue` elemento não tem atributos. Seu valor de texto é o hash calculado para o arquivo especificado.  

## <a name="remarks"></a>Comentários  
 Todos os assemblies usados pelo seu aplicativo devem ter um correspondente `dependency` elemento. Assemblies de dependentes não incluem assemblies que devem ser pré-instalados no cache de assembly global como assemblies de plataforma.  

## <a name="example"></a>Exemplo  
 O exemplo de código a seguir ilustra `dependency` elementos em um [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] manifesto do aplicativo. Este exemplo de código é parte de um exemplo maior fornecido para o [manifesto do aplicativo ClickOnce](../deployment/clickonce-application-manifest.md) tópico.  

```xml  
<dependency>  
  <dependentOS>  
    <osVersionInfo>  
      <os   
        majorVersion="4"   
        minorVersion="10"   
        buildNumber="0"   
        servicePackMajor="0" />  
    </osVersionInfo>  
  </dependentOS>  
</dependency>  
<dependency>  
  <dependentAssembly  
    dependencyType="preRequisite"  
    allowDelayedBinding="true">  
    <assemblyIdentity  
      name="Microsoft.Windows.CommonLanguageRuntime"  
      version="4.0.20506.0" />  
  </dependentAssembly>  
</dependency>  

<dependency>  
  <dependentAssembly  
    dependencyType="install"  
    allowDelayedBinding="true"  
    codebase="MyApplication.exe"  
    size="4096">  
    <assemblyIdentity  
      name="MyApplication"  
      version="1.0.0.0"  
      language="neutral"  
      processorArchitecture="x86" />  
    <hash>  
      <dsig:Transforms>  
        <dsig:Transform Algorithm="urn:schemas-microsoft-com:HashTransforms.Identity" />  
      </dsig:Transforms>  
      <dsig:DigestMethod Algorithm="http://www.w3.org/2000/09/xmldsig#sha1" />  
      <dsig:DigestValue>DpTW7RzS9IeT/RBSLj54vfTEzNg=</dsig:DigestValue>  
    </hash>  
  </dependentAssembly>  
</dependency>  
```  

## <a name="see-also"></a>Consulte também  
 [Manifesto do aplicativo ClickOnce](../deployment/clickonce-application-manifest.md)   
 [\<dependência > elemento](../deployment/dependency-element-clickonce-deployment.md)