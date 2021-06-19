---
title: Personalizando transformação de texto T4
description: Saiba como você pode estender o processo de transformação de modelo padrão personalização do processador de diretiva de modelo de texto ou o host do modelo de texto.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- text templates, API
- text templates, custom hosts
author: mgoertz-msft
ms.author: mgoertz
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 35942b5f87458d1ccaf4892d33b5bba1dcdbb8a0
ms.sourcegitcommit: e3a364c014ccdada0860cc4930d428808e20d667
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2021
ms.locfileid: "112389352"
---
# <a name="customize-t4-text-transformation"></a>Personalizar a transformação de texto T4

Os modelos de texto são um recurso Visual Studio que permitem que você gere o código do programa ou outros arquivos de texto por meio de um processo de transformação. Usando , você pode estender o processo de transformação de modelo padrão personalização do processador de diretiva de modelo de [!INCLUDE[vssdk_current_short](../modeling/includes/vssdk_current_short_md.md)] texto ou o host do modelo de texto.

## <a name="in-this-section"></a>Nesta seção

 [O processo de transformação modelo de texto](../modeling/the-text-template-transformation-process.md) Descreve como funciona a transformação de texto e explica a função do host do modelo e os processadores de diretiva.

 [Criando processadores de diretiva de modelo de texto T4 personalizados](../modeling/creating-custom-t4-text-template-directive-processors.md) O processador de diretiva lida com diretivas em seu modelo, como é executado durante a compilação do modelo, e pode carregar `<#@template#>.` assemblies e outros recursos. Ele também pode inserir código que carregará recursos em tempo de executar. Ao definir seu próprio processador de diretiva, você pode reduzir a complexidade de seus modelos.

 [Invocando transformação de texto em uma extensão do VS](../modeling/invoking-text-transformation-in-a-vs-extension.md) Se você estiver escrevendo uma extensão Visual Studio como um comando de menu ou manipulador de eventos, sua extensão poderá usar o Serviço de Seleção de Texto para transformar qualquer modelo de texto. Você pode passar dados de parâmetro para o modelo usando o objeto Session e obter os valores de dentro do modelo usando a `<#@parameter#>` diretiva .

 [Ing Text Templates by using a Custom Host](../modeling/processing-text-templates-by-using-a-custom-host.md) Quando o código do modelo de texto é executado, o host fornece acesso a arquivos externos e o estado do aplicativo. Por exemplo, o host que executa transformações de texto Visual Studio pode fornecer acesso ao **Gerenciador de Soluções**. Ele também exibe erros na janela de mensagem de erro. Se você quiser executar transformações de texto em um contexto diferente, poderá definir seu próprio host que fornece acesso aos serviços disponíveis nesse contexto.

 Se você estiver escrevendo uma extensão Visual Studio, considere usar o serviço de transformação de texto existente em vez de escrever seu próprio host. Para obter mais informações, consulte [Invocando a transformação de texto em uma extensão do VS.](../modeling/invoking-text-transformation-in-a-vs-extension.md)

## <a name="reference"></a>Referência

- [Escrever um modelo de texto T4](../modeling/writing-a-t4-text-template.md) fornece a sintaxe de diretivas de modelo de texto e blocos de controle.
