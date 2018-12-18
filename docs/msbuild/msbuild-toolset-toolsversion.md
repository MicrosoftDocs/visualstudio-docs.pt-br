---
title: MSBuild Toolset (ToolsVersion) | Microsoft Docs
ms.custom: ''
ms.date: 01/31/2018
ms.technology: msbuild
ms.topic: conceptual
helpviewer_keywords:
- MSBuild, multitargeting
- targeting a specific .NET framework [MSBuild]
- MSBuild, targeting a specific .NET framework
- multitargeting [MSBuild]
ms.assetid: 40040ee7-4620-4043-a6d8-ccba921421d1
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: feedf1789e4ee3f6b7e04966d945a5a2638242c3
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49821104"
---
# <a name="msbuild-toolset-toolsversion"></a>MSBuild Toolset (ToolsVersion)
O MSBuild usa um conjunto de ferramentas de tarefas, metas e ferramentas para compilar um aplicativo. Normalmente, um Conjunto de Ferramentas do MSBuild inclui um arquivo *microsoft.common.tasks*, um arquivo *microsoft.common.targets* e compiladores como o *csc.exe* e o *vbc.exe*. A maioria dos conjuntos de ferramentas pode ser usada para compilar aplicativos para mais de uma versão do .NET Framework e mais de uma plataforma de sistema. No entanto, o conjunto de ferramentas do MSBuild 2.0 pode ser usado para visar apenas o NET Framework 2.0.  
  
## <a name="toolsversion-attribute"></a>Atributo ToolsVersion  
 Especifique o conjunto de ferramentas no atributo `ToolsVersion` do elemento [Projeto](../msbuild/project-element-msbuild.md) no arquivo de projeto. O exemplo a seguir especifica que o projeto deve ser compilado usando o conjunto de ferramentas do MSBuild 15.0.  
  
```xml  
<Project ToolsVersion="15.0" ... </Project>  
``` 

> [!NOTE] 
> Alguns tipos de projeto usam o atributo `sdk` em vez do `ToolsVersion`. Para saber mais, confira [Pacotes, metadados e estruturas](/dotnet/core/packages) e [Adições ao formato csproj para .NET Core](/dotnet/core/tools/csproj).
  
## <a name="how-the-toolsversion-attribute-works"></a>Como funciona o atributo ToolsVersion  
 Ao criar um projeto no Visual Studio ou atualizar um projeto existente, um atributo chamado `ToolsVersion` é automaticamente incluído no arquivo de projeto e seu valor corresponde à versão do MSBuild incluída na edição do Visual Studio. Para saber mais, confira [Direcionar a uma versão específica do .NET Framework](../ide/targeting-a-specific-dotnet-framework-version.md).  
  
 Quando um valor `ToolsVersion` é definido em um arquivo do projeto, o MSBuild usa esse valor para determinar os valores das propriedades do conjunto de ferramentas que estão disponíveis para o projeto. Uma propriedade do conjunto de ferramentas é `$(MSBuildToolsPath)`, que especifica o caminho das ferramentas do .NET Framework. Só essa propriedade do conjunto de ferramentas (ou o `$(MSBuildBinPath)`) é necessária.  
  
 A partir do Visual Studio 2013, a versão do conjunto de ferramentas do MSBuild é a mesma que o número de versão do Visual Studio. O MSBuild assume o padrão deste Conjunto de Ferramentas no Visual Studio e na linha de comando, independentemente da versão do Conjunto de Ferramentas especificada no arquivo de projeto.  Esse comportamento pode ser substituído usando o sinalizador –ToolsVersion. Para saber mais, confira [Substituir as configurações de ToolsVersion](../msbuild/overriding-toolsversion-settings.md).  
  
 No exemplo a seguir, o MSBuild encontra o arquivo *Microsoft.CSharp.targets* usando a propriedade reservada `MSBuildToolsPath`.  
  
```xml  
<Import Project="$(MSBuildToolsPath)\Microsoft.CSharp.targets" />  
```  
  
 É possível modificar o valor do `MSBuildToolsPath` ao definir um conjunto de ferramentas personalizado. Para saber mais, confira [Configurações padrão e personalizadas do Conjunto de Ferramentas](../msbuild/standard-and-custom-toolset-configurations.md)  
  
 Quando você compila uma solução na linha de comando e especifica um `ToolsVersion` para *msbuild.exe*, todos os projetos e suas dependências projeto a projeto são compilados de acordo com o `ToolsVersion`, mesmo que cada projeto na solução especifique seu próprio `ToolsVersion`. Para definir o valor `ToolsVersion` em uma base por projeto, consulte [Substituir as configurações de ToolsVersion](../msbuild/overriding-toolsversion-settings.md).  
  
 O atributo `ToolsVersion` também é usado para migração de projeto. Por exemplo, se você abrir um projeto do Visual Studio 2008 no Visual Studio 2010, o arquivo de projeto será atualizado para incluir ToolsVersion="4.0". Em seguida, se você tentar abrir esse projeto no Visual Studio 2008, ele não reconhecerá o `ToolsVersion` atualizado e, consequentemente, criará o projeto como se o atributo ainda estivesse definido para 3.5.  
  
 Tanto o Visual Studio 2010 quanto o Visual Studio 2012 usam o ToolsVersion 4.0. O Visual Studio 2013 usa um ToolsVersion 12.0. O Visual Studio 2015 usa ToolsVersion 14.0 e o Visual Studio 2017 usa ToolsVersion 15.0. Em muitos casos, você pode abrir o projeto em várias versões do Visual Studio sem modificação. O Visual Studio sempre usa o conjunto de ferramentas correto, mas você será notificado se a versão usada não corresponder à versão encontrada no arquivo de projeto. Em quase todos os casos esse aviso é benigno, já que os conjuntos de ferramentas são compatíveis na maioria dos casos.  
  
 Os subconjuntos de ferramentas, descritos mais adiante neste tópico, permitem que o MSBuild alterne automaticamente o conjunto de ferramentas para ser usado com base no contexto em que a compilação está sendo executada. Por exemplo, o MSBuild usa um conjunto mais recente de ferramentas quando é executado no Visual Studio 2012 do que quando é executado no Visual Studio 2010, sem que seja necessário alterar explicitamente o arquivo do projeto.  
  
## <a name="toolset-implementation"></a>Implementação do Conjunto de Ferramentas  
 Implemente um conjunto de ferramentas selecionando os caminhos das várias ferramentas, destinos e tarefas que compõem o conjunto de ferramentas. As ferramentas do conjunto de ferramentas que o MSBuild define são fornecidas das seguintes fontes:  
  
- A pasta do .NET Framework.  
  
- Ferramentas gerenciadas adicionais.  
  
  As ferramentas gerenciadas incluem *ResGen.exe* e *TlbImp.exe*.  

O MSBuild fornece duas maneiras de acessar o conjunto de ferramentas:  
  
-   Usando as propriedades do conjunto de ferramentas  
  
-   Usando os métodos <xref:Microsoft.Build.Utilities.ToolLocationHelper>  

As propriedades do conjunto de ferramentas especificam os caminhos das ferramentas. Começando no Visual Studio 2017, o MSBuild deixa de ter um local fixo. Por padrão, ele está localizado na pasta *MSBuild\15.0\Bin* relativa ao local de instalação do Visual Studio. Nas versões anteriores, o MSBuild usa o valor do atributo `ToolsVersion` no arquivo de projeto para localizar a chave do Registro correspondente e, em seguida, usa as informações da chave do Registro para definir as propriedades do conjunto de ferramentas. Por exemplo, se `ToolsVersion` tiver um valor `12.0`, o MSBuild configurará as propriedades do Conjunto de Ferramentas de acordo com esta chave do Registro: **HKLM\Software\Microsoft\MSBuild\ToolsVersions\12.0**.  
  
 Estas são as propriedades do conjunto de ferramentas:  
  
-   `MSBuildToolsPath` especifica o caminho dos binários do MSBuild.  
  
-   `SDK40ToolsPath` especifica o caminho de ferramentas gerenciadas adicionais para o MSBuild 4.x (que pode ser 4.0 ou 4.5).  
  
-   `SDK35ToolsPath` especifica o caminho de ferramentas gerenciadas adicionais para o MSBuild 3.5.  

Você também pode determinar o conjunto de ferramentas programaticamente, chamando os métodos da classe <xref:Microsoft.Build.Utilities.ToolLocationHelper>. A classe inclui os seguintes métodos:  
  
-   <xref:Microsoft.Build.Utilities.ToolLocationHelper.GetPathToDotNetFramework%2A> retorna o caminho da pasta do .NET Framework.  
  
-   <xref:Microsoft.Build.Utilities.ToolLocationHelper.GetPathToDotNetFrameworkFile%2A> retorna o caminho de um arquivo na pasta do .NET Framework.  
  
-   <xref:Microsoft.Build.Utilities.ToolLocationHelper.GetPathToDotNetFrameworkSdk%2A> retorna o caminho da pasta das ferramentas gerenciadas.  
  
-   <xref:Microsoft.Build.Utilities.ToolLocationHelper.GetPathToDotNetFrameworkSdkFile%2A> retorna o caminho de um arquivo, que normalmente está localizado na pasta das ferramentas gerenciadas.  
  
-   <xref:Microsoft.Build.Utilities.ToolLocationHelper.GetPathToBuildTools%2A> retorna o caminho das ferramentas de compilação.  
  
### <a name="sub-toolsets"></a>Subconjunto de ferramentas  
 Para as versões do MSBuild anteriores à 15.0, o MSBuild usa uma chave do Registro para especificar o caminho das ferramentas básicas. Se a chave tiver uma subchave, o MSBuild a usará para especificar o caminho de um subconjunto de ferramentas que contém ferramentas adicionais. Nesse caso, o conjunto de ferramentas é definido pela combinação das definições de propriedades definidas nas duas chaves.  
  
> [!NOTE]
>  Se os nomes de propriedade do Conjunto de Ferramentas coincidirem, o valor que está definido para o caminho da subchave substituirá o valor que está definido para o caminho da chave raiz.  
  
 Os subconjuntos de ferramentas tornam-se ativos na presença da propriedade de compilação `VisualStudioVersion`. Essa propriedade pode usar um dos seguintes valores:  
  
-   “10.0” especifica o subconjunto de ferramentas do .NET Framework 4  
  
-   “11.0” especifica o subconjunto de ferramentas do .NET Framework 4.5  
  
-   “12.0” especifica o subconjunto de ferramentas do .NET Framework 4.5.1 

Os subconjuntos de ferramentas 10.0 e 11.0 devem ser usados com o ToolsVersion 4.0. Em versões posteriores, a versão do subconjunto de ferramentas e o ToolsVersion devem corresponder.  

Durante uma compilação, o MSBuild determina e define um valor padrão para a propriedade `VisualStudioVersion` se ele ainda não estiver definido.  

O MSBuild fornece sobrecargas para os métodos `ToolLocationHelper` que adicionam um valor enumerado `VisualStudioVersion` como parâmetro  

Os subconjuntos de ferramentas foram introduzidos no .NET Framework 4.5.  
  
## <a name="see-also"></a>Consulte também  
 [Configurações padrão e personalizadas do Conjunto de Ferramentas](../msbuild/standard-and-custom-toolset-configurations.md)   
 [Multiplataforma](../msbuild/msbuild-multitargeting-overview.md)
