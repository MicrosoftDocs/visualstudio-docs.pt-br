---
title: 'CA2106: Proteger declarações | Microsoft Docs'
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
- CA2106
- SecureAsserts
helpviewer_keywords:
- CA2106
- SecureAsserts
ms.assetid: 91feb36e-6e2c-436c-8272-5aee31f77e98
caps.latest.revision: 21
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: 6ca37a7bdcad290f9ab0c6d54814615731f6678c
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49864721"
---
# <a name="ca2106-secure-asserts"></a>CA2106: declarações seguras
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|NomeDoTipo|SecureAsserts|
|CheckId|CA2106|
|Categoria|Microsoft.Security|
|Alteração Significativa|Quebra|

## <a name="cause"></a>Causa
 Um método declara uma permissão e nenhuma verificação de segurança é realizada no chamador.

## <a name="rule-description"></a>Descrição da Regra
 A declaração de uma permissão de segurança sem realizar verificações de segurança pode deixar uma fraqueza de segurança explorável no código. Uma movimentação de pilha de segurança para quando uma permissão de segurança é declarada. Se você declarar uma permissão sem executar nenhuma verificação no chamador, o chamador pode executar indiretamente código por meio de suas permissões. Declara sem verificações de segurança são permitidos apenas quando tiver certeza de que a declaração não pode ser usada de modo prejudicial. Uma declaração é inofensiva, se o código que você chame é inofensivo, ou os usuários não é possível passar informações arbitrárias para código que você chama.

## <a name="how-to-fix-violations"></a>Como Corrigir Violações
 Para corrigir uma violação dessa regra, adicione uma exigência de segurança para o método ou seu tipo declarativo.

## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos
 Suprima um aviso nessa regra somente após uma análise atenta da segurança.

## <a name="see-also"></a>Consulte também
 <xref:System.Security.CodeAccessPermission.Assert%2A?displayProperty=fullName> [Diretrizes de codificação segura](http://msdn.microsoft.com/library/4f882d94-262b-4494-b0a6-ba9ba1f5f177)



