---
title: Elemento AppliesTo (modelos do Visual Studio) | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-general
ms.topic: conceptual
ms.assetid: 8fb1334b-d78c-405f-98b4-786e9f6b58d7
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 6f399e0b054b5f9b112733399d644e1357837049
ms.sourcegitcommit: 1ab675a872848c81a44d6b4bd3a49958fe673c56
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/10/2018
ms.locfileid: "44280709"
---
# <a name="appliesto-element-visual-studio-templates"></a>Elemento AppliesTo (modelos do Visual Studio)
Especifica uma expressão opcional para correspondência de um ou mais recursos. (Consulte <xref:Microsoft.VisualStudio.Shell.Interop.VsProjectCapabilityExpressionMatcher>.) Os recursos são expostos pelos tipos de projeto por meio da hierarquia como uma propriedade <xref:Microsoft.VisualStudio.Shell.Interop.__VSHPROPID5>. Dessa maneira, o modelo pode ser compartilhado por vários tipos de projeto que têm recursos aplicáveis comuns.  
  
 Esse elemento é opcional. Pode haver um máximo de uma instância em um arquivo de modelo. Esse elemento permite que apenas um modelo de item seja aceito como aplicável, com base nos recursos do projeto ativo atualmente selecionado. Ele não pode ser usado para tornar um modelo de item não aplicável. Se `AppliesTo` estiver ausente ou a expressão não for aceita com sucesso, `TemplateID` ou `TemplateGroupID` serão usados para tornar o modelo aplicável, como nas versões anteriores do produto.  
  
 Introduzido no Visual Studio 2013 Atualização 2. Para fazer referência a versão correta, consulte [referenciar assemblies entregues no Visual Studio 2013 SDK Update 2](https://msdn.microsoft.com/library/42b65c3e-e42b-4c39-98c8-bea285f25ffb).  
  
 \<VSTemplate >  
 \<TemplateData >  
 \<AppliesTo >  
  
## <a name="syntax"></a>Sintaxe  
  
```  
<AppliesTo>Capability1</AppliesTo>   
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
|[TemplateData](../extensibility/templatedata-element-visual-studio-templates.md)|Categoriza o modelo.|  
  
## <a name="text-value"></a>Valor de texto  
 Um valor de texto é obrigatório. Esse texto especifica os recursos do projeto.  
  
 A sintaxe da expressão válida é definida como:  
  
-   A expressão de recurso, como "(VisualC &#124; CSharp) + (MSTest &#124; NUnit)".  
  
-   O "&#124;" é o operador OR.  
  
-   Os caracteres "&" e "+" são operadores AND.  
  
-   O caractere "!" é o operador NOT.  
  
-   Parênteses forçam a ordem de precedência de avaliação.  
  
-   Uma expressão nula ou vazia é avaliada como uma correspondência.  
  
-   Recursos de projeto podem ser qualquer caractere, exceto os caracteres reservados: "' :;,+-*/\\! ~&#124;& %$@^() ={}<> []? \t\b\n\r  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir mostra três modelos diferentes. `Template1` aplica-se a todos os tipos de projeto do C# ou a qualquer outro tipo de projeto que ofereça suporte ao recurso `WindowsAppContainer`. `Template2` aplica-se a todos os projetos do C# de qualquer tipo. `Template3` aplica-se aos projetos do C# que não são projetos `WindowsAppContainer`.  
  
```xml  
<!--  Template 1 -->  
<?xml version="1.0" encoding="utf-8"?>  
<VSTemplate Version="3.0.0" Type="Item" xmlns="http://schemas.microsoft.com/developer/vstemplate/2005" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://schemas.microsoft.com/developer/vstemplate/2005">  
    <TemplateData>  
        <AppliesTo>CSharp | WindowsAppContainer</AppliesTo>   
    </TemplateData>  
</VSTemplate>  
  
<!--  Template 2 -->  
<?xml version="1.0" encoding="utf-8"?>  
<VSTemplate Version="3.0.0" Type="Item" xmlns="http://schemas.microsoft.com/developer/vstemplate/2005" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://schemas.microsoft.com/developer/vstemplate/2005">  
    <TemplateData>  
        <AppliesTo>CSharp</AppliesTo>   
    </TemplateData>  
</VSTemplate>  
  
<!--  Template 1 -->  
<?xml version="1.0" encoding="utf-8"?>  
<VSTemplate Version="3.0.0" Type="Item" xmlns="http://schemas.microsoft.com/developer/vstemplate/2005" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://schemas.microsoft.com/developer/vstemplate/2005">  
    <TemplateData>  
        <AppliesTo>CSharp_Class + (!WindowsAppContainer)</AppliesTo>   
    </TemplateData>  
</VSTemplate>  
  
```  
  
## <a name="see-also"></a>Consulte também  
 [Referência de esquema de modelo do Visual Studio](../extensibility/visual-studio-template-schema-reference.md)   
 [Criar modelos de projeto e de item](../ide/creating-project-and-item-templates.md)