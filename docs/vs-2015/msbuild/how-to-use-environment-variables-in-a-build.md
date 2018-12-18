---
title: Como usar variáveis de ambiente em um build | Microsoft Docs
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
- environment variables, referencing
- projects [.NET Framework], environment variables
- MSBuild, environment variables
ms.assetid: 7f9e4469-8865-4b59-aab3-3ff26bd36e77
caps.latest.revision: 21
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 463acc185a73b9a483bf74c98d4bde1cf0f42494
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49877498"
---
# <a name="how-to-use-environment-variables-in-a-build"></a>Como usar variáveis de ambiente em um build
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

  
Quando você compila projetos, geralmente é necessário definir opções de build usando informações que não estão no arquivo de projeto ou nos arquivos que compõem seu projeto. Normalmente, essas informações são armazenadas em variáveis de ambiente.  
  
## <a name="referencing-environment-variables"></a>Fazendo referência a variáveis de ambiente  
 Todas as variáveis de ambiente estão disponíveis para o arquivo de projeto [!INCLUDE[vstecmsbuildengine](../includes/vstecmsbuildengine-md.md)] ([!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)]) como propriedades.  
  
> [!NOTE]
>  Se o arquivo de projeto contiver uma definição explícita de uma propriedade que tem o mesmo nome que uma variável de ambiente, a propriedade no arquivo de projeto substituirá os valores de uma variável de ambiente.  
  
#### <a name="to-use-an-environment-variable-in-an-msbuild-project"></a>Para usar uma variável de ambiente em um projeto MSBuild  
  
- Faça referência à variável de ambiente da mesma maneira que faria com uma variável declarada em seu arquivo de projeto. Por exemplo, o código a seguir faz referência à variável de ambiente BIN_PATH:  
  
   `<FinalOutput>$(BIN_PATH)\MyAssembly.dll</FinalOutput>`  
  
  Você pode usar um atributo `Condition` para fornecer um valor padrão para uma propriedade se a variável de ambiente não foi definida.  
  
#### <a name="to-provide-a-default-value-for-a-property"></a>Para fornecer um valor padrão de uma propriedade  
  
-   Use um atributo `Condition` em uma propriedade para definir o valor somente se a propriedade não tiver nenhum valor. Por exemplo, o código a seguir definirá a propriedade `ToolsPath` como c:\Tools somente se a variável de ambiente `ToolsPath` não estiver definida:  
  
     `<ToolsPath Condition="'$(TOOLSPATH)' == ''">c:\tools</ToolsPath>`  
  
    > [!NOTE]
    >  Os nomes de propriedade não diferenciam maiúsculas de minúsculas então `$(ToolsPath)` e `$(TOOLSPATH)` fazem referência à mesma variável de ambiente ou propriedade.  
  
## <a name="example"></a>Exemplo  
 O arquivo de projeto a seguir usa variáveis de ambiente para especificar o local dos diretórios.  
  
```  
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

[MSBuild](msbuild.md)

[Propriedades MSBuild](../msbuild/msbuild-properties1.md)

[Como compilar os mesmos arquivos de origem com opções diferentes](../msbuild/how-to-build-the-same-source-files-with-different-options.md)


