---
title: Propriedades de documento XML, a janela de propriedades | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-general
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 9dbb34d9-02ea-4201-b445-c98a0eb0d6db
caps.latest.revision: 9
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: c93defe6f5c56966195f1514b5aa76464f6f3013
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49236555"
---
# <a name="xml-document-properties-properties-window"></a>Propriedades de documento XML, a janela de propriedades
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

  
O **propriedades** janela fornece informações básicas sobre o documento que está ativo no Editor de XML. As propriedades que estão disponíveis varia dependendo do tipo de documento XML que está atualmente ativa.  
  
> [!NOTE]
>  Todas as propriedades de documento XML são salvas na solução. Como resultado, você não tem que digitar novamente esses valores na próxima vez que você abrir a solução.  
  
 **Codificação**  
 A codificação de caractere para o arquivo. Alterar essa propriedade também altera o atributo de codificação na declaração XML, e vice-versa. A nova codificação será usada para codificar o arquivo quando você salvar o arquivo.  
  
 **Entrada**  
 O documento de entrada associado com a folha de estilos XSLT. Ele é usado pelas **ShowXSLT saída** comando. Um documento pode ser selecionado usando o botão Procurar (**...** ) botão.  
  
 Esta propriedade é visível somente quando um arquivo fonte é atualmente ativa na janela editor.  
  
 **Saída**  
 O arquivo que é gerado para transformar um documento XML.  
  
 Se um arquivo é não especificado, um nome de arquivo padrão é gerado com base no atributo de `method` no elemento de `xsl:output` que determina a extensão de arquivo. O arquivo padrão é localizado no diretório temporário do usuário atual.  
  
 **Esquemas**  
 Os esquemas a ser usado para validação. O botão abre a **esquemas XSD** caixa de diálogo que pode ser usada para selecionar os esquemas para usar.  
  
 Você também pode ir para o caminho para esquemas. Se vários esquemas são especificados, cada caminho de esquema deve ser colocado entre aspas duplas.  
  
 **Folha de estilos**  
 O arquivo XSLT que é usado para transformar o documento quando o **saída XSLT de apresentação** comando é usado. Se esse campo estiver em branco quando o **saída XSLT de apresentação** comando é usado, o editor usa o valor fornecido no `xml-stylesheet` o documento, ou instrução de processamento solicitará o nome do arquivo.  
  
 Ao editar um arquivo XSLT, essa propriedade pode ser usada para especificar que uma folha de estilo diferente deve ser usado quando o **saída XSLT de apresentação** ou **depuração XSLT** comando está selecionado. Por exemplo, você pode querer fazer isso quando você estiver editando uma folha de estilos incluída em uma folha de estilos pai.  
  
## <a name="see-also"></a>Consulte também  
 [Editor de XML](../xml-tools/xml-editor.md)   
 [Componentes do editor de XML](../xml-tools/xml-editor-components.md)



