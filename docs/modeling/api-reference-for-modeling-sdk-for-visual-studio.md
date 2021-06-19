---
title: Referência de API para modelagem do SDK
description: Saiba como o SDK Visual Studio visualização e modelagem fornece a plataforma na qual as ferramentas DSLs (linguagens específicas do domínio) são criadas.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
author: mgoertz-msft
ms.author: mgoertz
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 9603ace5751443c04d0a7503a43e08c044269817
ms.sourcegitcommit: e3a364c014ccdada0860cc4930d428808e20d667
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2021
ms.locfileid: "112385455"
---
# <a name="api-reference-for-modeling-sdk-for-visual-studio"></a>Referência de API do SDK de Modelagem para Visual Studio

O Visual Studio SDK de Visualização e Modelagem fornece a plataforma na qual as ferramentas DSL (linguagens específicas do domínio) são criadas.

Esta seção contém material de referência para namespaces que têm nomes que começam com "Microsoft.VisualStudio.Modeling".

|Namespace|Conteúdo|
|-|-|
|<xref:Microsoft.VisualStudio.Modeling?displayProperty=fullName>|Classes como ModelElement, que é a classe base de todas as classes de domínio que você define em uma DSL.|
|<xref:Microsoft.VisualStudio.Modeling.Design?displayProperty=fullName>|Classes que fazem parte de uma definição de DSL.|
|<xref:Microsoft.VisualStudio.Modeling.Diagnostics?displayProperty=fullName>|O modelo Visualizador da Loja e ferramentas de medição de desempenho.|
|<xref:Microsoft.VisualStudio.Modeling.Diagrams?displayProperty=fullName>|Classes como ShapeElement, que é a classe base de todas as formas que você define em uma DSL.|
|<xref:Microsoft.VisualStudio.Modeling.Diagrams.ExtensionEnablement?displayProperty=fullName>|Métodos de gesto e seleção.|
|<xref:Microsoft.VisualStudio.Modeling.DslDefinition?displayProperty=fullName>|A API do designer de Definição de DSL.|
|<xref:Microsoft.VisualStudio.Modeling.DslDefinition.Design?displayProperty=fullName>|Classes internas do designer de Definição de DSL.|
|<xref:Microsoft.VisualStudio.Modeling.DslDefinition.ExtensionEnablement?displayProperty=fullName>|Atributos que permitem estender o designer DSL com comandos, gestos e validação.|
|<xref:Microsoft.VisualStudio.Modeling.Extensibility?displayProperty=fullName>|Métodos de extensão para ModelElement que implementam extensibilidade de DSL.|
|<xref:Microsoft.VisualStudio.Modeling.ExtensionEnablement?displayProperty=fullName>|Atributos de extensibilidade|
|<xref:Microsoft.VisualStudio.Modeling.Immutability?displayProperty=fullName>|Permite que você faça partes de um modelo somente leitura.|
|[Microsoft.VisualStudio.Modeling.Integration](/previous-versions/ee904412(v=vs.140))|A API do Modelbus, que ajuda você a integrar modelos diferentes.|
|[Microsoft.VisualStudio.Modeling.Integration.Picker](/previous-versions/ee904394(v=vs.140))|A caixa de diálogo que permite que os usuários naveguem até modelos e elementos para criar referências modelbus.|
|`Microsoft.VisualStudio.Modeling.Integration.Picker.Hosting`|O serviço Se picker.|
|[Microsoft.VisualStudio.Modeling.Integration.Shell](/previous-versions/ee869435(v=vs.140))|Estrutura de adaptador do Modelbus para Visual Studio.|
|[Microsoft.VisualStudio.Modeling.Integration.Shell.Picker](/previous-versions/ee886769(v=vs.140))|A caixa de diálogo Seletor que permite que os usuários naveguem até modelos e elementos para criar referências modelbus.|
|<xref:Microsoft.VisualStudio.Modeling.Shell?displayProperty=fullName>|A interface entre DSLs e Visual Studio.|
|<xref:Microsoft.VisualStudio.Modeling.Shell.ExtensionEnablement?displayProperty=fullName>|Permite definir comandos de menu de atalho (contexto).|
|<xref:Microsoft.VisualStudio.Modeling.Validation?displayProperty=fullName>|Permite definir restrições de validação.|

## <a name="see-also"></a>Confira também

- [Personalizando transformação de texto T4](../modeling/customizing-t4-text-transformation.md)
