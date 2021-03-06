---
description: O elemento formRegion do namespace vstov4 identifica uma Microsoft Office região de formulário do Outlook que está associada a um suplemento do VSTO.
title: '&lt;&gt;elemento FormRegion (desenvolvimento do Office no Visual Studio)'
titleSuffix: ''
ms.custom: seodec18
ms.date: 02/02/2017
ms.topic: reference
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- application manifests [Office development in Visual Studio], <formRegion> element
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 0851ba9e117b464d3a2fbb9ad9903af17ceda0c4
ms.sourcegitcommit: f33ca1fc99f5d9372166431cefd0e0e639d20719
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102221074"
---
# <a name="ltformregiongt-element-office-development-in-visual-studio"></a>&lt;&gt;elemento FormRegion (desenvolvimento do Office no Visual Studio)
  O `formRegion` elemento do `vstov4` namespace identifica uma região de formulário Microsoft Office do Outlook que está associada a um suplemento do VSTO.

## <a name="syntax"></a>Sintaxe

```xml
<formRegion
  name>
  <messageClass
    name/>
</formRegion>
```

## <a name="elements-and-attributes"></a>Elementos e atributos
 O `formRegion` elemento do `vstov4` namespace identifica uma região de formulário que está associada a um suplemento do VSTO do Outlook. Ele é necessário apenas para suplementos do VSTO do Outlook que incluem regiões de formulário.

 Pode haver vários `formRegion` elementos definidos dentro de um `formRegions` elemento para um único suplemento do VSTO.

 O `formRegion` elemento tem o atributo a seguir.

|Atributo|Descrição|
|---------------|-----------------|
|`name`|Obrigatórios. Identifica o nome da região do formulário.|

 O `formRegion` elemento tem os seguintes elementos filho.

### <a name="messageclass"></a>Class
 O `messageClass` elemento identifica o formulário do Outlook que está associado à região do formulário.

 O `messageClass` elemento tem o atributo a seguir.

|Atributo|Descrição|
|---------------|-----------------|
|`name`|Obrigatórios. Identifica o formulário associado à região do formulário.|

## <a name="example"></a>Exemplo
 O exemplo de código a seguir ilustra um `formRegion` elemento em um manifesto de aplicativo para um suplemento do VSTO do Outlook implantado usando o [!INCLUDE[ndptecclick](../vsto/includes/ndptecclick-md.md)] . Há três classes de mensagem associadas a esta região de formulário. Este exemplo de código faz parte de um exemplo maior fornecido em [manifestos do aplicativo para soluções do Office](../vsto/application-manifests-for-office-solutions.md).

```xml
<vstov4:formRegion
    name="OutlookAddIn1.FormRegion1">
  <vstov4:messageClass name="IPM.Note" />
  <vstov4:messageClass name="IPM.Contact" />
  <vstov4:messageClass name="IPM.Appointment" />
</vstov4:formRegion>
```

## <a name="see-also"></a>Confira também

- [Criar regiões de formulário do Outlook](../vsto/creating-outlook-form-regions.md)
- [Manifestos do aplicativo para soluções do Office](../vsto/application-manifests-for-office-solutions.md)
- [Manifestos de implantação para soluções do Office](../vsto/deployment-manifests-for-office-solutions.md)
- [Manifesto do aplicativo ClickOnce](../deployment/clickonce-application-manifest.md)
