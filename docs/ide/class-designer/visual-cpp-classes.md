---
title: Classes do Visual C++ no Designer de Classe
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-ide-general
ms.topic: conceptual
f1_keywords:
- vs.classdesigner.inheritancelinelabel
helpviewer_keywords:
- Class Designer [Visual Studio], classes
ms.assetid: 75e56f8c-11ef-42a3-b7ec-3d2cf25c581b
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- cplusplus
ms.openlocfilehash: 6d2ff2b6660b7ef7530d3a37d251904fa54b5ce0
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49856191"
---
# <a name="visual-c-classes-in-class-designer"></a>Classes do Visual C++ no Designer de Classe

O **Designer de Classe** é compatível com classes do C++ e visualiza classes nativas do C++ da mesma maneira que as formas de classe do Visual Basic e do C#, exceto que as classes do C++ podem ter várias relações de herança. É possível expandir a forma de classe para exibir mais campos e métodos na classe ou recolhê-la para economizar espaço.

> [!NOTE]
> O **Designer de Classe** não é compatível com uniões (um tipo especial de classe em que a memória alocada é apenas a quantidade necessária para o maior membro de dados da união).

## <a name="simple-inheritance"></a>Herança simples

Quando você arrasta mais de uma classe para um diagrama de classe e as classes têm uma relação de herança de classe, uma seta as conecta. A seta aponta para a direção da classe base. Por exemplo, quando as classes a seguir são exibidas em um diagrama de classe, uma seta as conecta, apontando de B para A:

```cpp
class A {};
class B : A {};
```

Você também pode arrastar apenas a classe B para o diagrama de classe, clicar com o botão direito do mouse na forma de classe de B e, em seguida, clicar em **Mostrar Classes Base**. Isso exibe sua classe base: A.

## <a name="multiple-inheritance"></a>Herança múltipla

O **Designer de Classe** é compatível com a visualização de relações de herança com várias classes. A *herança múltipla* é usada quando uma classe derivada tem atributos com mais de uma classe base. A seguir, temos um exemplo de herança múltipla:

```cpp
class Bird {};
class Swimmer {};
class Penguin : public Bird, public Swimmer {};
```

Quando você arrasta mais de uma classe para o diagrama de classe e as classes têm uma relação de herança com várias classes, uma seta as conecta. A seta aponta para a direção das classes base.

Clicar com o botão direito do mouse em uma forma de classe e, depois, clicar em **Mostrar Classes Base** exibe as classes base da classe selecionada.

> [!NOTE]
> O comando **Mostrar Classes Derivadas** não tem suporte para código C++. É possível exibir as classes derivadas acessando o **Modo de Exibição de Classe**, expandindo o nó de tipo, expandindo a subpasta **Tipos Derivados** e, em seguida, arrastando esses tipos para o diagrama de classe.

Para obter mais informações sobre a herança de classes múltiplas, consulte [Herança múltipla](https://msdn.microsoft.com/library/6td5yws2.aspx) e [Classes Base Múltiplas](/cpp/cpp/multiple-base-classes).

## <a name="abstract-classes"></a>Classes abstratas

O **Designer de Classe** é compatível com classes abstratas (também chamadas de "classes base abstratas"). Essas são classes que você nunca instancia, mas das quais pode derivar outras classes. Usando um exemplo de "Herança múltipla" no início deste documento, você pode instanciar a classe `Bird` como objetos individuais, da seguinte maneira:

```cpp
int main()
{
   Bird sparrow;
   Bird crow;
   Bird eagle;
}
```

No entanto, talvez você não pretenda instanciar a classe `Swimmer` como objetos individuais. Talvez você pretenda apenas derivar outros tipos de classes de animal, por exemplo, `Penguin`, `Whale` e `Fish`. Nesse caso, você declararia a classe `Swimmer` como uma classe base abstrata.

Para declarar uma classe como abstrata, você pode usar a palavra-chave `abstract`. Membros marcados como abstratos, ou incluídos em uma classe abstrata, são virtuais e devem ser implementados por classes que derivam da classe abstrata.

```cpp
class Swimmer abstract
{
   virtual void swim();
   void dive();
};
```

Você também pode declarar uma classe como abstrata incluindo pelo menos uma função virtual pura:

```cpp
class Swimmer
{
   virtual void swim() = 0;
   void dive();
};
```

Quando você exibe essas declarações em um Diagrama de Classe, o nome da classe `Swimmer` e sua função virtual pura `swim` são exibidos em itálico em uma forma de classe abstrata, em conjunto com a notação **Classe Abstrata**. Observe que a forma do tipo de classe abstrata é a mesmo de uma classe regular, mas sua borda é uma linha pontilhada.

Uma classe derivada de uma classe base abstrata deve substituir cada função virtual pura na classe base, ou a classe derivada não poderá ser instanciada. Portanto, por exemplo, se você derivar uma classe `Fish` da classe `Swimmer`, `Fish` deverá substituir o método `swim`:

```cpp
class Fish : public Swimmer
{
   void swim(int speed);
};

int main()
{
   Fish guppy;
}
```

Quando você exibe esse código em um Diagrama de Classe, o **Designer de Classe** desenha uma linha de herança de `Fish` para `Swimmer`.

## <a name="anonymous-classes"></a>Classes anônimas

O **Designer de Classe** é compatível com classes anônimas. *Tipos de classe anônima* são classes declaradas sem um identificador. Elas não podem ter um construtor ou um destruidor, não podem ser passadas como argumentos para funções e não podem ser retornadas como valores retornados de funções. É possível usar uma classe anônima para substituir um nome de classe por um nome de typedef, como no exemplo a seguir:

```cpp
typedef struct
{
    unsigned x;
    unsigned y;
} POINT;
```

As estruturas também podem ser anônimas. O **Designer de Classe** exibe estruturas e classes anônimas da mesma forma que exibe o respectivo tipo. Embora você possa declarar e exibir estruturas e classes anônimas, o **Designer de Classe** não usará o nome de marca que você especificar. Ele usará o nome gerado pelo Modo de Exibição de Classe. A classe ou a estrutura aparece no Modo de Exibição de Classe e no **Designer de Classe** como um elemento chamado **__unnamed**.

Para obter mais informações sobre classes anônimas, consulte [Tipos de classe anônima](/cpp/cpp/anonymous-class-types).

## <a name="template-classes"></a>Classes de modelo

O **Designer de Classe** é compatível com a visualização de classes de modelo. Declarações aninhadas têm suporte. A tabela a seguir mostra algumas declarações típicas.


| Elemento de código | Modo de exibição do Designer de Classe |
| - | - |
| `template <class T>`<br /><br /> `class A {};` | `A<T>`<br /><br /> Classe de modelo |
| `template <class T, class U>`<br /><br /> `class A {};` | `A<T, U>`<br /><br /> Classe de modelo |
| `template <class T, int i>`<br /><br /> `class A {};` | `A<T, i>`<br /><br /> Classe de modelo |
| `template <class T, template <class K> class U>`<br /><br /> `class A {};` | `A<T, U>`<br /><br /> Classe de modelo |

A tabela a seguir mostra alguns exemplos de especialização parcial.

|Elemento de código|Modo de exibição do Designer de Classe|
|------------------| - |
|`template<class T, class U>`<br /><br /> `class A {};`|`A<T, U>`<br /><br /> Classe de modelo|
|`template<class T>`<br /><br /> `class A<T, T> {};`|`A<T, T>`<br /><br /> Classe de modelo|
|`template <class T>`<br /><br /> `class A<T, int> {};`|`A<T, int>`<br /><br /> Classe de modelo|
|`template <class T1, class T2>`<br /><br /> `class A<T1*, T2*> {};`|`A<T1*, T2*>`<br /><br /> Classe de modelo|

A tabela a seguir mostra alguns exemplos de herança na especialização parcial.

|Elemento de código|Modo de exibição do Designer de Classe|
|------------------| - |
|`template <class T, class U>`<br /><br /> `class A {};`<br /><br /> `template <class TC>`<br /><br /> `class A<T, int> {};`<br /><br /> `class B : A<int, float>`<br /><br /> `{};`<br /><br /> `class C : A<int, int>`<br /><br /> `{};`|`A<T, U>`<br /><br /> Classe de modelo<br /><br /> `B`<br /><br /> Classe<br /><br /> (aponta para a Classe A)<br /><br /> `C`<br /><br /> Classe<br /><br /> (aponta para a Classe A)|

A tabela a seguir mostra alguns exemplos de funções de modelo de especialização parcial.

|Elemento de código|Modo de exibição do Designer de Classe|
|------------------| - |
|`class A`<br /><br /> `{`<br /><br /> `template <class T, class U>`<br /><br /> `void func(T a, U b);`<br /><br /> `template <class T>`<br /><br /> `void func(T a, int b);`<br /><br /> `};`|`A`<br /><br /> func\<T, U> (+ 1 de sobrecarga)|
|`template <class T1>`<br /><br /> `class A {`<br /><br /> `template <class T2>`<br /><br /> `class B {};`<br /><br /> `};`<br /><br /> `template<> template<>`<br /><br /> `class A<type>::B<type> {};`|`A<T1>`<br /><br /> Classe de modelo<br /><br /> `B<T2>`<br /><br /> Classe de modelo<br /><br /> (B está contido na classe A em **Tipos Aninhados**)|
|`template <class T>`<br /><br /> `class C {};`<br /><br /> `class A : C<int> {};`|`A`<br /><br /> Classe<br /><br /> -> C\<int><br /><br /> `C<T>`<br /><br /> Classe de modelo|

A tabela a seguir mostra alguns exemplos de herança de modelo.

|Elemento de código|Modo de exibição do Designer de Classe|
|------------------| - |
|`template <class T>`<br /><br /> `class C {};`<br /><br /> `template<>`<br /><br /> `class C<int> {`<br /><br /> `class B {};`<br /><br /> `}`<br /><br /> `class A : C<int>::B {};`|`A`<br /><br /> Classe<br /><br /> ->B<br /><br /> `C<int>`<br /><br /> Classe<br /><br /> (B está contido na classe C em **Tipos Aninhados**)<br /><br /> `C<T>`<br /><br /> Classe de modelo|

A tabela a seguir mostra alguns exemplos de conexões de classe especializada canônicas.

|Elemento de código|Modo de exibição do Designer de Classe|
|------------------| - |
|`template <class T>`<br /><br /> `class C {};`<br /><br /> `template<>`<br /><br /> `class C<int> {};`<br /><br /> `class A : C<int> {};`<br /><br /> `class D : C<float> {};`|`A`<br /><br /> Classe<br /><br /> ->C\<int><br /><br /> `C<int>`<br /><br /> Classe<br /><br /> `C<T>`<br /><br /> Classe de modelo<br /><br /> `D`<br /><br /> Classe<br /><br /> ->C\<float>|
|`class B {`<br /><br /> `template <class T>`<br /><br /> `T min (const T &a, const T &b);`<br /><br /> `};`|`B`<br /><br /> min \<T>|

## <a name="see-also"></a>Consulte também

- [Trabalhando com código do Visual C++](working-with-visual-cpp-code.md)
- [Classes e Structs](/cpp/cpp/classes-and-structs-cpp)
- [Tipos de classe anônima](/cpp/cpp/anonymous-class-types)
- [Herança múltipla](https://msdn.microsoft.com/library/6td5yws2.aspx)
- [Classes base múltiplas](/cpp/cpp/multiple-base-classes)
- [Modelos](/cpp/cpp/templates-cpp)