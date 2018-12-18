---
title: Descrever o fluxo de controle com fragmentos em diagramas de sequência UML | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-tfs-dev14
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- vs.teamarch.sequencediagram.combinedfragment.interactionoperand
- vs.teamarch.sequencediagram.combinedfragment
helpviewer_keywords:
- UML sequence diagrams, control flow
- UML sequence diagrams, fragments
- sequence diagrams, fragments
- sequence diagrams, control flow
ms.assetid: efcc0949-be7e-4cf4-99ef-47c36b3803ae
caps.latest.revision: 17
author: gewarren
ms.author: gewarren
manager: douge
ms.openlocfilehash: 4ab4c65e554e9eef75a1761719ce19f3312e07ce
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51727656"
---
# <a name="describe-control-flow-with-fragments-on-uml-sequence-diagrams"></a>Descrever o fluxo de controle com fragmentos em diagramas de sequência UML
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Em um diagrama de sequência UML *fragmentos combinados* permitem que você mostre outras alternativas, ramificações e loops.  
  
 Um fragmento combinado consiste em um ou mais *operandos de interação*, e cada um deles inclui um ou mais mensagens, usos de interação ou fragmentos combinados.  
  
> [!NOTE]
>  Este tópico é sobre fragmentos em diagramas de sequência. Para obter mais informações sobre como ler diagramas de sequência UML, consulte [diagramas de sequência UML: referência](../modeling/uml-sequence-diagrams-reference.md). Para obter mais informações sobre como desenhar diagramas de sequência UML, consulte [diagramas de sequência UML: diretrizes](../modeling/uml-sequence-diagrams-guidelines.md).  
  
 ![Combinados fragmento com dois operandos de interação](../modeling/media/uml-seqfragments.png "UML_SeqFragments")  
  
 Os elementos mostrados na figura são da seguinte maneira.  
  
1.  Um fragmento combinado. Há vários tipos de fragmentos combinados. Este exemplo é um Alt fragmento combinado que você pode usar para mostrar que a alternativas sequências de mensagens podem ocorrer.  
  
2.  Operandos de interação. Cada fragmento combinado contém pelo menos um operando de interação, que pode conter mensagens, usos de interação e menores fragmentos combinados. Neste exemplo, a tecla Alt combinadas fragmento tem duas operações de interação, mostrando duas sequências alternativas de mensagens.  
  
3.  Você pode selecionar cada operando de interação separadamente clicando nele. Neste exemplo, o operando de interação superior é selecionado, para que seu limite pode ser visto. Normalmente, somente as linhas divisórias entre os operandos de interação é visível.  
  
    > [!NOTE]
    >  Para selecionar o operando de interação superior, você deve clicar em muito próximas à parte superior do fragmento combinado.  
  
4.  Protege. Você pode dar um protetor de cada operando de interação. Descreve a condição sob a qual as mensagens dentro do operando de interação serão executadas.  
  
## <a name="creating-combined-fragments"></a>Criando fragmentos combinados  
 Para obter uma lista dos tipos de fragmento, você pode criar, consulte [tipos de fragmento combinado](#KindsOfFragment).  
  
#### <a name="to-create-a-combined-fragment"></a>Para criar um fragmento combinado  
  
1. Selecione uma mensagem ou uma sequência de mensagens, que tudo comece na ocorrência de linha da vida ou execução mesma.  
  
   > [!NOTE]
   >  Se você selecionar mais de uma mensagem, eles devem formar uma sequência ininterrupta.  
  
2. Clique em uma das mensagens, aponte para **envolver com**e, em seguida, clique em tipo de fragmento combinado que você deseja, tal como **fragmento combinado de Alt**.  
  
    Um novo fragmento combinado é exibida. O cabeçalho indica o tipo de fragmento combinado que você selecionou, tais como **Alt**.  
  
    Dentro do fragmento combinado, há um fragmento que contém as mensagens que você selecionou.  
  
   Você pode adicionar mais operandos de interação a alguns tipos de fragmento combinado.  
  
   Depois que você reorganizar mensagens dentro de um fragmento combinado, escolha **reorganizar Layout** no menu de atalho para redimensionar o quadro de fragmento combinado.  
  
#### <a name="to-add-a-new-interaction-operand-to-a-combined-fragment"></a>Para adicionar um novo operando de interação para um fragmento combinado  
  
1. Clique com botão direito em um espaço em branco dentro do operando de interação (2), fora de qualquer fragmento independente e abaixo do título do fragmento combinado.  
  
2. Aponte para **adicionar**.  
  
3. Clique em **operando de interação antes**, ou **interação operando após**.  
  
4. Você pode adicionar mensagens dentro do novo operando de interação usando as ferramentas de mensagem, ou copiando e colando as mensagens existentes.  
  
   Você pode definir as **Guard** propriedade de um operando de interação para descrever as condições em que as mensagens dentro dele são executadas. Por exemplo, em um **Loop** combinados fragmento, você pode usar a proteção para especificar a condição durante o qual o loop continua. Em um **Alt** combinado de fragmento, você pode especificar uma condição separada para cada operando de interação.  
  
#### <a name="to-set-the-guard-of-an-interaction-operand"></a>Para definir o protetor de um operando de interação  
  
1. Clique em um espaço em branco dentro do operando de interação (2), fora de qualquer fragmento independente.  
  
    Uma borda de seleção aparece em torno do operando de interação e a condição de proteção.  
  
    O título na **propriedades** janela mostra **operando de interação**.  
  
2. Digite a condição de proteção.  
  
    A condição será exibida na parte superior do fragmento (4).  
  
   Você pode definir as propriedades de alguns tipos de fragmentos combinados.  
  
#### <a name="to-set-or-view-the-properties-of-a-combined-fragment"></a>Para definir ou exibir as propriedades de um fragmento combinado  
  
-   Clique com botão direito no título do fragmento combinado e, em seguida, clique em **propriedades**.  
  
    > [!NOTE]
    >  Tipos diferentes de fragmento combinado têm propriedades diferentes.  
  
##  <a name="KindsOfFragment"></a> Tipos de fragmento combinado  
  
### <a name="fragments-describing-control-flow"></a>Fragmentos que descreve o fluxo de controle  
 Um diagrama de sequência simples mostra apenas uma sequência típica. Você pode usar os seguintes tipos de fragmentos combinados para descrever as variações que podem ocorrer em ocasiões diferentes.  
  
|Tipo de fragmento|Descrição|  
|-------------------|-----------------|  
|**aceitar**|Opcional. Inclui uma sequência que podem ou não pode acontecer. Você pode especificar, em que a proteção, a condição sob a qual ele ocorre.|  
|**Alt**|Contém uma lista de fragmentos que contêm sequências alternativas de mensagens. Apenas uma sequência ocorre em qualquer ocasião.<br /><br /> Você pode colocar uma proteção em cada fragmento para indicar sob qual condição ele pode ser executado. Um protetor de **else** indica um fragmento que deve ser executado se nenhuma outra guard é true. Se todas as proteções forem falsas e não há nenhuma **else**, em seguida, nenhum dos fragmentos executa.|  
|**Loop**|O fragmento é repetida várias vezes. Você pode indicar em que o protetor da condição sob a qual ele deve ser repetida.<br /><br /> Fragmentos combinados de loop têm as propriedades **Min** e **Max**, que indicam o número mínimo e máximo de vezes que o fragmento pode ser repetido. O padrão é sem restrição.|  
|**quebra**|Se esse fragmento é executado, o restante da sequência é abandonado. Você pode usar o protetor para indicar a condição na qual ocorrerá a interrupção.|  
|**Par**|Paralelo. Os eventos em fragmentos podem ser intercalados.|  
|**Crítico**|Usado dentro de um fragmento de mesmo nível ou Seq. Indica que as mensagens desse fragmento não devem ser intercaladas com outras mensagens.|  
|**SEQ**|Há dois ou mais fragmentos do operando. As mensagens que envolvam a mesma linha da vida devem ocorrer na ordem de fragmentos. Em que eles não envolvem as mesmas linhas da vida, mensagens de diferentes fragmentos podem ser intercaladas em paralelo.|  
|**Strict**|Há dois ou mais fragmentos do operando. Os fragmentos devem ocorrer na ordem fornecida.|  
  
### <a name="fragments-about-how-to-interpret-the-sequence"></a>Fragmentos sobre como interpretar a sequência  
 Por padrão, o diagrama de sequência estabelece uma série de mensagens que podem ocorrer. No sistema em execução, outras mensagens podem acontecer se você não tenha escolhido Mostrar no diagrama.  
  
 Os seguintes tipos de fragmento podem ser usados para alterar essa interpretação.  
  
|Tipo de fragmento|Descrição|  
|-------------------|-----------------|  
|**Considere**|Especifica uma lista das mensagens que descreve esse fragmento. Outras mensagens podem ocorrer no sistema em execução, mas não são significativas para os fins desta descrição.<br /><br /> Digite a lista na **mensagens** propriedade.|  
|**Ignorar**|Uma lista das mensagens que não descreve esse fragmento. Eles podem ocorrer no sistema em execução, mas não são significativos para os fins desta descrição.<br /><br /> Digite a lista na **mensagens** propriedade.|  
|**Assert**|O fragmento de operando Especifica as sequências são válidas. Normalmente usado dentro de um fragmento considere ou ignorar.|  
|**Neg**|A sequência mostrada neste fragmento não deve ocorrer. Normalmente usado dentro de um fragmento considere ou ignorar.|  
  
## <a name="see-also"></a>Consulte também  
 [Diagramas de sequência UML: diretrizes](../modeling/uml-sequence-diagrams-guidelines.md)   
 [Diagramas de sequência UML: referência](../modeling/uml-sequence-diagrams-reference.md)   
 [Editar modelos e diagramas UML](../modeling/edit-uml-models-and-diagrams.md)



