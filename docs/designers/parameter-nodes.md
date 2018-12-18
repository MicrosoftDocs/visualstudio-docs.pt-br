---
title: Nós de parâmetro
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-ide-designers
ms.topic: reference
ms.assetid: da54db0b-3a3d-48dc-858c-7ac43aa04b13
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 52e7002deeba9d2d61eb860b2f5814375f2a18e6
ms.sourcegitcommit: e5a382de633156b85b292f35e3d740f817715d47
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/12/2018
ms.locfileid: "38977694"
---
# <a name="parameter-nodes"></a>Nós de parâmetro

No Designer de Sombreador, os nós de parâmetro representam entradas no sombreador que estão sob o controle do aplicativo em uma base por draw, por exemplo, propriedades de material, luzes direcionais, posição da câmera e tempo. Como você pode alterar esses parâmetros a cada chamada draw, é possível usar o mesmo sombreador para conceder aparências diferentes a um objeto.

## <a name="parameter-node-reference"></a>Referência do nó de parâmetro

|Nó|Detalhes|Propriedades|
|----------|-------------|----------------|
|**Posição mundial da câmera**|A posição da câmera no espaço de mundo.<br /><br /> **Saída:**<br /><br /> `Output`: `float4`<br /> A posição da câmera.|Nenhum|
|**Direção da Luz**|O vetor que define a direção na qual a luz é emitida de uma fonte de luz no espaço do mundo.<br /><br /> Você pode usar isso para calcular as contribuições de iluminação e especulares no espaço do mundo.<br /><br /> **Saída:**<br /><br /> `Output`: `float3`<br /> O vetor do pixel atual para uma fonte de luz.|Nenhum|
|**Material Ambiente**|A contribuição de cor difusa do pixel atual que é atribuída à iluminação indireta.<br /><br /> A cor de um pixel difusa simula como a iluminação interage com superfícies ásperas. Você pode usar o parâmetro Material Ambiente para calcular aproximadamente como a iluminação indireta contribui para a aparência de um objeto no mundo real.<br /><br /> **Saída:**<br /><br /> `Output`: `float4`<br /> A cor difusa do pixel atual é devido à luz indireta, ou seja, ambiente.|**Access**<br /> **Public** para permitir que esta propriedade possa ser configurada pelo Editor de Modelo; caso contrário, **Private**.<br /><br /> **Value**<br /> A cor difusa do pixel atual é devido à luz indireta, ou seja, ambiente.|
|**Material Difuso**|Uma cor que descreve como o pixel atual difunde a iluminação direta.<br /><br /> A cor de um pixel difusa simula como a iluminação interage com superfícies ásperas. Você pode usar o parâmetro Material Difuso para alterar como o pixel atual difunde a iluminação direta, ou seja, bidirecional, ponto e spot lights.<br /><br /> **Saída:**<br /><br /> `Output`: `float4`<br /> Uma cor que descreve como o pixel atual difunde a iluminação direta.|**Access**<br /> **Public** para permitir que esta propriedade possa ser configurada pelo Editor de Modelo; caso contrário, **Private**.<br /><br /> **Value**<br /> Uma cor que descreve como o pixel atual difunde a iluminação direta.|
|**Material Emissivo**|A contribuição da cor difusa do pixel atual que é atribuída à iluminação fornecido a si mesmo.<br /><br /> Você pode usar isso para simular um objeto brilhante, isto é, um objeto que fornece sua própria luz. Essa luz não afeta os outros objetos.<br /><br /> **Saída:**<br /><br /> `Output`: `float4`<br /> A contribuição de cor do pixel atual é devido à iluminação própria.|**Access**<br /> **Public** para permitir que esta propriedade possa ser configurada pelo Editor de Modelo; caso contrário, **Private**.<br /><br /> **Value**<br /> A contribuição de cor do pixel atual é devido à iluminação própria.|
|**Material Especular**|Uma cor que descreve como o pixel atual reflete a iluminação direta.<br /><br /> A cor especular de um pixel simula como a iluminação interage com superfícies lisas e espelhadas. Você pode usar o parâmetro Material Especular para alterar como o pixel atual reflete a iluminação direta, ou seja, direcional, ponto e spot lights.<br /><br /> **Saída:**<br /><br /> `Output`: `float4`<br /> Uma cor que descreve como o pixel atual reflete a iluminação direta.|**Access**<br /> **Public** para permitir que esta propriedade possa ser configurada pelo Editor de Modelo; caso contrário, **Private**.<br /><br /> **Value**<br /> Uma cor que descreve como o pixel atual reflete a iluminação direta.|
|**Material Energia Especular**|Um valor escalar que descreve a intensidade dos realces especulares.<br /><br /> Quanto maior a energia especular, mais intensa e abrangente se tornam os realces especulares.<br /><br /> **Saída:**<br /><br /> `Output`: `float`<br /> O termo exponencial que define a intensidade dos realces especulares no do pixel atual.|**Access**<br /> **Public** para permitir que esta propriedade possa ser configurada pelo Editor de Modelo; caso contrário, **Private**.<br /><br /> **Value**<br /> O expoente que define a intensidade dos realces especulares no pixel atual.|
|**Tempo Normalizado**|O tempo, em segundos, normalizado no intervalo [0, 1], de modo que quando tempo atinge 1, ele é redefinido como 0.<br /><br /> Você pode usar isso como um parâmetro em cálculos de sombreamento, por exemplo, para animar coordenadas de textura, valores de cor ou outros atributos.<br /><br /> **Saída:**<br /><br /> `Output`: `float`<br /> O tempo normalizado, em segundos.|Nenhum|
|**Time**|O tempo em segundos.<br /><br /> Você pode usar isso como um parâmetro em cálculos de sombreamento, por exemplo, para animar coordenadas de textura, valores de cor ou outros atributos.<br /><br /> **Saída:**<br /><br /> `Output`: `float`<br /> O tempo em segundos.|Nenhum|