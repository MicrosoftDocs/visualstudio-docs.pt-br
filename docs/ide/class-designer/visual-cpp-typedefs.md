---
title: Typedefs do Visual C++ no Designer de Classe
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-ide-general
ms.topic: conceptual
f1_keywords:
- vs.classdesigner.typedef
- vs.classdesigner.aliasofline
helpviewer_keywords:
- Class Designer [Visual Studio], typedefs
ms.assetid: c1984108-71fc-4d3a-b4d4-3eac2c6b4ebf
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- cplusplus
ms.openlocfilehash: 6eb831422df42a246a5d5c23ccdd480bce47a0e6
ms.sourcegitcommit: 4c0db930d9d5d8b857d3baf2530ae89823799612
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/10/2018
ms.locfileid: "33958328"
---
# <a name="visual-c-typedefs-in-class-designer"></a>Typedefs do Visual C++ no Designer de Classe

As instruções [typedef](/cpp/cpp/aliases-and-typedefs-cpp#typedefs) criam uma ou mais camadas de indireção entre um nome e seu tipo subjacente. O **Designer de Classe** é compatível com tipos de typedef do C++ declarados com a palavra-chave `typedef`, por exemplo:

```cpp
typedef class coord
{
   void P(x,y);
   unsigned x;
   unsigned y;
} COORD;
```

Então, você pode usar esse tipo para declarar uma instância:

`COORD OriginPoint;`

## <a name="class-and-struct-shapes"></a>Formas de classe e de struct

No **Designer de Classe**, um typedef do C++ tem a forma do tipo especificado no typedef. Se a fonte declarar `typedef class`, a forma terá cantos arredondados e o rótulo **Classe**. Para `typedef struct`, a forma tem cantos quadrados e o rótulo **Struct**.

Classes e estruturas podem ter typedefs aninhados declarados dentro delas. No **Designer de Classe**, formas de classe e de estrutura podem mostrar declarações de typedef aninhado como formas aninhadas.

As formas typedef dão suporte aos comandos **Mostrar como Associação** e **Mostrar como Associação de Coleções** no menu de contexto.

### <a name="class-typedef-example"></a>Exemplo do typedef de classe

```cpp
class B {};
typedef B MyB;
```

![Typedef de classe do C++ no Designer de Classe](media/cpp-class-typedef.png)

### <a name="struct-typedef-example"></a>Exemplo do typedef de struct

```cpp
typedef struct mystructtag
{
    int   i;
    double f;
} mystruct;
```

![Typedef de struct do C++ no Designer de Classe](media/cpp-struct-typedef.png)

## <a name="unnamed-typedefs"></a>Typedefs sem nome

Embora seja possível declarar um typedef sem um nome, o **Designer de Classe** não usará o nome da marca especificada. O **Designer de Classe** use o nome gerado pelo **Modo de Exibição de Classe**. Por exemplo, a declaração a seguir é válida, mas ela aparece no **Modo de Exibição de Classe** e no **Designer de Classe** como um objeto chamado **__unnamed**:

```cpp
typedef class coord
{
   void P(x,y);
   unsigned x;
   unsigned y;
};
```

> [!NOTE]
> O **Designer de Classe** não exibe typedefs cujo tipo de origem é um ponteiro de função.

## <a name="see-also"></a>Consulte também

- [Trabalhar com o código do Visual C++](working-with-visual-cpp-code.md)
- [Typedefs](/cpp/cpp/aliases-and-typedefs-cpp#typedefs)