---
title: Elemento ProjectItem (modelos de Item do Visual Studio) | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/vstemplate/2005#ProjectItem
helpviewer_keywords:
- <ProjectItem> element [Visual Studio item templates]
- ProjectItem element [Visual Studio item templates]
ms.assetid: 9ed94112-0c38-49df-b728-0dd2d0d1eb47
caps.latest.revision: 14
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 29b65f5cff9e2ffbed3c66c29c61f0a7e9e50f20
ms.sourcegitcommit: 8b538eea125241e9d6d8b7297b72a66faa9a4a47
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/23/2019
ms.locfileid: "58929163"
---
# <a name="projectitem-element-visual-studio-item-templates"></a>Elemento ProjectItem (modelos de item do Visual Studio)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Especifica um arquivo que está incluído no modelo de item.  
  
> [!NOTE]
>  O `ProjectItem` elemento aceita atributos diferentes, dependendo se o modelo é para um projeto ou um item. Este tópico explica o `ProjectItem` elemento para o item. Para obter uma explicação sobre o `ProjectItem` elemento para modelos de projeto, consulte [elemento ProjectItem (modelos de projeto do Visual Studio)](../extensibility/projectitem-element-visual-studio-project-templates.md).  
  
 \<VSTemplate>  
 \<TemplateContent>  
 \<ProjectItem>  
  
## <a name="syntax"></a>Sintaxe  
  
```  
<ProjectItem  
    SubType="Form/Component/CustomControl/UserControl"  
    CustomTool="string"  
    ItemType="string"  
    ReplaceParameters="true/false"  
    TargetFileName="TargetFileName.ext">  
        FileName.ext  
</ProjectItem>  
```  
  
## <a name="attributes-and-elements"></a>Atributos e elementos  
 As seções a seguir descrevem atributos, elementos filho e elementos pai.  
  
### <a name="attributes"></a>Atributos  
  
|Atributo|Descrição|  
|---------------|-----------------|  
|`SubType`|Atributo opcional.<br /><br /> Especifica o subtipo de um item em um modelo de item de vários arquivos. Esse valor é usado para determinar o editor que [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] usará para abrir o item.|  
|`CustomTool`|Atributo opcional.<br /><br /> Define o CustomTool para o item no arquivo de projeto.|  
|`ItemType`|Atributo opcional.<br /><br /> Define o ItemType para o item no arquivo de projeto.|  
|`ReplaceParameters`|Atributo opcional.<br /><br /> Um valor booliano que especifica se o item tem valores de parâmetros que devem ser substituídas quando um projeto é criado a partir do modelo. O valor padrão é `false`.|  
|`TargetFileName`|Atributo opcional.<br /><br /> Especifica o nome do item que é criado a partir do modelo. Esse atributo é útil para usar substituição de parâmetro para criar um nome de item.|  
  
### <a name="child-elements"></a>Elementos filho  
 nenhuma.  
  
### <a name="parent-elements"></a>Elementos pai  
  
|Elemento|Descrição|  
|-------------|-----------------|  
|[TemplateContent](../extensibility/templatecontent-element-visual-studio-templates.md)|Especifica o conteúdo do modelo.|  
  
## <a name="text-value"></a>Valor de texto  
 Um valor de texto é obrigatório.  
  
 Um `string` que representa o nome de um arquivo no arquivo. zip de modelo.  
  
## <a name="remarks"></a>Comentários  
 `ProjectItem` é um filho opcional de `TemplateContent`.  
  
 O `TargetFileName` atributo pode ser usado para renomear arquivos com parâmetros. Por exemplo, se o arquivo `MyFile.vb` existe no diretório raiz do arquivo. zip de modelo, mas você deseja que o arquivo será nomeado com base no nome do arquivo fornecido pelo usuário na **Adicionar Novo Item** caixa de diálogo, você usaria o seguinte XML:  
  
```  
<ProjectItem TargetFileName="$fileinputname$.vb">MyFile.vb</ProjectItem>  
```  
  
 Quando um item é criado com base neste modelo, o nome do arquivo será baseado no nome que o usuário inseriu na **Adicionar Novo Item** caixa de diálogo. Isso é útil durante a criação de modelos de item de vários arquivos. Para obter mais informações, confira [Como: Criar modelos de Item multiarquivos](../ide/how-to-create-multi-file-item-templates.md) e [parâmetros de modelo](../ide/template-parameters.md).  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir ilustra os metadados para o modelo de item padrão para um [!INCLUDE[csprcs](../includes/csprcs-md.md)] classe.  
  
```  
<VSTemplate Type="Item" Version="3.0.0"  
    xmlns="http://schemas.microsoft.com/developer/vstemplate/2005">  
    <TemplateData>  
        <Name>MyClass</Name>  
        <Description>My custom C# class.</Description>  
        <Icon>Icon.ico</Icon>  
        <ProjectType>CSharp</ProjectType>  
        <DefaultName>MyClass.cs</DefaultName>  
    </TemplateData>  
    <TemplateContent>  
        <ProjectItem ReplaceParameters="true">MyClass.cs</ProjectItem>  
    </TemplateContent>  
</VSTemplate>  
```  
  
## <a name="see-also"></a>Consulte também  
 [Referência de esquema de modelo do Visual Studio](../extensibility/visual-studio-template-schema-reference.md)   
 [Criando modelos de projeto e de item](../ide/creating-project-and-item-templates.md)   
 [Como: Criar modelos de Item multiarquivos](../ide/how-to-create-multi-file-item-templates.md)   
 [Parâmetros de modelo](../ide/template-parameters.md)
