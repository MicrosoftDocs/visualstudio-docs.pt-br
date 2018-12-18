---
title: Elemento EnableLocationBrowseButton (modelos do Visual Studio) | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-general
ms.topic: conceptual
f1_keywords:
- http://schemas.microsoft.com/developer/vstemplate/2005#EnableLocationBrowseButton
helpviewer_keywords:
- EnableLocationBrowseButton [Visual Studio project templates]
ms.assetid: a12d10d8-af49-482a-af77-e084fd07a47d
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 7bebf88b8d5c98722226f42f9a1b1666695a3b7e
ms.sourcegitcommit: 06db1892fff22572f0b0a11994dc547c2b7e2a48
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/08/2018
ms.locfileid: "39639533"
---
# <a name="enablelocationbrowsebutton-element-visual-studio-templates"></a>Elemento EnableLocationBrowseButton (modelos do Visual Studio)
Especifica se o **navegue** botão está disponível na **novo projeto** caixa de diálogo, para que os usuários podem facilmente modificar o diretório padrão em que um novo projeto é salvo.  
  
 \<VSTemplate >  
 \<TemplateData >  
 \<EnableLocationBrowseButton >  
  
## <a name="syntax"></a>Sintaxe  
  
```  
<EnableLocationBrowseButton> true/false </EnableLocationBrowseButton>  
```  
  
## <a name="attributes-and-elements"></a>Atributos e elementos  
 As seções a seguir descrevem atributos, elementos filho e elementos pai.  
  
### <a name="attributes"></a>Atributos  
 nenhuma.  
  
### <a name="child-elements"></a>Elementos filho  
 nenhuma.  
  
### <a name="parent-elements"></a>Elementos pai  
  
|Elemento|Descrição|  
|-------------|-----------------|  
|[TemplateData](../extensibility/templatedata-element-visual-studio-templates.md)|Elemento obrigatório.<br /><br /> Categoriza o modelo e define como ele é exibido em qualquer um de **novo projeto** ou o **Adicionar Novo Item** caixa de diálogo.|  
  
## <a name="text-value"></a>Valor de texto  
 Um valor de texto é obrigatório.  
  
 O texto deve ser `true` ou `false`, que indica se deve ou não exibir o **procurar** botão o **novo projeto** caixa de diálogo.  
  
## <a name="remarks"></a>Comentários  
 `EnableLocationBrowseButton` é um elemento opcional. O valor padrão é `true`, que exibe a **navegue** botão o **novo projeto** caixa de diálogo.  
  
 No **novo projeto** caixa de diálogo, o **local** caixa de texto Especifica o diretório em que um novo projeto é salvo. O **navegue** botão Ajuda você a modificar esse diretório, exibindo o **local do projeto** caixa de diálogo que permite que você navegue facilmente para um diretório diferente que está disponível no seu computador, e em seguida, escolha-o como o diretório onde o novo projeto é salvo.  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir ilustra os metadados para um [!INCLUDE[csprcs](../data-tools/includes/csprcs_md.md)] aplicativo do Windows.  
  
```  
<VSTemplate Type="Project" Version="3.0.0"  
    xmlns="http://schemas.microsoft.com/developer/vstemplate/2005">  
    <TemplateData>  
        <Name>My template</Name>  
        <Description>A basic starter kit</Description>  
        <Icon>TemplateIcon.ico</Icon>  
        <ProjectType>CSharp</ProjectType>  
        <EnableLocationBrowseButton>false</EnableLocationBrowseButton>  
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