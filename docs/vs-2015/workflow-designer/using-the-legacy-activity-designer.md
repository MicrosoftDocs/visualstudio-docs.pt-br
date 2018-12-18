---
title: Usando o Designer de atividade herdado | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: .net-framework-4.6
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- activities, configuring
- custom activities
- Activity Designer
- child activities, adding
- activities, adding child
- activities, creating custom
ms.assetid: 2fea8a05-6e58-423d-94bf-a822b15ffb80
caps.latest.revision: 5
author: gewarren
ms.author: gewarren
manager: erikre
ms.openlocfilehash: a6c8aafe9eac26080bfbf57d06c7d512d1e1e62d
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49843425"
---
# <a name="using-the-legacy-activity-designer"></a>Usando o designer herdado de atividades
Este tópico descreve como usar o designer de atividade em [!INCLUDE[wfd1](../includes/wfd1-md.md)]herdado. Use o designer herdado na definição [!INCLUDE[netfx35_long](../includes/netfx35-long-md.md)] ou [!INCLUDE[vstecwinfx](../includes/vstecwinfx-md.md)].  
  
 O designer de atividade permite que você crie suas próprias atividades personalizados.  
  
## <a name="creating-a-custom-activity"></a>Criando uma atividade personalizado  
 Siga estas etapas para criar uma atividade personalizado utilizando o designer de atividade:  
  
1. Sobre o **Project** menu, clique em **Adicionar atividade**.  
  
2. Selecione o **atividade** ou **atividade (com separação de código)** modelo.  
  
   1.  Use o **atividade** modelo para criar uma atividade com a definição de atividade e o código do usuário no mesmo arquivo de código.  
  
   2.  Use o **atividade (com separação de código)** modelo para criar uma atividade com a definição de atividade expressada como a marcação de fluxo de trabalho e o código do usuário em um arquivo separado código.  
  
3. Digite um nome de atividade ou mantenha o nome padrão e, em seguida, clique em **adicionar**.  
  
   Você também pode criar um conjunto de atividades personalizadas, criando um novo projeto do tipo **biblioteca de atividades de fluxo de trabalho**. Para obter mais informações sobre esse tipo de projeto, consulte [como: criar uma biblioteca de atividades de fluxo de trabalho (herdado)](../workflow-designer/how-to-create-a-workflow-activity-library-legacy.md).  
  
## <a name="configuring-an-activity"></a>Configurando uma atividade  
 Quando o designer de atividade estiver ativo, você pode usar o navegador de propriedade para configurar as propriedades listadas na tabela a seguir.  
  
|Propriedade|Comentários|  
|--------------|--------------|  
|**Nome**|Nome da atividade.|  
|**Classe base**|Classe base que a atividade deriva. A classe base padrão é [SequenceActivity](http://go.microsoft.com/fwlink?LinkID=65020). No **propriedades** janela, clique no **classe base** elipses **[...]**  para selecionar outra classe base em de [navegue e selecione uma caixa de diálogo do tipo .NET (herdado)](../workflow-designer/browse-and-select-a-dotnet-type-dialog-box-legacy.md).|  
|**Descrição**|Descrição definido pelo usuário de atividade.|  
|**Habilitado**|Definido como **verdadeira** por padrão para habilitar a validação e execução da atividade. Definido como **falsos** para desabilitar a validação e execução da atividade. Para obter informações sobre validação e execução da atividade, consulte [atividades de fluxo de trabalho de desenvolvimento](http://go.microsoft.com/fwlink?LinkID=65024).|  
  
## <a name="adding-child-activities"></a>Adicionando atividades filhos  
 Você pode arrastar atividades filhos da caixa de ferramentas para a atividade que você está criando. Você pode então configurar cada atividade filho usando o navegador de propriedade.  
  
## <a name="see-also"></a>Consulte também  
 [Desenvolvimento de atividades de fluxo de trabalho](http://go.microsoft.com/fwlink?LinkID=65024)   
 [Criação de atividades personalizadas](http://go.microsoft.com/fwlink?LinkID=65021)   
 [Atividades de fluxo de trabalho herdado](../workflow-designer/legacy-workflow-activities.md)   
 [Exemplos de atividades personalizadas](http://go.microsoft.com/fwlink?LinkID=65022)   
 [Como: criar uma biblioteca de atividades de fluxo de trabalho (herdado)](../workflow-designer/how-to-create-a-workflow-activity-library-legacy.md)   
 [Usando o Designer de Fluxo de Trabalho herdado](../workflow-designer/using-the-legacy-workflow-designer.md)