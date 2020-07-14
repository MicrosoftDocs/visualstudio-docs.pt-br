---
title: 'CA1301: evitar aceleradores duplicados | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA1301
- AvoidDuplicateAccelerators
helpviewer_keywords:
- CA1301
- AvoidDuplicateAccelerators
ms.assetid: 20570a00-864b-459c-a1fa-a6e9db5f1001
caps.latest.revision: 19
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 772c9bee3f43c42701bfa460c622f4a225ec59cb
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85539172"
---
# <a name="ca1301-avoid-duplicate-accelerators"></a>CA1301: Evitar aceleradores duplicados
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|Valor|
|-|-|
|TypeName|AvoidDuplicateAccelerators|
|CheckId|CA1301|
|Categoria|Microsoft. Globalization|
|Alteração Significativa|Sem interrupção|

## <a name="cause"></a>Causa
 Um tipo estende <xref:System.Windows.Forms.Control?displayProperty=fullName> e contém dois ou mais controles de nível superior que têm chaves de acesso idênticas que são armazenadas em um arquivo de recurso.

## <a name="rule-description"></a>Descrição da Regra
 Uma tecla de acesso, também conhecida como acelerador, dá ao teclado acesso a um controle usando-se a tecla ALT. Quando vários controles têm teclas de acesso duplicadas, o comportamento da tecla de acesso não é bem definido. O usuário pode não ser capaz de acessar o controle pretendido usando a tecla de acesso e um controle diferente daquele que está intencionado pode estar habilitado.

 A implementação atual dessa regra ignora itens de menu. No entanto, os itens de menu no mesmo submenu não devem ter chaves de acesso idênticas.

## <a name="how-to-fix-violations"></a>Como Corrigir Violações
 Para corrigir uma violação dessa regra, defina chaves de acesso exclusivas para todos os controles.

## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos
 Não suprima um aviso nessa regra.

## <a name="example"></a>Exemplo
 O exemplo a seguir mostra uma forma mínima que contém dois controles que têm chaves de acesso idênticas. As chaves são armazenadas em um arquivo de recurso, que não é mostrado; no entanto, seus valores aparecem nas linhas comentadas `checkBox.Text` . O comportamento de aceleradores duplicados pode ser examinado pela troca de `checkBox.Text` linhas com suas contrapartes comentadas. No entanto, nesse caso, o exemplo não gerará um aviso da regra.

 [!code-csharp[FxCop.Globalization.AvoidDuplicateAccels#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Globalization.AvoidDuplicateAccels/cs/FxCop.Globalization.AvoidDuplicateAccels.cs#1)]

## <a name="see-also"></a>Consulte Também
 <xref:System.Resources.ResourceManager?displayProperty=fullName>[Recursos em aplicativos da área de trabalho](https://msdn.microsoft.com/library/8ad495d4-2941-40cf-bf64-e82e85825890)
