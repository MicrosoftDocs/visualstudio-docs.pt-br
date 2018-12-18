---
title: Validação de documento XML | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-general
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: abb353bd-6c4a-4978-b03b-a8c245bbfb55
caps.latest.revision: 9
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: 4b765efcfc01384a14bba6eb46cbaadd915e7752
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49914255"
---
# <a name="xml-document-validation"></a>Validação de documento XML
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

  
O Editor XML verifica a sintaxe do XML 1.0 e também executa validação de dados conforme você digita. O editor pode validar usando uma DTD (definição de tipo de documento) ou um esquema. Os sublinhados ondulados vermelhos realçam todos os erros de XML 1.0 bem-formado. Os sublinhados ondulados azuis mostram os erros semânticos com base na validação de DTD ou de esquema. Cada erro tem uma entrada associada na lista de erros. Você também pode exibir a mensagem de erro pausando o mouse sobre o sublinhado ondulado.  
  
 Os esquemas usados na validação são encontrados correspondendo o `targetNamespace` de um esquema compilado com a declaração xmlns do elemento. Os esquemas compilados são carregados de um dos seguintes locais, listados por ordem de prioridade:  
  
- Do nome de arquivo especificado na **esquemas** campo da janela de propriedades do documento.  
  
- Um esquema ou DTD embutido.  
  
- Uma DTD externa ou os atributos `xsd:schemaLocation` e `xsd:noNamespaceSchemaLocation`  
  
- Um URI de um namespace do esquema XDR "x-schema".  
  
  Os esquemas também podem ser encontrados nos seguintes locais adicionais quando o esquema tiver um namespace de destino não vazio:  
  
- Outra janela do editor que contenha o esquema.  
  
- Um esquema na solução atual.  
  
- Um esquema do diretório de cache de esquema.  
  
## <a name="xslt-files"></a>Arquivos XSLT  
 Ao editar um arquivo XSLT, o arquivo de xslt.xsd localizado no cache de esquema é usado para validação. Os erros de validação são mostrados como sublinhados ondulados azuis. Os erros do compilador XSLT são mostrados como sublinhados ondulados vermelhos.  
  
## <a name="xml-schema-xsd-files"></a>Arquivos XSD (esquema XML)  
 Ao editar um arquivo de esquema XML, o arquivo de xsdschema.xsd localizado no cache de esquema é usado para validação. Os erros de validação são mostrados como sublinhados ondulados azuis. Todos os erros de compilação também são mostrados com traços ondulados vermelhos.  
  
## <a name="see-also"></a>Consulte também  
 [Editor de XML](../xml-tools/xml-editor.md)



