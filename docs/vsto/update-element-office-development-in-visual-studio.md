---
title: '&lt;&gt;elemento Update (desenvolvimento do Office no Visual Studio)'
description: O elemento Update especifica o intervalo no qual a solução verificará se há atualizações.
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
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 59e7b21902c486bd78548cd79f2e79a5056042a5
ms.sourcegitcommit: 8590cf6b3351e82827fd21159beefef0c02bf162
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/08/2021
ms.locfileid: "102468500"
---
# <a name="ltupdategt-element-office-development-in-visual-studio"></a>&lt;&gt;elemento Update (desenvolvimento do Office no Visual Studio)
  O `update` elemento Especifica o intervalo no qual a solução verificará se há atualizações.

## <a name="syntax"></a>Syntax

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
