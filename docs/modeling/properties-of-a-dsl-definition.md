---
title: Propriedades de uma definição de DSL
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- Domain-Specific Language, definition file
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.prod: visual-studio-dev15
ms.technology: vs-ide-modeling
ms.openlocfilehash: 1fd001f5371e346a07f82c9c48a3acb699cefd52
ms.sourcegitcommit: 768d7877fe826737bafdac6c94c43ef70bf45076
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/02/2018
ms.locfileid: "50966759"
---
# <a name="properties-of-a-dsl-definition"></a>Propriedades de uma definição de DSL
Definem propriedades de DslDefinition *linguagem específica do domínio* propriedades de definição, como numeração de versão. As propriedades de DslDefinition aparecem na **propriedades** janela quando você clica em uma área aberta do diagrama na *Designer de linguagem específica do domínio*.

 Para obter mais informações, consulte [como definir uma linguagem específica do domínio](../modeling/how-to-define-a-domain-specific-language.md). Para obter mais informações sobre como usar essas propriedades, consulte [personalizando e estendendo uma linguagem específica do domínio](../modeling/customizing-and-extending-a-domain-specific-language.md).

 DslDefinition tem as propriedades na tabela a seguir:

|Propriedade|Descrição|Padrão|
|-|-|-|
|Modificador de acesso|Determina se o modificador de acesso para a classe de domínio é público ou interno.|públicos|
|Atributos personalizados|Personalizadas definidas atributos para a classe de domínio.<br /><br /> **Observação** Use o botão Procurar para adicionar um atributo.|\<Nenhum >|
|Nome da empresa|O nome do nome da empresa no registro do sistema.|Nome da empresa atual|
|Nome|O nome dessa classe de domínio.|Nome atual|
|Namespace|O namespace afiliado a essa classe de domínio.|Namespace atual|
|Guid do pacote|O guid do pacote do Visual Studio gerado para esta DSL.|\<Nenhum >|
|Namespace do pacote|O namespace para o pacote do Visual Studio gerado para esta DSL.|\<Nenhum >|
|Nome do produto|O nome do produto que será registrado para o pacote do Visual Studio gerado para esta DSL.|\<Nenhum >|
|Observações|Anotações associadas a essa classe de domínio.|\<Nenhum >|
|Descrição|Descrição para essa classe de domínio.|\<Nenhum >|
|Nome de Exibição|O nome que será exibido no designer gerado para essa classe de domínio.|\<Nenhum >|
|Palavra-chave de ajuda|A palavra-chave ajuda associada a essa classe de domínio.|\<Nenhum >|
|Build|O número de build incremental para essa definição de linguagem específica do domínio.|0|
|Versão principal|O número de compilação principal incrementais para esta definição de linguagem específica do domínio.|1|
|Versão secundária|O número de compilação secundária incrementais para esta definição de linguagem específica do domínio.|0|
|Revisão|A versão incremental build número para essa definição de linguagem específica do domínio.|0|

## <a name="see-also"></a>Consulte também

- [Glossário de ferramentas de linguagem específica do domínio](https://msdn.microsoft.com/ca5e84cb-a315-465c-be24-76aa3df276aa)