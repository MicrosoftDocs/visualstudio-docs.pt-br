---
title: 'CA2153: Evite lidar com exceções de estado corrompidas | Microsoft Docs'
ms.date: 11/15/2016
ms.technology: vs-ide-code-analysis
ms.topic: reference
ms.assetid: 418cc9cb-68ad-47e9-a6c8-a48b9c35db45
caps.latest.revision: 7
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 27d837c09e5f2f90796c149bf58d1114d7e6352d
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85546309"
---
# <a name="ca2153-avoid-handling-corrupted-state-exceptions"></a>CA2153: Evitar tratamento de exceções de estado corrompido
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|Valor|
|-|-|
|TypeName|AvoidHandlingCorruptedStateExceptions|
|CheckId|CA2153|
|Categoria|Microsoft.Security|
|Alteração Significativa|Sem interrupção|

## <a name="cause"></a>Causa
 As [exceções de estado corrompidas (CSE)](https://msdn.microsoft.com/magazine/dd419661.aspx) indicam que há corrupção de memória em seu processo. A captura deles, em vez de permitir que o processo falhe, pode levar a vulnerabilidades de segurança se um invasor puder fazer uma exploração na região de memória corrompida.

## <a name="rule-description"></a>Descrição da Regra
 CSE indica que o estado de um processo foi corrompido e não detectado pelo sistema. No cenário de estado corrompido, um manipulador geral só capturará a exceção se você marcar o método com o `HandleProcessCorruptedStateExceptions` atributo apropriado. Por padrão, o [CLR (Common Language Runtime)](https://msdn.microsoft.com/library/8bs2ecf4.aspx) não invocará manipuladores catch para CSEs.

 Permitir que o processo falhe sem capturar esses tipos de exceções é a opção mais segura, pois mesmo o código de registro em log pode permitir que os invasores explorem bugs de corrupção de memória.

 Esse aviso dispara ao capturar CSEs com um manipulador geral que captura todas as exceções, como catch (Exception) ou catch (sem especificação de exceção).

## <a name="how-to-fix-violations"></a>Como Corrigir Violações
 Para resolver esse aviso, você deve executar um dos seguintes procedimentos:

 1. Remova o atributo `HandleProcessCorruptedStateExceptions`. Isso reverte para o comportamento de tempo de execução padrão em que CSEs não são passados para manipuladores catch.

 2. Remova o manipulador de catch geral em preferência de manipuladores que capturam tipos de exceção específicos.  Isso pode incluir CSEs supondo que o código do manipulador possa tratá-los com segurança (muito raro).

 3. Relançou o CSE no manipulador catch, que garante que a exceção seja passada para o chamador e resultará na finalização do processo em execução.

## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos
 Não suprima um aviso nessa regra.

## <a name="pseudo-code-example"></a>Exemplo de pseudo-código

### <a name="violation"></a>Infra
 O pseudocódigo a seguir ilustra o padrão detectado por essa regra.

```
[HandleProcessCorruptedStateExceptions]
//method to handle and log CSE exceptions
void TestMethod1()
{
    try
    {
        FileStream fileStream = new FileStream("name", FileMode.Create);
    }
    catch (Exception e)
    {
        // Handle error
    }
}
```

### <a name="solution-1"></a>Solução 1
 Remover o atributo HandleProcessCorruptedExceptions garante que as exceções não serão tratadas.

```
void TestMethod1()
{
    try
    {
        FileStream fileStream = new FileStream("name", FileMode.Create);
    }
    catch (IOException e)
    {
        // Handle error
    }
    catch (UnauthorizedAccessException e)
    {
        // Handle error
    }
}
```

### <a name="solution-2"></a>Solução 2
 Remova o manipulador de catch geral e Capture apenas tipos de exceção específicos.

```
void TestMethod1()
{
    try
    {
        FileStream fileStream = new FileStream("name", FileMode.Create);
    }
    catch (IOException e)
    {
        // Handle error
    }
    catch (UnauthorizedAccessException e)
    {
        // Handle error
    }
}
```

### <a name="solution-3"></a>Solução 3
 Relançou a exceção.

```
void TestMethod1()
{
    try
    {
        FileStream fileStream = new FileStream("name", FileMode.Create);
    }
    catch (Exception e)
    {
        // Handle error
        throw;
    }
}
```
