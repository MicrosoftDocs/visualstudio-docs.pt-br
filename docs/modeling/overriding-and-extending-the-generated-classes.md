---
title: Substituindo e estendendo as classes geradas
description: Saiba como sua Definição de DSL é uma plataforma na qual você pode criar um conjunto poderoso de ferramentas baseadas em um idioma específico do domínio.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Domain-Specific Language, providing overridable classes
author: mgoertz-msft
ms.author: mgoertz
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 07c44e7ff7a603f339ec268b06bd78cc84cd6be2
ms.sourcegitcommit: e3a364c014ccdada0860cc4930d428808e20d667
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2021
ms.locfileid: "112390939"
---
# <a name="override-and-extend-the-generated-classes"></a>Substituir e estender as classes geradas

Sua Definição de DSL é uma plataforma na qual você pode criar um conjunto poderoso de ferramentas baseadas em uma linguagem específica do domínio. Muitas extensões e adaptações podem ser feitas substituindo e estendendo as classes geradas a partir da definição de DSL. Essas classes incluem não apenas as classes de domínio que você definiu explicitamente no diagrama de Definição de DSL, mas também outras classes que definem a caixa de ferramentas, o explorer, a serialização e assim por diante.

## <a name="extensibility-mechanisms"></a>Mecanismos de extensibilidade

Vários mecanismos são fornecidos para permitir que você estenda o código gerado.

### <a name="override-methods-in-a-partial-class"></a>Substituir métodos em uma classe parcial

Definições de classe parciais permitem que uma classe seja definida em mais de um local. Isso permite separar o código gerado do código que você escreve por conta própria. No código escrito manualmente, você pode substituir classes herdadas pelo código gerado.

Por exemplo, se na definição de DSL você definir uma classe de domínio chamada , você poderá escrever código personalizado que `Book` adiciona métodos de substituição:

```csharp
public partial class Book
{
   protected override void OnDeleting()
   {
      MessageBox.Show("Deleting book " + this.Title);
      base.OnDeleting();
   }
}
```

> [!NOTE]
> Para substituir métodos em uma classe gerada, sempre escreva seu código em um arquivo separado dos arquivos gerados. Normalmente, o arquivo está contido em uma pasta chamada CustomCode. Se você fizer alterações no código gerado, elas serão perdidas quando você regenerar o código da Definição de DSL.

Para descobrir quais métodos você pode substituir, digite **override** na classe , seguido por um espaço. A dica de ferramenta do IntelliSense lhe dirá quais métodos podem ser substituídos.

### <a name="double-derived-classes"></a>Double-Derived classes

A maioria dos métodos em classes geradas é herdada de um conjunto fixo de classes nos namespaces de Modelagem. No entanto, alguns métodos são definidos no código gerado. Normalmente, isso significa que você não pode substituí-los; você não pode substituir em uma classe parcial os métodos definidos em outra definição parcial da mesma classe.

No entanto, você pode substituir esses métodos definindo o sinalizador **Gera Derivada** Dupla para a classe de domínio. Isso faz com que duas classes sejam geradas, uma sendo uma classe base abstrata da outra. Todos os métodos e definições de propriedade estão na classe base e apenas o construtor está na classe derivada.

Por exemplo, no library.dsl de exemplo, a classe `CirculationBook` de domínio tem a propriedade definida como `Generates``Double Derived` `true` . O código gerado para essa classe de domínio contém duas classes:

- `CirculationBookBase`, que é um abstrato e que contém todos os métodos e propriedades.

- `CirculationBook`, que é derivado de `CirculationBookBase` . Ele está vazio, exceto para seus construtores.

Para substituir qualquer método, crie uma definição parcial da classe derivada, como `CirculationBook` . Você pode substituir os métodos gerados e os métodos herdados da estrutura de modelagem.

Você pode usar esse método com todos os tipos de elemento, incluindo elementos de modelo, relações, formas, diagramas e conectores. Você também pode substituir métodos de outras classes geradas. Algumas classes geradas, como ToolboxHelper, sempre são derivadas duplas.

### <a name="custom-constructors"></a>Construtores personalizados

Não é possível substituir um construtor. Mesmo em classes derivadas duplas, o construtor deve estar na classe derivada.

Se você quiser fornecer seu próprio construtor, poderá fazer isso definindo para a classe de domínio `Has Custom Constructor` na Definição de DSL. Quando você clicar **em Transformar Todos os Modelos**, o código gerado não incluirá um construtor para essa classe. Ele incluirá uma chamada para o construtor ausente. Isso causa um relatório de erros quando você cria a solução. Clique duas vezes no relatório de erros para ver um comentário no código gerado que explica o que você deve fornecer.

Escreva uma definição de classe parcial em um arquivo separado dos arquivos gerados e forneça o construtor.

### <a name="flagged-extension-points"></a>Pontos de extensão sinalizados

Um ponto de extensão sinalizado é um local na Definição de DSL em que você pode definir uma propriedade ou uma caixa de seleção para indicar que fornecerá um método personalizado. Construtores personalizados são um exemplo. Outros exemplos incluem definir o de uma propriedade de domínio como Armazenamento Calculado ou Personalizado ou definir o sinalizador `Kind` **É** Personalizado em um construtor de conexões.

Em cada caso, quando você definir o sinalizador e regenerar o código, um erro de build resultará. Clique duas vezes no erro para ver um comentário que explica o que você precisa fornecer.

### <a name="rules"></a>Regras

O gerenciador de transações permite que você defina regras que são executados antes do final de uma transação na qual ocorreu um evento designado, como uma alteração em uma propriedade. As regras normalmente são usadas para manter o sincronismo entre diferentes elementos no armazenamento. Por exemplo, as regras são usadas para certificar-se de que o diagrama exibe o estado atual do modelo.

As regras são definidas por classe, de modo que você não precisa ter um código que registre a regra para cada objeto. Para obter mais informações, consulte [Regras propagam alterações dentro do modelo](../modeling/rules-propagate-changes-within-the-model.md).

### <a name="store-events"></a>Eventos da Loja

O armazenamento de modelagem fornece um mecanismo de evento que você pode usar para escutar tipos específicos de alteração no armazenamento, incluindo adição e exclusão de elementos, alterações em valores de propriedade e assim por diante. Os manipuladores de eventos são chamados após o fechamento da transação na qual as alterações foram feitas. Normalmente, esses eventos são usados para atualizar recursos fora do armazenamento.

### <a name="net-events"></a>Eventos do .NET

Você pode assinar alguns eventos em formas. Por exemplo, você pode escutar cliques do mouse em uma forma. Você precisa escrever um código que assine o evento para cada objeto. Esse código pode ser escrito em uma substituição de InitializeInstanceResources().

Alguns eventos são gerados em ShapeFields, que são usados para desenhar decoradores em uma forma. Para ver um exemplo, [consulte Como interceptar um clique em uma forma ou decorador.](../modeling/how-to-intercept-a-click-on-a-shape-or-decorator.md)

Esses eventos geralmente não ocorrem dentro de uma transação. Você deverá criar uma transação se quiser fazer alterações no armazenamento.
