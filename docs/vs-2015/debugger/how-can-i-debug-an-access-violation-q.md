---
title: Como posso depurar uma violação de acesso? | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- vs.debug.access
dev_langs:
- FSharp
- VB
- CSharp
- C++
- C++
helpviewer_keywords:
- access violation debugging
- debugging [Visual Studio], access violations
ms.assetid: 9311d754-0ce9-4145-b147-88b6ca77ba63
caps.latest.revision: 21
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: f6188cc273cdea1755071e36f606fb8f041508d7
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/02/2020
ms.locfileid: "74297319"
---
# <a name="how-can-i-debug-an-access-violation"></a>Como posso depurar uma violação de acesso?
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Descrição do problema  
 Meu programa produz uma violação de acesso. Como posso depurar isso?  
  
## <a name="solution"></a>Solução  
 Se você obtiver uma violação de acesso em uma linha de código que faz referência a vários ponteiros, pode ser difícil descobrir qual ponteiro causou a violação de acesso. A partir do Visual Studio 2015 atualização 1, a caixa de diálogo de exceção agora nomeia explicitamente o ponteiro que causou a violação de acesso.  
  
 Por exemplo, considerando o código a seguir, você deve obter uma violação de acesso:  
  
```cpp  
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
  
 Se você executar esse código no Visual Studio 2015 atualização 1, verá a seguinte caixa de diálogo de exceção:  
  
 ![AccessViolationCPlus](../debugger/media/accessviolationcplus.png "AccessViolationCPlus")  
  
 Se você não puder determinar por que o ponteiro causou uma violação de acesso, rastreie o código para certificar-se de que o ponteiro que está causando o problema tenha sido atribuído corretamente.  Se ele for passado como um parâmetro, verifique se ele foi passado corretamente e se você não está criando acidentalmente uma [cópia superficial](https://stackoverflow.com/questions/184710/what-is-the-difference-between-a-deep-copy-and-a-shallow-copy). Em seguida, verifique se os valores não estão sendo acidentalmente alterados em algum lugar no programa criando um ponto de interrupção de dados para o ponteiro em questão para verificar se ele não está sendo modificado em outro lugar no programa. Para obter mais informações sobre pontos de interrupção de dados, consulte a seção ponto de interrupção de dados em [usando pontos de interrupção](../debugger/using-breakpoints.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Perguntas frequentes de depuração do código nativo](../debugger/debugging-native-code-faqs.md)
