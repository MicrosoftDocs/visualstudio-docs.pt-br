---
title: Ler modelos e diagramas em outras edições do Visual Studio | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-tfs-dev14
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- models, versions of Visual Studio
ms.assetid: 46eee279-a9e4-4742-a024-5bd2cf032b86
caps.latest.revision: 22
author: gewarren
ms.author: gewarren
manager: douge
ms.openlocfilehash: 6d104d8d92345ba56d390fdd7ad9b856432b4c92
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51757363"
---
# <a name="read-models-and-diagrams-in-other-visual-studio-editions"></a>Ler modelos e diagramas em outras edições do Visual Studio
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Quando você abre um modelo em uma versão do Visual Studio que não dá suporte à criação de modelo, o modelo é aberto no modo somente leitura. Nesse modo, você pode alterar o layout dos diagramas, mas você não pode alterar o modelo.  
  
 Para ver quais versões do Visual Studio dão suporte a criação de modelos, consulte [suporte de versão para a arquitetura e ferramentas de modelagem](../modeling/what-s-new-for-design-in-visual-studio.md#VersionSupport).  
  
## <a name="obtaining-access-to-a-model-and-diagrams"></a>Obtendo acesso a um modelo e diagramas  
 Para ler um diagrama UML ou em um diagrama de camada, você deve primeiro usar o Visual Studio para abrir o projeto de modelagem e, em seguida, abra o diagrama dentro dele.  
  
 Por esse motivo, se você quiser ler um diagrama UML ou diagrama de camada, deve também ter acesso ao projeto de modelagem no qual ele foi criado. Você pode fazer isso acessando o projeto do [!INCLUDE[esprscc](../includes/esprscc-md.md)], ou obtendo uma cópia dos arquivos de projeto.  
  
> [!NOTE]
>  Isso não se aplica ao código gerados a partir de código de diagramas de classe de mapas e .NET. Esses diagramas podem ser exibidos independentemente de um projeto de modelagem.  
  
 Para ler um diagrama UML ou em um diagrama de camada, o conjunto mínimo de arquivos que você precisa é da seguinte maneira:  
  
-   Os dois arquivos para o diagrama que você deseja ler, por exemplo, de diagrama **MyDiagram.classdiagram e MyDiagram.classdiagram.layout**.  
  
    > [!NOTE]
    >  Para obter diagramas de camada, você também deve ter o arquivo chamado _MyDiagram_**. layerdiagram.suppressions**.  
  
-   Arquivo de projeto de modelagem (**MyModel.modelproj**)  
  
-   O arquivo de modelo de raiz (**ModelDefinition\MyModel.uml**)  
  
-   Os arquivos de pacote para qualquer pacote referenciado no diagrama (**ModelDefinition\MyPackage.uml**)  
  
## <a name="changes-that-you-can-make-in-read-only-mode"></a>Alterações que você pode fazer no modo somente leitura  
 Se você abrir um modelo e seus diagramas em uma versão do Visual Studio que não dá suporte à criação de modelo, você não pode alterar o modelo. Ou seja, você não pode alterar os elementos e relações que são exibidas em diagramas ou no Gerenciador de modelos. No entanto, você pode fazer algumas alterações no layout dos diagramas:  
  
- Reorganize as formas e conectores no diagrama.  
  
- Expandir e recolher formas.  
  
  Você pode salvar essas alterações. Se você quiser fazer as alterações visíveis para outros usuários, você deve pelo menos enviar atualizada **. layout** arquivos.  
  
##  <a name="RelatedTopics"></a> Tópicos relacionados  
  
|Título|Descrição|  
|-----------|-----------------|  
|[Diagramas de camada: referência](../modeling/layer-diagrams-reference.md)|Um diagrama de camada mostra a estrutura de uma arquitetura existente ou proposta. Quando o código é escrito, ele pode ser automaticamente validado em relação a um diagrama de camada.|  
|[Diagramas de atividade UML: referência](../modeling/uml-activity-diagrams-reference.md)|Um diagrama de atividade mostra um fluxo de trabalho, em um processo comercial ou no software.|  
|[Diagramas de classe UML: referência](../modeling/uml-class-diagrams-reference.md)|Um diagrama de classe mostra os tipos e relações usadas em muitos contextos, como código, os esquemas de banco de dados, protocolos de comunicação ou o Glossário de termos usados para descrever um domínio de negócios.|  
|[Diagramas de componente UML: referência](../modeling/uml-component-diagrams-reference.md)|Um diagrama de componente mostra partes separáveis em um design de software e suas interfaces.|  
|[Diagramas de sequência UML: referência](../modeling/uml-sequence-diagrams-reference.md)|Um diagrama de sequência mostra as interações entre os elementos em um design de software.|  
|[Diagramas de caso de uso UML: referência](../modeling/uml-use-case-diagrams-reference.md)|Um diagrama de caso de uso mostra os usuários de um sistema e as atividades que realizam para atingir metas específicas.|  
  
## <a name="see-also"></a>Consulte também  
 [Criar modelos para o aplicativo](../modeling/create-models-for-your-app.md)



