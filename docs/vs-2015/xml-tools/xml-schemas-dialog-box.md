---
title: Caixa de diálogo de esquemas XML | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-xml-tools
ms.topic: conceptual
ms.assetid: 0271fa26-2205-49bd-96e0-ae1441571808
caps.latest.revision: 9
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 82247c2510d64f712cc4b703154ea16a4bb7e7e1
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "68150661"
---
# <a name="xml-schemas-dialog-box"></a>A caixa de diálogo de esquemas XML
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

O **esquemas XML** caixa de diálogo é usada para selecionar quais esquemas XSD (linguagem) de definição de esquema XML para associar um documento XML. Você pode selecionar um esquema de cache do esquema, ou especificar um esquema que não está localizado no cache. Os esquemas selecionados são considerados parte de um conjunto de esquema. O esquema é usado para o IntelliSense e também validação de documento XML.  
  
 Você pode acessar o **esquemas XML** caixa de diálogo clicando o **esquemas** botão na janela Propriedades do documento, ou selecionando **esquemas** do **XML** menu.  
  
## <a name="uielement-list"></a>Lista UIElement  
 **Use**  
 Selecione como o esquema XML deve ser usada.  
  
- **Automático**. Este esquema não está em uso pelo documento atual mas está disponível para a associação automática. Se o documento XML declarar um namespace que corresponde `targetNamespace` deste esquema, o esquema será associado e é automaticamente encapsulado no conjunto de esquema.  
  
- **Usar este esquema**. Este esquema está sendo usado pelo documento atual. Qualquer o usuário que solicitou explicitamente este esquema está usado clicando nessa coluna, ou o esquema foi associado automaticamente com base em `targetNamespace`correspondente.  
  
- **Não use esquemas selecionados**. Este esquema não é usado pelo documento atual, mesmo se o esquema tem `targetNamespace`correspondente. Essa configuração pode ser útil para resolver conflitos quando há mais de uma versão do mesmo esquema no cache ou na solução de esquema.  
  
  **Namespace de destino**  
  Exibe o namespace de destino associada com o esquema XML.  
  
  **Nome do arquivo**  
  Exibe o nome do arquivo de esquema XML.  
  
  **Adicionar**  
  Abre o **abrir esquema XSD** caixa de diálogo, que permite que você selecionar esquemas adicionais para adicionar ao conjunto de esquema. Quando você adiciona um esquema para o esquema definido, o **uso** o valor da coluna é definido como **usar este esquema**.  
  
  **Removerr**  
  Remove o esquema do dataset selecionado de esquema. Remove o esquema de cache de memória do esquema, mas não no sistema de arquivos.  
  
## <a name="see-also"></a>Consulte também  
 [Componentes do Editor de XML](../xml-tools/xml-editor-components.md)   
 [Como: Selecione os esquemas XML para usar](../xml-tools/how-to-select-the-xml-schemas-to-use.md)   
 [Cache de esquema](../xml-tools/schema-cache.md)
