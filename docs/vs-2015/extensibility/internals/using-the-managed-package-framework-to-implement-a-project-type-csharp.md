---
title: Usando a estrutura de pacote gerenciado para implementar um tipo de projeto (c#) | Microsoft Docs
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
- projects [Visual Studio SDK], creating with MPF
- MPF projects
- managed package framework, creating projects
ms.assetid: 926de536-eead-415b-9451-f1ddc8c44630
caps.latest.revision: 21
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: f248bdafaf0fdd632069e6cffe367cf0ed21135f
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51741980"
---
# <a name="using-the-managed-package-framework-to-implement-a-project-type-c"></a>Usando a estrutura de pacote gerenciado para implementar um tipo de projeto (C#)
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

Estrutura de pacote gerenciado (MPF) fornece as classes do c# você pode usar ou herdar de implementar seus próprios tipos de projeto. MPF implementa a muitas das interfaces do que Visual Studio espera um tipo de projeto para fornecer, deixando-o livre para se concentrar em como implementar as particularidades de seu tipo de projeto.  
  
## <a name="using-the-mpf-project-source-code"></a>Usando o código-fonte MPF projeto  
 A estrutura de pacote gerenciado para projetos (MPFProj) fornece classes auxiliares para criar e gerenciar o novo sistema de projeto. Ao contrário de outras classes no MPF, as classes do projeto não estão incluídas nos assemblies que acompanham o Visual Studio. Em vez disso, as classes do projeto são fornecidas como código-fonte no [MPF de projetos 2013](http://mpfproj12.codeplex.com).  
  
 Para adicionar esse projeto à sua solução de VSPackage, faça o seguinte:  
  
1.  Baixar os arquivos MPFProj *MPFProjectDir*.  
  
2.  No *MPFProjectDir*\Dev10\Src\CSharp\ProjectBase.file, altere o seguinte bloco:  
  
```  
<!-- Provide a default value for $(ProjectBasePath) -->  
  <PropertyGroup>  
    <ProjectBasePath >MPFProjDir\Dev10\Src\CSharp</ProjectBasePath>  
  </PropertyGroup>  
```  
  
1.  Crie um projeto de VSPackage.  
  
2.  Descarregue o projeto de VSPackage.  
  
3.  Editar o arquivo. csproj VSPackage adicionando o seguinte bloco antes das outras `<Import>` blocos:  
  
```  
<Import Project="MPFProjectDir\Dev10\Src\CSharp\ProjectBase.files" />  
  <PropertyGroup>  
    <!--To specify a different registry root to register your package, uncomment the TargetRegistryRoot tag and specify a registry root in it.  
    <TargetRegistryRoot></TargetRegistryRoot>-->  
    <RegisterOutputPackage>true</RegisterOutputPackage>  
    <RegisterWithCodebase>true</RegisterWithCodebase>  
  </PropertyGroup>  
```  
  
1.  Salvar o projeto.  
  
2.  Feche e reabra a solução de VSPackage.  
  
3.  Reabra o projeto de VSPackage. Você deve ver um novo diretório chamado ProjectBase.  
  
4.  Adicione a seguinte referência ao projeto de VSPackage:  
  
     Microsoft.Build.Tasks.4.0  
  
5.  Compile o projeto.  
  
## <a name="hierarchy-classes"></a>Hierarquia de Classes  
 A tabela a seguir resume as classes do MPFProj que dão suporte a hierarquias de projeto. Para obter mais informações, consulte [seleção e hierarquias](../../extensibility/internals/hierarchies-and-selection.md).  
  
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
  
## <a name="document-handling-classes"></a>Classes de manuseio de documento  
 A tabela a seguir lista as classes no MPF que dão suporte ao processamento de documentos. Para obter mais informações, consulte [abrindo e salvando itens de projeto](../../extensibility/internals/opening-and-saving-project-items.md).  
  
|Nome da classe|  
|----------------|  
|`Microsoft.VisualStudio.Package.DocumentManager`|  
|`Microsoft.VisualStudio.Package.FileDocumentManager`|  
  
## <a name="configuration-and-output-classes"></a>Configuração e Classes de saída  
 A tabela a seguir lista as classes no MPF que permitem que os tipos de projeto dão suporte a várias configurações, como debug e release e coleções de saída do projeto. Para obter mais informações, consulte [opções de configuração de gerenciamento de](../../extensibility/internals/managing-configuration-options.md).  
  
|Nome da classe|  
|----------------|  
|`Microsoft.VisualStudio.Package.ConfigProvider`|  
|`Microsoft.VisualStudio.Package.ProjectConfig`|  
|`Microsoft.VisualStudio.Package.BuildableProjectConfig`|  
|`Microsoft.VisualStudio.Package.OutputGroup`|  
|`Microsoft.VisualStudio.Package.ProjectElement`|  
  
## <a name="automation-support-classes"></a>Classes de suporte de automação  
 A tabela a seguir lista as classes do MPF que oferecem suporte à automação para que os usuários do seu tipo de projeto podem escrever suplementos.  
  
|Nome da classe|  
|----------------|  
|`Microsoft.VisualStudio.Package.Automation.OAProject`|  
|`Microsoft.VisualStudio.Package.Automation.OANavigableProjectItems`|  
|`Microsoft.VisualStudio.Package.Automation.OAProjectItems`|  
|`Microsoft.VisualStudio.Package.Automation.OAProjectItem`|  
|`Microsoft.VisualStudio.Package.Automation.OANestedProjectItem`|  
  
## <a name="properties-classes"></a>Classes de propriedades  
 A tabela a seguir lista as classes que permitem que os tipos de projeto MPF adicionar propriedades que os usuários podem procurar e modificar em um navegador de propriedade.  
  
|Nome da classe|  
|----------------|  
|`Microsoft.VisualStudio.Package.LocalizableProperties`|  
|`Microsoft.VisualStudio.Package.NodeProperties`|  
|`Microsoft.VisualStudio.Package.FileNodeProperties`|  
|`Microsoft.VisualStudio.Package.ProjectNodeProperties`|  
|`Microsoft.VisualStudio.Package.FolderNodeProperties`|  
|`Microsoft.VisualStudio.Package.ReferenceNodeProperties`|

