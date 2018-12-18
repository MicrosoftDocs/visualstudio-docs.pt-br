---
title: Depurar uma violação de acesso do C++ | Microsoft Docs
ms.custom: seodec18
ms.date: 05/23/2017
ms.technology: vs-ide-debug
ms.topic: conceptual
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
manager: douge
ms.workload:
- cplusplus
ms.openlocfilehash: 6f463f4e14e5be90422f73b299cb927a54fcfcef
ms.sourcegitcommit: 708f77071c73c95d212645b00fa943d45d35361b
ms.translationtype: MTE95
ms.contentlocale: pt-BR
ms.lasthandoff: 12/07/2018
ms.locfileid: "53067254"
---
# <a name="how-can-i-debug-a-c-access-violation"></a>Como posso depurar uma violação de acesso de C++?
## <a name="problem-description"></a>Descrição do problema  
 Meu programa produz uma violação de acesso. Como posso depurar isso?  
  
## <a name="solution"></a>Solução  
 Se você receber uma violação de acesso em uma linha de código que cancela a referência de vários ponteiros, pode ser difícil descobrir quais ponteiro causou a violação de acesso. A partir do Visual Studio 2015 atualização 1, a caixa de diálogo de exceção agora explicitamente nomeia o ponteiro que causou a violação de acesso.  
  
 Por exemplo, dado o código a seguir, você deve obter uma violação de acesso:  
  
```C++  
#include <iostream>  
using namespace std;  
  
class ClassB {  
public:  
        ClassC* C;  
        ClassB() {  
                C = new ClassC();  
        }  
     void printHello() {  
                cout << "hello world";  
        }  
};  
  
class ClassA {  
public:  
    ClassB* B;  
      ClassA() {  
                B = nullptr;  
        }  
};  
  
int main() {  
    ClassA* A = new ClassA();  
      A->B->printHello();  
}  
```  
  
 Se você executar esse código no Visual Studio 2015 atualização 1, você deverá ver a seguinte caixa de diálogo de exceção:  
  
 ![AccessViolationCPlus](../debugger/media/accessviolationcplus.png "AccessViolationCPlus")  
  
 Se você não puder determinar por que o ponteiro causou uma violação de acesso, rastrear o código para certificar-se de que o ponteiro causando o problema foi atribuído corretamente.  Se ele é passado como um parâmetro, certifique-se de que ele é passado corretamente, e você não criar acidentalmente um [cópia superficial](http://stackoverflow.com/questions/184710/what-is-the-difference-between-a-deep-copy-and-a-shallow-copy). Em seguida, verifique se que os valores não sejam sendo inadvertidamente alterados em algum lugar no programa, criando um ponto de interrupção de dados para o ponteiro em questão para certificar-se de que não está sendo modificada em outro lugar no programa. Para obter mais informações sobre pontos de interrupção de dados, consulte a seção de ponto de interrupção de dados no [usando pontos de interrupção](../debugger/using-breakpoints.md).  
  
## <a name="see-also"></a>Consulte também  
 [Perguntas frequentes de depuração de código nativo](../debugger/debugging-native-code-faqs.md)