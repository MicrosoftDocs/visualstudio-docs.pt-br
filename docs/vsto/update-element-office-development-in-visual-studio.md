---
title: '&lt;&gt;elemento Update (desenvolvimento do Office no Visual Studio)'
ms.date: 02/02/2017
ms.topic: reference
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- update element
- <update> element
- application manifests [Office development in Visual Studio], <update> element
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 241bddb8c79a01bb1ba6921486a4dc46d99940cc
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85537378"
---
# <a name="ltupdategt-element-office-development-in-visual-studio"></a>&lt;&gt;elemento Update (desenvolvimento do Office no Visual Studio)
  O `update` elemento Especifica o intervalo no qual a solução verificará se há atualizações.

## <a name="syntax"></a>Sintaxe

```xml
<update
  enabled>
  <expiration
    maximumAge
    unit
  />
</update>
```

## <a name="elements-and-attributes"></a>Elementos e atributos
 O `update` elemento é obrigatório e está no `vstav3` namespace.

 O `update` elemento tem os atributos a seguir.

|Atributo|Descrição|
|---------------|-----------------|
|`enabled`|Obrigatórios. Defina habilitado como um dos seguintes valores:<br /><br /> -   **true** para verificar se há atualizações.<br />-   **false** para impedir a verificação de atualizações.|

 O `update` elemento tem os seguintes elementos filho.

### <a name="expiration"></a>expiração
 O `expiration` elemento é obrigatório e está no `vstav3` namespace. Esse elemento Especifica o intervalo no qual a solução verifica se há atualizações.

 O `expiration` elemento tem os atributos a seguir.

|Atributo|Descrição|
|---------------|-----------------|
|`maximumAge`| Obrigatórios. Defina isso igual a um inteiro.|
|`unit`|Obrigatórios. Defina `unit` como um dos seguintes valores:<br /><br /> -   **duração**<br />-   **dias**<br />-   **semanas**|

## <a name="example-of-always-checking-for-updates"></a>Exemplo de sempre verificar se há atualizações

### <a name="description"></a>Descrição
 O exemplo de código a seguir ilustra um `update` elemento que é definido para sempre verificar se há atualizações nas soluções do Office.

### <a name="code"></a>Código

```xml
<vstav3:update enabled="true" />
```

## <a name="example-of-setting-a-default-update-interval"></a>Exemplo de configuração de um intervalo de atualização padrão

### <a name="description"></a>Descrição
 O exemplo de código a seguir ilustra um `update` elemento em um manifesto de aplicativo para soluções do Office. Este exemplo de código faz parte de um exemplo maior fornecido em [manifestos do aplicativo para soluções do Office](../vsto/application-manifests-for-office-solutions.md).

### <a name="code"></a>Código

```xml
<vstav3:update enabled="true">
    <vstav3:expiration maximumAge="7" unit="days" />
</vstav3:update>
```

## <a name="see-also"></a>Confira também

- [Implantar uma solução do Office usando o ClickOnce](../vsto/deploying-an-office-solution-by-using-clickonce.md)
- [Manifestos do aplicativo para soluções do Office](../vsto/application-manifests-for-office-solutions.md)
- [Manifestos de implantação para soluções do Office](../vsto/deployment-manifests-for-office-solutions.md)
- [Manifesto do aplicativo ClickOnce](../deployment/clickonce-application-manifest.md)
