---
title: Substituindo e estendendo as Classes geradas | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-tfs-dev14
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Domain-Specific Language, providing overridable classes
ms.assetid: 30baa60d-a8ea-4611-96c1-8fcc3317cf21
caps.latest.revision: 17
author: gewarren
ms.author: gewarren
manager: douge
ms.openlocfilehash: a5aef90403babfd7a30812cac59b8c0c5acff79f
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49933424"
---
# <a name="overriding-and-extending-the-generated-classes"></a>Substituindo e estendendo as classes geradas
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Sua definição de DSL é uma plataforma na qual você pode criar um conjunto poderoso de ferramentas com base em uma linguagem específica de domínio. Muitas extensões e adaptações podem ser feitas substituindo e estendendo as classes que são geradas a partir da definição de DSL. Essas classes incluem não apenas as classes de domínio que você definiu explicitamente no diagrama de definição de DSL, mas também outras classes que definem a caixa de ferramentas, explorer, serialização e assim por diante.  
  
## <a name="extensibility-mechanisms"></a>Mecanismos de extensibilidade  
 Vários mecanismos são fornecidos para permitir que você estenda o código gerado.  
  
### <a name="overriding-methods-in-a-partial-class"></a>Substituindo métodos em uma classe parcial  
 Definições de classes parciais permitem que uma classe seja definida em mais de um único lugar. Isso permite que você separe o código gerado do código que você escreve. Em seu código escrito manualmente, você pode substituir as classes herdadas pelo código gerado.  
  
 Por exemplo, se em sua definição de DSL, você define uma classe de domínio chamada `Book`, você pode escrever código personalizado que adiciona métodos de substituição:  
  
 `public partial class Book`  
  
 `{`  
  
 `protected override void OnDeleting()`  
  
 `{`  
  
 `MessageBox.Show("Deleting book " + this.Title);`  
  
 `base.OnDeleting();`  
  
 `} }`  
  
> [!NOTE]
>  Para substituir métodos em uma classe gerada, sempre escreva seu código em um arquivo separado dos arquivos gerados. Normalmente, o arquivo está contido em uma pasta chamada CustomCode. Se você fizer alterações no código gerado, eles serão perdidos quando você regenera o código da definição de DSL.  
  
 Para descobrir quais você pode substituir os métodos, digite **substituir** na classe, seguido por um espaço. A dica de ferramenta do IntelliSense informará quais métodos podem ser substituídos.  
  
### <a name="double-derived-classes"></a>Classes derivadas de duplo  
 A maioria dos métodos de classes geradas é herdada de um conjunto fixo de classes nos namespaces de modelagem. No entanto, alguns métodos são definidos no código gerado. Normalmente, isso significa que você não pode substituí-los; Você não pode substituir em uma classe parcial os métodos que são definidos em outra definição parcial da mesma classe.  
  
 No entanto, você pode substituir esses métodos, definindo o **gera derivado duplo** sinalizador para a classe de domínio. Este faz com que duas classes a ser gerado, um sendo uma classe base abstrata da outra. Todas as definições de método e propriedade estão na classe base, e somente o construtor é na classe derivada.  
  
 Por exemplo, no exemplo Library.dsl, o `CirculationBook` classe de domínio tem o `Generates``Double Derived` propriedade definida como `true`. O código gerado para essa classe de domínio contém duas classes:  
  
- `CirculationBookBase`, que é um resumo e que contém todos os métodos e propriedades.  
  
- `CirculationBook`, que é derivado de `CirculationBookBase`. Ele está vazio, exceto seus construtores.  
  
  Para substituir qualquer método, você cria uma definição parcial da classe derivada, como `CirculationBook`. Você pode substituir os métodos gerados e os métodos herdados da estrutura de modelagem.  
  
  Você pode usar esse método com todos os tipos de elemento, incluindo conectores, relações, formas, diagramas e elementos de modelo. Você também pode substituir métodos de outras classes geradas. Algumas classes geradas, como o ToolboxHelper sempre são derivados de double.  
  
### <a name="custom-constructors"></a>Construtores personalizados  
 Você não pode substituir um construtor. Mesmo em classes derivadas de duplo, o construtor deve ser na classe derivada.  
  
 Se você quiser fornecer seu próprio construtor, você pode fazer isso definindo `Has Custom Constructor` para a classe de domínio na definição de DSL. Quando você clica em **transformar todos os modelos**, o código gerado não incluirá um construtor para essa classe. Ele incluirá uma chamada para o construtor ausente. Isso faz com que um relatório de erros quando você compila a solução. Clique duas vezes o relatório de erros para ver um comentário no código gerado que explica o que você deve fornecer.  
  
 Gravar uma definição de classe parcial em um arquivo separado dos arquivos gerados e forneça o construtor.  
  
### <a name="flagged-extension-points"></a>Pontos de extensão sinalizados  
 Um ponto de extensão sinalizados é um lugar na definição de DSL, onde é possível definir uma propriedade ou uma caixa de seleção para indicar que você fornecerá um método personalizado. Construtores personalizados são um exemplo. Outros exemplos incluem a configuração do `Kind` de uma propriedade de domínio para Calculated ou armazenamento personalizado ou configuração o **personalizado é** sinalizador em um construtor de conexão.  
  
 Em cada caso, quando você define o sinalizador e gerar novamente o código, compilação ocorrerá um erro. Clique duas vezes no erro para ver um comentário que explica o que você precisa fornecer.  
  
### <a name="rules"></a>Regras  
 O Gerenciador de transações permite que você defina regras que são executados antes do final de uma transação na qual um evento designado tenha ocorrido, como uma alteração em uma propriedade. As regras geralmente são usadas para manter synchronism entre os diferentes elementos no repositório. Por exemplo, as regras são usadas para certificar-se de que o diagrama exibe o estado atual do modelo.  
  
 As regras são definidas em uma base por classe, para que você não precise ter código que registra a regra para cada objeto. Para obter mais informações, consulte [propagam alterações dentro do modelo de regras](../modeling/rules-propagate-changes-within-the-model.md).  
  
### <a name="store-events"></a>Eventos de Store  
 O repositório de modelagem fornece um mecanismo de eventos que você pode usar para escutar para tipos específicos de alterações no repositório, incluindo a adição e a exclusão de elementos, alterações nos valores de propriedade e assim por diante. Os manipuladores de eventos são chamados após o encerramento da transação na qual as alterações foram feitas. Normalmente, esses eventos são usados para atualizar recursos fora do repositório.  
  
### <a name="net-events"></a>Eventos do .NET  
 Você pode assinar alguns eventos nas formas. Por exemplo, você pode escutar cliques do mouse em uma forma. Você precisa escrever código que assina o evento para cada objeto. Esse código pode ser escrito em uma substituição de InitializeInstanceResources().  
  
 Alguns eventos são gerados em ShapeFields, que são usados para desenhar os decoradores em uma forma. Por exemplo, consulte [como: interceptar um clique em uma forma ou um decorador](../modeling/how-to-intercept-a-click-on-a-shape-or-decorator.md).  
  
 Normalmente, esses eventos não ocorrem dentro de uma transação. Se você quiser fazer alterações no repositório, você deve criar uma transação.



