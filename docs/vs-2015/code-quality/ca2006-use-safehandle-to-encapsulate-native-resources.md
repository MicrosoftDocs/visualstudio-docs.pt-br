---
title: 'CA2006: usar SafeHandle para encapsular recursos nativos | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA2006
- UseSafeHandleToEncapsulateNativeResources
helpviewer_keywords:
- UseSafeHandleToEncapsulateNativeResources
- CA2006
ms.assetid: a71950bd-bcc1-463d-b1f2-5233bc451456
caps.latest.revision: 19
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: fdf3ff02c86a878e9c955d2b3b92879870700efa
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85521141"
---
# <a name="ca2006-use-safehandle-to-encapsulate-native-resources"></a>CA2006: Usar SafeHandle para encapsular recursos nativos
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|Valor|
|-|-|
|TypeName|UseSafeHandleToEncapsulateNativeResources|
|CheckId|CA2006|
|Categoria|Microsoft. confiabilidade|
|Alteração Significativa|Sem interrupção|

## <a name="cause"></a>Causa
 O código gerenciado usa o <xref:System.IntPtr> para acessar recursos nativos.

## <a name="rule-description"></a>Descrição da Regra
 O uso do `IntPtr` em código gerenciado pode indicar um problema de segurança e confiabilidade em potencial. Todos os usos do `IntPtr` devem ser revisados para determinar se o uso de uma <xref:System.Runtime.InteropServices.SafeHandle> tecnologia, ou semelhante, é necessário em seu lugar. Ocorrerão problemas se o `IntPtr` representar algum recurso nativo, como memória, um identificador de arquivo ou um soquete, que o código gerenciado é considerado proprietário. Se o código gerenciado possui o recurso, ele também deve liberar os recursos nativos associados a ele, pois uma falha ao fazer isso causaria o vazamento de recursos.

 Nesses cenários, problemas de segurança ou confiabilidade também existirão se o acesso multithread for permitido para o `IntPtr` e uma maneira de liberar o recurso que é representado pelo `IntPtr` for fornecido. Esses problemas envolvem a reciclagem do `IntPtr` valor na liberação de recursos enquanto o uso simultâneo do recurso está sendo feito em outro thread. Isso pode causar condições de corrida em que um thread pode ler ou gravar dados associados ao recurso errado. Por exemplo, se o seu tipo armazena um identificador de sistema operacional como um `IntPtr` e permite que os usuários chamem o **fechamento** e qualquer outro método que usa esse identificador simultaneamente e sem algum tipo de sincronização, seu código tem um problema de reciclagem de identificador.

 Esse problema de reciclagem de identificador pode causar corrupção de dados e, frequentemente, uma vulnerabilidade de segurança. `SafeHandle`e sua classe irmã <xref:System.Runtime.InteropServices.CriticalHandle> fornece um mecanismo para encapsular um identificador nativo para um recurso para que tais problemas de Threading possam ser evitados. Além disso, você pode usar `SafeHandle` e sua classe irmã `CriticalHandle` para outros problemas de Threading, por exemplo, para controlar cuidadosamente o tempo de vida de objetos gerenciados que contêm uma cópia do identificador nativo em chamadas para métodos nativos. Nessa situação, muitas vezes você pode remover chamadas para `GC.KeepAlive` . A sobrecarga de desempenho tailandês que você incorrerá ao usar `SafeHandle` e, para um menor grau, `CriticalHandle` , muitas vezes, pode ser reduzida por meio de um design cuidadoso.

## <a name="how-to-fix-violations"></a>Como Corrigir Violações
 Converta o `IntPtr` uso para `SafeHandle` para gerenciar com segurança o acesso a recursos nativos. Consulte o <xref:System.Runtime.InteropServices.SafeHandle> tópico de referência para obter exemplos.

## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos
 Você não deve suprimir este aviso.

## <a name="see-also"></a>Consulte Também
 <xref:System.IDisposable>
