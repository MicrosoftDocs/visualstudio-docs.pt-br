---
title: Elemento Project (MSBuild) | Microsoft Docs
ms.date: 03/13/2017
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/msbuild/2003#Project
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- ToolsVersion attribute [MSBuild]
- <Project> element [MSBuild]
- Project element [MSBuild]
ms.assetid: d1cda56a-dbef-4109-9201-39e962e3f653
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 1bb7c49e4f3dc86594c8a3211bacb538d3f10c4f
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/01/2020
ms.locfileid: "75597432"
---
# <a name="project-element-msbuild"></a>Elemento Project (MSBuild)
Elemento raiz necessário de um arquivo de projeto [!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)].

## <a name="syntax"></a>Sintaxe

```xml
<Project InitialTargets="TargetA;TargetB"
         DefaultTargets="TargetC;TargetD"
         TreatAsLocalProperty="PropertyA;PropertyB"
         ToolsVersion=<version number>
         Sdk="name[/version]"
         xmlns="http://schemas.microsoft.com/developer/msbuild/2003">
    <Sdk... />
    <Choose>... </Choose>
    <PropertyGroup>... </PropertyGroup>
    <ItemGroup>... </ItemGroup>
    <Target>... </Target>
    <UsingTask.../>
    <ProjectExtensions>... </ProjectExtensions>
    <Import... />
</Project>
```

## <a name="attributes-and-elements"></a>Atributos e elementos
 As seções a seguir descrevem os atributos, bem como os elementos filhos e pais.

### <a name="attributes"></a>{1&gt;{2&gt;Atributos&lt;2}&lt;1}

| Atributo | Descrição |
|------------------------| - |
| `DefaultTargets` | Atributo opcional.<br /><br /> Os destinos padrão serão o ponto de entrada do build se nenhum destino for especificado. Vários destinos são separados por ponto e vírgula (;).<br /><br /> Se nenhum destino padrão for especificado no atributo `DefaultTargets` ou na linha de comando [!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)], o mecanismo executa o primeiro destino no arquivo de projeto após os elementos [Import](../msbuild/import-element-msbuild.md) serem avaliados. |
| `InitialTargets` | Atributo opcional.<br /><br /> Os destinos iniciais serão executados antes dos destinos especificados no atributo `DefaultTargets` ou na linha de comando. Vários destinos são separados por ponto e vírgula (`;`). Se vários arquivos importados definirem `InitialTargets`, todos os destinos mencionados serão executados, na ordem em que as importações forem encontradas. |
| `Sdk` | Atributo opcional. <br /><br /> O nome e a versão opcional do SDK a ser usado para criar instruções Import implícitas adicionadas ao arquivo .proj. Se nenhuma versão for especificada, o MSBuild tentará resolver uma versão padrão.  Por exemplo `<Project Sdk="Microsoft.NET.Sdk" />` ou `<Project Sdk="My.Custom.Sdk/1.0.0" />`. |
| `ToolsVersion` | Atributo opcional.<br /><br /> A versão do Conjunto de Ferramentas MSBuild usada para determinar os valores para $(MSBuildBinPath) e $(MSBuildToolsPath). |
| `TreatAsLocalProperty` | Atributo opcional.<br /><br /> Nomes de propriedade não serão considerados globais. Esse atributo impede que as propriedades específicas de linha de comando substituam valores de propriedade definidos em um arquivo de projeto ou destinos e todas as importações subsequentes. Várias propriedades são separadas por ponto e vírgula (;).<br /><br /> Normalmente, propriedades globais substituem os valores de propriedade que são definidos no arquivo de projeto ou destinos. Se a propriedade está listada no valor `TreatAsLocalProperty`, o valor da propriedade global não substitui os valores de propriedade definidos no arquivo e as importações subsequentes. Para saber mais, confira [Como compilar os mesmos arquivos de origem com opções diferentes](../msbuild/how-to-build-the-same-source-files-with-different-options.md). **Observação:** defina as propriedades globais na linha de comandos usando a opção **-property** (ou **-p**). Você também pode definir ou modificar as propriedades globais para projetos filho em um build de vários projetos usando o atributo `Properties` da tarefa MSBuild. Para obter mais informações, confira [Tarefa do MSBuild](../msbuild/msbuild-task.md). |
| `xmlns` | Atributo opcional.<br /><br /> Quando especificado, o atributo `xmlns` deve ter o valor `http://schemas.microsoft.com/developer/msbuild/2003`. |

### <a name="child-elements"></a>Child elements

| Elemento | Descrição |
| - | - |
| [Choose](../msbuild/choose-element-msbuild.md) | Elemento opcional.<br /><br /> Avalia a elementos filho para selecionar um conjunto de elementos `ItemGroup` e/ou `PropertyGroup` a ser avaliado. |
| [Import](../msbuild/import-element-msbuild.md) | Elemento opcional.<br /><br /> Permite que um arquivo de projeto importe outro arquivo de projeto. Pode ser que não haja nenhum ou mais de um elemento `Import` em um projeto. |
| [ImportGroup](../msbuild/importgroup-element.md) | Elemento opcional.<br /><br /> Contém uma coleção de elementos `Import` que são agrupados em uma condição opcional. |
| [ItemGroup](../msbuild/itemgroup-element-msbuild.md) | Elemento opcional.<br /><br /> Um elemento de agrupamento para itens individuais. Itens são especificados usando o elemento [Item](../msbuild/item-element-msbuild.md). Pode ser que não haja nenhum ou mais de um elemento `ItemGroup` em um projeto. |
| [ItemDefinitionGroup](../msbuild/itemdefinitiongroup-element-msbuild.md) | Elemento opcional.<br /><br /> Permite definir um conjunto de Definições de Item, que são valores de metadados aplicados por padrão a todos os itens do projeto. ItemDefinitionGroup substitui a necessidade de usar as tarefas `CreateItem` e `CreateProperty`. |
| [ProjectExtensions](../msbuild/projectextensions-element-msbuild.md) | Elemento opcional.<br /><br /> Fornece uma maneira de manter informações não [!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)] em um arquivo de projeto [!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)]. Pode ser que não haja nenhum ou um elemento `ProjectExtensions` em um projeto. |
| [PropertyGroup](../msbuild/propertygroup-element-msbuild.md) | Elemento opcional.<br /><br /> Um elemento de agrupamento para propriedades individuais. Propriedades são especificadas usando o elemento [Property](../msbuild/property-element-msbuild.md). Pode ser que não haja nenhum ou mais de um elemento `PropertyGroup` em um projeto. |
| [Sdk](../msbuild/sdk-element-msbuild.md) | Elemento opcional.<br /><br /> Faz referência a um SDK do projeto [!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)].  Esse elemento pode ser usado como uma alternativa para o atributo Sdk. |
| [Target](../msbuild/target-element-msbuild.md) | Elemento opcional.<br /><br /> Contém um conjunto de tarefas para [!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)] executar em sequência. Tarefas são especificadas usando o elemento [Task](../msbuild/task-element-msbuild.md). Pode ser que não haja nenhum ou mais de um elemento `Target` em um projeto. |
| [UsingTask](../msbuild/usingtask-element-msbuild.md) | Elemento opcional.<br /><br /> Fornece uma maneira para registrar tarefas em [!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)]. Pode ser que não haja nenhum ou mais de um elemento `UsingTask` em um projeto. |

### <a name="parent-elements"></a>Elementos pai
 Nenhuma.

## <a name="see-also"></a>Veja também
- [Como especificar qual destino deve ser compilado primeiro](../msbuild/how-to-specify-which-target-to-build-first.md)
- [Referência de linha de comando](../msbuild/msbuild-command-line-reference.md)
- [Referência de esquema de arquivos de projeto](../msbuild/msbuild-project-file-schema-reference.md)
- [MSBuild](../msbuild/msbuild.md)
