---
title: Editar folhas de estilos XSLT | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-general
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 080bed0f-0ca9-4be7-aecd-6bdaebc04007
caps.latest.revision: 11
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: 7dd25a531682c74284a74f065dc729f37ac7fb1a
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49286995"
---
# <a name="editing-xslt-style-sheets"></a>Folhas de estilos XSLT de edição
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

  
O editor XML pode ser usado para editar folhas de estilos XSLT. Você pode tirar proveito dos recursos do editor padrão como o IntelliSense, estruturação, snippets XML, e assim por diante. Além disso, há também os novos recursos que tornam ficar em XSLT.  
  
## <a name="xslt-features"></a>Recursos de fonte  
 A tabela a seguir descreve os recursos específicos para trabalhar com folhas de estilos XSLT.  
  
 **Coloração de sintaxe**  
 Palavras-chave XSLT, tais como `template`, `match`e assim por diante, são exibidos na cor da palavra-chave XSLT especificada pela **fontes e cores** configurações.  
  
 **Sublinhados ondulados**  
 O editor XML usa o arquivo de xslt.xsd instalado para validar folhas de estilos XSLT. Os erros de validação são mostrados como sublinhados ondulados azuis. O editor XML também compila a folha de estilos em segundo plano e relatar erros ou avisos do compilador com traços ondulados apropriadas.  
  
 **Suporte para blocos de script**  
 O código nos blocos de script é suportado pelo depurador XSLT para que você pode definir pontos de interrupção e percorrer o código de bloco de script.  
  
 **Saída XSLT de exibição**  
 Você pode executar uma transformação XSL e exibir a saída do editor XML. Para obter mais informações, consulte [como: executar uma transformação XSLT do Editor XML](../xml-tools/how-to-execute-an-xslt-transformation-from-the-xml-editor.md).  
  
 **Depurar o XSLT**  
 Você pode iniciar o depurador XSLT de um arquivo fonte no editor XML. O depurador oferece suporte pontos de interrupção no arquivo XSLT, estado de configuração de execução XSLT de exibição, e assim por diante. Passa sobre uma variável XSLT traz anterior um ToolTip com o valor da variável. O depurador pode ser usado para depurar uma folha de estilos, ou depurar uma transformação XSL compilado chamada de outro aplicativo. Para obter mais informações, consulte [depuração XSLT](../xml-tools/debugging-xslt.md).  
  
## <a name="see-also"></a>Consulte também  
 [Editor de XML](../xml-tools/xml-editor.md)



