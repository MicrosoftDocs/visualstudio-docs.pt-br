---
title: Depurar uma violação de acesso de C++ | Microsoft Docs
description: Confira dicas sobre como solucionar problemas de violação de acesso quando mais de um ponteiro é um candidato. As versões recentes do Visual Studio nomeam o ponteiro errônea.
ms.custom: SEO-VS-2020, seodec18
ms.date: 02/05/2019
ms.topic: how-to
f1_keywords:
- vs.debug.access
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- access violation debugging
- debugging [Visual Studio], access violations
ms.assetid: 9311d754-0ce9-4145-b147-88b6ca77ba63
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- cplusplus
ms.openlocfilehash: b0fb7e6f5ae71cf336f9fe206bc7b0208566b615
ms.sourcegitcommit: 40d758f779d42c66cb02ae7face8a62763a8662b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97398564"
---
# <a name="how-can-i-debug-a-c-access-violation"></a>Como posso depurar uma violação de acesso de C++?

## <a name="problem-description"></a>Descrição do problema

Meu programa produz uma violação de acesso. Como posso depurar isso?

## <a name="solution"></a>Solução

Se você obtiver uma violação de acesso em uma linha de código que faz referência a vários ponteiros, pode ser difícil descobrir qual ponteiro causou a violação de acesso. A partir do Visual Studio 2015 atualização 1, a caixa de diálogo de exceção agora nomeia explicitamente o ponteiro que causou a violação de acesso.

Por exemplo, considerando o código a seguir, você deve obter uma violação de acesso:

```C++
#include <iostream>
using namespace std;

class ClassC {
public:
  void printHello() {
    cout << "hello world";
  }
};

class ClassB {
public:
  ClassC* C;
  ClassB() {
    C = new ClassC();
  }
};

class ClassA {
public:
  ClassB* B;
  ClassA() {
    // Uncomment to fix
    // B = new ClassB();
  }
};

int main() {
  ClassA* A = new ClassA();
  A->B->C->printHello();

}
```

Se você executar esse código no Visual Studio 2015 atualização 1, verá a seguinte caixa de diálogo de exceção:

![AccessViolationCPlus](../debugger/media/accessviolationcplus.png "AccessViolationCPlus")

Se você não puder determinar por que o ponteiro causou uma violação de acesso, rastreie o código para certificar-se de que o ponteiro que está causando o problema tenha sido atribuído corretamente.  Se ele for passado como um parâmetro, verifique se ele foi passado corretamente e se você não está criando acidentalmente uma [cópia superficial](https://stackoverflow.com/questions/184710/what-is-the-difference-between-a-deep-copy-and-a-shallow-copy). Em seguida, verifique se os valores não estão sendo acidentalmente alterados em algum lugar no programa criando um ponto de interrupção de dados para o ponteiro em questão para verificar se ele não está sendo modificado em outro lugar no programa. Para obter mais informações sobre pontos de interrupção de dados, consulte a seção ponto de interrupção de dados em [usando pontos de interrupção](../debugger/using-breakpoints.md).

## <a name="see-also"></a>Consulte também
- [Perguntas frequentes sobre depuração de código nativo](../debugger/debugging-native-code-faqs.md)