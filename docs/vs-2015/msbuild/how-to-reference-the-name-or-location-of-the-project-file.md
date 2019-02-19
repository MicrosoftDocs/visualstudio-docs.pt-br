---
title: Como referenciar o nome ou local do arquivo de projeto | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: msbuild
ms.topic: conceptual
helpviewer_keywords:
- locations, referencing
- locations
- MSBuildProjectName property
- MSBuild, referencing the project file
- names, referencing
- reserved properties
- project files, referencing
ms.assetid: c8fcc594-5d37-4e2e-b070-4d9c012043b5
caps.latest.revision: 16
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 9a5d07c374e75bd7f042f466f13fc5727241e252
ms.sourcegitcommit: a83c60bb00bf95e6bea037f0e1b9696c64deda3c
ms.translationtype: MTE95
ms.contentlocale: pt-BR
ms.lasthandoff: 02/19/2019
ms.locfileid: "54780996"
---
# <a name="how-to-reference-the-name-or-location-of-the-project-file"></a>Como referenciar o nome ou local do arquivo de projeto
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

  
Você pode usar o nome ou local do projeto no próprio arquivo de projeto sem ter de criar sua própria propriedade. O [!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] fornece propriedades reservadas que referenciam o nome do arquivo de projeto e outras propriedades relacionadas ao projeto. Para obter mais informações sobre propriedades reservadas, consulte [Propriedades reservadas e conhecidas do MSBuild](../msbuild/msbuild-reserved-and-well-known-properties.md).  
  
## <a name="using-the-msbuildprojectname-property"></a>Usar a propriedade MSBuildProjectName  
 O [!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] fornece algumas propriedades reservadas que você pode usar em seus arquivos de projeto sem defini-los a cada vez. Por exemplo, a propriedade reservada `MSBuildProjectName` fornece uma referência ao nome do arquivo de projeto.  
  
#### <a name="to-use-the-msbuildprojectname-property"></a>Para usar a propriedade MSBuildProjectName  
  
- Faça referência à propriedade no arquivo de projeto com a notação $(), como faria com qualquer propriedade. Por exemplo:  
  
  ```  
  <CSC Sources = "@(CSFile)"   
      OutputAssembly = "$(MSBuildProjectName).exe"/>  
  </CSC>  
  ```  
  
  Uma vantagem de usar uma propriedade reservada é que qualquer alteração no nome do arquivo de projeto é incorporada automaticamente. Na próxima vez que você compilar o projeto, o arquivo de saída terá o novo nome sem necessidade de ação adicional de sua parte.  
  
> [!NOTE]
>  As propriedades reservadas não podem ser redefinidas no arquivo de projeto.  
  
## <a name="example"></a>Exemplo  
 O arquivo de projeto de exemplo a seguir faz referência ao nome de projeto como uma propriedade reservada para especificar o nome para a saída.  
  
```  
<Project xmlns="http://scheams.microsoft.com/developer/msbuild/2003"   
    DefaultTargets = "Compile">  
  
    <!-- Specify the inputs -->  
    <ItemGroup>  
        <CSFile Include = "consolehwcs1.cs"/>  
    </ItemGroup>  
    <Target Name = "Compile">  
        <!-- Run the Visual C# compilation using  
        input files of type CSFile -->  
        <CSC Sources = "@(CSFile)"  
            OutputAssembly = "$(MSBuildProjectName).exe" >  
            <!-- Set the OutputAssembly attribute of the CSC task  
            to the name of the project -->  
            <Output  
                TaskParameter = "OutputAssembly"  
                ItemName = "EXEFile" />  
        </CSC>  
        <!-- Log the file name of the output file -->  
        <Message Text="The output file is @(EXEFile)"/>  
    </Target>  
</Project>  
```  
  
## <a name="see-also"></a>Consulte também  
[MSBuild](msbuild.md)  
 [Propriedades reservadas e conhecidas do MSBuild](../msbuild/msbuild-reserved-and-well-known-properties.md)
