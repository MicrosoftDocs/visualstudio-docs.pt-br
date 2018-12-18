---
title: Configurações padrão e personalizadas do Conjunto de Ferramentas | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-sdk
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- MSBuild, custom toolset configurations
- MSBuild, msbuild.exe.config
ms.assetid: 15a048c8-5ad3-448e-b6e9-e3c5d7147ed2
caps.latest.revision: 34
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 1a1d57903ec2a8c3afb439f27433898467028eb6
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49906696"
---
# <a name="standard-and-custom-toolset-configurations"></a>Configurações padrão e personalizadas do Toolset
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]


Um Conjunto de Ferramentas MSBuild contém referências a tarefas, destinos e ferramentas que você pode usar para criar um projeto de aplicativo. MSBuild inclui um Conjunto de Ferramentas padrão, mas você também pode criar ferramentas personalizadas. Para obter informações sobre como especificar um Conjunto de Ferramentas, consulte [Conjunto de Ferramentas (ToolsVersion)](../msbuild/msbuild-toolset-toolsversion.md)  

## <a name="standard-toolset-configurations"></a>Configurações padrão do Conjunto de Ferramentas  
 O MSBuild 12.0 inclui os seguintes conjuntos de ferramentas padrão:  


| ToolsVersion | Caminho do conjunto de ferramentas (conforme especificado na propriedade de build do MSBuildToolsPath ou MSBuildBinPath) |
|--------------|--------------------------------------------------------------------------------------|
|     2.0      |           *Caminho de instalação do Windows*\Microsoft.Net\Framework\v2.0.50727\            |
|     3.5      |              *Caminho de instalação do Windows*\Microsoft.NET\Framework\v3.5\               |
|     4.0      |           *Caminho de instalação do Windows*\Microsoft.NET\Framework\v4.0.30319\            |
|     12.0     |                          *%ProgramFiles%* \MSBuild\12.0\bin                           |

 O valor `ToolsVersion` determina qual conjunto de ferramentas é usado por um projeto que o Visual Studio gera. Em [!INCLUDE[vs_dev12](../includes/vs-dev12-md.md)] o valor padrão é "12.0" (não importa qual a versão especificada no arquivo de projeto), mas você pode substituir esse atributo usando a opção **/toolsversion** em um prompt de comando. Para obter informações sobre esse atributo e outras formas de especificar o `ToolsVersion`, consulte [Substituindo as configurações do ToolsVersion](../msbuild/overriding-toolsversion-settings.md).  

 Se o `ToolsVersion` não for especificado, a chave do Registro **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSBuild\\<Version Number\>\DefaultToolsVersion** define o `ToolsVersion`, que é sempre 2.0.  

 As seguintes chaves do Registro especificam o caminho de instalação do MSBuild.exe.  

|Chave do Registro|Nome da chave|Valor-chave da cadeia de caracteres|  
|------------------|--------------|----------------------|  
|\HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSBuild\ToolsVersions\2.0\|MSBuildToolsPath|Caminho de instalação do .NET Framework 2.0|  
|\HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\ MSBuild\ToolsVersions\3.5\|MSBuildToolsPath|Caminho de instalação do .NET Framework 3.5|  
|\HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\ MSBuild\ToolsVersions\4.0\|MSBuildToolsPath|Caminho de instalação do .NET Framework 4|  
|\HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\ MSBuild\ToolsVersions\12.0\|MSBuildToolsPath|Caminho de instalação do MSBuild|  

### <a name="sub-toolsets"></a>Subconjunto de ferramentas  
 Se a chave do Registro na tabela anterior tiver uma subchave, MSBuild usará para determinar que o caminho de um subconjunto de ferramentas pode substituir o caminho no conjunto de ferramentas pai. A seguinte sub-chave é um exemplo:  

 \HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSBuild\ToolsVersions\12.0\12.0  

 Se todas as propriedades são definidas no conjunto de ferramentas base e o subconjunto de ferramentas selecionado, as definições de propriedade no conjunto de ferramentas sub são usadas. Por exemplo, o conjunto de ferramentas do MSBuild 4.0 define `SDK40ToolsPath` para apontar para o 7.0A SDK, mas o conjunto de ferramentas MSBuild 4.0\11.0 define a mesma propriedade para apontar para o 8.0A SDK. Se `VisualStudioVersion` não está definido, `SDK40ToolsPath` apontaria para 7.0A, mas se `VisualStudioVersion` for definido como 11.0, em vez disso, a propriedade apontaria para 8.0A.  

 A propriedade do build `VisualStudioVersion` indica se um subconjunto de ferramentas se torna ativo. Por exemplo, um valor `VisualStudioVersion` de "12.0" especifica o subconjunto de ferramentas MSBuild 12.0. Para obter mais informações, consulte a seção de subconjuntos de ferramentas de [Conjunto de ferramentas (ToolsVersion)](../msbuild/msbuild-toolset-toolsversion.md).  

> [!NOTE]
>  É recomendável que você evite a alteração dessas configurações. No entanto, você pode adicionar suas próprias configurações e definir as definições personalizadas do conjunto de ferramentas em todo o computador, conforme descrito na próxima seção.  

## <a name="custom-toolset-definitions"></a>Definições personalizadas do conjunto de ferramentas  
 Quando um conjunto de ferramentas padrão não atender a seus requisitos de build, você pode criar um conjunto de ferramentas personalizado. Por exemplo, você pode ter um cenário de laboratório de build que você deve ter um sistema separado para projetos de build [!INCLUDE[vcprvc](../includes/vcprvc-md.md)]. Usando um conjunto de ferramentas personalizado, você pode atribuir valores personalizados para o `ToolsVersion` atributo ao criar projetos ou executar MSBuild.exe. Fazendo isso, você também pode usar a `$(MSBuildToolsPath)` propriedade para importar arquivos .targets do diretório, bem como definir suas próprias propriedades de conjunto de ferramentas personalizadas que podem ser usadas para qualquer projeto que usa esse conjunto de ferramentas.  

 Especifique um conjunto de ferramentas personalizado no arquivo de configuração para MSBuild.exe (ou a ferramenta personalizada que hospeda o mecanismo do MSBuild, se você estiver usando). Por exemplo, o arquivo de configuração para MSBuild.exe poderia incluir a seguinte definição de conjunto de ferramentas se você quisesse substituir o comportamento padrão de ToolsVersion 12.0.  

```  
<msbuildToolsets default="12.0">  
   <toolset toolsVersion="12.0">  
      <property name="MSBuildToolsPath"   
        value="C:\SpecialPath" />  
   </toolset>  
</msbuildToolsets>  
```  

 `<msbuildToolsets>` também deve ser definido no arquivo de configuração, da seguinte maneira.  

```  
<configSections>  
   <section name="msbuildToolsets"         
       Type="Microsoft.Build.BuildEngine.ToolsetConfigurationSection,   
       Microsoft.Build.Engine, Version=12.0.0.0, Culture=neutral,   
       PublicKeyToken=b03f5f7f11d50a3a"  
   </section>  
</configSections>  
```  

> [!NOTE]
>  Para ser lido corretamente, `<configSections>` deve ser a primeira subseção na seção `<configuration>`.  

 `ToolsetConfigurationSection` é uma seção de configuração personalizada que pode ser usada por qualquer hose de MSBuild para configuração personalizada. Se você usar um conjunto de ferramentas personalizado, um host não precisará fazer nada para inicializar o mecanismo de build, exceto fornecer as entradas de arquivo de configuração. Ao definir as entradas no Registro, você pode especificar conjuntos de ferramentas em todo o computador que se aplicam a MSBuild.exe, [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] e todos os hosts do MSBuild.  

> [!NOTE]
>  Se um arquivo de configuração define as configurações para um `ToolsVersion` que já foi definido no Registro, as duas definições não são mescladas. A definição no arquivo de configuração tem precedência e as configurações no Registro para esse `ToolsVersion` são ignoradas.  

 As seguintes propriedades são específicas para o valor de `ToolsVersion`, que é usado em projetos:  

- **$(MSBuildBinPath)** é definido como o valor `ToolsPath`, que é especificado no Registro ou no arquivo de configuração em que o `ToolsVersion` é definido. A configuração `$(MSBuildToolsPath)` no Registro ou no arquivo de configuração especifica o local das principais tarefas e destinos. No arquivo de projeto, isso mapeia para a propriedade $(MSBuildBinPath) e também para a propriedade $(MSBuildToolsPath).  

- `$(MSBuildToolsPath)` é uma propriedade reservada que é fornecida pela propriedade MSBuildToolsPath especificada no arquivo de configuração. (Essa propriedade substitui `$(MSBuildBinPath)`. No entanto, `$(MSBuildBinPath)` é repassada para compatibilidade.) Um conjunto de ferramentas personalizado deve definir o `$(MSBuildToolsPath)` ou `$(MSBuildBinPath)`, mas não ambos, a menos que ambos tenham o mesmo valor.  

  Você também pode adicionar propriedades personalizadas, propriedades específicas do ToolsVersion para o arquivo de configuração usando a mesma sintaxe que você pode usar para adicionar a propriedade MSBuildToolsPath. Para disponibilizar essas propriedades personalizadas para o arquivo de projeto, use o mesmo nome como o nome do valor que é especificado no arquivo de configuração. Você pode definir conjuntos de ferramentas, mas não os subconjuntos de ferramentas no arquivo de configuração.  

## <a name="see-also"></a>Consulte também  
 [Conjunto de Ferramentas (ToolsVersion)](../msbuild/msbuild-toolset-toolsversion.md)



