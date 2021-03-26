---
title: Managed Extensibility Framework no editor | Microsoft Docs
description: Saiba mais sobre o Managed Extensibility Framework, que permite que você crie seus próprios componentes para estender o editor no SDK do Visual Studio.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], new - using MEF for extensions
ms.assetid: 3f59a285-6c33-4ae3-a4fb-ec1f5aa21bd1
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 881b0f4d112b7739ff33099b26a30ab073f55924
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105073164"
---
# <a name="managed-extensibility-framework-in-the-editor"></a>Managed Extensibility Framework no editor
O editor é criado usando componentes Managed Extensibility Framework (MEF). Você pode criar seus próprios componentes do MEF para estender o editor, e seu código também pode consumir componentes do editor.

## <a name="overview-of-the-managed-extensibility-framework"></a>Visão geral do Managed Extensibility Framework
 O MEF é uma biblioteca .NET que permite adicionar e modificar recursos de um aplicativo ou componente que segue o modelo de programação do MEF. O editor do Visual Studio pode fornecer e consumir partes do componente MEF.

 O MEF está contido no assembly do .NET Framework versão 4 *System.ComponentModel.Composition.dll* .

 Para obter mais informações sobre o MEF, consulte [Managed Extensibility Framework (MEF)](/dotnet/framework/mef/index).

### <a name="component-parts-and-composition-containers"></a>Partes de componentes e contêineres de composição
 Uma parte de componente é uma classe ou um membro de uma classe que pode fazer uma (ou ambas) das seguintes opções:

- Consumir outro componente

- Ser consumido por outro componente

  Por exemplo, considere um aplicativo de compras que tem um componente de entrada de pedido que depende dos dados de disponibilidade do produto fornecidos por um componente de inventário de depósito. Em termos do MEF, a parte de inventário pode *Exportar* dados de disponibilidade do produto e a parte de entrada do pedido pode *importar* os dados. A parte de entrada de pedidos e a parte de inventário não precisam se conhecer umas com as outras; o *contêiner de composição* (fornecido pelo aplicativo host) é responsável por manter o conjunto de exportações e resolver as exportações e importações.

  O contêiner de composição, <xref:System.ComponentModel.Composition.Hosting.CompositionContainer> , normalmente é de Propriedade do host. O contêiner de composição mantém um *Catálogo* de partes de componentes exportadas.

### <a name="export-and-import-component-parts"></a>Exportar e importar partes de componentes
 Você pode exportar qualquer funcionalidade, desde que ela seja implementada como uma classe pública ou um membro público de uma classe (Propriedade ou método). Você não precisa derivar a parte do componente do <xref:System.ComponentModel.Composition.Primitives.ComposablePart> . Em vez disso, você deve adicionar um <xref:System.ComponentModel.Composition.ExportAttribute> atributo à classe ou membro de classe que você deseja exportar. Esse atributo especifica o *contrato* pelo qual outra parte de componente pode importar sua funcionalidade.

### <a name="the-export-contract"></a>O contrato de exportação
 O <xref:System.ComponentModel.Composition.ExportAttribute> define a entidade (classe, interface ou estrutura) que está sendo exportada. Normalmente, o atributo de exportação usa um parâmetro que especifica o tipo da exportação.

```
[Export(typeof(ContentTypeDefinition))]
class TestContentTypeDefinition : ContentTypeDefinition {   }
```

 Por padrão, o <xref:System.ComponentModel.Composition.ExportAttribute> atributo define um contrato que é o tipo da classe de exportação.

```
[Export]
[Name("Structure")]
[Order(After = "Selection", Before = "Text")]
class TestAdornmentLayerDefinition : AdornmentLayerDefinition {   }
```

 No exemplo, o atributo padrão `[Export]` é equivalente a `[Export(typeof(TestAdornmentLayerDefinition))]` .

 Você também pode exportar uma propriedade ou um método, conforme mostrado no exemplo a seguir.

```
[Export]
[Name("Scarlet")]
[Order(After = "Selection", Before = "Text")]
public AdornmentLayerDefinition scarletLayerDefinition;
```

### <a name="import-a-mef-export"></a>Importar uma exportação do MEF
 Quando desejar consumir uma exportação de MEF, você deve saber o contrato (normalmente o tipo) pelo qual ele foi exportado e adicionar um <xref:System.ComponentModel.Composition.ImportAttribute> atributo com esse valor. Por padrão, o atributo de importação usa um parâmetro, que é o tipo da classe que ele modifica. As linhas de código a seguir importam o <xref:Microsoft.VisualStudio.Text.Classification.IClassificationTypeRegistryService> tipo.

```
[Import]
internal IClassificationTypeRegistryService ClassificationRegistry;
```

## <a name="get-editor-functionality-from-a-mef-component-part"></a>Obter a funcionalidade do editor de uma parte de componente do MEF
 Se o código existente for uma parte de componente do MEF, você poderá usar metadados do MEF para consumir partes do componente do editor.

#### <a name="to-consume-editor-functionality-from-a-mef-component-part"></a>Para consumir a funcionalidade do editor de uma parte de componente do MEF

1. Adicione referências a *System.Composition.ComponentModel.dll*, que está no GAC (cache de assembly global) e aos assemblies do editor.

2. Adicione as diretivas de uso relevantes.

    ```
    using System.ComponentModel.Composition;
    using Microsoft.VisualStudio.Text;
    ```

3. Adicione o `[Import]` atributo à sua interface de serviço da seguinte maneira.

    ```
    [Import]
    ITextBufferFactoryService textBufferService;
    ```

4. Depois de obter o serviço, você pode consumir qualquer um de seus componentes.

5. Depois de compilar o assembly, coloque-o no *.. \* Pasta \Common7\IDE\Components da instalação do Visual Studio.

## <a name="see-also"></a>Confira também
- [Pontos de extensão do serviço de linguagem e do editor](../extensibility/language-service-and-editor-extension-points.md)
