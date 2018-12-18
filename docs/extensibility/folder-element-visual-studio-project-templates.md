---
title: Elemento folder (modelos de projeto do Visual Studio) | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-general
ms.topic: conceptual
f1_keywords:
- http://schemas.microsoft.com/developer/vstemplate/2005#Folder
helpviewer_keywords:
- Folder element [Visual Studio project templates]
ms.assetid: 558e3d41-0db5-4c44-82bb-6bb87892b093
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: b4fca64abf91105e0363ecd67ea5244c533996f3
ms.sourcegitcommit: 1c2ed640512ba613b3bbbc9ce348e28be6ca3e45
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2018
ms.locfileid: "39497169"
---
# <a name="folder-element-visual-studio-project-templates"></a>Elemento folder (modelos de projeto do Visual Studio)
Especifica uma pasta que será adicionada ao projeto.  
  
 \<VSTemplate >  
 \<TemplateContent >  
 \<Project>  
 \<Pasta >  
  
## <a name="syntax"></a>Sintaxe  
  
```  
<Folder Name="Project Folder">  
    <Folder> ... </Folder>  
    <ProjectItem> ... </ProjectItem>  
</Folder>  
```  
  
## <a name="attributes-and-elements"></a>Atributos e elementos  
 As seções a seguir descrevem atributos, elementos filho e elementos pai.  
  
### <a name="attributes"></a>Atributos  
  
|Atributo|Descrição|  
|---------------|-----------------|  
|`Name`|Atributo obrigatório.<br /><br /> O nome da pasta do projeto.|  
|`TargetFolderName`|Atributo opcional.<br /><br /> Especifica o nome a ser atribuído a pasta quando um projeto é criado a partir do modelo. Esse atributo é útil para usar substituição de parâmetro para criar um nome de pasta ou uma pasta com uma cadeia de caracteres internacional de nomenclatura que não pode ser usado diretamente na *. zip* arquivo.|  
  
### <a name="child-elements"></a>Elementos filho  
  
|Elemento|Descrição|  
|-------------|-----------------|  
|`Folder`|Especifica uma pasta a ser adicionada ao projeto. `Folder` os elementos podem conter filho `Folder` elementos.|  
|[Item de projeto](../extensibility/projectitem-element-visual-studio-item-templates.md)|Especifica um arquivo para adicionar ao projeto.|  
  
### <a name="parent-elements"></a>Elementos pai  
  
|Elemento|Descrição|  
|-------------|-----------------|  
|[Projeto](../extensibility/project-element-visual-studio-templates.md)|Elemento filho opcional de [TemplateContent](../extensibility/templatecontent-element-visual-studio-templates.md).|  
  
## <a name="remarks"></a>Comentários  
 `Folder` é um filho opcional de `Project`.  
  
 Você pode usar qualquer um dos seguintes métodos para organizar itens de projeto em pastas em um modelo:  
  
-   Incluir as pastas no modelo *. zip* do arquivo e adicioná-los ao projeto na *. vstemplate* arquivo, especificando o caminho para o arquivo no `ProjectItem` elementos, sem nenhum `Folder` elementos. Esse é o método recomendado. Por exemplo:  
  
     `...`  
  
     `<ProjectItem>\Folder\item.cs</ProjectItem>`  
  
     `<ProjectItem>Form1.cs</ProjectItem>`  
  
     `...`  
  
-   Incluir as pastas no modelo *. zip* do arquivo e adicioná-los ao projeto na *. vstemplate* arquivo com `Folder` elementos. Por exemplo:  
  
     `...`  
  
     `<Folder name="Folder">`  
  
     `<ProjectItem>item.cs</ProjectItem>`  
  
     `</Folder>`  
  
     `<ProjectItem>Form1.cs</ProjectItem>`  
  
     `...`  
  
-   Não inclua pastas no modelo *. zip* do arquivo, mas adicionar pastas usando o `TargetFileName` atributo do `ProjectItem` elemento. Por exemplo:  
  
     `...`  
  
     `<ProjectItem TargetFileName="\Folder\item.cs">item.cs</ProjectItem>`  
  
     `<ProjectItem>Form1.cs</ProjectItem>`  
  
     `...`  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir ilustra os metadados para um modelo de projeto para um [!INCLUDE[csprcs](../data-tools/includes/csprcs_md.md)] aplicativo do Windows.  
  
```  
<VSTemplate Type="Project" Version="3.0.0"  
    xmlns="http://schemas.microsoft.com/developer/vstemplate/2005">  
    <TemplateData>  
        <Name>My template</Name>  
        <Description>A basic template</Description>  
        <Icon>TemplateIcon.ico</Icon>  
        <ProjectType>CSharp</ProjectType>  
    </TemplateData>  
    <TemplateContent>  
        <Project File="MyTemplate.csproj">  
            <ProjectItem>Form1.cs<ProjectItem>  
            <ProjectItem>Form1.Designer.cs</ProjectItem>  
            <ProjectItem>Program.cs</ProjectItem>  
            <Folder Name="Properties">  
                <ProjectItem>AssemblyInfo.cs</ProjectItem>  
                <ProjectItem>Resources.resx</ProjectItem>  
                <ProjectItem>Resources.Designer.cs</ProjectItem>  
                <ProjectItem>Settings.settings</ProjectItem>  
                <ProjectItem>Settings.Designer.cs</ProjectItem>  
            </Folder>  
        </Project>  
    </TemplateContent>  
</VSTemplate>  
```  
  
## <a name="see-also"></a>Consulte também  
 [Referência de esquema de modelo do Visual Studio](../extensibility/visual-studio-template-schema-reference.md)   
 [Criando modelos de projeto e item](../ide/creating-project-and-item-templates.md)   
 [Elemento ProjectItem (modelos de item do Visual Studio)](../extensibility/projectitem-element-visual-studio-item-templates.md)