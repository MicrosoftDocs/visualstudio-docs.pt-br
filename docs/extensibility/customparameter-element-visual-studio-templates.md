---
title: Elemento CustomParameter (modelos do Visual Studio) | Microsoft Docs
ms.date: 11/04/2016
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/vstemplate/2005#CustomParameter
helpviewer_keywords:
- CustomParameters element [Visual Studio project templates]
ms.assetid: 743c4489-74ac-403a-bbaa-eed7d785a3ac
author: gregvanl
ms.author: gregvanl
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 6cb97e6b4c111689cb94c0df7c04c565e96a39cb
ms.sourcegitcommit: 2193323efc608118e0ce6f6b2ff532f158245d56
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/25/2019
ms.locfileid: "54966758"
---
# <a name="customparameter-element-visual-studio-templates"></a>Elemento CustomParameter (modelos do Visual Studio)
Contém um nome de parâmetro personalizado e o valor a ser usado quando um projeto ou item é criado a partir do modelo.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
<CustomParameter Name="name" Value="value">  
```  
  
## <a name="attributes-and-elements"></a>Atributos e elementos  
 As seções a seguir descrevem atributos, elementos filho e elementos pai.  
  
### <a name="attributes"></a>Atributos  
  
|Atributo|Descrição|  
|---------------|-----------------|  
|`Name`|Necessário. O nome do parâmetro. O formato dos parâmetros é $*nome*$.|  
|`Value`|Necessário. O valor de substituição para o parâmetro.|  
  
### <a name="child-elements"></a>Elementos filho  
 nenhuma.  
  
### <a name="parent-elements"></a>Elementos pai  
  
|Elemento|Descrição|  
|-------------|-----------------|  
|[CustomParameters](../extensibility/customparameters-element-visual-studio-templates.md)|Agrupa os parâmetros personalizados devem ser passados para o Assistente de modelo quando o assistente faz as substituições de parâmetro.|  
  
## <a name="remarks"></a>Comentários  
 Quando um modelo contém `CustomParameter` elementos, cada instância do `Name` atributo é substituído pelo `Value` atributo nos arquivos de projeto ou item criados.  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir mostra como usar vários parâmetros personalizados em um modelo. Quando um projeto ou item é criado de um modelo com os seguintes parâmetros personalizados, todas as instâncias do `$color1$` e `$color2$` no modelo de arquivos serão substituídos pela `Red` e `Blue`, respectivamente.  
  
```  
<CustomParameters>  
    <CustomParameter Name="$color1$" Value="Red"/>  
    <CustomParameter Name="$color2$" Value="Blue "/>  
</CustomParameters>  
```  
  
## <a name="see-also"></a>Consulte também  
 [Elemento CustomParameters (modelos do Visual Studio)](../extensibility/customparameters-element-visual-studio-templates.md)   
 [Parâmetros de modelo](../ide/template-parameters.md)   
 [Referência de esquema de modelo do Visual Studio](../extensibility/visual-studio-template-schema-reference.md)