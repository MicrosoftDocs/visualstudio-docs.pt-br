---
title: Classes do Visual C++ no Designer de Classe | Microsoft Docs
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
- vs.classdesigner.inheritancelinelabel
helpviewer_keywords:
- Class Designer [Visual Studio], classes
ms.assetid: 75e56f8c-11ef-42a3-b7ec-3d2cf25c581b
caps.latest.revision: 23
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: d4193dda70aeda8534b9dc2fa3428ca08a9d89fa
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49285682"
---
# <a name="visual-c-classes-in-class-designer"></a>Classes do Visual C++ no Designer de Classe
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

O Designer de Classe dá suporte a classes do C++ e visualiza classes nativas do C++ da mesma maneira que formas de classe do Visual Basic e do Visual C#, exceto pelo fato de classes do C++ poderem ter múltiplas relações de herança. É possível expandir a forma de classe para exibir mais campos e métodos na classe ou recolhê-la para economizar espaço.  
  
> [!NOTE]
>  O Designer de Classe não dá suporte a uniões (um tipo especial de classe em que a memória alocada é apenas a quantidade necessária para o maior membro de dados da união).  
  
## <a name="simple-inheritance"></a>Herança simples  
 Quando você arrasta mais de uma classe para um diagrama de classe e as classes têm uma relação de herança de classe, uma seta as conecta. A seta aponta para a direção da classe base. Por exemplo, quando as classes a seguir são exibidas em um diagrama de classe, uma seta as conecta, apontando de B para A:  
  
```  
class A {};  
class B : A {};  
```  
  
 Você também pode arrastar apenas a classe B para o diagrama de classe, clicar com o botão direito do mouse na forma de classe de B e, em seguida, clicar em **Mostrar Classes Base**. Isso exibe sua classe base: A.  
  
## <a name="multiple-inheritance"></a>Várias heranças  
 O Designer de Classe dá suporte à visualização de relações de herança com várias classes. A *herança múltipla* é usada quando uma classe derivada tem atributos com mais de uma classe base. A seguir, temos um exemplo de herança múltipla:  
  
```  
class Bird {};  
class Swimmer {};  
class Penguin : public Bird, public Swimmer {};  
```  
  
 Quando você arrasta mais de uma classe para o diagrama de classe e as classes têm uma relação de herança com várias classes, uma seta as conecta. A seta aponta para a direção das classes base.  
  
 Clicar com o botão direito do mouse em uma forma de classe e, depois, clicar em **Mostrar Classes Base** exibe as classes base da classe selecionada.  
  
> [!NOTE]
>  O comando **Mostrar Classes Derivadas** não tem suporte para código C++. É possível exibir as classes derivadas indo até o Modo de Exibição de Classe, expandindo o nó de tipo, expandindo a subpasta **Tipos Derivados** e, em seguida, arrastando esses tipos para o diagrama de classe.  
  
 Para obter mais informações sobre a herança de classes múltiplas, consulte [(NOTINBUILD) Herança múltipla](http://msdn.microsoft.com/en-us/3b74185e-2beb-4e29-8684-441e51d2a2ca) e [Classes Base Múltiplas](http://msdn.microsoft.com/library/a30c69fe-401c-4a87-96a0-e0da70c7c740).  
  
## <a name="abstract-classes"></a>Classes abstratas  
 O Designer de Classe dá suporte a classes abstratas (também chamadas de "classes base abstratas"). Essas são classes que você nunca instancia, mas das quais pode derivar outras classes. Usando um exemplo de "Herança múltipla" no início deste documento, você pode instanciar a classe `Bird` como objetos individuais, da seguinte maneira:  
  
```  
int main()  
{  
   Bird sparrow;  
   Bird crow;  
   Bird eagle;  
}  
```  
  
 No entanto, talvez você não pretenda instanciar a classe `Swimmer` como objetos individuais. Talvez você pretenda apenas derivar outros tipos de classes de animal, por exemplo, `Penguin`, `Whale` e `Fish`. Nesse caso, você declararia a classe `Swimmer` como uma classe base abstrata.  
  
 Para declarar uma classe como abstrata, você pode usar a palavra-chave `abstract`. Membros marcados como abstratos, ou incluídos em uma classe abstrata, são virtuais e devem ser implementados por classes que derivam da classe abstrata.  
  
```  
class Swimmer abstract  
{  
   virtual void swim();  
   void dive();  
};  
```  
  
 Você também pode declarar uma classe como abstrata incluindo pelo menos uma função virtual pura:  
  
```  
class Swimmer  
{  
   virtual void swim() = 0;  
   void dive();  
};  
```  
  
 Quando você exibe essas declarações em um Diagrama de Classe, o nome da classe `Swimmer` e sua função virtual pura `swim` são exibidos em itálico em uma forma de classe abstrata, em conjunto com a notação **Classe Abstrata**. Observe que a forma do tipo de classe abstrata é a mesmo de uma classe regular, mas sua borda é uma linha pontilhada.  
  
 Uma classe derivada de uma classe base abstrata deve substituir cada função virtual pura na classe base, ou a classe derivada não poderá ser instanciada. Portanto, por exemplo, se você derivar uma classe `Fish` da classe `Swimmer`, `Fish` deverá substituir o método `swim`:  
  
```  
class Fish : public Swimmer  
{  
   void swim(int speed);  
};  
  
int main()  
{  
   Fish guppy;  
}  
```  
  
 Quando você exibe esse código em um Diagrama de Classe, o Designer de Classe desenha uma linha de herança de `Fish` para `Swimmer`.  
  
## <a name="anonymous-classes"></a>Classes anônimas  
 O Designer de Classe dá suporte a classes anônimas. *Tipos de classe anônima* são classes declaradas sem um identificador. Elas não podem ter um construtor ou um destruidor, não podem ser passadas como argumentos para funções e não podem ser retornadas como valores retornados de funções. É possível usar uma classe anônima para substituir um nome de classe por um nome de typedef, como no exemplo a seguir:  
  
```  
typedef struct  
{  
    unsigned x;  
    unsigned y;  
} POINT;  
```  
  
 As estruturas também podem ser anônimas. O Designer de Classe exibe estruturas e classes anônimas da mesma forma como exibe o respectivo tipo. Embora você possa declarar e exibir estruturas e classes anônimas, o Designer de Classe não usará o nome de marcação que você especificar. Ele usará o nome gerado pelo Modo de Exibição de Classe. A classe ou estrutura aparece no Modo de Exibição de Classe e no Designer de Classe como um elemento chamado **__unnamed**.  
  
 Para obter mais informações sobre classes anônimas, consulte [Tipos de classe anônima](http://msdn.microsoft.com/library/9ba667b2-8c2a-4c29-82a6-fa120b9233c8).  
  
## <a name="template-classes"></a>Classes de modelo  
 O Designer de Classe dá suporte à visualização de classes de modelo. Declarações aninhadas têm suporte. A tabela a seguir mostra algumas declarações típicas.  
  
|Elemento de código|Modo de exibição do Designer de Classe|  
|------------------|-------------------------|  
|`template <class T>`<br /><br /> `class A {};`|`A<T>`<br /><br /> Classe de modelo|  
|`template <class T, class U>`<br /><br /> `class A {};`|`A<T, U>`<br /><br /> Classe de modelo|  
|`template <class T, int i>`<br /><br /> `class A {};`|`A<T, i>`<br /><br /> Classe de modelo|  
|`template <class T, template <class K> class U>`<br /><br /> `class A {};`|`A<T, U>`<br /><br /> Classe de modelo|  
  
 A tabela a seguir mostra alguns exemplos de especialização parcial.  
  
|Elemento de código|Modo de exibição do Designer de Classe|  
|------------------|-------------------------|  
|`template<class T, class U>`<br /><br /> `class A {};`|`A<T, U>`<br /><br /> Classe de modelo|  
|`template<class T>`<br /><br /> `class A<T, T> {};`|`A<T, T>`<br /><br /> Classe de modelo|  
|`template <class T>`<br /><br /> `class A<T, int> {};`|`A<T, int>`<br /><br /> Classe de modelo|  
|`template <class T1, class T2>`<br /><br /> `class A<T1*, T2*> {};`|`A<T1*, T2*>`<br /><br /> Classe de modelo|  
  
 A tabela a seguir mostra alguns exemplos de herança na especialização parcial.  
  
|Elemento de código|Modo de exibição do Designer de Classe|  
|------------------|-------------------------|  
|`template <class T, class U>`<br /><br /> `class A {};`<br /><br /> `template <class TC>`<br /><br /> `class A<T, int> {};`<br /><br /> `class B : A<int, float>`<br /><br /> `{};`<br /><br /> `class C : A<int, int>`<br /><br /> `{};`|`A<T, U>`<br /><br /> Classe de modelo<br /><br /> `B`<br /><br /> Classe<br /><br /> (aponta para a Classe A)<br /><br /> `C`<br /><br /> Classe<br /><br /> (aponta para a Classe A)|  
  
 A tabela a seguir mostra alguns exemplos de funções de modelo de especialização parcial.  
  
|Elemento de código|Modo de exibição do Designer de Classe|  
|------------------|-------------------------|  
|`class A`<br /><br /> `{`<br /><br /> `template <class T, class U>`<br /><br /> `void func(T a, U b);`<br /><br /> `template <class T>`<br /><br /> `void func(T a, int b);`<br /><br /> `};`|`A`<br /><br /> func\<T, U> (+ 1 de sobrecarga)|  
|`template <class T1>`<br /><br /> `class A {`<br /><br /> `template <class T2>`<br /><br /> `class B {};`<br /><br /> `};`<br /><br /> `template<> template<>`<br /><br /> `class A<type>::B<type> {};`|`A<T1>`<br /><br /> Classe de modelo<br /><br /> `B<T2>`<br /><br /> Classe de modelo<br /><br /> (B está contido na classe A em **Tipos Aninhados**)|  
|`template <class T>`<br /><br /> `class C {};`<br /><br /> `class A : C<int> {};`|`A`<br /><br /> Classe<br /><br /> -> C\<int><br /><br /> `C<T>`<br /><br /> Classe de modelo|  
  
 A tabela a seguir mostra alguns exemplos de herança de modelo.  
  
|Elemento de código|Modo de exibição do Designer de Classe|  
|------------------|-------------------------|  
|`template <class T>`<br /><br /> `class C {};`<br /><br /> `template<>`<br /><br /> `class C<int> {`<br /><br /> `class B {};`<br /><br /> `}`<br /><br /> `class A : C<int>::B {};`|`A`<br /><br /> Classe<br /><br /> ->B<br /><br /> `C<int>`<br /><br /> Classe<br /><br /> (B está contido na classe C em **Tipos Aninhados**)<br /><br /> `C<T>`<br /><br /> Classe de modelo|  
  
 A tabela a seguir mostra alguns exemplos de conexões de classe especializada canônicas.  
  
|Elemento de código|Modo de exibição do Designer de Classe|  
|------------------|-------------------------|  
|`template <class T>`<br /><br /> `class C {};`<br /><br /> `template<>`<br /><br /> `class C<int> {};`<br /><br /> `class A : C<int> {};`<br /><br /> `class D : C<float> {};`|`A`<br /><br /> Classe<br /><br /> ->C\<int><br /><br /> `C<int>`<br /><br /> Classe<br /><br /> `C<T>`<br /><br /> Classe de modelo<br /><br /> `D`<br /><br /> Classe<br /><br /> ->C\<float>|  
|`class B {`<br /><br /> `template <class T>`<br /><br /> `T min (const T &a, const T &b);`<br /><br /> `};`|`B`<br /><br /> min \<T>|  
  
## <a name="see-also"></a>Consulte também  
 [Trabalhando com código do Visual C++ (Designer de Classe)](../ide/working-with-visual-cpp-code-class-designer.md)   
 [Classes e structs](http://msdn.microsoft.com/library/516dd496-13fb-4f17-845a-e9ca45437873)   
 [Tipos de classe anônima](http://msdn.microsoft.com/library/9ba667b2-8c2a-4c29-82a6-fa120b9233c8)   
 [(NOTINBUILD) Herança múltipla](http://msdn.microsoft.com/en-us/3b74185e-2beb-4e29-8684-441e51d2a2ca)   
 [Classes base múltiplas](http://msdn.microsoft.com/library/a30c69fe-401c-4a87-96a0-e0da70c7c740)   
 [Modelos](http://msdn.microsoft.com/library/90fcc14a-2092-47af-9d2e-dba26d25b872)



