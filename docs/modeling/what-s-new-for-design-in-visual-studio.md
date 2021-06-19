---
title: Novidades no design no Visual Studio 2017
description: Saiba mais sobre os novos recursos para o design de código, como a validação de dependência ao vivo, que estão disponíveis no Visual Studio 2017.
ms.custom: SEO-VS-2020
titleSuffix: ''
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- what's new [Visual Studio], architecture and modeling
- architecture [Visual Studio], modeling
- modeling software [Visual Studio], What's New
author: mgoertz-msft
ms.author: mgoertz
manager: jmartens
ms.workload:
- multiple
monikerRange: vs-2017
ms.openlocfilehash: ed67836507d8328a4ba394986564820c6af7308f
ms.sourcegitcommit: e3a364c014ccdada0860cc4930d428808e20d667
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2021
ms.locfileid: "112388094"
---
# <a name="whats-new-for-design-in-visual-studio-2017"></a>Novidades no design no Visual Studio 2017

## <a name="live-dependency-validation"></a>Validação de dependência ao vivo

A remoção de dependências indesejadas é uma parte importante do gerenciamento da dívida técnica. O Visual Studio fornece validação dinâmica de dependências, incluindo informações precisas sobre problemas, como onde estão localizadas. A validação de dependência ao vivo aproveita todas as vantagens dos novos recursos no Lista de Erros e no editor.

![Validação de dependência ao vivo em ação](media/dep-validation-whatsnew-01.png)

A experiência de criação foi alterada para tornar a validação de dependência mais detectável e mais acessível. A terminologia mudou de "diagrama de camada" para "diagrama de dependência".

O menu **arquitetura** agora contém um comando para criar diretamente um diagrama de dependência:

![Item de dependência dinâmica no menu arquitetura](media/dep-validation-whatsnew-02.png)

Descrições e nomes de propriedade de camada foram alterados para torná-los mais significativos:

![Nomes de propriedade atualizados de dependência ao vivo](media/dep-validation-whatsnew-03.png)

Você verá imediatamente o impacto de suas alterações nos resultados da análise para o código atual na solução sempre que salvar o diagrama. Você não precisa aguardar a conclusão do comando **validar dependências** .

Para obter mais detalhes, consulte [esta postagem no blog](https://devblogs.microsoft.com/devops/live-architecture-dependency-validation-in-visual-studio-15-preview-5/).

## <a name="uml-designers-have-been-removed"></a>Os designers UML foram removidos

Os designers UML foram removidos do Visual Studio.

* Os diagramas UML agora são apresentados como arquivos XML
* O Gerenciador de modelos UML não existe mais
* As referências de projeto de modelagem não são mais usadas para validação de dependência
* O nó "referências de camada" no Gerenciador de Soluções não é mais exibido
* A ação de compilação "validar" em um diagrama de dependência (camada) não é mais usada-a tarefa de compilação foi removida
* A estrutura do projeto é mantida para ida e volta entre as versões
* Você ainda pode abrir, criar, editar e salvar um diagrama de dependência (camada) como XML
* Os itens de trabalho do TFS vinculados a um diagrama de dependência (camada) não estão acessíveis na superfície de design
* Não há mais suporte para a vinculação de volta do para DSL ou uma camada
* Não há mais suporte para a extensibilidade UML no SDK de modelagem

O suporte para visualizar a arquitetura do código .NET e C++ está disponível por meio de [mapas de código](map-dependencies-across-your-solutions.md).

Se você for um usuário significativo dos designers UML, poderá continuar usando o Visual Studio 2015 ou versões anteriores enquanto decide em uma ferramenta alternativa para suas necessidades de UML.

Para obter mais detalhes, consulte [esta postagem no blog](https://devblogs.microsoft.com/devops/uml-designers-have-been-removed-layer-designer-now-supports-live-architectural-analysis/).

[!INCLUDE[modeling_sdk_info](includes/modeling_sdk_info.md)]

## <a name="edition-support-for-architecture-and-modeling-tools"></a><a name="VersionSupport" />Suporte de edição para ferramentas de arquitetura e modelagem

O Visual Studio está disponível em várias edições. Nem todos eles oferecem suporte para as ferramentas de arquitetura e modelagem. A tabela a seguir mostra a disponibilidade de cada ferramenta.

|**Recurso**|**Enterprise Edition**|**Professional Edition**|**Community Edition**|
|-|-|-|-|
|**Mapas de código**|Sim|Dá suporte apenas à leitura de mapas de código, filtragem de mapas de código, adição de novos nós genéricos e criação de um novo grafo direcionado a partir de uma seleção.|-|
|**Diagramas de dependência**|Sim|Dá suporte apenas à leitura de diagramas de dependência.|Dá suporte apenas à leitura de diagramas de dependência.|
|**Grafos direcionados** (diagramas dgml)|Sim|Sim|Sim|
|**Clone de código**|Sim|-|-|
