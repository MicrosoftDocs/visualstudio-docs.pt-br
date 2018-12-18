---
title: Transformações do MSBuild | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology: msbuild
ms.topic: conceptual
helpviewer_keywords:
- MSBuild, transforms
- transforms [MSBuild]
ms.assetid: d0bcfc3c-14fa-455e-805c-63ccffa4a3bf
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: b1a3ff7cbd2025a909ab0c5fb044bb61b24388ff
ms.sourcegitcommit: 0e5289414d90a314ca0d560c0c3fe9c88cb2217c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/19/2018
ms.locfileid: "39151194"
---
# <a name="msbuild-transforms"></a>Transformações do MSBuild
Uma transformação é uma conversão individual de uma lista de itens para outra. Além de habilitar um projeto para converter as lista de itens, uma transformação permite que um destino identifique um mapeamento direto entre suas entradas e saídas. Este tópico explica as transformações e como o [!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)] as utiliza na criação de projetos com mais eficiência.  
  
## <a name="transform-modifiers"></a>Modificadores de transformação  
As transformações não são arbitrárias, mas são limitadas pela sintaxe especial na qual todos os modificadores de transformação devem estar no formato %(\<ItemMetaDataName>). Quaisquer metadados de item podem ser usados como um modificador de transformação. Isso inclui os metadados de item bem conhecidos atribuídos a cada item criado. Para obter uma lista de metadados de item conhecidos, confira [Metadados de itens conhecidos](../msbuild/msbuild-well-known-item-metadata.md).  
  
No exemplo a seguir, uma lista de arquivos *.resx* é transformada em uma lista de arquivos *.resources*. O modificador de transformação %(filename) especifica que cada arquivo *.resources* tem o mesmo nome de arquivo do que o arquivo *.resx* correspondente.  
  
```xml  
@(RESXFile->'%(filename).resources')  
```

Por exemplo, se os itens na lista @(RESXFile) *Form1.resx*, *Form2.resx* e *Form3.resx*, as saídas na lista transformada serão *Form1.resources*, *Form2.resources* e *Form3.resources*.  

> [!NOTE]
>  Você pode especificar um separador personalizado para uma lista de itens transformados da mesma maneira que especifica um separador para uma lista de itens padrão. Por exemplo, para separar uma lista de itens transformados usando uma vírgula (,) em vez do ponto-e-vírgula (;) padrão, use o XML a seguir:  
> `@(RESXFile->'Toolset\%(filename)%(extension)', ',')`
  
## <a name="use-multiple-modifiers"></a>Uso de vários modificadores  
 Uma expressão de transformação pode conter vários modificadores, que podem ser combinados em qualquer ordem e podem ser repetidos. No exemplo a seguir, o nome do diretório que contém os arquivos é alterado, mas os arquivos de reter a extensão de nome de arquivo e de nome original.  
  
```xml  
@(RESXFile->'Toolset\%(filename)%(extension)')  
```  
  
 Por exemplo, se os itens contidos na lista de itens `RESXFile` forem *Project1\Form1.resx*, *Project1\Form2.resx* e *Project1\Form3.text*, as saídas na lista transformada serão *Toolset\Form1.resx*, *Toolset\Form2.resx* e *Toolset\Form3.text*.  
  
## <a name="dependency-analysis"></a>Análise de dependência  
 Transformações garantem um mapeamento individual entre a lista de itens transformados e a lista do item original. Portanto, se um destino cria saídas que são transformações das entradas, [!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)] pode analisar os carimbos de hora das entradas e saídas e decida se deseja ignorar, compilar ou recompilar parcialmente um destino.  
  
 Na [tarefa Copy](../msbuild/copy-task.md) no exemplo a seguir, todos os arquivos na lista de itens `BuiltAssemblies` são mapeados para um arquivo na pasta de destino da tarefa especificada usando uma transformação no atributo `Outputs`. Se um arquivo na lista de itens `BuiltAssemblies` for alterado, a tarefa `Copy` será executada somente para o arquivo alterado e todos os outros arquivos serão ignorados. Para saber mais sobre a análise de dependência e como usar transformações, confira [Como compilar incrementalmente](../msbuild/how-to-build-incrementally.md).  
  
```xml  
<Target Name="CopyOutputs"  
    Inputs="@(BuiltAssemblies)"  
    Outputs="@(BuiltAssemblies -> '$(OutputPath)%(Filename)%(Extension)')">  
  
    <Copy  
        SourceFiles="@(BuiltAssemblies)"  
        DestinationFolder="$(OutputPath)"/>  
  
</Target>  
```  
  
## <a name="example"></a>Exemplo  
  
### <a name="description"></a>Descrição  
 O exemplo a seguir mostra um arquivo de projeto [!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)] que usa transformações. Este exemplo supõe que haja apenas um arquivo *.xsd* no diretório *c:\sub0\sub1\sub2\sub3* e o diretório de trabalho é *c:\sub0*.  
  
### <a name="code"></a>Código  
  
```xml  
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">  
    <ItemGroup>  
        <Schema Include="sub1\**\*.xsd"/>  
    </ItemGroup>  
  
    <Target Name="Messages">  
        <Message Text="rootdir: @(Schema->'%(rootdir)')"/>  
        <Message Text="fullpath: @(Schema->'%(fullpath)')"/>  
        <Message Text="rootdir + directory + filename + extension: @(Schema->'%(rootdir)%(directory)%(filename)%(extension)')"/>  
        <Message Text="identity: @(Schema->'%(identity)')"/>  
        <Message Text="filename: @(Schema->'%(filename)')"/>  
        <Message Text="directory: @(Schema->'%(directory)')"/>  
        <Message Text="relativedir: @(Schema->'%(relativedir)')"/>  
        <Message Text="extension: @(Schema->'%(extension)')"/>  
    </Target>  
</Project>  
```  
  
### <a name="comments"></a>Comentários  
 Este exemplo gera a seguinte saída:  
  
```  
rootdir: C:\  
fullpath: C:\xmake\sub1\sub2\sub3\myfile.xsd  
rootdir + directory + filename + extension: C:\xmake\sub1\sub2\sub3\myfile.xsd  
identity: sub1\sub2\sub3\myfile.xsd  
filename: myfile  
directory: xmake\sub1\sub2\sub3\  
relativedir: sub1\sub2\sub3\  
extension: .xsd  
```  
  
## <a name="see-also"></a>Consulte também  
 [Conceitos do MSBuild](../msbuild/msbuild-concepts.md)   
 [Referência do MSBuild](../msbuild/msbuild-reference.md)   
 [Como criar de forma incremental](../msbuild/how-to-build-incrementally.md)