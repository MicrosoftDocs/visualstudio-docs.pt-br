---
title: Elemento MaxFrameworkVersion (modelos do Visual Studio) | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-general
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- <MaxFrameworkVersion> Element (Visual Studio Templates)
- MaxFrameworkVersion Element (Visual Studio Templates)
ms.assetid: f732a9d3-fc29-405b-9298-01ea83fc58b8
caps.latest.revision: 10
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: c5201d42bddb02eade61546ee61ae99283347082
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51778170"
---
# <a name="maxframeworkversion-element-visual-studio-templates"></a>Elemento MaxFrameworkVersion (modelos do Visual Studio)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Especifica a versão máxima do .NET Framework que é necessário para o modelo. Determina se o modelo é exibido na **modelos** seção o **adicionar novo projeto** com base no valor selecionado na caixa de diálogo, o **versão do Framework de destino** caixa do **adicionar novo projeto** caixa de diálogo.  
  
 \<VSTemplate >  
 \<MaxFrameworkVersion >  
  
## <a name="syntax"></a>Sintaxe  
  
```  
<MaxFrameworkVersion> ... </MaxFrameworkVersion>  
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
  
 O texto deve ser o maior número de versão do .NET Framework que é permitido pelo modelo.  
  
## <a name="remarks"></a>Comentários  
 `MaxFrameworkVersion` é um elemento opcional. O elemento na `TemplateData` seção do arquivo. vstemplate atua como um filtro para o **modelos** seção os **adicionar novo projeto** caixa de diálogo. Somente os modelos cujos requisitos de .NET Framework são menor que `MaxFrameworkVersion` valores de elemento serão exibidos, com base no valor selecionado na **versão do Framework de destino** caixa do **adicionar novo projeto**caixa de diálogo. O `MaxFrameworkVersion` elemento deve ser omitido, a menos que ele for necessário, portanto, não para inadvertidamente, causar modelos seja exibida quando eles são usados com as versões mais recentes do .NET Framework.  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir ilustra os metadados para um padrão [!INCLUDE[csprcs](../includes/csprcs-md.md)] modelo de classe.  
  
```  
<VSTemplate Type="Item" Version="3.0.0"  
    xmlns="http://schemas.microsoft.com/developer/vstemplate/2005">  
    <TemplateData>  
        <Name>MyClass</Name>  
        <Description>My custom C# class template.</Description>  
        <Icon>Icon.ico</Icon>  
        <ProjectType>CSharp</ProjectType>  
        <MaxFrameworkVersion>3.5</MaxFrameworkVersion>  
        <DefaultName>MyClass</DefaultName>  
    </TemplateData>  
    <TemplateContent>  
        <ProjectItem>MyClass.cs</ProjectItem>  
    </TemplateContent>  
</VSTemplate>  
```  
  
 Neste exemplo, a versão máxima do .NET Framework que é exigido pelo modelo, representado por `MaxFrameworkVersion`, é a 3.5. O modelo acima será exibido somente quando você seleciona 3.0 ou 3.5 na **versão do Framework de destino** caixa de **adicionar novo projeto** caixa de diálogo.  
  
## <a name="see-also"></a>Consulte também  
 [Referência de esquema de modelo do Visual Studio](../extensibility/visual-studio-template-schema-reference.md)   
 [Criando modelos de projeto e de item](../ide/creating-project-and-item-templates.md)

