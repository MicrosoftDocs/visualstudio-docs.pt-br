---
title: Opções, Editor de texto, XML, Diversos
ms.date: 10/29/2018
ms.prod: visual-studio-dev15
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- VS.ToolsOptionsPages.Text_Editor.XML.Miscellaneous
ms.assetid: b6538cbe-badd-4313-a1fb-39e906736bbe
author: gewarren
ms.author: gewarren
manager: douge
ms.openlocfilehash: fed24e39b29907784d6101f7871f7a292850c457
ms.sourcegitcommit: dd839de3aa24ed7cd69f676293648c6c59c6560a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/27/2018
ms.locfileid: "52389345"
---
# <a name="options-text-editor-xml-miscellaneous"></a>Opções, Editor de texto, XML, Diversos

Use a página de propriedades **Diversos** para alterar as configurações de preenchimento automático e de esquema para o Editor XML. Para abrir a caixa de diálogo **Opções**, clique no menu **Ferramentas** e clique em **Opções**. Para acessar a página de propriedades **Diversos**, expanda o nó **Editor de texto** > **XML** > **Diversos**.

## <a name="auto-insert"></a>AutoInserção

**Marcas de fechamento**

O Editor de texto adiciona marcas de fechamento ao criar elementos XML. Se uma marca de início de elemento for selecionada, o editor inserirá a marca de fechamento correspondente, incluindo um prefixo de namespace correspondente. Por padrão, a caixa de seleção fica marcada.

**Aspas de atributo**

Ao criar atributos XML, o editor insere os caracteres `="` e `"` e posiciona o acento circunflexo (**^**) dentro de aspas duplas. Por padrão, a caixa de seleção fica marcada.

**Declarações de namespace**

O editor inserir automaticamente declarações namespace onde quer que são necessárias. Por padrão, a caixa de seleção fica marcada.

**Outra marcação (Comentários, CDATA)**

Comentários, CDATA, DOCTYPE, instruções de processamento e a outra marcação automática são concluídos. Por padrão, a caixa de seleção fica marcada.

## <a name="network"></a>Rede

**Baixar automaticamente DTDs e esquemas**

Os esquemas e as definições de tipo (DTDs) de documentos são baixados automaticamente locais HTTP. Esse recurso usa o System.Net com a detecção do servidor autoproxy habilitada. Por padrão, a caixa de seleção fica marcada.

## <a name="outlining"></a>Estrutura de tópicos

**Entrar no modo de estrutura de tópicos na abertura dos arquivos**

Ativa o recurso de estruturação quando um arquivo é aberto. Por padrão, a caixa de seleção fica marcada.

## <a name="caching"></a>Cache

**Esquemas**

Especifica o local do cache de esquema. O botão Procurar (...) abre a localização do cache do esquema atual em uma nova janela. A localização padrão é *\<diretório de instalação do Management Studio>* \Xml\Schemas.

## <a name="see-also"></a>Consulte também

- [Como criar documentação XML (Visual Basic)](/dotnet/visual-basic/programming-guide/program-structure/how-to-create-xml-documentation)
- [Geração de código](../code-generation-in-visual-studio.md)