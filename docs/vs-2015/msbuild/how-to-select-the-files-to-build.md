---
title: Como selecionar os arquivos para compilar | Microsoft Docs
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
- MSBuild, including files
- Include attribute [MSBuild]
ms.assetid: f5ff182f-7b3a-46fb-9335-37df54cfb8eb
caps.latest.revision: 17
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 7b8eeb62b8a5091743345c1a5c136bc2fa87269c
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49223802"
---
# <a name="how-to-select-the-files-to-build"></a>Como selecionar os arquivos a serem compilados
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

  
Quando você compila um projeto que contém vários arquivos, é possível listar cada arquivo separadamente no arquivo de projeto ou usar caracteres curinga para incluir todos os arquivos em um diretório ou um conjunto aninhado de diretórios.  
  
## <a name="specifying-inputs"></a>Especificando as entradas  
 Os itens representam as entradas para um build. Para obter mais informações sobre os itens, consulte [Itens](../msbuild/msbuild-items.md).  
  
 Para incluir arquivos para um build, eles devem ser incluídos em uma lista de itens no arquivo de projeto [!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)]. Vários arquivos podem ser adicionados a listas de itens incluindo os arquivos individualmente ou usando caracteres curinga para incluir vários arquivos ao mesmo tempo.  
  
#### <a name="to-declare-items-individually"></a>Para declarar itens individualmente  
  
-   Use os atributos `Include` semelhantes ao seguinte:  
  
     `<CSFile Include="form1.cs"/>`  
  
     – ou –  
  
     `<VBFile Include="form1.vb"/>`  
  
    > [!NOTE]
    >  Se os itens em uma coleção de itens não estiverem no mesmo diretório que o arquivo de projeto, será necessário especificar o caminho completo ou relativo para o item. Por exemplo: `Include="..\..\form2.cs"`.  
  
#### <a name="to-declare-multiple-items"></a>Para declarar vários itens  
  
-   Use os atributos `Include` semelhantes ao seguinte:  
  
     `<CSFile Include="form1.cs;form2.cs"/>`  
  
     – ou –  
  
     `<VBFile Include="form1.vb;form2.vb"/>`  
  
## <a name="specifying-inputs-with-wildcards"></a>Especificando entradas com caracteres curinga  
 Você também pode usar caracteres curinga para incluir recursivamente todos os arquivos ou apenas arquivos específicos de subdiretórios como entradas para um build. Para obter mais informações sobre caracteres curinga, consulte [Itens](../msbuild/msbuild-items.md)  
  
 Os exemplos a seguir baseiam-se em um projeto que contém os arquivos de elementos gráficos nos seguintes diretórios e subdiretórios, com o arquivo de projeto localizado no diretório do Projeto:  
  
 Project\Images\BestJpgs  
  
 Project\Images\ImgJpgs  
  
 Project\Images\ImgJpgs\Img1  
  
#### <a name="to-include-all-jpg-files-in-the-images-directory-and-subdirectories"></a>Para incluir todos os arquivos. jpg no diretório Imagens e subdiretórios  
  
-   Use o seguinte atributo `Include`:  
  
     `Include="Images\**\*.jpg"`  
  
#### <a name="to-include-all-jpg-files-starting-with-img"></a>Para incluir todos os arquivos. jpg, começando com "img"  
  
-   Use o seguinte atributo `Include`:  
  
     `Include="Images\**\img*.jpg"`  
  
#### <a name="to-include-all-files-in-directories-with-names-ending-in-jpgs"></a>Para incluir todos os arquivos em diretórios com nomes que terminam em "jpgs"  
  
-   Use um dos seguintes atributos `Include`:  
  
     `Include="Images\**\*jpgs\*.*"`  
  
     – ou –  
  
     `Include="Images\**\*jpgs\*"`  
  
## <a name="passing-items-to-a-task"></a>Passando itens para uma tarefa  
 Em um arquivo de projeto, você pode usar a notação @() em tarefas para especificar uma lista completa de itens como a entrada para um build. Você pode usar essa notação se listar todos os arquivos separadamente ou usar caracteres curinga.  
  
#### <a name="to-use-all-visual-c-or-visual-basic-files-as-inputs"></a>Para usar todos os arquivos do Visual c# ou Visual Basic como entradas  
  
-   Use os atributos `Include` semelhantes ao seguinte:  
  
     `<CSC Sources="@(CSFile)">...</CSC>`  
  
     – ou –  
  
     `<VBC Sources="@(VBFile)">...</VBC>`  
  
> [!NOTE]
>  Você deve usar caracteres curinga com itens para especificar as entradas para um build; não é possível especificar as entradas usando o atributo `Sources` em tarefas de [!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] como [Csc](../msbuild/csc-task.md) ou [Vbc](../msbuild/vbc-task.md). O exemplo a seguir não é válido em um arquivo de projeto:  
>   
>  `<CSC Sources="*.cs">...</CSC>`  
  
## <a name="example"></a>Exemplo  
 O exemplo de código a seguir mostra um projeto que inclui todos os arquivos de entrada separadamente.  
  
```  
<Project DefaultTargets="Compile"  
    xmlns="http://schemas.microsoft.com/developer/msbuild/2003" >  
    <PropertyGroup>  
        <Builtdir>built</Builtdir>  
    </PropertyGroup>  
  
    <ItemGroup>  
        <CSFile Include="Form1.cs"/>  
        <CSFile Include="AssemblyInfo.cs"/>  
  
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
  
## <a name="example"></a>Exemplo  
 O exemplo de código a seguir usa um caractere curinga para incluir todos os arquivos .cs.  
  
```  
<Project DefaultTargets="Compile"  
    xmlns="http://schemas.microsoft.com/developer/msbuild/2003" >  
  
    <PropertyGroup>  
        <builtdir>built</builtdir>  
    </PropertyGroup>  
  
    <ItemGroup>  
        <CSFile Include="*.cs"/>  
  
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
 [Como excluir arquivos do build](../msbuild/how-to-exclude-files-from-the-build.md)   
 [Itens](../msbuild/msbuild-items.md)



