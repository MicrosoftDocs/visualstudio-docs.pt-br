---
title: 'CA2103: Revisar segurança imperativa | Microsoft Docs'
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-devops-test
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- CA2103
- ReviewImperativeSecurity
helpviewer_keywords:
- CA2103
- ReviewImperativeSecurity
ms.assetid: d24fde71-bdf6-46c0-8965-9a73dc33c1aa
caps.latest.revision: 20
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: dd075c4c6edc84422c6c09846d23ef0049d55002
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49886546"
---
# <a name="ca2103-review-imperative-security"></a>CA2103: revisar segurança obrigatória
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|NomeDoTipo|ReviewImperativeSecurity|
|CheckId|CA2103|
|Categoria|Microsoft.Security|
|Alteração Significativa|Quebra|

## <a name="cause"></a>Causa
 Um método usa segurança obrigatória e pode construir a permissão usando as informações de estado ou os valores de retorno que podem ser alterados desde que a demanda esteja ativa.

## <a name="rule-description"></a>Descrição da Regra
 Segurança imperativa usa objetos gerenciados para especificar as permissões e as ações de segurança durante a execução de código, em comparação comparada a segurança declarativa, que usa atributos para armazenar as permissões e as ações nos metadados. Segurança obrigatória é muito flexível, pois você pode definir o estado de um objeto de permissão e selecione as ações de segurança usando as informações que não estão disponíveis até que o tempo de execução. Junto com que a flexibilidade vem o risco de que as informações de tempo de execução que você usa para determinar que o estado de uma permissão não permanece inalteradas desde que a ação está em vigor.

 Use a segurança declarativa sempre que possível. As solicitações declarativas são mais fáceis de entender.

## <a name="how-to-fix-violations"></a>Como Corrigir Violações
 Examine as demandas de segurança obrigatória para certificar-se de que o estado da permissão não se baseia nas informações que podem ser alterados desde que a permissão está sendo usada.

## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos
 É seguro suprimir um aviso nessa regra, se a permissão não se baseia na alteração de dados. No entanto, é melhor alterar a demanda imperativa para seu equivalente declarativo.

## <a name="see-also"></a>Consulte também
 [Diretrizes de codificação segura](http://msdn.microsoft.com/library/4f882d94-262b-4494-b0a6-ba9ba1f5f177) [dados e modelagem](http://msdn.microsoft.com/library/8c37635d-e2c1-4b64-a258-61d9e87405e6)



