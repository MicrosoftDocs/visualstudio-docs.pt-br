---
title: Elemento SortOrder (modelos do Visual Studio) | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-general
ms.topic: conceptual
f1_keywords:
- http://schemas.microsoft.com/developer/vstemplate/2005#SortOrder
helpviewer_keywords:
- SortOrder element [Visual Studio Templates]
- <SortOrder> element [Visual Studio Templates]
ms.assetid: 151932c1-f08a-4f78-a8d0-bd2f32211a9c
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: b963b6e74b7c24d31ddc611407df22380ff8bb60
ms.sourcegitcommit: 6a9d5bd75e50947659fd6c837111a6a547884e2a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
ms.locfileid: "31140317"
---
# <a name="sortorder-element-visual-studio-templates"></a>Elemento SortOrder (modelos do Visual Studio)
Especifica um valor que é usado para organizar o modelo, entre outros modelos na mesma categoria, como ele aparece no **novo projeto** ou **Adicionar Novo Item** caixa de diálogo.  
  
 \<VSTemplate >  
 \<TemplateData >  
 \<Ordem de classificação >  
  
## <a name="syntax"></a>Sintaxe  
  
```  
<SortOrder> ... </SortOrder>  
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
|[TemplateData](../extensibility/templatedata-element-visual-studio-templates.md)|Elemento obrigatório.<br /><br /> Categoriza o modelo e define como ele exibe em um a **novo projeto** ou **Adicionar Novo Item** caixa de diálogo.|  
  
## <a name="text-value"></a>Valor de texto  
 Um valor de texto é obrigatório.  
  
 Um `integer` que representa o valor de ordem de classificação.  
  
## <a name="remarks"></a>Comentários  
 `SortOrder` é um elemento opcional. O valor padrão é 100 e todos os valores devem ser múltiplos de 10.  
  
 O `SortOrder` elemento é ignorado para modelos criados pelo usuário. Todos os modelos criados pelo usuário são classificados em ordem alfabética.  
  
 Modelos que têm valores de ordem de classificação baixa aparecem em ambos o **novo projeto** ou **Novo Item adicionar** caixa de diálogo antes de modelos que têm valores de ordem de classificação alta.  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir ilustra os metadados para um padrão [!INCLUDE[csprcs](../data-tools/includes/csprcs_md.md)] modelo de classe.  
  
```  
<VSTemplate Type="Item" Version="3.0.0"  
    xmlns="http://schemas.microsoft.com/developer/vstemplate/2005">  
    <TemplateData>  
        <Name>MyClass</Name>  
        <Description>My custom C# class template.</Description>  
        <Icon>Icon.ico</Icon>  
        <ProjectType>CSharp</ProjectType>  
        <SortOrder>290</SortOrder>  
        <DefaultName>MyClass</DefaultName>  
    </TemplateData>  
    <TemplateContent>  
        <ProjectItem>MyClass.cs</ProjectItem>  
    </TemplateContent>  
</VSTemplate>  
```  
  
 Neste exemplo, o `SortOrder` elemento é relativamente alto. É provável que outros [!INCLUDE[csprcs](../data-tools/includes/csprcs_md.md)] modelos de item terá um `SortOrder` valor menor do que `290` e aparecerá antes desse modelo no **Novo Item** caixa de diálogo.  
  
## <a name="see-also"></a>Consulte também  
 [Referência de esquema de modelo do Visual Studio](../extensibility/visual-studio-template-schema-reference.md)   
 [Criando modelos de projeto e de item](../ide/creating-project-and-item-templates.md)