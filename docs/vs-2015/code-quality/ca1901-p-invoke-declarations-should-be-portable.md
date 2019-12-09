---
title: 'CA1901: as declarações de invocação P devem ser portáveis | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA1901
- PInvokeDeclarationsShouldBePortable
helpviewer_keywords:
- CA1901
- PInvokeDeclarationsShouldBePortable
ms.assetid: 90361812-55ca-47f7-bce9-b8775d3b8803
caps.latest.revision: 25
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: d1b4c0c5bcf22db6558f156fd1acd0be94026b08
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/19/2019
ms.locfileid: "72661057"
---
# <a name="ca1901-pinvoke-declarations-should-be-portable"></a>CA1901: as declarações de P/Invoke devem ser portáteis
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|NomeDoTipo|PInvokeDeclarationsShouldBePortable|
|CheckId|CA1901|
|Categoria|Microsoft. portabilidade|
|Alteração Significativa|Quebrando – se o P/Invoke estiver visível fora do assembly. Não separável – se a P/Invoke não estiver visível fora do assembly.|

## <a name="cause"></a>Causa
 Essa regra avalia o tamanho de cada parâmetro e o valor de retorno de um P/Invoke e verifica se o tamanho deles, quando marshaled para código não gerenciado em plataformas de 32 bits e 64 bits, está correto. A violação mais comum dessa regra é passar um inteiro de tamanho fixo onde uma variável de tamanho de ponteiro dependente de plataforma é necessária.

## <a name="rule-description"></a>Descrição da Regra
 Qualquer um dos seguintes cenários viola essa regra ocorre:

- O valor ou o parâmetro de retorno é digitado como um inteiro de tamanho fixo quando deve ser digitado como um `IntPtr`.

- O valor ou o parâmetro de retorno é digitado como um `IntPtr` quando deve ser digitado como um inteiro de tamanho fixo.

## <a name="how-to-fix-violations"></a>Como Corrigir Violações
 Você pode corrigir essa violação usando `IntPtr` ou `UIntPtr` para representar identificadores em vez de `Int32` ou `UInt32`.

## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos
 Você não deve suprimir este aviso.

## <a name="example"></a>Exemplo
 O exemplo a seguir demonstra uma violação dessa regra.

```csharp
internal class NativeMethods
{
    [DllImport("shell32.dll", CharSet=CharSet.Auto)]
    internal static extern IntPtr ExtractIcon(IntPtr hInst,
        string lpszExeFileName, IntPtr nIconIndex);
}
```

 Neste exemplo, o parâmetro `nIconIndex` é declarado como um `IntPtr`, que tem 4 bytes de largura em uma plataforma de 32 bits e 8 bytes de largura em uma plataforma de 64 bits. Na declaração não gerenciada a seguir, você pode ver que `nIconIndex` é um inteiro sem sinal de 4 bytes em todas as plataformas.

```csharp
HICON ExtractIcon(HINSTANCE hInst, LPCTSTR lpszExeFileName,
    UINT nIconIndex);
```

## <a name="example"></a>Exemplo
 Para corrigir a violação, altere a declaração para o seguinte:

```csharp
internal class NativeMethods{
    [DllImport("shell32.dll", CharSet=CharSet.Auto)]
    internal static extern IntPtr ExtractIcon(IntPtr hInst,
        string lpszExeFileName, uint nIconIndex);
}
```

## <a name="see-also"></a>Consulte também
 [Avisos de portabilidade](../code-quality/portability-warnings.md)
