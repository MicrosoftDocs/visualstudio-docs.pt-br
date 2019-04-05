---
title: Elemento folder (modelos de projeto do Visual Studio) | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/vstemplate/2005#Folder
helpviewer_keywords:
- Folder element [Visual Studio project templates]
ms.assetid: 558e3d41-0db5-4c44-82bb-6bb87892b093
caps.latest.revision: 12
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 18c19025329a603b0854b016dc50d9b2ab9c9e69
ms.sourcegitcommit: 8b538eea125241e9d6d8b7297b72a66faa9a4a47
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/23/2019
ms.locfileid: "58929236"
---
# <a name="folder-element-visual-studio-project-templates"></a>Elemento de pasta (modelos de projeto do Visual Studio)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Especifica uma pasta que será adicionada ao projeto.  
  
 \<VSTemplate>  
 \<TemplateContent>  
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
|`TargetFolderName`|Atributo opcional.<br /><br /> Especifica o nome a ser atribuído a pasta quando um projeto é criado a partir do modelo. Esse atributo é útil para usar substituição de parâmetro para criar um nome de pasta ou uma pasta com uma cadeia de caracteres internacional de nomenclatura que não pode ser usado diretamente no arquivo. zip.|  
  
### <a name="child-elements"></a>Elementos filho  
  
|Elemento|Descrição|  
|-------------|-----------------|  
|`Folder`|Especifica uma pasta a ser adicionada ao projeto. `Folder` os elementos podem conter filho `Folder` elementos.|  
|[ProjectItem](../extensibility/projectitem-element-visual-studio-item-templates.md)|Especifica um arquivo para adicionar ao projeto.|  
  
### <a name="parent-elements"></a>Elementos pai  
  
|Elemento|Descrição|  
|-------------|-----------------|  
|[Projeto](../extensibility/project-element-visual-studio-templates.md)|Elemento filho opcional de [TemplateContent](../extensibility/templatecontent-element-visual-studio-templates.md).|  
  
## <a name="remarks"></a>Comentários  
 `Folder` é um filho opcional de `Project`.  
  
 Você pode usar qualquer um dos seguintes métodos para organizar itens de projeto em pastas em um modelo:  
  
-   Incluir as pastas em que o arquivo. zip de modelo e adicioná-los ao projeto no arquivo. vstemplate, especificando o caminho para o arquivo na `ProjectItem` elementos, sem nenhum `Folder` elementos. Esse é o método recomendado. Por exemplo:  
  
     `...`  
  
     `<ProjectItem>\Folder\item.cs</ProjectItem>`  
  
     `<ProjectItem>Form1.cs</ProjectItem>`  
  
     `...`  
  
-   Incluir as pastas em que o arquivo. zip de modelo e adicioná-los ao projeto no arquivo. vstemplate com `Folder` elementos. Por exemplo:  
  
     `...`  
  
     `<Folder name="Folder">`  
  
     `<ProjectItem>item.cs</ProjectItem>`  
  
     `</Folder>`  
  
     `<ProjectItem>Form1.cs</ProjectItem>`  
  
     `...`  
  
-   Não inclua pastas no arquivo. zip de modelo, mas adicionar pastas usando o `TargetFileName` atributo do `ProjectItem` elemento. Por exemplo:  
  
     `...`  
  
     `<ProjectItem TargetFileName="\Folder\item.cs">item.cs</ProjectItem>`  
  
     `<ProjectItem>Form1.cs</ProjectItem>`  
  
     `...`  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir ilustra os metadados para um modelo de projeto para um [!INCLUDE[csprcs](../includes/csprcs-md.md)] aplicativo do Windows.  
  
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
 [Criando modelos de projeto e de item](../ide/creating-project-and-item-templates.md)   
 [Elemento ProjectItem (Modelos de item do Visual Studio)](../extensibility/projectitem-element-visual-studio-item-templates.md)
