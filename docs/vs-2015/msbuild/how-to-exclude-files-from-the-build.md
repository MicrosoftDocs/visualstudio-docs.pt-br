---
title: Como excluir arquivos do build | Microsoft Docs
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
- MSBuild, wildcards
- MSBuild, excluding files
- wildcards, MSBuild
ms.assetid: 1be36e45-01da-451c-972d-f9fc0e7d663c
caps.latest.revision: 19
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 114c973246c325604c79ca248cc3487fd495a19a
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49230579"
---
# <a name="how-to-exclude-files-from-the-build"></a>Como excluir arquivos do build
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

  
Em um arquivo de projeto, você pode usar curingas para incluir todos os arquivos em um diretório ou um conjunto aninhado de diretórios como entradas para um build. No entanto, pode haver um arquivo no diretório ou um diretório em um conjunto aninhado de diretórios que você não deseja incluir como entrada para um build. Você pode excluir explicitamente esse arquivo ou diretório da lista de entradas. Também pode haver um arquivo em um projeto que você deseja incluir somente em determinadas condições. Você pode declarar explicitamente as condições sob as quais um arquivo é incluído em um build.  
  
## <a name="excluding-a-file-or-directory-from-the-inputs-for-a-build"></a>Excluir um arquivo ou diretório das entradas para um build  
 Listas de itens são os arquivos de entrada para um build. Os itens que você deseja incluir são declarados separadamente ou como um grupo usando o atributo `Include`. Por exemplo:  
  
```  
<CSFile Include="Form1.cs"/>  
<CSFile Include ="File1.cs;File2.cs"/>  
<CSFile Include="*.cs"/>  
<JPGFile Include="Images\**\*.jpg"/>  
```  
  
 Se você usou curingas para incluir todos os arquivos em um diretório ou um conjunto aninhado de diretórios como entradas para um build, poderá haver um ou mais arquivos no diretório ou um diretório no conjunto aninhado de diretórios que você não deseja incluir. Para excluir um item da lista de itens, use o atributo `Exclude`.  
  
#### <a name="to-include-all-cs-or-vb-files-except-form2"></a>Para incluir todos os arquivos .cs ou .vb, exceto o Form2  
  
-   Use um dos atributos `Include` e `Exclude` a seguir:  
  
    ```  
    <CSFile Include="*.cs" Exclude="Form2.cs"/>  
    ```  
  
     - ou –  
  
    ```  
    <VBFile Include="*.vb" Exclude="Form2.vb"/>  
    ```  
  
#### <a name="to-include-all-cs-or-vb-files-except-form2-and-form3"></a>Para incluir todos os arquivos .cs ou .vb, exceto o Form2 e o Form3  
  
-   Use um dos atributos `Include` e `Exclude` a seguir:  
  
    ```  
    <CSFile Include="*.cs" Exclude="Form2.cs;Form3.cs"/>  
    ```  
  
     - ou –  
  
    ```  
    <VBFile Include="*.vb" Exclude="Form2.vb;Form3.vb"/>  
    ```  
  
#### <a name="to-include-all-jpg-files-in-subdirectories-of-the-images-directory-except-those-in-the-version2-directory"></a>Para incluir todos os arquivos .jpg em subdiretórios do diretório Images, exceto aqueles no diretório Version2  
  
-   Use os atributos `Include` e `Exclude` a seguir:  
  
    ```  
    <JPGFile  
        Include="Images\**\*.jpg"  
        Exclude = "Images\**\Version2\*.jpg"/>  
    ```  
  
    > [!NOTE]
    >  Você deve especificar o caminho para os dois atributos. Se você usar um caminho absoluto para especificar locais de arquivo no atributo `Include`, também é necessário usar um caminho absoluto no atributo `Exclude`. Se você usar um caminho relativo no atributo `Include`, também deverá usar um caminho relativo no atributo `Exclude`.  
  
## <a name="using-conditions-to-exclude-a-file-or-directory-from-the-inputs-for-a-build"></a>Usar condições para excluir um arquivo ou diretório das entradas para um build  
 Se houver itens que você deseja incluir, por exemplo, em um build de depuração, mas não em um build de versão, você poderá usar o atributo `Condition` para especificar as condições sob as quais o item será incluído.  
  
#### <a name="to-include-the-file-formulavb-only-in-release-builds"></a>Para incluir o arquivo Formula.vb somente em compilações de versão  
  
-   Use um atributo `Condition` semelhante ao seguinte:  
  
    ```  
    <Compile  
        Include="Formula.vb"  
        Condition=" '$(Configuration)' == 'Release' " />  
    ```  
  
## <a name="example"></a>Exemplo  
 O exemplo de código a seguir compila um projeto com todos os arquivos .cs no diretório, exceto o Form2.cs.  
  
```  
<Project DefaultTargets="Compile"  
    xmlns="http://schemas.microsoft.com/developer/msbuild/2003" >  
  
    <PropertyGroup>  
        <builtdir>built</builtdir>  
    </PropertyGroup>  
  
    <ItemGroup>  
        <CSFile Include="*.cs Exclude="Form2.cs"/>  
  
        <Reference Include="System.dll"/>  
        <Reference Include="System.Data.dll"/>  
        <Reference Include="System.Drawing.dll"/>  
        <Reference Include="System.Windows.Forms.dll"/>  
        <Reference Include="System.XML.dll"/>  
    </ItemGroup>  
  
    <Target Name="PreBuild">  
        <Exec Command="if not exist $(builtdir) md $(builtdir)"/>  
    </Target>  
  
    <Target Name="Compile" DependsOnTargets="PreBuild">  
        <Csc Sources="@(CSFile)"  
            References="@(Reference)"  
            OutputAssembly="$(builtdir)\$(MSBuildProjectName).exe"  
            TargetType="exe" />  
    </Target>  
</Project>  
```  
  
## <a name="see-also"></a>Consulte também  
 [Itens](../msbuild/msbuild-items.md)   
 [MSBuild](msbuild.md) [Como selecionar os arquivos a serem compilados](../msbuild/how-to-select-the-files-to-build.md)


