---
title: Como usar o mesmo destino em vários arquivos de projeto | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology: msbuild
ms.topic: conceptual
helpviewer_keywords:
- MSBuild, importing
- MSBuild, using the same target in multiple project files
ms.assetid: 163734bd-1bfd-4093-a730-7741fc21742d
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 8fe68d4d6d970ee0c1e5db566caf7c812436589c
ms.sourcegitcommit: 8ee7efb70a1bfebcb6dd9855b926a4ff043ecf35
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/17/2018
ms.locfileid: "39077514"
---
# <a name="how-to-use-the-same-target-in-multiple-project-files"></a>Como usar o mesmo destino em vários arquivos de projeto
Se você tiver criado vários arquivos de projeto [!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)], talvez você tenha descoberto que precisa usar as mesmas tarefas e destinos em diferentes arquivos de projeto. Em vez de incluir a descrição completa dessas tarefas ou destinos em todos os arquivos de projeto, você pode salvar um destino em um arquivo de projeto separado e, em seguida, importar o projeto para qualquer outro projeto que precise usar o destino.  
  
## <a name="use-the-import-element"></a>Usar o elemento Import  
 O elemento `Import` é usado para inserir um arquivo de projeto em outro arquivo de projeto. O arquivo de projeto que está sendo importado deve ser um arquivo de projeto [!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)] válido e conter XML bem formado. O atributo `Project` especifica o caminho para o arquivo de projeto importado. Para obter mais informações sobre o elemento `Import`, confira [Elemento Import (MSBuild)](../msbuild/import-element-msbuild.md).  
  
#### <a name="to-import-a-project"></a>Para importar um projeto  
  
1.  Defina, no arquivo de projeto para o qual está sendo realizada a importação, todas as propriedades e itens que são usados como parâmetros para propriedades e itens no projeto importado.  
  
2.  Use o elemento `Import` para importar o projeto. Por exemplo:  
  
     `<Import Project="MyCommon.targets"/>`  
  
3.  Após o elemento `Import`, defina todas as propriedades e itens que devem substituir as definições padrão de propriedades e itens no projeto importado.  
  
## <a name="order-of-evaluation"></a>Ordem de avaliação  
 Quando [!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)] atinge um elemento `Import`, o projeto importado é inserido efetivamente no projeto para o qual está sendo realizada a importação, no local do elemento `Import`. Portanto, o local do elemento `Import` pode afetar os valores de propriedades e de itens. É importante entender as propriedades e os itens que são definidos pelo projeto importado e as propriedades e itens usados pelo projeto importado.  
  
 Quando o projeto é compilado, todas as propriedades são avaliadas primeiro, seguidas dos itens. Por exemplo, o seguinte XML define o arquivo de projeto importado *MyCommon.targets*:  
  
```xml  
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">  
    <PropertyGroup>  
        <Name>MyCommon</Name>  
    </PropertyGroup>  
  
    <Target Name="Go">  
        <Message Text="Name=$(Name)"/>  
    </Target>  
</Project>  
```  
  
 O seguinte XML define *MyApp.proj*, que importa *MyCommon.targets*:  
  
```xml  
<Project  
    DefaultTargets="Go"  
    xmlns="http://schemas.microsoft.com/developer/msbuild/2003">  
    <PropertyGroup>  
        <Name>MyApp</Name>  
    </PropertyGroup>  
    <Import Project="MyCommon.targets"/>  
</Project>  
```  
  
 Quando o projeto é compilado, a seguinte mensagem é exibida:  
  
 `Name="MyCommon"`  
  
 Como o projeto é importado depois de a propriedade `Name` ser definida em *MyApp.proj*, a definição de `Name` em *MyCommon.targets* substitui a definição em *MyApp.proj*. Se o projeto é importado antes de a propriedade Name ser definida, o build exibe a seguinte mensagem:  
  
 `Name="MyApp"`  
  
#### <a name="use-the-following-approach-when-importing-projects"></a>Usar a abordagem a seguir ao importar projetos  
  
1.  Defina, no arquivo de projeto, todas as propriedades e itens que são usados como parâmetros para propriedades e itens no projeto importado.  
  
2.  Importe o projeto.  
  
3.  Defina, no arquivo de projeto, todas as propriedades e itens que devem substituir as definições padrão de propriedades e itens no projeto importado.  
  
## <a name="example"></a>Exemplo  
 O exemplo de código a seguir mostra o arquivo *MyCommon.targets*, importado pelo segundo exemplo de código. O arquivo *.targets* avalia propriedades do projeto de importação para configurar o build.  
  
```xml  
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">  
    <PropertyGroup>  
        <Flavor Condition="'$(Flavor)'==''">DEBUG</Flavor>  
        <Optimize Condition="'$(Flavor)'=='RETAIL'">yes</Optimize>  
        <appname>$(MSBuildProjectName)</appname>  
    <PropertyGroup>  
    <Target Name="Build">  
        <Csc Sources="hello.cs"  
            Optimize="$(Optimize)"  
            OutputAssembly="$(appname).exe"/>  
    </Target>  
</Project>  
```  
  
## <a name="example"></a>Exemplo  
 O exemplo de código a seguir importa o arquivo *MyCommon.targets*.  
  
```xml  
<Project DefaultTargets="Build"  
    xmlns="http://schemas.microsoft.com/developer/msbuild/2003">  
    <PropertyGroup>  
        <Flavor>RETAIL</Flavor>  
    </PropertyGroup>  
    <Import Project="MyCommon.targets"/>  
</Project>  
```  
  
## <a name="see-also"></a>Consulte também  
 [Elemento Import (MSBuild)](../msbuild/import-element-msbuild.md)   
 [Destinos](../msbuild/msbuild-targets.md)