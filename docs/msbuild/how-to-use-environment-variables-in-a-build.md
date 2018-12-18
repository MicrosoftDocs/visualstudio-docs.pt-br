---
title: Como usar variáveis de ambiente em um build | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology: msbuild
ms.topic: conceptual
helpviewer_keywords:
- environment variables, referencing
- projects [.NET Framework], environment variables
- MSBuild, environment variables
ms.assetid: 7f9e4469-8865-4b59-aab3-3ff26bd36e77
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: d57709b2e1ff4f3721644f2f61e030ea8ccccf82
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49828345"
---
# <a name="how-to-use-environment-variables-in-a-build"></a>Como usar variáveis de ambiente em um build
Quando você compila projetos, geralmente é necessário definir opções de build usando informações que não estão no arquivo de projeto ou nos arquivos que compõem seu projeto. Normalmente, essas informações são armazenadas em variáveis de ambiente.  
  
## <a name="reference-environment-variables"></a>Referenciar variáveis de ambiente  
 Todas as variáveis de ambiente estão disponíveis para o arquivo de projeto [!INCLUDE[vstecmsbuildengine](../msbuild/includes/vstecmsbuildengine_md.md)] ([!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)]) como propriedades.  
  
> [!NOTE]
>  Se o arquivo de projeto contiver uma definição explícita de uma propriedade que tem o mesmo nome que uma variável de ambiente, a propriedade no arquivo de projeto substituirá os valores de uma variável de ambiente.  
  
#### <a name="to-use-an-environment-variable-in-an-msbuild-project"></a>Para usar uma variável de ambiente em um projeto MSBuild  
  
- Faça referência à variável de ambiente da mesma maneira que faria com uma variável declarada em seu arquivo de projeto. Por exemplo, o código a seguir faz referência à variável de ambiente BIN_PATH:  
  
   `<FinalOutput>$(BIN_PATH)\MyAssembly.dll</FinalOutput>`  
  
  Você pode usar um atributo `Condition` para fornecer um valor padrão para uma propriedade se a variável de ambiente não foi definida.  
  
#### <a name="to-provide-a-default-value-for-a-property"></a>Para fornecer um valor padrão de uma propriedade  
  
-   Use um atributo `Condition` em uma propriedade para definir o valor somente se a propriedade não tiver nenhum valor. Por exemplo, o seguinte código define a propriedade `ToolsPath` como *c:\tools* somente se a variável de ambiente `ToolsPath` não está definida:  
  
     `<ToolsPath Condition="'$(TOOLSPATH)' == ''">c:\tools</ToolsPath>`  
  
    > [!NOTE]
    >  Os nomes de propriedade não diferenciam maiúsculas de minúsculas então `$(ToolsPath)` e `$(TOOLSPATH)` fazem referência à mesma variável de ambiente ou propriedade.  
  
## <a name="example"></a>Exemplo  
 O arquivo de projeto a seguir usa variáveis de ambiente para especificar o local dos diretórios.  
  
```xml  
<Project DefaultTargets="FakeBuild">  
    <PropertyGroup>  
        <FinalOutput>$(BIN_PATH)\myassembly.dll</FinalOutput>  
        <ToolsPath Condition=" '$(ToolsPath)' == '' ">  
            C:\Tools  
        </ToolsPath>  
    </PropertyGroup>  
    <Target Name="FakeBuild">  
        <Message Text="Building $(FinalOutput) using the tools at $(ToolsPath)..."/>  
    </Target>  
</Project>  
```  
  
## <a name="see-also"></a>Consulte também  
[MSBuild ](../msbuild/msbuild.md)  
[Propriedades do MSBuild](../msbuild/msbuild-properties.md)  
[Como criar os mesmos arquivos de origem com opções diferentes](../msbuild/how-to-build-the-same-source-files-with-different-options.md)  
