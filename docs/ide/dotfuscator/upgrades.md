---
title: Atualizar o Dotfuscator CE (Community Edition)
ms.date: 02/08/2017
ms.devlang: dotnet
ms.prod: visual-studio-dev15
ms.technology: vs-ide-general
ms.topic: conceptual
keywords: Dotfuscator, Dotfuscator CE, PreEmptive, PreEmptive Solutions, PreEmptive Protection, proteção, community edition, ofuscação, .NET, gratuito, Visual Studio 2017, atualização, linha de comando
helpviewer_keywords:
- PreEmptive Protection Dotfuscator
- Dotfuscator Community Edition
- Dotfuscator CE
- Dotfuscator
- obfuscation
- protection
- Dotfuscator upgrade
- upgrade Dotfuscator
- upgrading Dotfuscator
- register Dotfuscator
- registering Dotfuscator
- Dotfuscator command line
- Dotfuscator Professional
description: Saiba como atualizar o Dotfuscator Community Edition gratuito incluído no Visual Studio 2017.
ms.assetid: c7c60904-27f9-4f1f-b79b-ddf65041b810
author: Joe-Sewell-PreEmptive
ms.author: gewarren
manager: douge
ms.openlocfilehash: f1158b0e5f438e49acafad79af1b33ec43690e9a
ms.sourcegitcommit: 0cf1e63b6e0e6a0130668278489b21a6e5038084
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/02/2018
ms.locfileid: "39468537"
---
# <a name="upgrade-dotfuscator-community-edition-ce"></a>Atualizar o Dotfuscator CE (Community Edition)

O Dotfuscator CE (Dotfuscator Community Edition) oferece vários recursos de proteção do aplicativo imediatamente para todos os desenvolvedores que usam o Microsoft Visual Studio.
No entanto, há mais recursos disponíveis aos usuários que atualizam a versão do Dotfuscator.

## <a name="registering-dotfuscator-ce"></a>Registrando o Dotfuscator CE

Os usuários registrados do Dotfuscator CE obtêm acesso a recursos adicionais, como [suporte a linha de comando][cli], o que facilita a integração do Dotfuscator CE no processo de build automatizado. Além disso, o registro concede acesso ao Lucidator, uma ferramenta interna usada para [decodificar rastreamentos de pilha ocultados][decode-obfuscated].

O registro é rápido, simples e gratuito.
Para registrar o Dotfuscator CE, consulte [a seção Registrando o Dotfuscator CE na página Introdução do Guia do Usuário completo do Dotfuscator CE][register-ce].

## <a name="dotfuscator-professional"></a>Dotfuscator Professional

Embora o Dotfuscator Community Edition forneça um nível básico de proteção, o **_PreEmptive Protection – Dotfuscator_ Professional Edition** inclui funcionalidades de proteção e transformações de ofuscação avançadas. As transformações e os recursos aprimorados incluem:

* *Proteção de propriedade intelectual*
  * Opções de renomeação avançadas, incluindo Enhanced Overload Induction™ e seleção de identificador aleatória.
  * Ferramentas de decodificação de rastreamentos de pilha ofuscados.
  * Acesso a transformações de ofuscação de nível empresarial, incluindo [transformações destinadas a acabar com a descompilação automatizada de código][control-flow].
  * A capacidade de [obscurecer cadeias de caracteres confidenciais][string-encryption], impossibilitando uma pesquisa simples do código descompilado.
  * A capacidade de [inserir discretamente cadeias de caracteres de propriedade e de distribuição nos assemblies][watermarking], permitindo determinar a origem de perdas de software não autorizadas.
  * A capacidade de [combinar vários assemblies em um][linking], tornando ainda mais difícil para invasores determinar as funções de elementos de código, pois a separação de preocupações foi eliminada.
  * A capacidade de [remover automaticamente o código não utilizado do aplicativo][pruning], reduzindo a quantidade de código confidencial fornecido.
* *Proteção de integridade do aplicativo*
  * [Comportamentos de defesa do aplicativo][check-actions] adicionais.
  * A capacidade de fornecer um período de aviso antes da data limite do fim da vida útil do aplicativo.
  * A capacidade de notificar o código do aplicativo durante um período de aviso do fim da vida útil ou após a data limite.

O Dotfuscator Professional é o [.NET Obfuscator][net-obfuscator] padrão do setor e é adequado para desenvolvedores empresariais que precisam de atualizações de produto, manutenção e suporte contínuos.
Além disso, o Dotfuscator Professional oferece maior integração com o Visual Studio e é licenciado para uso comercial.

Para obter mais informações sobre os recursos avançados de proteção de aplicativo do Dotfuscator Professional, visite a [página de Visão geral do Dotfuscator][product-about] da PreEmptive Solutions e [faça uma comparação com o Community Edition][product-compare].
[Avaliações com suporte completo estão disponíveis em preemptive.com][eval].

## <a name="see-also"></a>Consulte também

[Este artigo no guia do usuário completo do Dotfuscator CE][full]

<!-- Copyright © 2017 PreEmptive Solutions, LLC -->

[control-flow]:  https://www.preemptive.com/products/dotfuscator/features#controlflow
[string-encryption]:  https://www.preemptive.com/products/dotfuscator/features#string
[watermarking]:  https://www.preemptive.com/products/dotfuscator/features#watermarking
[linking]:  https://www.preemptive.com/products/dotfuscator/features#linking
[pruning]:  https://www.preemptive.com/products/dotfuscator/features#pruning

[check-actions]:  https://www.preemptive.com/dotfuscator/pro/userguide/en/protection_checks_overview.html#actions

[net-obfuscator]:  https://www.preemptive.com/products/dotfuscator/overview
[eval]:  https://www.preemptive.com/eval-request

[product-about]:  https://www.preemptive.com/products/dotfuscator/overview
[product-compare]:  https://www.preemptive.com/products/dotfuscator/compare-editions

[cli]:  https://www.preemptive.com/dotfuscator/ce/docs/help/intro_cli.html
[register-ce]:  https://www.preemptive.com/dotfuscator/ce/docs/help/gui_getstarted.html#register

[full]:  https://www.preemptive.com/dotfuscator/ce/docs/help/intro_upgrades.html
[decode-obfuscated]:  https://www.preemptive.com/dotfuscator/ce/docs/help/gui_decode_stack_trace.html