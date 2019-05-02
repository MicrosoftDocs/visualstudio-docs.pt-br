---
title: '&lt;atualizar&gt; elemento (desenvolvimento do Office no Visual Studio)'
ms.date: 02/02/2017
ms.topic: conceptual
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
ms.openlocfilehash: 461fae79e3af346d64017166b6dae3ace67599e1
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62967527"
---
# <a name="ltupdategt-element-office-development-in-visual-studio"></a>&lt;atualizar&gt; elemento (desenvolvimento do Office no Visual Studio)
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
 O `update` elemento é necessário e está no `vstav3` namespace.

 O `update` elemento tem os seguintes atributos.

|Atributo|Descrição|
|---------------|-----------------|
|`enabled`|Necessário. Defina habilitado para um dos seguintes valores:<br /><br /> -   **True** para verificar se há atualizações.<br />-   **False** para evitar a verificação de atualizações.|

 O `update` elemento tem os seguintes elementos filho.

### <a name="expiration"></a>expiração
 O `expiration` elemento é necessário e está no `vstav3` namespace. Esse elemento Especifica o intervalo em que a solução verifica atualizações.

 O `expiration` elemento tem os seguintes atributos.

|Atributo|Descrição|
|---------------|-----------------|
|`maximumAge`| Necessário. Defina isso igual a um número inteiro.|
|`unit`|Necessário. Definir `unit` para um dos seguintes valores:<br /><br /> -   **Horas**<br />-   **Dias**<br />-   **semanas**|

## <a name="example-of-always-checking-for-updates"></a>Exemplo de sempre verificar se há atualizações

### <a name="description"></a>Descrição
 O exemplo de código a seguir ilustra um `update` elemento que está definido para sempre verificar se há atualizações em soluções do Office.

### <a name="code"></a>Código

```xml
<vstav3:update enabled="true" />
```

## <a name="example-of-setting-a-default-update-interval"></a>Exemplo de como definir um intervalo de atualização padrão

### <a name="description"></a>Descrição
 O exemplo de código a seguir ilustra um `update` elemento em um manifesto de aplicativo para soluções do Office. Este exemplo de código é parte de um exemplo maior fornecido no [manifestos de aplicativo para soluções do Office](../vsto/application-manifests-for-office-solutions.md).

### <a name="code"></a>Código

```xml
<vstav3:update enabled="true">
    <vstav3:expiration maximumAge="7" unit="days" />
</vstav3:update>
```

## <a name="see-also"></a>Consulte também

- [Implantar uma solução do Office usando o ClickOnce](../vsto/deploying-an-office-solution-by-using-clickonce.md)
- [Manifestos de aplicativo para soluções do Office](../vsto/application-manifests-for-office-solutions.md)
- [Manifestos de implantação para soluções do Office](../vsto/deployment-manifests-for-office-solutions.md)
- [Manifesto do aplicativo ClickOnce](../deployment/clickonce-application-manifest.md)
