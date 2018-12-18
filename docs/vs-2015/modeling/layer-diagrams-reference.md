---
title: 'Diagramas de camada: Referência | Microsoft Docs'
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-tfs-dev14
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- vs.teamarch.layerdiagram.layerexplorer.artifactlink
- vs.teamarch.layerdiagram.layerexplorer.artifactlink.properties
- vs.teamarch.layerdiagram.diagram
- vs.teamarch.UMLModelExplorer.layerdiagram
- vs.teamarch.layerdiagram.layerexplorer
- vs.teamarch.layerdiagram.shapes.properties
- vs.teamarch.layerdiagram.toolbox
helpviewer_keywords:
- architecture, layer diagrams
- layer diagrams
- diagrams - modeling, layer
- constraints, architectural
ms.assetid: f26c986c-1e79-420e-b29a-a283e6d8a71d
caps.latest.revision: 35
author: gewarren
ms.author: gewarren
manager: douge
ms.openlocfilehash: 904b92a058b8fb50f3f2e53f093f4add3730dfbf
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51783214"
---
# <a name="layer-diagrams-reference"></a>Diagramas de camada: referência
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

No Visual Studio, você pode usar um *diagrama de camada* para visualizar a arquitetura lógica de alto nível do sistema. Um diagrama de camada organiza os artefatos físicos no seu sistema em grupos abstratos, lógicos, chamados *camadas*. Essas camadas descrevem tarefas principais realizadas pelos artefatos ou os principais componentes do seu sistema. Cada camada também pode conter camadas aninhadas que descrevem tarefas mais detalhadas.  
  
 Para ver quais versões do Visual Studio dão suporte a esse recurso, consulte [suporte de versão para a arquitetura e ferramentas de modelagem](../modeling/what-s-new-for-design-in-visual-studio.md#VersionSupport).  
  
 Você pode especificar as dependências desejadas ou existentes entre camadas. Essas dependências, que são representadas como setas, indicam quais camadas podem usar ou atualmente usam a funcionalidade representada por outras camadas. Organizando seu sistema em camadas que descrevem funções distintas e funções, um diagrama de camada pode ajudar a tornar mais fácil para você entender, reutilizar e manter seu código.  
  
 Use um diagrama de camada para ajudá-lo a executar as seguintes tarefas:  
  
- Comunicar-se a arquitetura lógica existente ou pretendida de seu sistema.  
  
- Descubra os conflitos entre o código existente e a arquitetura pretendida.  
  
- Visualize o impacto das alterações na arquitetura pretendida quando refatorar, atualizar ou evoluir seu sistema.  
  
- Reforce a arquitetura pretendida durante o desenvolvimento e manutenção do seu código, incluindo validação com seu check-in e operações de compilação.  
  
  Este tópico descreve os elementos que você pode usar em um diagrama de camada. Para obter mais informações sobre como criar e desenhar diagramas de camada, consulte [diagramas de camada: diretrizes](../modeling/layer-diagrams-guidelines.md). Para obter mais informações sobre padrões de disposição em camadas, visite o [site padrões & práticas](http://go.microsoft.com/fwlink/?LinkId=145794).  
  
## <a name="reading-layer-diagrams"></a>Diagramas de camada de leitura  
 ![Elementos em diagramas de camada](../modeling/media/uml-layerrefreading.png "UML_LayerRefReading")  
  
 A tabela a seguir descreve os elementos que você pode usar em um diagrama de camada.  
  
|**Forma**|**Elemento**|**Descrição**|  
|---------------|-----------------|---------------------|  
|1|**Camada**|Um grupo lógico de artefatos físicos no seu sistema. Esses artefatos podem ser namespaces, projetos, classes, métodos e assim por diante.<br /><br /> Para ver os artefatos que estão vinculados a uma camada, abra o menu de atalho para a camada e, em seguida, escolha **Exibir Links** para abrir **Gerenciador de camadas**.<br /><br /> Para obter mais informações, consulte [Gerenciador de camadas](#Explorer).<br /><br /> -   **Proibido dependências de Namespace** -Especifica que artefatos associados a essa camada não podem depender de namespaces especificados.<br />-   **Proibido Namespaces** -Especifica que os artefatos associados a essa camada não devem pertencer aos namespaces especificados.<br />-   **Necessário Namespaces** -Especifica que os artefatos associados a essa camada devem pertencer a um dos namespaces especificados.|  
|2|**dependência**|Indica que uma camada pode usar a funcionalidade em outra camada, mas não vice-versa.<br /><br /> -   **Direção** -Especifica a direção da dependência.|  
|3|**Dependência bidirecional**|Indica que uma camada pode usar a funcionalidade em outra camada e vice-versa.<br /><br /> -   **Direção** -Especifica a direção da dependência.|  
|4|**Comentário**|Use para adicionar observações gerais para o diagrama ou os elementos no diagrama.|  
|5|**Link de comentário**|Use para vincular comentários aos elementos no diagrama.|  
  
##  <a name="Explorer"></a> Gerenciador de camadas  
 Você pode vincular cada camada para artefatos em sua solução, como projetos, classes, namespaces, arquivos de projeto e outras partes do seu software. O número em uma camada mostra o número de artefatos que estão associados à camada. No entanto, ao ler o número de artefatos em uma camada, lembre-se do seguinte:  
  
- Se uma camada estiver vinculada a um artefato que contenha outros artefatos, mas não estiver vinculada diretamente a outros artefatos, o número incluirá apenas o artefato vinculado. No entanto, os outros artefatos estão incluídos para análise durante a validação da camada.  
  
   Por exemplo, se uma camada estiver vinculada a um único namespace, o número de artefatos vinculados será 1, mesmo se o namespace contiver classes. Se a camada também tiver links para cada classe no namespace, o número incluirá as classes vinculadas.  
  
- Se uma camada contiver outras camadas vinculadas a artefatos, a camada de contêiner também estará vinculada a esses artefatos, mesmo que o número na camada de contêiner não inclua esses artefatos.  
  
  Para obter mais informações sobre a vinculação de camadas e artefatos, consulte:  
  
- [Diagramas de camada: diretrizes](../modeling/layer-diagrams-guidelines.md)  
  
- [Criar diagramas de camada por meio de código](../modeling/create-layer-diagrams-from-your-code.md)  
  
#### <a name="to-examine-the-linked-artifacts"></a>Para examinar os artefatos vinculados  
  
-   No diagrama de camada, abra o menu de atalho para uma ou mais camadas e, em seguida, escolha **Exibir Links**.  
  
     **Gerenciador de camada** é aberta e mostra os artefatos que são vinculados para as camadas selecionadas. **Gerenciador de camada** tem uma coluna que mostra cada uma das propriedades dos links de artefato.  
  
    > [!NOTE]
    >  Se você não vir todas essas propriedades, expanda o **Gerenciador de camadas** janela.  
  
    |**Coluna no Gerenciador de camadas**|**Descrição**|  
    |----------------------------------|---------------------|  
    |**Categorias**|O tipo de artefato, como uma classe, namespace, arquivo de origem e assim por diante|  
    |**Camada**|A camada que contém links para o artefato|  
    |**Dá suporte à validação**|Se **verdadeira**, em seguida, o processo de validação de camada pode verificar que o projeto está de acordo com as dependências de ou para este elemento.<br /><br /> Se **falsos**, em seguida, o link não participa no processo de validação de camada.<br /><br /> Para obter mais informações, consulte [diagramas de camada: diretrizes](../modeling/layer-diagrams-guidelines.md).|  
    |**Identificador**|A referência para o artefato vinculado|  
  
## <a name="see-also"></a>Consulte também  
 [Criar modelos para o aplicativo](../modeling/create-models-for-your-app.md)



