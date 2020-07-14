---
title: 'CA1821: remover finalizadores vazios | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- RemoveEmptyFinalizers
- CA1821
helpviewer_keywords:
- CA1821
ms.assetid: 3f4855a0-e4a0-46e6-923c-4c3b7074048d
caps.latest.revision: 15
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: a2e704202773447e353f041df66b05cb5f648c00
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85545347"
---
# <a name="ca1821-remove-empty-finalizers"></a>CA1821: Remover finalizadores vazios
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|Valor|
|-|-|
|TypeName|RemoveEmptyFinalizers|
|CheckId|CA1821|
|Categoria|Microsoft. performance|
|Alteração Significativa|Sem interrupção|

## <a name="cause"></a>Causa
 Um tipo implementa um finalizador que está vazio, chama apenas o finalizador de tipo base ou chama apenas métodos emitidos condicionalmente.

## <a name="rule-description"></a>Descrição da Regra
 Sempre que possível, evite finalizadores por conta da sobrecarga adicional no desempenho envolvida no acompanhamento do tempo de vida do objeto. O coletor de lixo executará o finalizador antes de coletar o objeto. Isso significa que duas coleções serão necessárias para coletar o objeto. Um finalizador vazio incorre nessa sobrecarga adicional sem nenhum benefício.

## <a name="how-to-fix-violations"></a>Como Corrigir Violações
 Remova o finalizador vazio. Se um finalizador for necessário para a depuração, coloque todo o finalizador em `#if DEBUG / #endif` diretivas.

## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos
 Não suprimir uma mensagem dessa regra. Falha ao suprimir a finalização diminui o desempenho e não fornece nenhum benefício.

## <a name="example"></a>Exemplo
 O exemplo a seguir mostra um finalizador vazio que deve ser removido, um finalizador que deve ser colocado entre `#if DEBUG / #endif` diretivas e um finalizador que usa as `#if DEBUG / #endif` diretivas corretamente.

 [!code-csharp[FxCop.Performance.RemoveEmptyFinalizers#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Performance.RemoveEmptyFinalizers/cs/FxCop.Performance.RemoveEmptyFinalizers.cs#1)]
