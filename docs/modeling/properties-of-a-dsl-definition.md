---
title: Propriedades de uma definição de DSL
description: Saiba que as propriedades DslDefinition definem propriedades de definição de linguagem específicas de domínio, como numeração de versão.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- Domain-Specific Language, definition file
author: mgoertz-msft
ms.author: mgoertz
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 6212dfcb9e93110a97e7143e5b1c946efebee89f
ms.sourcegitcommit: e3a364c014ccdada0860cc4930d428808e20d667
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2021
ms.locfileid: "112390835"
---
# <a name="properties-of-a-dsl-definition"></a>Propriedades de uma definição de DSL
As propriedades DslDefinition definem propriedades *de definição de linguagem específicas de domínio* , como numeração de versão. As propriedades DslDefinition aparecem na janela **Propriedades** quando você clica em uma área aberta do diagrama na *Designer de linguagem específica de domínio*.

 Para obter mais informações, consulte [como definir um idioma de Domain-Specific](../modeling/how-to-define-a-domain-specific-language.md). Para obter mais informações sobre como usar essas propriedades, consulte [Personalizando e estendendo uma linguagem de Domain-Specific](../modeling/customizing-and-extending-a-domain-specific-language.md).

 DslDefinition tem as propriedades na tabela a seguir:

|Propriedade|Descrição|Padrão|
|-|-|-|
|Modificador de acesso|Determina se o modificador de acesso para a classe de domínio é público ou interno.|públicos|
|Atributos personalizados|Atributos definidos personalizados para a classe de domínio.<br /><br /> **Observação** Use o botão procurar para adicionar um atributo.|\<none>|
|Nome da empresa|O nome do nome da empresa atual no registro do sistema.|Nome da empresa atual|
|Name|O nome desta classe de domínio.|Nome atual|
|Namespace|O namespace afiliado a esta classe de domínio.|Namespace atual|
|GUID do pacote|O GUID do pacote do Visual Studio gerado para esta DSL.|\<none>|
|Namespace do pacote|O namespace do pacote do Visual Studio gerado para esta DSL.|\<none>|
|Nome do Produto|O nome do produto que será registrado para o pacote do Visual Studio gerado para essa DSL.|\<none>|
|Observações|Observações associadas a esta classe de domínio.|\<none>|
|Descrição|Descrição para esta classe de domínio.|\<none>|
|Nome de exibição|O nome que será exibido no designer gerado para essa classe de domínio.|\<none>|
|Palavra-chave de ajuda|A palavra-chave Help associada a essa classe de domínio.|\<none>|
|Build|O número de Build incremental para esta definição de linguagem específica de domínio.|0|
|Versão Principal|O número de Build principal incremental para essa definição de linguagem específica de domínio.|1|
|Versão Secundária|O número de Build secundário incremental para essa definição de linguagem específica de domínio.|0|
|Revisão|O número da versão da revisão incremental para essa definição de linguagem específica de domínio.|0|

## <a name="see-also"></a>Confira também

- [Glossário das Ferramentas de Linguagem Específica de Domínio](/previous-versions/bb126564(v=vs.100))