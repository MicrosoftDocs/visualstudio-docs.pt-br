---
title: Elemento ProvideDefaultName (modelos do Visual Studio) | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-general
ms.topic: conceptual
f1_keywords:
- http://schemas.microsoft.com/developer/vstemplate/2005#ProvideDefaultName
helpviewer_keywords:
- ProvideDefaultName element [Visual Studio project templates]
ms.assetid: 7b0e7b20-fd6b-42e2-81d0-e5100cea0528
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: a187df0e50a2948ab6f1ef3a0fffea651dca23b9
ms.sourcegitcommit: 06db1892fff22572f0b0a11994dc547c2b7e2a48
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/08/2018
ms.locfileid: "39636006"
---
# <a name="providedefaultname-element-visual-studio-templates"></a>Elemento ProvideDefaultName (modelos do Visual Studio)
Especifica se o [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] sistema de projeto irá gerar um nome padrão para o modelo a **Adicionar Novo Item** ou **novo projeto** caixa de diálogo.  
  
 \<VSTemplate >  
 \<TemplateData >  
 \<ProvideDefaultName >  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
<ProvideDefaultName> true/false </ProvideDefaultName>  
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
  
 O texto deve ser `true` ou `false`, que indica se deve ou não gerar um nome padrão para o modelo na **Adicionar Novo Item** ou **novo projeto** caixa de diálogo.  
  
## <a name="remarks"></a>Comentários  
 `ProvideDefaultName` é um elemento opcional. O valor padrão é `true`.  
  
 Se o `ProvideDefaultName` elemento é `false`, o **nome** caixas dos **Add New Item** e **novo projeto** caixas de diálogo contêm o valor `<Enter_name>`.  
  
 Use o [DefaultName](../extensibility/defaultname-element-visual-studio-templates.md) elemento para especificar o nome padrão do projeto ou item a **Adicionar Novo Item** e **novo projeto** caixas de diálogo. Quando o valor da `ProvideDefaultName` elemento é `true`, omissão do `DefaultName` elemento para projetos preenche a caixa de diálogo com o nome do modelo, ou seja, o valor da [nome](../extensibility/name-element-visual-studio-templates.md) elemento.
  
## <a name="example"></a>Exemplo  
 O seguinte exemplo de código define a `ProvideDefaultName` elemento para `false`.  
  
```  
<VSTemplate Type="Item" Version="3.0.0"  
    xmlns="http://schemas.microsoft.com/developer/vstemplate/2005">  
    <TemplateData>  
        <Name>MyClass</Name>  
        <Description>My custom C# class.</Description>  
        <Icon>Icon.ico</Icon>  
        <ProjectType>CSharp</ProjectType>  
        <ProvideDefaultName>false</ProvideDefaultName>  
    </TemplateData>  
    <TemplateContent>  
        <ProjectItem>MyClass.cs</ProjectItem>  
    </TemplateContent>  
</VSTemplate>  
```  
  
## <a name="see-also"></a>Consulte também  
 [Referência de esquema de modelo do Visual Studio](../extensibility/visual-studio-template-schema-reference.md)   
 [Criar modelos de projeto e de item](../ide/creating-project-and-item-templates.md)
