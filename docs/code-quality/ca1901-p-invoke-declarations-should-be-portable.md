---
title: 'CA1901: as declarações de P-Invoke devem ser portáteis'
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA1901
- PInvokeDeclarationsShouldBePortable
helpviewer_keywords:
- CA1901
- PInvokeDeclarationsShouldBePortable
ms.assetid: 90361812-55ca-47f7-bce9-b8775d3b8803
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 94067aad31c25db64d0732ebd67c442fd9466328
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49937363"
---
# <a name="ca1901-pinvoke-declarations-should-be-portable"></a>CA1901: as declarações de P/Invoke devem ser portáteis

|||
|-|-|
|NomeDoTipo|PInvokeDeclarationsShouldBePortable|
|CheckId|CA1901|
|Categoria|Microsoft.Portability|
|Alteração Significativa|Quebrando - se o valor de P/Invoke é visível fora do assembly. Não separável - se o valor de P/Invoke não é visível fora do assembly.|

## <a name="cause"></a>Causa
 Essa regra avalia o tamanho de cada parâmetro e o valor retornado de um P/Invoke e verifica se o seu tamanho, quando passa por marshaling para código não gerenciado em plataformas de 32 bits e 64 bits, está correto. A violação dessa regra mais comuns é passar um inteiro de tamanho fixo em que uma variável dependente de plataforma, tamanho de ponteiro é necessária.

## <a name="rule-description"></a>Descrição da regra
 Qualquer um dos cenários a seguir viola essa regra ocorre:

- O valor de retorno ou parâmetro é digitado como um inteiro de tamanho fixo quando ele deve ser digitado como um `IntPtr`.

- O valor de retorno ou parâmetro é digitado como um `IntPtr` quando ele deve ser digitado como um inteiro de tamanho fixo.

## <a name="how-to-fix-violations"></a>Como corrigir violações
 Você pode corrigir essa violação usando `IntPtr` ou `UIntPtr` para representar os identificadores em vez de `Int32` ou `UInt32`.

## <a name="when-to-suppress-warnings"></a>Quando suprimir avisos
 Você não deve suprimir esse aviso.

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

 Neste exemplo, o `nIconIndex` parâmetro é declarado como um `IntPtr`, que é de 4 bytes de largura em uma plataforma de 32 bits e 8 bytes de largura em uma plataforma de 64 bits. Na declaração não gerenciada que segue, você pode ver que `nIconIndex` é um inteiro sem sinal de 4 bytes em todas as plataformas.

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