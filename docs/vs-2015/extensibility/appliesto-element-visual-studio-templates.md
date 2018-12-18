---
title: Elemento AppliesTo (modelos do Visual Studio) | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-general
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 8fb1334b-d78c-405f-98b4-786e9f6b58d7
caps.latest.revision: 11
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 6f789a574b7db1c30dceea32e5d2c0d4ef9afb7f
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51788557"
---
# <a name="appliesto-element-visual-studio-templates"></a>Elemento AppliesTo (modelos do Visual Studio)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Especifica uma expressão opcional para correspondência de um ou mais recursos. (Consulte <xref:Microsoft.VisualStudio.Shell.Interop.VsProjectCapabilityExpressionMatcher>.) Os recursos são expostos pelos tipos de projeto por meio da hierarquia como uma propriedade <xref:Microsoft.VisualStudio.Shell.Interop.__VSHPROPID5>. Dessa maneira, o modelo pode ser compartilhado por vários tipos de projeto que têm recursos aplicáveis comuns.  
  
 Esse elemento é opcional. Pode haver um máximo de uma instância em um arquivo de modelo. Esse elemento permite que apenas um modelo de item seja aceito como aplicável, com base nos recursos do projeto ativo atualmente selecionado. Ele não pode ser usado para tornar um modelo de item não aplicável. Se `AppliesTo` estiver ausente ou a expressão não for aceita com sucesso, `TemplateID` ou `TemplateGroupID` serão usados para tornar o modelo aplicável, como nas versões anteriores do produto.  
  
 Introduzido no Visual Studio 2013 Atualização 2. Para fazer referência a versão correta, consulte [Referenciando Assemblies entregues no Visual Studio 2013 SDK Update 2](http://msdn.microsoft.com/en-us/42b65c3e-e42b-4c39-98c8-bea285f25ffb).  
  
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
 [Criando modelos de projeto e de item](../ide/creating-project-and-item-templates.md)

