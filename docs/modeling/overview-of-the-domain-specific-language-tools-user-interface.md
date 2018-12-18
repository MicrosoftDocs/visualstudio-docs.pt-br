---
title: Visão geral da interface de usuário das Ferramentas de Linguagem Específica do Domínio
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- vs.dsltools.dsldesigner.editor
helpviewer_keywords:
- Domain-Specific Language Tools, user interface
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.prod: visual-studio-dev15
ms.technology: vs-ide-modeling
ms.openlocfilehash: d54ba969e06f3bd951556f8d8f347977419fc015
ms.sourcegitcommit: 768d7877fe826737bafdac6c94c43ef70bf45076
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/02/2018
ms.locfileid: "50966486"
---
# <a name="overview-of-the-domain-specific-language-tools-user-interface"></a>Visão geral da interface de usuário das Ferramentas de Linguagem Específica do Domínio
Quando você abre uma solução de ferramentas de linguagem específica do domínio (ferramentas DSL) no Visual Studio, a interface do usuário será semelhante a figura a seguir.

 ![designer de DSL](../modeling/media/dsl_designer.png)

 A tabela a seguir explica como as partes da interface do usuário são usadas.

|**Elemento**|**Definição**|
|-|-|
|Diagrama|O diagrama exibe o modelo de domínio.<br /><br /> O diagrama tem dois lados. Um dos lados define os tipos dos elementos em seus modelos. Por outro lado define como seus modelos aparecerá na tela.|
|Caixa de Ferramentas|Arraste as ferramentas da caixa de ferramentas para adicionar classes de domínio e tipos ao diagrama de forma. Para adicionar mapas de formas, conectores e relações, a ferramenta, clique o nó de origem no diagrama e, em seguida, o nó de destino.|
|DSL Explorer|**Gerenciador de DSL** é exibida quando uma definição de DSL é a janela ativa. Ele mostra a DSL como uma árvore. Gerenciador de DSL permite editar os recursos do modelo que não são exibidos no diagrama. Por exemplo, você pode adicionar itens de caixa de ferramentas e ative o processo de validação usando o **Gerenciador de DSL**.|
|Janela de detalhes de DSL|O **detalhes de DSL** janela mostra as propriedades do domínio de elementos do modelo que permitem que você controle como os elementos são exibidos, e como os elementos são copiados e excluídos.<br /><br /> -Por padrão, o **detalhes de DSL** janela aparece ao lado de **lista de erros** e **saída** windows.|

## <a name="the-domain-model-diagram"></a>O diagrama de modelo de domínio
 O diagrama de modelo de domínio é dividido em duas partes. Um dos lados do diagrama mostra os elementos e as relações no modelo. Por outro lado mostra como o modelo será exibido e inclui as formas que são usadas para exibir os elementos e as propriedades do diagrama de modelo. A imagem a seguir mostra os elementos do diagrama.

 ![designer de DSL com raias](../modeling/media/dsl_desinger.png)

 A tabela a seguir explica alguns dos elementos do diagrama de modelo de domínio.

|**Termo**|**Definição**|
|-|-|
|Classe de domínio|Classes de domínio são os tipos de elementos em seus modelos.<br /><br /> Uma classe de domínio pode aparecer mais de uma vez em um diagrama, se ele é o destino de mais de uma relação.<br /><br /> Para adicionar uma classe de domínio, arraste a ferramenta de classe de domínio do **caixa de ferramentas** para o **Classes e relacionamentos** lado do diagrama.|
|Relacionamento de domínio|As relações de domínio são os tipos de links entre os elementos em seus modelos.<br /><br /> Uma *relacionamento de incorporação* indica que o elemento de destino é de propriedade ou contido pelo elemento de origem e aparece como uma linha sólida. Cada elemento em um modelo deve ser o destino de uma relação de incorporação, para que o modelo de uma árvore de formulários. Um *relação de referência* indica um link geral entre elementos de modelo e aparece como uma linha tracejada. Qualquer elemento pode ter qualquer número de links de referência.<br /><br /> Criar uma relação clicando na ferramenta sobre o **caixa de ferramentas**, clicando na classe de domínio de origem e, em seguida, clicando na classe de destino.|
|Formas e Conectores|Formas de especificam como os elementos de modelo devem ser exibidos em um diagrama DSL., conectores de especificam as linhas em um diagrama DSL que pode ser usado para exibir relações.<br /><br /> Para criar uma forma ou um conector, arraste a ferramenta para o **elementos de diagrama** lado do diagrama.|
|Mapas de formas|Um mapa de formas aparece como uma linha no diagrama de modelo de domínio, uma forma de vinculação para a classe de domínio que ele exibe, ou um conector para a relação de domínio que ele exibe.|

## <a name="see-also"></a>Consulte também

- [Visão geral das Ferramentas de Linguagem Específica de Domínio](../modeling/overview-of-domain-specific-language-tools.md)
- [Glossário de ferramentas de linguagem específica do domínio](https://msdn.microsoft.com/ca5e84cb-a315-465c-be24-76aa3df276aa)
- [Personalizando e estendendo uma linguagem específica de domínio](../modeling/customizing-and-extending-a-domain-specific-language.md)