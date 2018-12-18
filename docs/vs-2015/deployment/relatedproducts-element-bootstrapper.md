---
title: '&lt;RelatedProducts&gt; elemento (Bootstrapper) | Microsoft Docs'
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-deployment
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- MSBuild.GenerateBootstrapper.MissingDependency
- MSBuild.GenerateBootstrapper.DuplicateItems
- MSBuild.GenerateBootstrapper.IncludedProductIncluded
- MSBuild.GenerateBootstrapper.DependencyNotFound
- MSBuild.GenerateBootstrapper.PackageFileNotFound
dev_langs:
- FSharp
- VB
- CSharp
- C++
helpviewer_keywords:
- <RelatedProducts> element [bootstrapper]
ms.assetid: bf152712-4c1e-48bd-9b7f-311cf0fdb832
caps.latest.revision: 14
author: mikejo5000
ms.author: mikejo
manager: wpickett
ms.openlocfilehash: c78aa559bf64b110909134426c676f302ca5fe04
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49296290"
---
# <a name="ltrelatedproductsgt-element-bootstrapper"></a>&lt;RelatedProducts&gt; elemento (Bootstrapper)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

O `RelatedProducts` elemento define outros produtos que dependem de ou que estão incluídos no produto atual.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
<RelatedProducts>  
    <DependsOnProduct  
        Code  
    />  
    <EitherProducts>  
        <DependsOnProduct  
            Code  
        />  
    </EitherProducts>  
    <IncludesProduct  
        Code  
    />  
</RelatedProducts>  
```  
  
## <a name="elements-and-attributes"></a>Elementos e atributos  
 O `RelatedProducts` um filho do elemento é o `Product` elemento. Ele não tem atributos.  
  
## <a name="dependsonproduct"></a>DependsOnProduct  
 O `DependsOnProduct` elemento significa que o produto atual depende do produto e que o produto deve ser instalado antes do atual. Ele é um filho de `RelatedProducts` elemento. Um `RelatedProducts` elemento pode ter um ou mais `DependsOnProduct` elementos.  
  
 `DependsOnProduct` tem o seguinte atributo.  
  
|Atributo|Descrição|  
|---------------|-----------------|  
|`Code`|O nome do código do produto incluído, conforme especificado pelo `ProductCode` atributo do `Product` elemento. Para obter mais informações, consulte [ \<produto > elemento](../deployment/product-element-bootstrapper.md).|  
  
## <a name="eitherproducts"></a>EitherProducts  
 O `EitherProducts` elemento define zero ou mais `DependsOnProduct` elementos, e não tem atributos. Pelo menos um `DependsOnProduct` neste conjunto deve ser instalado antes do produto atual. Um `RelatedProducts` elemento pode ter zero ou mais `EitherProducts` elementos.  
  
## <a name="includesproduct"></a>IncludesProduct  
 O `IncludesProduct` elemento significa que um produto está incluído com a instalação atual e não requer uma instalação separada. Ele é um filho de `RelatedProducts` elemento. Um `RelatedProducts` elemento pode ter um ou mais `IncludesProduct` elementos.  
  
 `IncludesProduct` tem o seguinte atributo.  
  
|Atributo|Descrição|  
|---------------|-----------------|  
|`Code`|O nome do código do produto incluído, conforme especificado pelo `ProductCode` atributo do `Product` elemento. Para obter mais informações, consulte [ \<produto > elemento](../deployment/product-element-bootstrapper.md).|  
  
## <a name="example"></a>Exemplo  
 O exemplo de código a seguir especifica que o Microsoft Installer é instalado com o [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)]e, portanto, não precisará de uma instalação separada.  
  
```  
<RelatedProducts>  
    <IncludesProduct Code="Microsoft.Windows.Installer.2.0" />  
</RelatedProducts>  
```  
  
## <a name="see-also"></a>Consulte também  
 [\<Produto > elemento](../deployment/product-element-bootstrapper.md)



