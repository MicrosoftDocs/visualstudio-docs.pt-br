---
title: Elemento (modelos do Visual Studio) Project | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-general
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- http://schemas.microsoft.com/developer/vstemplate/2005#Project
helpviewer_keywords:
- Project element [Visual Studio Templates]
- <Project> element [Visual Studio Templates]
ms.assetid: 1da15ea6-26e2-462b-a03e-584ef4996579
caps.latest.revision: 17
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 07700501ae2a76337fed499aeb0a66b8b19dbeba
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51741121"
---
# <a name="project-element-visual-studio-templates"></a>Elemento de projeto (Modelos do Visual Studio)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Especifica os arquivos ou diretórios a serem adicionados ao projeto.  
  
 \<VSTemplate >  
 \<TemplateContent >  
 \<Project>  
  
## <a name="syntax"></a>Sintaxe  
  
```  
<Project  
    File="MyProject.proj"  
    TargetFileName="MyTargetProject.proj"  
    ReplaceParameters="true/false">  
    IgnoreProjectParameter="$myCustomParameter$"  
        ...  
</Project>  
```  
  
## <a name="attributes-and-elements"></a>Atributos e elementos  
 As seções a seguir descrevem atributos, elementos filho e elementos pai.  
  
### <a name="attributes"></a>Atributos  
  
|Atributo|Descrição|  
|---------------|-----------------|  
|`File`|Atributo obrigatório.<br /><br /> Especifica o nome do arquivo de projeto no modelo de arquivo. zip.|  
|`ReplaceParameters`|Atributo opcional.<br /><br /> Um valor booliano que especifica se o arquivo de projeto tem valores de parâmetros que devem ser substituídas quando um projeto é criado a partir do modelo. O valor padrão é `false`.|  
|`TargetFileName`|Atributo opcional.<br /><br /> Especifica o nome do arquivo de projeto quando um projeto é criado a partir do modelo.|  
|`IgnoreProjectParameter`|Atributo opcional.<br /><br /> Especifica se o projeto deve ser adicionado à solução atual. Se o valor do parâmetro personalizado, "$*myCustomParameter*$" existe no arquivo de substituição de parâmetro, o projeto é criado, mas não é adicionado como parte da solução atualmente aberta.|  
  
### <a name="child-elements"></a>Elementos filho  
  
|Elemento|Descrição|  
|-------------|-----------------|  
|[Pasta](../extensibility/folder-element-visual-studio-project-templates.md)|Elemento opcional.<br /><br /> Especifica uma pasta a ser adicionada ao projeto.|  
|[Item de projeto](../extensibility/projectitem-element-visual-studio-project-templates.md)|Elemento opcional.<br /><br /> Especifica um arquivo para adicionar a um projeto.|  
  
### <a name="parent-elements"></a>Elementos pai  
  
|Elemento|Descrição|  
|-------------|-----------------|  
|[TemplateContent](../extensibility/templatecontent-element-visual-studio-templates.md)|Elemento obrigatório.|  
  
## <a name="remarks"></a>Comentários  
 O `Project` é um elemento filho opcional de `TemplateContent`.  
  
 O `Project` elemento é usado para especificar um projeto e, portanto, só é válido em modelos de projeto.  
  
 `Project` elementos podem ter [pasta](../extensibility/folder-element-visual-studio-project-templates.md) elementos filhos ou [ProjectItem](../extensibility/projectitem-element-visual-studio-project-templates.md) elementos filhos, mas não uma mistura de ambos `Folder` e `ProjectItem` elementos filhos.  
  
 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] Renomeia automaticamente o nome do arquivo de projeto com base no nome inserido pelo usuário na **novo projeto** caixa de diálogo. Use o `TargetFileName` se você quiser fornecer um nome de arquivo alternativo para os arquivos de projeto criados com o modelo de atributo.  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir mostra os metadados para um modelo de projeto para um [!INCLUDE[csprcs](../includes/csprcs-md.md)] aplicativo.  
  
```  
<VSTemplate Type="Project" Version="3.0.0"  
    xmlns="http://schemas.microsoft.com/developer/vstemplate/2005">  
    <TemplateData>  
        <Name>My template</Name>  
        <Description>A basic starter kit</Description>  
        <Icon>TemplateIcon.ico</Icon>  
        <ProjectType>CSharp</ProjectType>  
    </TemplateData>  
    <TemplateContent>  
        <Project File="MyStarterKit.csproj">  
            <ProjectItem>Form1.cs<ProjectItem>  
            <ProjectItem>Form1.Designer.cs</ProjectItem>  
            <ProjectItem>Program.cs</ProjectItem>  
            <ProjectItem>Properties\AssemblyInfo.cs</ProjectItem>  
            <ProjectItem>Properties\Resources.resx</ProjectItem>  
            <ProjectItem>Properties\Resources.Designer.cs</ProjectItem>  
            <ProjectItem>Properties\Settings.settings</ProjectItem>  
            <ProjectItem>Properties\Settings.Designer.cs</ProjectItem>  
        </Project>  
    </TemplateContent>  
</VSTemplate>  
```  
  
## <a name="see-also"></a>Consulte também  
 [Referência de esquema de modelo do Visual Studio](../extensibility/visual-studio-template-schema-reference.md)   
 [Criando modelos de projeto e de item](../ide/creating-project-and-item-templates.md)   
 [Elemento ProjectItem (modelos de projeto do Visual Studio)](../extensibility/projectitem-element-visual-studio-project-templates.md)   
 [Elemento Folder (Modelos do Visual Studio)](../extensibility/folder-element-visual-studio-project-templates.md)

