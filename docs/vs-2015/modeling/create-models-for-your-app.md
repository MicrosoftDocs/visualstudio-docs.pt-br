---
title: Criar modelos para seu aplicativo | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-tfs-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-devops-techdebt
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- vs.teamarch.common.commentlink.properties
- vs.teamarch.UMLModelExplorer.dependency
- vs.teamarch.UMLModelExplorer.commentlink
- vs.teamarch.common.dependency.properties
- Microsoft.VisualStudio.Uml.Diagrams.CommentShape.IsTransparent
- vs.teamarch.common.comment.properties
- vs.teamarch.UMLModelExplorer.comment
helpviewer_keywords:
- diagrams - modeling, sequence
- software design
- diagrams - modeling, use case
- diagrams - modeling, component
- diagrams - modeling, UML component
- UML model
- diagrams - modeling, UML use case
- diagrams - modeling, class
- diagrams - modeling, activity
- diagrams - modeling, UML activity
- software modeling
- diagrams - modeling, UML sequence
- UML
- diagrams - modeling, UML
- diagrams - modeling, layer
- software, designing
- diagrams - modeling, UML class
- software, modeling
- UML diagrams
ms.assetid: b69d9d91-c7e7-4dee-8eb6-706076eecb85
caps.latest.revision: 60
author: gewarren
ms.author: gewarren
manager: douge
ms.openlocfilehash: 9e3aa389441914121493148ecb8fa45b9f86beed
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51745133"
---
# <a name="create-models-for-your-app"></a>Criar modelos para o aplicativo
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Diagramas de modelagem ajudarão-lo a entender, esclarecer e comunicar ideias sobre seu código e os requisitos de usuário que deve oferecer suporte a seu sistema de software. Por exemplo, para descrever e comunicar requisitos do usuário, você pode usar o caso de uso (UML Unified Modeling Language), atividade, classe e diagramas de sequência. Para descrever e comunicar a funcionalidade de seu sistema, você pode usar o componente, classe, atividade e diagramas de sequência UML.  
  
 Ver [vídeo do Channel 9: melhorar a arquitetura com modelagem](http://go.microsoft.com/fwlink/?LinkID=252078).  
  
 Você pode criar os seguintes diagramas UML nesta versão:  
  
|**Diagrama**|**programas**|  
|-----------------|---------------|  
|[Diagramas de atividade UML: referência](../modeling/uml-activity-diagrams-reference.md)|Fluxo de trabalho entre ações e participantes em um processo comercial|  
|[Diagramas de componente UML: referência](../modeling/uml-component-diagrams-reference.md)|Componentes de um sistema, suas interfaces, portas e relações|  
|[Diagramas de classe UML: referência](../modeling/uml-class-diagrams-reference.md)|Tipos que são usados para armazenar e troca de dados no sistema e suas relações|  
|[Diagramas de sequência UML: referência](../modeling/uml-sequence-diagrams-reference.md)|Sequências de interações entre objetos, componentes, sistemas ou atores|  
|[Diagramas de caso de uso UML: referência](../modeling/uml-use-case-diagrams-reference.md)|Metas de usuário e tarefas que dá suporte a um sistema|  
  
 Para ver quais versões do Visual Studio dão suporte a cada tipo de diagrama, consulte [suporte de versão para a arquitetura e ferramentas de modelagem](../modeling/what-s-new-for-design-in-visual-studio.md#VersionSupport).  
  
 Para visualizar a arquitetura de um sistema ou o código existente, crie diagramas a seguir:  
  
|**Diagrama**|**programas**|  
|-----------------|---------------|  
|[Diagramas de camada: diretrizes](../modeling/layer-diagrams-guidelines.md)<br /><br /> [Diagramas de camada: referência](../modeling/layer-diagrams-reference.md)|Arquitetura de alto nível do sistema|  
|Mapas de código<br /><br /> [Mapear as dependências nas soluções](../modeling/map-dependencies-across-your-solutions.md)<br /><br /> [Encontrar possíveis problemas usando analisadores de mapa de códigos](../modeling/find-potential-problems-using-code-map-analyzers.md)|Dependências e outros relacionamentos no código existente|  
|Diagramas de classe do código gerado<br /><br /> [Trabalhando com diagramas de classe (Designer de Classe)](../ide/working-with-class-diagrams-class-designer.md)|Tipos e suas relações no código do .NET|  
  
## <a name="common-tasks"></a>Tarefas comuns  
  
|**Tópico**|**Tarefa**|  
|---------------|--------------|  
|[Criar projetos e diagramas de modelagem UML](../modeling/create-uml-modeling-projects-and-diagrams.md)|**Criar modelos** e adicionar diagramas.|  
|[Editar modelos e diagramas UML](../modeling/edit-uml-models-and-diagrams.md)|**Desenhar diagramas** para editar o modelo.|  
|[Definir pacotes e namespaces](../modeling/define-packages-and-namespaces.md)|**Criar pacotes** para dividir um modelo em unidades diferentes membros da equipe podem trabalhar em.|  
|[Gerar código por meio de diagramas de classe UML](../modeling/generate-code-from-uml-class-diagrams.md)|**Gerar o código c# de diagramas de classe** para iniciar sua implementação.|  
|[Personalizar o modelo com perfis e estereótipos](../modeling/customize-your-model-with-profiles-and-stereotypes.md)|**Personalizar elementos de modelo** usando estereótipos, para estender os elementos de modelo UML padrão para fins específicos.|  
|[Vincular elementos de modelo e itens de trabalho](../modeling/link-model-elements-and-work-items.md)|**Criar links entre elementos de modelo e itens de trabalho** para ajudar você a acompanhar tarefas, casos de teste, bugs, requisitos, problemas ou outros tipos de trabalho que estão associados a partes específicas do seu modelo.|  
|[Exportar diagramas como imagens](../modeling/export-diagrams-as-images.md)|**Salvar o modelo e os diagramas** para que você pode compartilhá-los com outros usuários, incluindo aqueles que não use [!INCLUDE[vsUltShort](../includes/vsultshort-md.md)].|  
  
## <a name="related-tasks"></a>Tarefas relacionadas  
  
|**Tópico**|**Tarefa**|  
|---------------|--------------|  
|[Visualizar código](../modeling/visualize-code.md)|Criar mapas de código e diagramas de camada para melhor compreendam o código não familiar.|  
|[Requisitos de usuário do modelo](../modeling/model-user-requirements.md)|Use modelos para esclarecer e comunicar as necessidades de usuários.|  
|[Modelar a arquitetura do aplicativo](../modeling/model-your-app-s-architecture.md)|Use modelos para descrever a estrutura geral e o comportamento do seu sistema e certifique-se de que ele atenda às necessidades dos usuários.|  
|[Validar o sistema durante o desenvolvimento](../modeling/validate-your-system-during-development.md)|Certifique-se de que seu software permaneça consistente com suas necessidades de usuários e a arquitetura geral do seu sistema.|  
|[Usar modelos no processo de desenvolvimento](../modeling/use-models-in-your-development-process.md)<br /><br /> [Usar modelos no desenvolvimento Agile](http://msdn.microsoft.com/en-us/592ac27c-3d3e-454a-9c38-b76658ed137f)|Use modelos para ajudá-lo a entender e alterar o seu sistema durante seu desenvolvimento.|  
|[Estruturar a solução de modelagem](../modeling/structure-your-modeling-solution.md)|Organize modelos em um projeto grande ou médio.|  
  
## <a name="external-resources"></a>Recursos externos  
  
|**Categoria**|**Links**|  
|------------------|---------------|  
|**Fóruns**|-   [Visualização do Visual Studio e ferramentas de modelagem](http://go.microsoft.com/fwlink/?LinkId=184720)<br />-   [Visualização do Visual Studio e modelagem (ferramentas DSL) do SDK](http://go.microsoft.com/fwlink/?LinkId=184721)|



