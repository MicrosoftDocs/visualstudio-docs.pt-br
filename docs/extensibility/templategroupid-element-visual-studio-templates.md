---
title: Elemento TemplateGroupID (modelos do Visual Studio) | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-general
ms.topic: conceptual
f1_keywords:
- http://schemas.microsoft.com/developer/vstemplate/2005#TemplateGroupID
helpviewer_keywords:
- TemplateGroupID element [Visual Studio Templates]
- <TemplateGroupID> element [Visual Studio Templates]
ms.assetid: bce7b49a-90bc-4691-aff3-a87e209f6d83
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 91631975d48f6e7e13646c428cdd5b5473bbeed2
ms.sourcegitcommit: 6a9d5bd75e50947659fd6c837111a6a547884e2a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
ms.locfileid: "31144431"
---
# <a name="templategroupid-element-visual-studio-templates"></a>Elemento TemplateGroupID (modelos do Visual Studio)
Especifica o tipo de projeto um modelos de item aparecerá no. Esse elemento é significativo quando [ShowByDefault (modelos do Visual Studio)](../extensibility/showbydefault-visual-studio-templates.md) é definido como `false`. Quando [ShowByDefault (modelos do Visual Studio)](../extensibility/showbydefault-visual-studio-templates.md) é definido como `true`, em seguida, um modelo de item está disponível em todos os tipos de projeto.  
  
 \<VSTemplate >  
 \<TemplateData >  
 \<TemplateGroupID >  
  
## <a name="syntax"></a>Sintaxe  
  
```  
<TemplateGroupID> ... </TemplateGroupID>  
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
|[TemplateData](../extensibility/templatedata-element-visual-studio-templates.md)|Categoriza o modelo e define como ele exibe em um a **novo projeto** ou **Adicionar Novo Item** caixa de diálogo.|  
  
## <a name="text-value"></a>Valor de texto  
 Um valor de texto é obrigatório.  
  
 O texto Especifica um identificador para uma categoria de modelos de item.  
  
## <a name="remarks"></a>Comentários  
 `TemplateGroupID` é um elemento.  
  
 O valor de `TemplateGroupID` elemento é usado junto com o registro do sistema de projeto (HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\\*\<o número de versão >* \Projects\\) para modelos de filtro que aparecem no **Adicionar Novo Item** caixa de diálogo.  
  
|Valor do Visual C++|Significado|  
|------------------------|-------------|  
|VC nativo|Usado para projetos nativos. Também o padrão se um tipo de projeto não pode ser determinado.|  
|VC gerenciados|Usado para gerenciada (/ clr) projetos|  
|VC-Windows|Usado para todos os projetos para destinar a plataforma do windows (nativo/gerenciado/store)|  
|WinRT-nativo-UAP|Usado para projetos de armazenamento do Windows 10|  
|CodeSharing nativo|Usado para projetos de item compartilhado|  
|6.3 de nativo de WinRT|Usado para projetos de armazenamento do Windows 8.1|  
|WinRT nativo-Phone 6.3|Usado para projetos do Windows Phone 8.1|  
|WinRT nativo|Usado para projetos de armazenamento do Windows 8.0|  
|VC-Android|Usado em projetos Android|  
  
## <a name="see-also"></a>Consulte também  
 [Referência de esquema de modelo do Visual Studio](../extensibility/visual-studio-template-schema-reference.md)   
 [Criando modelos de projeto e de item](../ide/creating-project-and-item-templates.md)