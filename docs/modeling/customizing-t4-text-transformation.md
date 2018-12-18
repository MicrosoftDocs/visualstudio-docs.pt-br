---
title: Personalizando transformação de texto T4
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- text templates, API
- text templates, custom hosts
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.prod: visual-studio-dev15
ms.technology: vs-ide-modeling
ms.openlocfilehash: 7755444781bb0205e7483e2365d80cac909c62c6
ms.sourcegitcommit: 495bba1d8029646653f99ad20df2f80faad8d58b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/31/2018
ms.locfileid: "39380097"
---
# <a name="customize-t4-text-transformation"></a>Personalizar a transformação de texto T4

Modelos de texto são um recurso do Visual Studio que permitem que você gerar o código do programa ou outros arquivos de texto por meio de um processo de transformação. Usando [!INCLUDE[vssdk_current_short](../modeling/includes/vssdk_current_short_md.md)], você pode estender o processo de transformação de modelo padrão, personalizando o processador de diretriz de modelo de texto ou o host de modelo de texto.

## <a name="in-this-section"></a>Nesta seção

 [O processo de transformação do modelo de texto](../modeling/the-text-template-transformation-process.md) descreve como a transformação de texto funciona e explica a função de host de modelo e os processadores de diretriz.

 [Criando processadores de diretiva de modelo de texto de T4 personalizados](../modeling/creating-custom-t4-text-template-directive-processors.md) o processador de diretriz lida com diretivas em seu modelo, tal como `<#@template#>.` ele é executado durante a compilação do modelo e pode carregar assemblies e outros recursos. Ele também pode inserir o código que irá carregar recursos em tempo de execução. Ao definir seu próprio processador de diretriz, você pode reduzir a complexidade de seus modelos.

 [Invocando transformação de texto em uma extensão do VS](../modeling/invoking-text-transformation-in-a-vs-extension.md) se você estiver escrevendo uma extensão do Visual Studio como um manipulador de evento ou comando de menu, a extensão pode usar o serviço de modelagem de texto para transformar qualquer modelo de texto. Você pode passar dados de parâmetro para o modelo usando o objeto de sessão e obter os valores de dentro do modelo usando o `<#@parameter#>` diretiva.

 [Processando modelos de texto usando um Host personalizado](../modeling/processing-text-templates-by-using-a-custom-host.md) quando o código do modelo de texto é executado, o host fornece acesso a arquivos externos e o estado do aplicativo. Por exemplo, o host que executa transformações de texto no Visual Studio pode fornecer acesso aos **Gerenciador de soluções**. Ele também exibe os erros na janela de mensagem de erro. Se você quiser executar transformações de texto em um contexto diferente, você pode definir seu próprio host que fornece acesso aos serviços disponíveis nesse contexto.

 Se você estiver escrevendo uma extensão do Visual Studio, considere usar o serviço de transformação de texto existente em vez de escrever seu próprio host. Para obter mais informações, consulte [invocando transformação de texto em uma extensão do VS](../modeling/invoking-text-transformation-in-a-vs-extension.md).

## <a name="reference"></a>Referência

- [Escrever um modelo de texto T4](../modeling/writing-a-t4-text-template.md) fornece a sintaxe de diretivas de modelo de texto e blocos de controle.