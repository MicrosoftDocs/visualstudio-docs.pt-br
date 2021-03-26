---
title: Usar estrutura de pacote gerenciado para um tipo de projeto (C#)
description: Saiba mais sobre a estrutura de pacote gerenciada, que fornece classes .NET que você pode usar ou herdar do para implementar seus próprios tipos de projeto.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- projects [Visual Studio SDK], creating with MPF
- MPF projects
- managed package framework, creating projects
ms.assetid: 926de536-eead-415b-9451-f1ddc8c44630
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: cb047c9ef8c5c47c6509a6a5947be77a488e22f5
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105060725"
---
# <a name="using-the-managed-package-framework-to-implement-a-project-type-c"></a>Usando a estrutura de pacote gerenciado para implementar um tipo de projeto (C#)
A MPF (estrutura de pacote gerenciada) fornece classes C# que você pode usar ou herdar de para implementar seus próprios tipos de projeto. O MPF implementa muitas das interfaces que o Visual Studio espera que um tipo de projeto forneça, deixando você livre para se concentrar em implementar as particularidades do seu tipo de projeto.

## <a name="using-the-mpf-project-source-code"></a>Usando o código-fonte do projeto MPF
 A estrutura de pacote gerenciada para projetos (MPFProj) fornece classes auxiliares para criar e gerenciar o novo sistema de projeto. Ao contrário de outras classes no MPF, as classes de projeto não são incluídas nos assemblies fornecidos com o Visual Studio. Em vez disso, as classes de projeto são fornecidas como código-fonte no [MPF para projetos 2013](https://github.com/tunnelvisionlabs/MPFProj10).

 Para adicionar esse projeto à solução VSPackage, faça o seguinte:

1. Baixe os arquivos MPFProj para *MPFProjectDir*.

2. No *MPFProjectDir*\Dev10\Src\CSharp\ProjectBase.File, altere o bloco a seguir:

```
<!-- Provide a default value for $(ProjectBasePath) -->
  <PropertyGroup>
    <ProjectBasePath >MPFProjDir\Dev10\Src\CSharp</ProjectBasePath>
  </PropertyGroup>
```

1. Crie um projeto VSPackage.

2. Descarregue o projeto VSPackage.

3. Edite o arquivo VSPackage. csproj adicionando o bloco a seguir antes dos outros `<Import>` blocos:

```
<Import Project="MPFProjectDir\Dev10\Src\CSharp\ProjectBase.files" />
  <PropertyGroup>
    <!--To specify a different registry root to register your package, uncomment the TargetRegistryRoot tag and specify a registry root in it.
    <TargetRegistryRoot></TargetRegistryRoot>-->
    <RegisterOutputPackage>true</RegisterOutputPackage>
    <RegisterWithCodebase>true</RegisterWithCodebase>
  </PropertyGroup>
```

1. Salve o projeto.

2. Feche e reabra a solução VSPackage.

3. Reabra o projeto VSPackage. Você deverá ver um novo diretório chamado ProjectBase.

4. Adicione a seguinte referência ao projeto VSPackage:

     Microsoft. Build. Tasks. 4.0

5. Compile o projeto.

## <a name="hierarchy-classes"></a>Classes de hierarquia
 A tabela a seguir resume as classes no MPFProj que dão suporte a hierarquias de projeto. Para obter mais informações, consulte [hierarquias e seleção](../../extensibility/internals/hierarchies-and-selection.md).

|Nome da classe|
|----------------|
|`Microsoft.VisualStudio.Package.HierarchyNode`|
|`Microsoft.VisualStudio.Package.ProjectNode`|
|`Microsoft.VisualStudio.Package.ProjectContainerNode`|
|`Microsoft.VisualStudio.Package.FileNode`|
|`Microsoft.VisualStudio.Package.FolderNode`|
|`Microsoft.VisualStudio.Package.ReferenceContainerNode`|
|`Microsoft.VisualStudio.Package.ReferenceNode`|
|`Microsoft.VisualStudio.Package.ProjectReferenceNode`|
|`Microsoft.VisualStudio.Package.ComReferenceNode`|
|`Microsoft.VisualStudio.Package.AssemblyReferenceNode`|
|`Microsoft.VisualStudio.Package.BuildDependency`|

## <a name="document-handling-classes"></a>Classes de Document-Handling
 A tabela a seguir lista as classes no MPF que dão suporte ao manuseio de documentos. Para obter mais informações, consulte [abrindo e salvando itens de projeto](../../extensibility/internals/opening-and-saving-project-items.md).

|Nome da classe|
|----------------|
|`Microsoft.VisualStudio.Package.DocumentManager`|
|`Microsoft.VisualStudio.Package.FileDocumentManager`|

## <a name="configuration-and-output-classes"></a>Classes de configuração e saída
 A tabela a seguir lista as classes no MPF que permitem que os tipos de projeto ofereçam suporte a várias configurações, como depuração e liberação, e coleções de saída do projeto. Para obter mais informações, consulte [Gerenciando opções de configuração](../../extensibility/internals/managing-configuration-options.md).

|Nome da classe|
|----------------|
|`Microsoft.VisualStudio.Package.ConfigProvider`|
|`Microsoft.VisualStudio.Package.ProjectConfig`|
|`Microsoft.VisualStudio.Package.BuildableProjectConfig`|
|`Microsoft.VisualStudio.Package.OutputGroup`|
|`Microsoft.VisualStudio.Package.ProjectElement`|

## <a name="automation-support-classes"></a>Classes de Automation-Support
 A tabela a seguir lista as classes no MPF que dão suporte à automação para que os usuários do tipo de projeto possam gravar suplementos.

|Nome da classe|
|----------------|
|`Microsoft.VisualStudio.Package.Automation.OAProject`|
|`Microsoft.VisualStudio.Package.Automation.OANavigableProjectItems`|
|`Microsoft.VisualStudio.Package.Automation.OAProjectItems`|
|`Microsoft.VisualStudio.Package.Automation.OAProjectItem`|
|`Microsoft.VisualStudio.Package.Automation.OANestedProjectItem`|

## <a name="properties-classes"></a>Classes de propriedades
 A tabela a seguir lista as classes no MPF que permitem que os tipos de projeto adicionem propriedades que os usuários podem procurar e modificar em um navegador de propriedades.

|Nome da classe|
|----------------|
|`Microsoft.VisualStudio.Package.LocalizableProperties`|
|`Microsoft.VisualStudio.Package.NodeProperties`|
|`Microsoft.VisualStudio.Package.FileNodeProperties`|
|`Microsoft.VisualStudio.Package.ProjectNodeProperties`|
|`Microsoft.VisualStudio.Package.FolderNodeProperties`|
|`Microsoft.VisualStudio.Package.ReferenceNodeProperties`|
