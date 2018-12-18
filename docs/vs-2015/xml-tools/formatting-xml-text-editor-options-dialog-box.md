---
title: Formatação, XML, Editor de texto, caixa de diálogo Opções | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-general
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: bb539b3a-027c-4b2f-906e-403e0e22ba8d
caps.latest.revision: 9
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: 5c8379393dd5327359789f8621cf67ed55e89209
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49256666"
---
# <a name="formatting-xml-text-editor-options-dialog-box"></a>Formatação, XML, editor de texto, a caixa de diálogo opções
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

  
Esta caixa de diálogo permite que você especifique as configurações de formatação para o editor XML. Você pode acessar o **opções** caixa de diálogo do **ferramentas** menu.  
  
> [!NOTE]
>  Essas configurações estão disponíveis quando você seleciona os **Editor de texto** pasta, o **XML** pasta e, em seguida, o **formatação** opção o **opções** caixa de diálogo.  
  
## <a name="attributes"></a>Atributos  
 **Preservar formatação manual de atributos**  
 Os atributos não são reformatados. Esse é o padrão.  
  
> [!NOTE]
>  Se os atributos estão em várias linhas, o editor recua cada linha de atributos para coincidir com o recuo de elemento pai.  
  
 **Alinhar cada atributo em sua própria linha**  
 Alinha os segundos e atributos subsequentes verticalmente para coincidir com o recuo do primeiro atributo. O texto a seguir XML é um exemplo de como os atributos seriam alinhados.  
  
```  
<item id = "123-A"  
      name = "hammer"  
      price = "9.95">  
</item>  
```  
  
## <a name="auto-reformat"></a>Reformatação Automática  
 **Ao colar da área de transferência**  
 Reformatar o texto XML colado da área de transferência.  
  
 **Após a conclusão de marca de fim**  
 Reformatar o elemento quando a marca de fim é concluída.  
  
## <a name="mixed-content"></a>Conteúdo Misto  
 **Conteúdo misturado preserve por padrão**  
 Determina se o editor reformate conteúdo misturado. Por padrão, o editor tenta reformatar conteúdo misturado, a não ser que quando o conteúdo for encontrado em um escopo de `xml:space="preserve"` .  
  
 Se um elemento contém uma mistura de texto e de marcação, os conteúdos são consideradas conteúdo misturado. O código a seguir é um exemplo de um elemento com conteúdo misturado.  
  
```  
<dir>c:\data\AlphaProject\  
  <file readOnly="false">test1.txt</file>  
  <file readOnly="false">test2.txt</file>  
</dir>  
```  
  
## <a name="see-also"></a>Consulte também  
 [Propriedades de documento XML, janela Propriedades](../xml-tools/xml-document-properties-properties-window.md)   
 [Componentes do editor de XML](../xml-tools/xml-editor-components.md)



