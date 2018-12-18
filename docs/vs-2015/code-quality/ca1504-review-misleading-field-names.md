---
title: 'CA1504: Revisar nomes de campo | Microsoft Docs'
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
- ReviewMisleadingFieldNames
- CA1504
helpviewer_keywords:
- CA1504
- ReviewMisleadingFieldNames
ms.assetid: 94136ff1-4aaf-4dc2-9170-48c171ab7499
caps.latest.revision: 17
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: c927457e2e16f19c221204ba445dad6c127da850
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49878375"
---
# <a name="ca1504-review-misleading-field-names"></a>CA1504: revisar nomes de campo confusos
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|NomeDoTipo|ReviewMisleadingFieldNames|
|CheckId|CA1504|
|Categoria|Microsoft.Maintainability|
|Alteração Significativa|Não são significativas|

## <a name="cause"></a>Causa
 O nome de um campo de instância começa com "s _" ou o nome de um `static` (`Shared` em [!INCLUDE[vbprvb](../includes/vbprvb-md.md)]) campo começa com "m _".

## <a name="rule-description"></a>Descrição da Regra
 Nomes de campo que começam com "s _" são associados a dados estáticos por muitos usuários. Da mesma forma, os nomes de campo que começam com "m _" são associados a dados da instância (membro). Para o código mais fácil manutenção, os nomes devem seguir convenções geralmente usadas.

## <a name="how-to-fix-violations"></a>Como Corrigir Violações
 Para corrigir uma violação dessa regra, renomeie o campo usando o prefixo apropriado. Como alternativa, tornar o campo concordar com o sufixo atual, adicionando ou removendo o `static` modificador.

## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos
 Não suprima um aviso nessa regra.



