---
title: Elemento RequiredFrameworkVersion (modelos do Visual Studio) | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: reference
helpviewer_keywords:
- <RequiredFrameworkVersion> (Visual Studio Templates)
- RequiredFrameworkVersion (Visual Studio Templates)
ms.assetid: 08a4f609-51a5-4723-b89f-99277fb18871
caps.latest.revision: 11
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: ce312d7951f4c1be720604c006f9afcd63f364d3
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "68163658"
---
# <a name="requiredframeworkversion-element-visual-studio-templates"></a>Elemento RequiredFrameworkVersion (modelos do Visual Studio)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Especifica a versão mínima do .NET Framework que é exigida pelo modelo. Hierarquia de esquema.  
  
 \<VSTemplate >  
 \<TemplateData >  
 \<RequiredFrameworkVersion>  
  
## <a name="syntax"></a>Sintaxe  
  
```  
<RequiredFrameworkVersion> .... </RequiredFrameworkVersion>  
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
|[TemplateData](../extensibility/templatedata-element-visual-studio-templates.md)|Elemento obrigatório.<br /><br /> Categoriza o modelo e a define como ele é exibido em qualquer um de **novo projeto** ou o **Adicionar Novo Item** caixa de diálogo.|  
  
## <a name="text-value"></a>Valor de texto  
 Um valor de texto é obrigatório.  
  
 O texto deve ser o número de versão mínima do .NET Framework que é necessário para o modelo.  
  
## <a name="remarks"></a>Comentários  
 `RequiredFrameworkVersion` é um elemento opcional. Use esse elemento se o modelo só dá suporte a uma versão específica de mínimo e versões posteriores, se houver, do .NET Framework.  
  
## <a name="see-also"></a>Consulte também  
 [Referência de esquema de modelo do Visual Studio](../extensibility/visual-studio-template-schema-reference.md)   
 [Criando modelos de projeto e de item](../ide/creating-project-and-item-templates.md)   
 [Direcionamento de uma versão específica do .NET Framework](../ide/targeting-a-specific-dotnet-framework-version.md)
