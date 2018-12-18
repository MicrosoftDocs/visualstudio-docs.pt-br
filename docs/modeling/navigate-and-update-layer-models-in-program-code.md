---
title: Navegar e atualizar modelos de camada no código do programa
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- layer models, navigating in program code
- layer models, updating in program code
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.prod: visual-studio-dev15
ms.technology: vs-ide-modeling
ms.openlocfilehash: 8ca10b8504dc4383ad6251e3819c14b7102d32d3
ms.sourcegitcommit: ef828606e9758c7a42a2f0f777c57b2d39041ac3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/06/2018
ms.locfileid: "39566733"
---
# <a name="navigate-and-update-layer-models-in-program-code"></a>Navegar e atualizar modelos de camada no código do programa

Este artigo descreve os elementos e relações em modelos de camada, o que você pode navegar e atualizar usando o código do programa. Para obter mais informações sobre diagramas de dependência do ponto de vista do usuário, consulte [diagramas de dependência: referência](../modeling/layer-diagrams-reference.md) e [diagramas de dependência: diretrizes](../modeling/layer-diagrams-guidelines.md).

O <xref:Microsoft.VisualStudio.ArchitectureTools.Extensibility.Layer> modelo descrito neste tópico é uma fachada em um mais geral <xref:Microsoft.VisualStudio.GraphModel> modelo. Se você estiver escrevendo uma [extensão de gesto ou comando de menu](../modeling/add-commands-and-gestures-to-layer-diagrams.md), use o `Layer` modelo. Se você estiver escrevendo uma [extensão de validação de camada](../modeling/add-custom-architecture-validation-to-layer-diagrams.md), é mais fácil de usar o `GraphModel`.

## <a name="transactions"></a>Transações

Quando você atualiza um modelo, considere incluir as alterações em um `ILinkedUndoTransaction`, que agrupa as alterações em uma transação. Se qualquer uma das alterações falhar, toda a transação será revertida. Se o usuário desfizer uma alteração, todas as alterações serão desfeitas em conjunto.

```csharp
using (ILinkedUndoTransaction t =
        LinkedUndoContext.BeginTransaction("a name"))
{
    // Make changes here ....
    t.Commit(); // Don't forget this!
}
```

## <a name="containment"></a>Confinamento

![ILayer e ILayerModel podem conter ILayers.](../modeling/media/layerapi_containment.png)

As camadas (<xref:Microsoft.VisualStudio.ArchitectureTools.Extensibility.Layer.ILayer>) e o modelo de camada (<xref:Microsoft.VisualStudio.ArchitectureTools.Extensibility.Layer.ILayerModel>) podem conter Comentários e Camadas.

Uma camada (`ILayer`) pode estar contida em um modelo de camada (`ILayerModel`) ou pode ser aninhada em outra `ILayer`.

Para criar um comentário ou uma camada, use os métodos de criação no contêiner apropriado.

## <a name="dependency-links"></a>Vínculos de dependência

Um vínculo de dependência é representado por um objeto. Ele pode ser navegado em qualquer direção:

![Um ILayerDependencyLink conecta dois ILayers.](../modeling/media/layerapi_dependency.png)

Para criar um vínculo de dependência, chame `source.CreateDependencyLink(target)`.

## <a name="comments"></a>Comentários

Os comentários podem ser encontrados dentro de camadas ou do modelo de camada e também podem ser vinculados a qualquer elemento de camada:

![Comentários podem ser anexados a qualquer elemento de camada.](../modeling/media/layerapi_comments.png)

Um comentário pode ser vinculado a qualquer número de elementos, incluindo zero.

Para obter os comentários anexados a um elemento de camada, use:

```csharp
ILayerModel model = diagram.GetLayerModel();
IEnumerable<ILayerComment> comments =
   model.Comments.Where(comment =>
      comment.Links.Any(link => link.Target == layerElement));
```

> [!CAUTION]
> A propriedade `Comments` de uma `ILayer` recebe comentários que estão contidos na `ILayer`. Não recebe os comentários vinculados a ela.

Criar um comentário chamando `CreateComment()` no contêiner apropriado.

Crie um link usando `CreateLink()` no comentário.

## <a name="layer-elements"></a>Elementos de camada

Todos os tipos de elementos que podem estar contidos em um modelo são elementos de camada:

![conteúdo do diagrama de dependência é ILayerElements.](../modeling/media/layerapi_layerelements.png)

## <a name="properties"></a>Propriedades

Cada `ILayerElement` tem um dicionário de cadeia chamado `Properties`. Você pode usar este dicionário para anexar informações arbitrárias a qualquer elemento da camada.

## <a name="artifact-references"></a>Referências de artefato

Uma referência de artefato (<xref:Microsoft.VisualStudio.ArchitectureTools.Extensibility.Layer.ILayerArtifactReference>) representa um vínculo entre uma camada e um item de projeto, como um arquivo, classe ou pasta. O usuário cria artefatos quando criar uma camada ou adicionar a ele arrastando itens do Gerenciador de soluções, exibição de classe ou Pesquisador de objetos para um diagrama de dependência. Qualquer número de referências de artefato pode ser vinculado a uma camada.

Cada linha do Gerenciador de Camadas exibe uma referência de artefato. Para obter mais informações, consulte [criar diagramas de dependência do seu código](../modeling/create-layer-diagrams-from-your-code.md).

Os principais tipos e métodos relacionados a referências de artefato são os seguintes:

<xref:Microsoft.VisualStudio.ArchitectureTools.Extensibility.Layer.ILayerArtifactReference>. A propriedade Categorias indica que tipo de artefato é referenciado, tal como uma classe, arquivo executável ou assembly. A propriedade categorias determina como o identificador identifica o artefato de destino.

<xref:Microsoft.VisualStudio.ArchitectureTools.Extensibility.Layer.ArtifactReferenceExtensions.CreateArtifactReferenceAsync%2A> cria uma referência de artefato de um <xref:EnvDTE.Project> ou <xref:EnvDTE.ProjectItem>. Esta é uma operação assíncrona. Portanto, você geralmente fornece um retorno de chamada que é chamado quando a criação for concluída.

Referências de artefato de camada são diferentes para artefatos em diagramas de caso de uso.

## <a name="shapes-and-diagrams"></a>Formas e diagramas

Dois objetos são usados para representar cada elemento em um modelo de camadas: um <xref:Microsoft.VisualStudio.ArchitectureTools.Extensibility.Layer.ILayerElement> e um <xref:Microsoft.VisualStudio.ArchitectureTools.Extensibility.Presentation.IShape>. O `IShape` representa a posição e o tamanho da forma no diagrama. Nos modelos de camadas, cada `ILayerElement` tem um `IShape`e cada `IShape` em uma dependência diagrama tem um `ILayerElement`. `IShape` também é usado para modelos UML. Portanto, nem todo `IShape` tem um elemento de camada.

Da mesma maneira, o <xref:Microsoft.VisualStudio.ArchitectureTools.Extensibility.Layer.ILayerModel> é exibido em um <xref:Microsoft.VisualStudio.ArchitectureTools.Extensibility.Presentation.IDiagram>.

No código de um comando personalizado ou manipulador de gestos, você pode obter o diagrama atual e a seleção atual de formas da importação do `DiagramContext`:

```csharp
public class ... {
[Import]
    public IDiagramContext DiagramContext { get; set; }
...
public void ... (...)
{ IDiagram diagram = this.DiagramContext.CurrentDiagram;
  ILayerModel model = diagram.GetLayerModel();
  if (model != null)
  { foreach (ILayer layer in model.Layers) { ... }}
  foreach (IShape selected in diagram.SelectedShapes)
  { ILayerElement element = selected.GetLayerElement();
    if (element != null) ... }}
```

![Cada ILayerElement é apresentado por um IShape.](../modeling/media/layerapi_shapes.png)

<xref:Microsoft.VisualStudio.ArchitectureTools.Extensibility.Presentation.IShape> e <xref:Microsoft.VisualStudio.ArchitectureTools.Extensibility.Presentation.IDiagram> também são usados para exibir modelos UML.

## <a name="see-also"></a>Consulte também

- [Adicionar comandos e gestos aos diagramas de dependência](../modeling/add-commands-and-gestures-to-layer-diagrams.md)
- [Adicionar validação de arquitetura personalizada a diagramas de dependência](../modeling/add-custom-architecture-validation-to-layer-diagrams.md)
- [Adicionar propriedades personalizadas a diagramas de dependência](../modeling/add-custom-properties-to-layer-diagrams.md)
- [Diagramas de dependência: referência](../modeling/layer-diagrams-reference.md)
- [Diagramas de dependência: diretrizes](../modeling/layer-diagrams-guidelines.md)
