---
title: Snippets de código do Visual C++ | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-general
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 74e26fd4-e5ca-4611-a816-0a521b4947a0
caps.latest.revision: 6
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: ed64d9dde53b31cfe5f52ce708e4ee96d91fe8ff
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49861352"
---
# <a name="visual-c-code-snippets"></a>Snippets de código do Visual C++
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

No Visual Studio, você pode usar snippets de código para adicionar código comumente usado nos seus arquivos de código do C++. Em geral, você pode usar os snippets de código de forma bem parecida com o C#, mas o conjunto de snippets de código padrão é diferente.  
  
 Você pode adicionar um snippet de código em um local específico no seu código (inserção) ou envolver algum código selecionado com um snippet de código.  
  
## <a name="inserting-a-code-snippet"></a>Inserindo um snippet de código  
 Para inserir um snippet de código, abra um arquivo de código do C++ (.cpp ou .h), clique em algum lugar dentro do arquivo e siga um destes procedimentos:  
  
- Clique com o botão direito do mouse para obter o menu de contexto e selecione **Inserir Snippet**  
  
- No menu **Editar / IntelliSense**, selecione **Inserir Snippet**  
  
- Use as teclas de atalho: **CTRL + K + X**  
  
  Você deve ver uma lista de opções que começam com **#if**. Ao selecionar **#if**, você verá o seguinte código adicionado ao arquivo:  
  
```cpp  
#if 0  
  
#endif // 0  
```  
  
 Em seguida, você pode substituir o 0 pela condição correta.  
  
## <a name="using-a-code-snippet-to-surround-selected-code"></a>Usar um snippet de código para envolver o código selecionado  
 Para usar um snippet de código para envolver o código selecionado, selecione uma linha (ou várias linhas) e siga um destes procedimentos:  
  
1. Clique com o botão direito do mouse para obter o menu de contexto e selecione **Envolver com**  
  
2. No menu **Editar / IntelliSense**, selecione **Envolver com**  
  
3. Use as teclas de atalho: **CTRL + K + S**  
  
   Selecione **#if**. Você deve ver algo parecido com isso:  
  
```cpp  
#if 0  
#include "pch.h"  // or whatever line you had selected  
#endif // 0  
```  
  
 Em seguida, você pode substituir o 0 pela condição correta.  
  
## <a name="where-can-i-find-a-complete-list-of-the-c-code-snippets"></a>Onde posso encontrar uma lista completa dos snippets de código do C++?  
 Você pode encontrar a lista completa de snippets de código do C++ indo até o **Gerenciador de Snippets de Código** (no menu **Ferramentas**) e configurando a **Linguagem** para **Visual C++**. Na janela abaixo, expanda **Visual C++**. Você verá os nomes de todos os snippets de código do C++ em ordem alfabética.  
  
 Os nomes da maioria dos snippets de código são auto-explicativos, mas alguns nomes podem ser confusos.  
  
## <a name="class-vs-classi"></a>Class versus classi  
 O snippet **class** fornece a definição de uma classe chamada MyClass, com o construtor e o destruidor padrão apropriado, em que as definições do construtor e do destruidor estão localizadas fora da classe:  
  
```cpp  
class MyClass  
{  
public:  
MyClass();  
~MyClass();  
  
private:  
  
};  
  
MyClass::MyClass()  
{  
}  
  
MyClass::~MyClass()  
{  
}  
```  
  
 O snippet de código classi também fornece a definição de uma classe chamada MyClass, mas o construtor e o destruidor padrão estão definidos dentro da definição de classe:  
  
```cpp  
class MyClass  
{  
public:  
MyClass()  
{  
}  
  
~MyClass()  
{  
}  
  
private:  
  
};  
```  
  
## <a name="for-vs-foreach-vs-forr-vs-rfor"></a>For versus foreach versus forr versus rfor  
 Há quatro snippets for diferentes que fornecem diferentes tipos de loops de for.  
  
 O snippet **for** fornece um loop `for` em que a condição é baseada no comprimento (em `size_t`) de um objeto:  
  
```cpp  
for (size_t i = 0; i < length; i++)  
{  
  
}  
```  
  
 O snippet **foreach** fornece um loop `for each` que itera sobre os membros de uma coleção:  
  
```cpp  
for each (object var in collection_to_loop)  
{  
  
}  
```  
  
 O snippet **forr** fornece um loop `for` reverso em que a condição é baseada no comprimento (em inteiros) de um objeto:  
  
```cpp  
for (int i = length - 1; i >= 0; i--)  
{  
  
}  
```  
  
 O snippet **rfor** fornece um loop for (link) [baseado em intervalo](http://msdn.microsoft.com/library/5750ba1d-ba48-4236-a923-e32de8345c2d):  
  
```cpp  
for (auto& i : v)  
{  
  
}  
```  
  
## <a name="the-destructor-snippet-"></a>O snippet de destruidor (~)  
 O snippet de destruidor (**~**) apresenta comportamento diferente em diferentes contextos. Se você inserir este snippet dentro de uma classe, ele fornecerá um destruidor para essa classe. Por exemplo, considerando o seguinte código:  
  
```cpp  
class SomeClass {  
  
};  
```  
  
 Se você inserir o snippet de destruidor, ele fornecerá um destruidor para a SomeClass:  
  
```cpp  
class SomeClass {  
    ~SomeClass()  
    {  
  
    }  
};  
```  
  
 Se você tentar inserir o snippet de destruidor fora de uma classe, ele fornecerá um destruidor com um nome de espaço reservado:  
  
```cpp  
~TypeNamePlaceholder()  
{  
  
```



