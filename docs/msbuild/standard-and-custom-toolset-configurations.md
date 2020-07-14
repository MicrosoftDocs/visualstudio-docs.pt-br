---
title: Configurações padrão e personalizadas do Conjunto de Ferramentas | Microsoft Docs
ms.date: 01/31/2018
ms.topic: conceptual
helpviewer_keywords:
- MSBuild, custom toolset configurations
- MSBuild, msbuild.exe.config
ms.assetid: 15a048c8-5ad3-448e-b6e9-e3c5d7147ed2
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: bb75d6fc02f2841383127482503799b2c78512cf
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/23/2020
ms.locfileid: "85289177"
---
# <a name="standard-and-custom-toolset-configurations"></a>Configurações padrão e personalizadas do Conjunto de Ferramentas

Um Conjunto de Ferramentas MSBuild contém referências a tarefas, destinos e ferramentas que você pode usar para criar um projeto de aplicativo. MSBuild inclui um Conjunto de Ferramentas padrão, mas você também pode criar ferramentas personalizadas. Para obter informações sobre como especificar um Conjunto de Ferramentas, consulte [Conjunto de Ferramentas (ToolsVersion)](../msbuild/msbuild-toolset-toolsversion.md)

## <a name="standard-toolset-configurations"></a>Configurações padrão do Conjunto de Ferramentas

::: moniker range=">=vs-2019"
 O MSBuild 16.0 inclui os seguintes conjuntos de ferramentas padrão:

|ToolsVersion|Caminho do Conjunto de Ferramentas (conforme especificado na propriedade de build MSBuildToolsPath ou MSBuildBinPath)|
|------------------| - |
|2,0|*\<Windows installation path>\Microsoft.Net\Framework\v2.0.50727\\*|
|3,5|*\<Windows installation path>\Microsoft.NET\Framework\v3.5\\*|
|4,0|*\<Windows installation path>\Microsoft.NET\Framework\v4.0.30319\\*|
|Current|*\<Visual Studio installation path>\MSBuild\Current\bin*|

 O valor `ToolsVersion` determina qual conjunto de ferramentas é usado por um projeto que o Visual Studio gera. No Visual Studio 2019, o valor padrão é "Atual" (independentemente da versão especificada no arquivo de projeto), mas você pode substituir esse atributo usando a opção **/toolsversion** em um prompt de comando. Para saber mais sobre esse atributo e outras formas de especificar o `ToolsVersion`, confira [Substituir as configurações de ToolsVersion](../msbuild/overriding-toolsversion-settings.md).

 ::: moniker-end

::: moniker range="vs-2017"
 O MSBuild 15.0 inclui os seguintes conjuntos de ferramentas padrão:

|ToolsVersion|Caminho do Conjunto de Ferramentas (conforme especificado na propriedade de build MSBuildToolsPath ou MSBuildBinPath)|
|------------------| - |
|2,0|*\<Windows installation path>\Microsoft.Net\Framework\v2.0.50727\\*|
|3,5|*\<Windows installation path>\Microsoft.NET\Framework\v3.5\\*|
|4,0|*\<Windows installation path>\Microsoft.NET\Framework\v4.0.30319\\*|
|15.0|*\<Visual Studio installation path>\MSBuild\15.0\bin*|

 O valor `ToolsVersion` determina qual conjunto de ferramentas é usado por um projeto que o Visual Studio gera. No Visual Studio de 2017, o valor padrão é "15.0" (independentemente da versão especificada no arquivo de projeto), mas você pode substituir esse atributo usando a opção **/toolsversion** em um prompt de comando. Para saber mais sobre esse atributo e outras formas de especificar o `ToolsVersion`, confira [Substituir as configurações de ToolsVersion](../msbuild/overriding-toolsversion-settings.md).
 ::: moniker-end

O Visual Studio 2017 e versões posteriores não usam uma chave do Registro no caminho do MSBuild. Para as versões do MSBuild anteriores à 15.0 que são instaladas com o Visual Studio 2017, as seguintes chaves do Registro especificam o caminho de instalação do MSBuild.exe.

|Chave do Registro|Nome da chave|Valor da chave de cadeia de caracteres|
|------------------|--------------|----------------------|
|**\ HKEY_LOCAL_MACHINE \SOFTWARE\Microsoft\ MSBuild\ToolsVersions\2.0\\** |**MSBuildToolsPath**|**Caminho de instalação do .NET Framework 2.0**|
|**\HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\ MSBuild\ToolsVersions\3.5\\** |**MSBuildToolsPath**|**Caminho de instalação do .NET Framework 3.5**|
|**\HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\ MSBuild\ToolsVersions\4.0\\** |**MSBuildToolsPath**|**Caminho de instalação do .NET Framework 4**|

### <a name="sub-toolsets"></a>Subconjunto de ferramentas

 Se a chave do registro na tabela anterior tiver uma subchave, o MSBuild a usará para determinar o caminho de um subconjunto de ferramentas que substitua o caminho no Conjunto de Ferramentas pai. A seguinte sub-chave é um exemplo:

 **\HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSBuild\ToolsVersions\12.0\12.0**

 Se houver propriedades definidas no Conjunto de Ferramentas base e no subconjunto de ferramentas selecionado, as definições de propriedade do subconjunto de ferramentas serão usadas. Por exemplo, o Conjunto de Ferramentas do MSBuild 4.0 define `SDK40ToolsPath` para apontar para o 7.0A SDK, mas o Conjunto de Ferramentas MSBuild 4.0\11.0 define a mesma propriedade para apontar para o 8.0A SDK. Se `VisualStudioVersion` não está definido, `SDK40ToolsPath` apontaria para 7.0A, mas se `VisualStudioVersion` for definido como 11.0, em vez disso, a propriedade apontaria para 8.0A.

 A propriedade do build `VisualStudioVersion` indica se um subconjunto de ferramentas se torna ativo. Por exemplo, um valor `VisualStudioVersion` de "12.0" especifica o subconjunto de ferramentas MSBuild 12.0. Para saber mais,confira a seção de subconjuntos de ferramentas de [Conjunto de ferramentas (ToolsVersion)](../msbuild/msbuild-toolset-toolsversion.md).

> [!NOTE]
> É recomendável que você evite a alteração dessas configurações. No entanto, você pode adicionar suas próprias configurações e definir as definições personalizadas do Conjunto de Ferramentas em todo o computador, conforme descrito na próxima seção.

## <a name="custom-toolset-definitions"></a>Definições personalizadas do Conjunto de Ferramentas

 Quando um conjunto de ferramentas padrão não atender a seus requisitos de build, você pode criar um conjunto de ferramentas personalizado. Por exemplo, você pode ter um cenário de laboratório de compilação no qual você deve ter um sistema separado para criar projetos C++. Usando um Conjunto de Ferramentas personalizado, você pode atribuir valores personalizados para o `ToolsVersion` atributo ao criar projetos ou executar *MSBuild.exe*. Fazendo isso, você também pode usar a propriedade `$(MSBuildToolsPath)` para importar arquivos *.targets* do diretório, bem como definir suas próprias propriedades de Conjunto de Ferramentas personalizadas, as quais podem ser usadas para qualquer projeto que use esse Conjunto de Ferramentas.

 Especifique um Conjunto de Ferramentas personalizado no arquivo de configuração de *MSBuild.exe* (ou da ferramenta personalizada que hospeda o mecanismo MSBuild, se for o seu caso). Por exemplo, o arquivo de configuração de *MSBuild.exe* poderia incluir a seguinte definição de Conjunto de Ferramentas caso deseje definir um conjunto de ferramentas chamado *MyCustomToolset*.

```xml
<msbuildToolsets default="MyCustomToolset">
   <toolset toolsVersion="MyCustomToolset">
      <property name="MSBuildToolsPath"
        value="C:\SpecialPath" />
   </toolset>
</msbuildToolsets>
```

 `<msbuildToolsets>` também deve ser definido no arquivo de configuração, da seguinte maneira.

```xml
<configSections>
   <section name="msbuildToolsets"
       Type="Microsoft.Build.BuildEngine.ToolsetConfigurationSection,
       Microsoft.Build, Version=15.1.0.0, Culture=neutral,
       PublicKeyToken=b03f5f7f11d50a3a"
   </section>
</configSections>
```

> [!NOTE]
> Para ser lido corretamente, `<configSections>` deve ser a primeira subseção na seção `<configuration>`.

 `ToolsetConfigurationSection` é uma seção de configuração personalizada que pode ser usada por qualquer hose de MSBuild para configuração personalizada. Se você usar um conjunto de ferramentas personalizado, um host não precisará fazer nada para inicializar o mecanismo de build, exceto fornecer as entradas de arquivo de configuração.

 As seguintes propriedades são específicas para o valor de `ToolsVersion`, que é usado em projetos:

- **$(MSBuildBinPath)** é definido como o valor `ToolsPath`, que é especificado no Registro ou no arquivo de configuração em que o `ToolsVersion` é definido. A configuração `$(MSBuildToolsPath)` no Registro ou no arquivo de configuração especifica o local das principais tarefas e destinos. No arquivo de projeto, isso mapeia para a propriedade $(MSBuildBinPath) e também para a propriedade $(MSBuildToolsPath).

- `$(MSBuildToolsPath)` é uma propriedade reservada que é fornecida pela propriedade MSBuildToolsPath especificada no arquivo de configuração. (Essa propriedade substitui `$(MSBuildBinPath)`. No entanto, o `$(MSBuildBinPath)` é postergado para compatibilidade.) Um conjunto de ferramentas personalizado deve definir um `$(MSBuildToolsPath)` ou `$(MSBuildBinPath)` , mas não ambos, a menos que ambos tenham o mesmo valor.

  Você também pode adicionar propriedades personalizadas, propriedades específicas do ToolsVersion para o arquivo de configuração usando a mesma sintaxe que você pode usar para adicionar a propriedade MSBuildToolsPath. Para disponibilizar essas propriedades personalizadas para o arquivo de projeto, use o mesmo nome como o nome do valor que é especificado no arquivo de configuração. Você pode definir Conjuntos de Ferramentas, mas não os subconjuntos de ferramentas no arquivo de configuração.

## <a name="see-also"></a>Veja também

- [Conjunto de Ferramentas (ToolsVersion)](../msbuild/msbuild-toolset-toolsversion.md)
