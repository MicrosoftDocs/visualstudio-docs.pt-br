---
title: Typedefs do Visual C++ no Designer de Classe | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-general
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- vs.classdesigner.typedef
- vs.classdesigner.aliasofline
helpviewer_keywords:
- Class Designer [Visual Studio], typedefs
ms.assetid: c1984108-71fc-4d3a-b4d4-3eac2c6b4ebf
caps.latest.revision: 16
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: 1ba65af46589e01aa5473b5757124ed184da2197
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49230224"
---
# <a name="visual-c-typedefs-in-class-designer"></a>Typedefs do Visual C++ no Designer de Classe
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

As instruções typedef criam uma ou mais camadas de indireção entre um nome e seu tipo subjacente. O Designer de Classe oferece suporte a tipos de typedef do C++ que são declarados com a palavra-chave `typedef`, por exemplo:  
  
```  
typedef class coord  
{  
   void P(x,y);  
   unsigned x;  
   unsigned y;  
} COORD;  
```  
  
 Então, você pode usar esse tipo para declarar uma instância:  
  
 `COORD OriginPoint;`  
  
 Embora seja possível declarar um typedef sem um nome, o Designer de Classe não usará o nome de marca que você especificar. Ele usará o nome que o Modo de Exibição de Classe gerar. Por exemplo, a declaração a seguir é válida, mas ela aparece no Modo de Exibição de Classe e no Designer de Classe como um objeto chamado **__unnamed**:  
  
```  
typedef class coord  
{  
   void P(x,y);  
   unsigned x;  
   unsigned y;  
};  
```  
  
 Para obter mais informações sobre como usar o tipo `typedef`, consulte [Especificador (NOTINBUILD)typedef](http://msdn.microsoft.com/en-us/cc96cf26-ba93-4179-951e-695d1f5fdcf1).  
  
 Uma forma de typedef do C++ tem a forma do tipo especificado no typedef. Por exemplo, se a fonte declara `typedef class`, a forma terá cantos arredondados e o rótulo **Classe**. Para `typedef struct`, a forma tem cantos quadrados e o rótulo **Struct**.  
  
 Classes e estruturas podem ter typedefs aninhados declarados dentro deles. Sendo assim, formas de classe e de estrutura podem mostrar declarações de typedef aninhado como formas aninhadas.  
  
 As formas typedef dão suporte aos comandos **Mostrar como Associação** e **Mostrar como Associação de Coleções** no menu de contexto.  
  
 A seguir estão alguns exemplos dos tipos de typdef aos quais o Designer de Classe oferece suporte:  
  
 `typedef type name`  
  
 *nome* : *tipo*  
  
 typedef  
  
 Desenha uma linha de associação conectando-se ao tipo *nome*, se possível.  
  
 `typedef void (*func)(int)`  
  
 `func: void (*)(int)`  
  
 typedef  
  
 Typedef para ponteiros de função. Nenhuma linha de associação é desenhada.  
  
 O Designer de Classe não exibirá um typedef se seu tipo de origem for um ponteiro de função.  
  
```  
typedef int MyInt;  
class A {  
   MyInt I;  
};  
```  
  
 `MyInt: int`  
  
 typedef  
  
 `A`  
  
 Classe  
  
 Desenha uma linha de associação apontando da forma do tipo de origem para a forma do tipo de destino.  
  
 `Class B {};`  
  
 `typedef B MyB;`  
  
 `B`  
  
 Classe  
  
 `MyB : B`  
  
 typedef  
  
 Ao clicar com o botão direito do mouse em uma forma de typedef e clicar em **Mostrar como Associação** exibe o typedef ou a classe e uma linha **Alias de** unindo as duas formas (semelhante a uma linha de associação).  
  
 `typedef B MyB;`  
  
 `typedef MyB A;`  
  
 `MyBar : Bar`  
  
 typedef  
  
 Mesmo que anterior.  
  
```  
Class B {};  
typedef B MyB;  
  
class A {  
   MyB B;  
};  
```  
  
 `B`  
  
 Classe  
  
 `MyB : B`  
  
 typedef  
  
 `A`  
  
 Classe  
  
 `MyB` é uma forma de typedef aninhado.  
  
 `#include <vector>`  
  
 `...`  
  
 `using namespace std;`  
  
 `...`  
  
 `typedef vector<int> MyIntVect;`  
  
 `vector<T>`Classe  
  
 `MyIntVect : vector<int>`  
  
 typedef  
  
 `class B {};`  
  
 `typedef B MyB;`  
  
 `class A : MyB {};`  
  
 `MyB : B`  
  
 typedef  
  
 -> B  
  
 `B`  
  
 `A`  
  
 Classe  
  
 -> MyB  
  
 O Designer de Classe não oferece suporte para exibir esse tipo de relacionamento usando um comando de menu de contexto.  
  
 `#include <vector>`  
  
 `Typedef MyIntVect std::vector<int>;`  
  
 `Class MyVect : MyIntVect {};`  
  
 `std::vector<T>`  
  
 Classe  
  
 `MyIntVect : std::vector<int>`  
  
 typedef  
  
 `MyVect`  
  
 Classe  
  
 -> MyIntVect  
  
## <a name="see-also"></a>Consulte também  
 [Trabalhando com código do Visual C++ (Designer de Classe)](../ide/working-with-visual-cpp-code-class-designer.md)   
 [Especificador (NOTINBUILD)typedef](http://msdn.microsoft.com/en-us/cc96cf26-ba93-4179-951e-695d1f5fdcf1)



