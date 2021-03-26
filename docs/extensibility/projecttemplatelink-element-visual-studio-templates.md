---
title: Elemento ProjectTemplateLink (modelos do Visual Studio) | Microsoft Docs
description: Saiba mais sobre o <element> elemento e como ele especifica o caminho para o arquivo. vstemplate de um projeto em um modelo de vários projetos.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/vstemplate/2005#ProjectTemplateLink
helpviewer_keywords:
- <ProjectTemplateLink> element [Visual Studio Templates]
- ProjectTemplateLink element [Visual Studio Templates]
ms.assetid: b0449111-8b48-45a1-a031-ea24b765e969
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 8f1dc03239481e59d26445161dcd7c0137b18d75
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105068655"
---
# <a name="projecttemplatelink-element-visual-studio-templates"></a>Elemento ProjectTemplateLink (modelos do Visual Studio)
Especifica o caminho para o arquivo *. vstemplate* de um projeto em um modelo de vários projetos.

 \<VSTemplate> \<TemplateContent>
 \<ProjectCollection>
 \<ProjectTemplateLink>
or \<VSTemplate>
 \<TemplateContent>
 \<ProjectCollection>
 \<SolutionFolder>
 \<ProjectTemplateLink>

## <a name="syntax"></a>Sintaxe

```xml
<ProjectTemplateLink ProjectName="Name">
    PathToTemplateFile
</ProjectTemplateLink>
```

## <a name="attributes-and-elements"></a>Atributos e elementos
 As seções a seguir descrevem atributos, elementos filho e elementos pai.

### <a name="attributes"></a>Atributos

|Atributo|Descrição|
|---------------|-----------------|
|`ProjectName`|Atributo opcional.<br /><br /> Especifica o nome de cada projeto individual em um modelo de vários projetos. A caixa de diálogo **novo projeto** não pode atribuir nomes a projetos individuais.|
|`CopyParameters`|Permite que todas as variáveis no modelo de grupo principal sejam copiadas em cada um dos modelos vinculados.<br /><br /> Os parâmetros nos modelos vinculados têm um prefixo `"$ext_*$"`. Por exemplo, se no modelo de grupo pai, o parâmetro `$projectname$` tem um valor **ExampleProject1**, quando o modelo vinculado obtém sua vez de ser executado, ele adquire um parâmetro `$ext_projectname$` , que é uma cópia do `$projectname$` parâmetro do modelo de grupo pai.<br /><br /> Isso permite que modelos vinculados compartilhem alguns parâmetros comuns, que podem ser convenientemente criados somente no modelo de grupo pai.<br /><br /> Esse atributo é opcional e padronizado automaticamente para `false` quando não é incluído.<br /><br /> Introduzido no Visual Studio 2013 Atualização 2. Para fazer referência à versão correta do produto, consulte [assemblies de referência entregues na atualização 2 do SDK do Visual Studio 2013](/previous-versions/dn632168(v=vs.120)).|

### <a name="child-elements"></a>Elementos filho
 Nenhum.

### <a name="parent-elements"></a>Elementos pai

|Elemento|Descrição|
|-------------|-----------------|
|[ProjectCollection](../extensibility/projectcollection-element-visual-studio-templates.md)|Especifica a organização e o conteúdo de modelos de vários projetos.|
|[SolutionFolder](../extensibility/solutionfolder-element-visual-studio-templates.md)|Agrupa projetos em modelos de vários projetos.|

## <a name="text-value"></a>Valor de texto
 Um valor de texto é obrigatório.

 Esse texto especifica o caminho para o arquivo *. vstemplate* do modelo.

## <a name="remarks"></a>Comentários
 Os modelos de vários projetos atuam como contêineres para dois ou mais projetos. O `ProjectTemplateLink` elemento é usado para especificar o local do arquivo *. vstemplate* para um dos projetos no modelo. O arquivo *. vstemplate* de um modelo de vários projetos contém um `ProjectTemplateLink` elemento para cada projeto no modelo. Para obter mais informações sobre modelos de vários projetos, consulte [como: criar modelos de vários projetos](../ide/how-to-create-multi-project-templates.md).

## <a name="example"></a>Exemplo
 Este exemplo mostra um arquivo de raiz *. vstemplate* de vários projetos simples. Neste exemplo, o modelo contém dois projetos, `My Windows Application` e `My Class Library`. O atributo `ProjectName` no elemento `ProjectTemplateLink` define o nome do [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] para atribuir este projeto. Se o `ProjectName` atributo não existir, o nome do arquivo *. vstemplate* será usado como o nome do projeto.

```
<VSTemplate Version="3.0.0" Type="ProjectGroup"
    xmlns="http://schemas.microsoft.com/developer/vstemplate/2005">
    <TemplateData>
        <Name>Multi-Project Template Sample</Name>
        <Description>An example of a multi-project template</Description>
        <Icon>Icon.ico</Icon>
        <ProjectType>VisualBasic</ProjectType>
    </TemplateData>
    <TemplateContent>
        <ProjectCollection>
            <ProjectTemplateLink ProjectName="My Windows Application">
                WindowsApp\MyTemplate.vstemplate
            </ProjectTemplateLink>
            <ProjectTemplateLink ProjectName="My Class Library" CopyParameters="true">
                ClassLib\MyTemplate.vstemplate
            </ProjectTemplateLink>
        </ProjectCollection>
    </TemplateContent>
</VSTemplate>
```

## <a name="see-also"></a>Confira também
- [Referência de esquema de modelo do Visual Studio](../extensibility/visual-studio-template-schema-reference.md)
- [Criar modelos de projeto e de item](../ide/creating-project-and-item-templates.md)
- [Como: criar modelos de vários projetos](../ide/how-to-create-multi-project-templates.md)