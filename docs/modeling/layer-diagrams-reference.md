---
title: Referência de diagramas de dependência
description: Saiba que, Visual Studio, você pode usar um diagrama de dependência para visualizar a arquitetura lógica de alto nível do sistema.
ms.custom: SEO-VS-2020
ms.date: 09/28/2018
ms.topic: reference
f1_keywords:
- vs.teamarch.layerdiagram.layerexplorer.artifactlink
- vs.teamarch.layerdiagram.layerexplorer.artifactlink.properties
- vs.teamarch.layerdiagram.diagram
- vs.teamarch.UMLModelExplorer.layerdiagram
- vs.teamarch.layerdiagram.layerexplorer
- vs.teamarch.layerdiagram.shapes.properties
- vs.teamarch.layerdiagram.toolbox
helpviewer_keywords:
- architecture, dependency diagrams
- dependency diagrams
- diagrams - modeling, layer
- constraints, architectural
author: mgoertz-msft
ms.author: mgoertz
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 6bb138164cfab44778c932a4bcb93572a3053a70
ms.sourcegitcommit: e3a364c014ccdada0860cc4930d428808e20d667
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2021
ms.locfileid: "112391030"
---
# <a name="dependency-diagrams-reference"></a>Diagramas de dependência: referência

No Visual Studio, você pode usar um diagrama de *dependência* para visualizar a arquitetura lógica de alto nível do sistema. Um diagrama de dependência organiza os artefatos físicos em seu sistema em grupos lógicos abstratos chamados *camadas*. Essas camadas descrevem as principais tarefas que os artefatos executam ou os principais componentes do sistema. Cada camada também pode conter camadas aninhadas que descrevem tarefas mais detalhadas.

Para ver quais edições do Visual Studio suporte a esse recurso, confira [Suporte à edição para ferramentas de arquitetura e modelagem](../modeling/analyze-and-model-your-architecture.md#VersionSupport).

> [!NOTE]
> Há suporte para diagramas de dependência para projetos do .NET Core Visual Studio 2019 versão 16.2.

Você pode especificar as dependências pretendido ou existente entre camadas. Essas dependências, representadas como setas, indicam quais camadas podem ser usadas ou atualmente usam a funcionalidade representada por outras camadas. Ao organizar seu sistema em camadas que descrevem funções e funções distintas, um diagrama de dependência pode ajudar a facilitar o entendimento, a reutilização e a manutenção do código.

Use um diagrama de dependência para ajudá-lo a executar as seguintes tarefas:

- Comunique a arquitetura lógica existente ou pretendido do seu sistema.

- Descubra conflitos entre o código existente e a arquitetura pretendido.

- Visualize o impacto das alterações na arquitetura pretendido ao refactorar, atualizar ou evoluir seu sistema.

- Reforce a arquitetura pretendida durante o desenvolvimento e a manutenção do código, incluindo a validação com suas operações de check-in e build.

Este tópico descreve os elementos que você pode usar em um diagrama de dependência. Para obter informações mais detalhadas sobre como criar e desenhar diagramas de dependência, consulte [Diagramas de dependência: Diretrizes](../modeling/layer-diagrams-guidelines.md). Para obter mais informações sobre padrões de camadas, visite o [site Padrões & Práticas](https://archive.codeplex.com/?p=apparch).

## <a name="reading-dependency-diagrams"></a>Lendo diagramas de dependência

![Elementos em diagramas de dependência](../modeling/media/uml_layerrefreading.png)

A tabela a seguir descreve os elementos que você pode usar em um diagrama de dependência.

|**Forma**|**Element**|**Descrição**|
|-|-|-|
|1|**Camada**|Um grupo lógico de artefatos físicos em seu sistema. Esses artefatos podem ser namespaces, projetos, classes, métodos e assim por diante.<br /><br /> Para ver os artefatos vinculados a uma camada, abra o menu de atalho da camada e escolha Exibir **Links** para abrir o **Layer Explorer.**<br /><br /> Para obter mais informações, consulte [Layer Explorer](#Explorer).<br /><br /> -   **Dependências de namespace proibidas** – especifica que os artefatos associados a essa camada não podem depender dos namespaces especificados.<br />-   **Namespaces proibidos** – especifica que os artefatos associados a essa camada não devem pertencer aos namespaces especificados.<br />-   **Namespaces necessários** – especifica que os artefatos associados a essa camada devem pertencer a um dos namespaces especificados.|
|2|**Dependência**|Indica que uma camada pode usar a funcionalidade em outra camada, mas não vice-versa.<br /><br /> -   **Direção** – especifica a direção da dependência.|
|3|**Dependência bidirecional**|Indica que uma camada pode usar a funcionalidade em outra camada e vice-versa.<br /><br /> -   **Direção** – especifica a direção da dependência.|
|4|**Comentário**|Use para adicionar observações gerais ao diagrama ou elementos no diagrama.|
|5|**Link de comentário**|Use para vincular comentários a elementos no diagrama.|

## <a name="layer-explorer"></a><a name="Explorer"></a> Layer Explorer

Você pode vincular cada camada a artefatos em sua solução, como projetos, classes, namespaces, arquivos de projeto e outras partes do seu software. O número em uma camada mostra o número de artefatos que estão vinculados à camada. No entanto, ao ler o número de artefatos em uma camada, lembre-se do seguinte:

- Se uma camada estiver vinculada a um artefato que contenha outros artefatos, mas não estiver vinculada diretamente a outros artefatos, o número incluirá apenas o artefato vinculado. No entanto, os outros artefatos estão incluídos para análise durante a validação da camada.

     Por exemplo, se uma camada estiver vinculada a um único namespace, o número de artefatos vinculados será 1, mesmo se o namespace contiver classes. Se a camada também tiver links para cada classe no namespace, o número incluirá as classes vinculadas.

- Se uma camada contiver outras camadas vinculadas a artefatos, a camada de contêiner também estará vinculada a esses artefatos, mesmo que o número na camada de contêiner não inclua esses artefatos.

Para obter mais informações sobre como vincular camadas e artefatos, consulte:

- [Diagramas de dependência: diretrizes](../modeling/layer-diagrams-guidelines.md)

- [Criar diagramas de dependência do código](../modeling/create-layer-diagrams-from-your-code.md)

### <a name="examine-the-linked-artifacts"></a>Examinar os artefatos vinculados

No diagrama de dependência, abra o menu de atalho de uma ou mais camadas e escolha **Exibir Links**.

**O Layer Explorer** é aberto e mostra os artefatos vinculados às camadas selecionadas. **O Layer Explorer** tem uma coluna que mostra cada uma das propriedades dos links de artefato.

> [!NOTE]
> Se você não conseguir ver todas essas propriedades, expanda a janela **Explorador de** Camadas.

|**Coluna no Layer Explorer**|**Descrição**|
|-|-|
|**Categorias**|O tipo de artefato, como uma classe, namespace, arquivo de origem e assim por diante|
|**Camada**|A camada que se vincula ao artefato|
|**Dá suporte à validação**|Se **True**, o processo de validação de camada poderá verificar se o projeto está em conformidade com as dependências desse elemento.<br /><br /> Se **False**, o link não participará do processo de validação de camada.<br /><br /> Para obter mais informações, consulte [Diagramas de dependência: Diretrizes](../modeling/layer-diagrams-guidelines.md).|
|**Identificador**|A referência ao artefato vinculado|

## <a name="see-also"></a>Confira também

- [Criar modelos para o aplicativo](../modeling/create-models-for-your-app.md)
