---
title: 'CA1301: Evitar aceleradores duplicados | Microsoft Docs'
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
- CA1301
- AvoidDuplicateAccelerators
helpviewer_keywords:
- CA1301
- AvoidDuplicateAccelerators
ms.assetid: 20570a00-864b-459c-a1fa-a6e9db5f1001
caps.latest.revision: 19
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: 92c5baefff76626a42553d6ba5380fd07448b109
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49886630"
---
# <a name="ca1301-avoid-duplicate-accelerators"></a>CA1301: evitar aceleradores duplicados
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|NomeDoTipo|AvoidDuplicateAccelerators|
|CheckId|CA1301|
|Categoria|Microsoft.Globalization|
|Alteração Significativa|Não são significativas|

## <a name="cause"></a>Causa
 Estende um tipo <xref:System.Windows.Forms.Control?displayProperty=fullName> e contém duas ou mais controles de nível superior que têm chaves de acesso idêntico que são armazenadas em um arquivo de recurso.

## <a name="rule-description"></a>Descrição da Regra
 Uma tecla de acesso, também conhecida como acelerador, dá ao teclado acesso a um controle usando-se a tecla ALT. Quando vários controles têm teclas de acesso duplicadas, o comportamento da tecla de acesso não é bem definido. O usuário pode não ser capaz de acessar o controle desejado usando a chave de acesso e um controle diferente daquele que destina-se deve estar habilitado.

 A implementação atual desta regra ignora os itens de menu. No entanto, os itens de menu no mesmo submenu não devem ter as chaves de acesso idênticos.

## <a name="how-to-fix-violations"></a>Como Corrigir Violações
 Para corrigir uma violação dessa regra, defina chaves de acesso exclusivo para todos os controles.

## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos
 Não suprima um aviso nessa regra.

## <a name="example"></a>Exemplo
 O exemplo a seguir mostra um formulário mínimo que contém dois controles que têm chaves de acesso idênticos. As chaves são armazenadas em um arquivo de recurso, que não é exibido; No entanto, seus valores aparecerão no comentado out `checkBox.Text` linhas. O comportamento de aceleradores duplicados pode ser examinado por meio da troca de `checkBox.Text` linhas com suas contrapartes comentadas. No entanto, nesse caso, o exemplo não irá gerar um aviso da regra.

 [!code-csharp[FxCop.Globalization.AvoidDuplicateAccels#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Globalization.AvoidDuplicateAccels/cs/FxCop.Globalization.AvoidDuplicateAccels.cs#1)]

## <a name="see-also"></a>Consulte também
 <xref:System.Resources.ResourceManager?displayProperty=fullName> [Recursos em aplicativos da área de trabalho](http://msdn.microsoft.com/library/8ad495d4-2941-40cf-bf64-e82e85825890)



