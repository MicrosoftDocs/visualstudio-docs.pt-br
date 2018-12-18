---
title: 'Como: editar arquivos XML | Microsoft Docs'
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-general
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 07fa3ecf-6345-4d30-9d85-d5ef5b083319
caps.latest.revision: 7
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: ac3864b3d3a3074f9b6be2529e8f674df90532c8
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49245291"
---
# <a name="how-to-edit-xml-files"></a>Como editar arquivos XML
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

  
O editor XML é o novo editor para arquivos XML. Ele pode ser usado em um arquivo XML independente, ou em um arquivo associado a um projeto o Visual Studio. O Editor de XML está associado às seguintes extensões de arquivo: .config, .dtd, .xml, .xsd, .xdr, .xsl, .xslt e .vssettings. O Editor de XML também está associado a qualquer outro tipo de arquivo que não tenha nenhum editor específico registrado e que contenha o conteúdo XML ou DTD.  
  
> [!NOTE]
>  Os documentos XHTML são tratados pelo Editor de HTML.  
  
### <a name="to-edit-an-xml-file"></a>Para editar um arquivo XML  
  
1.  Clique duas vezes no arquivo que você deseja editar.  
  
### <a name="to-add-a-new-xml-file-to-a-project"></a>Para adicionar um novo arquivo XML a um projeto  
  
1.  Dos **Project** menu, selecione **Adicionar Novo Item**.  
  
2.  Selecione **arquivo XML** da **modelos** painel.  
  
3.  Insira o nome do arquivo a **nome** campo e pressione **Add**.  
  
     O arquivo XML é adicionado ao projeto e aberto no Editor de XML. O arquivo contém a declaração XML padrão, `<?xml version="1.0" encoding="utf-8" ?>`.  
  
### <a name="to-add-an-existing-xml-file-to-a-project"></a>Para adicionar um arquivo XML existente a um projeto  
  
1.  Dos **Project** menu, selecione **Add Existing Item**.  
  
     O **Add Existing Item** caixa de diálogo é exibida.  
  
2.  Selecione um arquivo XML e pressione **adicionar**.  
  
### <a name="to-create-a-new-xml-or-xslt-file"></a>Para criar um novo arquivo XML ou XSLT  
  
1.  Dos **arquivo** menu, selecione **New**.  
  
     O **novo arquivo** caixa de diálogo é exibida.  
  
2.  Selecione **arquivo XML** para criar um novo arquivo XML; ou, selecione **arquivo XSLT** para criar uma nova folha de estilos XSLT.  
  
3.  Clique em **aberto**.  
  
### <a name="to-create-a-project-for-xml-files"></a>Para criar um projeto para arquivos XML  
  
1.  Dos **arquivo** menu, selecione **New**e, em seguida, selecione **projeto**.  
  
     A caixa de diálogo **Novo Projeto** é exibida.  
  
2.  Selecione o idioma de código de sua escolha, selecione **projeto vazio**e clique em **Okey**.  
  
3.  Adicionar arquivos XML ao projeto.  
  
     O Editor de XML localiza os esquemas que você adiciona a esse projeto e os usa para validação e IntelliSense em qualquer XML, esquema ou arquivos XSLT que você editar quando o projeto for aberto.  
  
## <a name="see-also"></a>Consulte também  
 [Editor de XML](../xml-tools/xml-editor.md)   
 [Propriedades de documento XML, janela Propriedades](../xml-tools/xml-document-properties-properties-window.md)   
 [Como criar um esquema XML de um documento XML](../xml-tools/how-to-create-an-xml-schema-from-an-xml-document.md)



