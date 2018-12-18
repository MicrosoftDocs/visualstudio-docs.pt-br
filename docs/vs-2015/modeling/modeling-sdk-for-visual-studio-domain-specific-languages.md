---
title: SDK de modelagem para Visual Studio - linguagens específicas do domínio | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-tfs-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-devops-techdebt
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Domain-Specific Language Tools
- Domain-Specific Language
ms.assetid: 17a531e2-1964-4a9d-84fd-6fb1b4aee662
caps.latest.revision: 79
author: gewarren
ms.author: gewarren
manager: douge
ms.openlocfilehash: 1a294c9c1eaeb0c59f8c2e9c58c75a161c0d61e6
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49883322"
---
# <a name="modeling-sdk-for-visual-studio---domain-specific-languages"></a>SDK de Modelagem para Visual Studio - linguagens específicas ao domínio
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Usando o SDK de modelagem para [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] (MSDK), você pode criar ferramentas de desenvolvimento baseado em modelo avançadas que você pode integrar [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]. Como exemplo, as ferramentas UML são criadas usando MSDK. Da mesma forma, você pode criar uma ou mais definições de modelo e integrá-las em um conjunto de ferramentas.  
  
 No centro do MSDK está a definição de um modelo que você cria para representar conceitos em sua área de negócios. Você pode cercar o modelo com várias ferramentas, como uma exibição diagramática, a capacidade de gerar código e outros artefatos, comandos para transformar o modelo, e a capacidade de interagir com código e os outros objetos em [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]. À medida que o modelo é desenvolvido, você pode combiná-lo com outros modelos e ferramentas para formar um conjunto de ferramentas avançadas centradas em seu desenvolvimento.  
  
 O MSDK permite desenvolver rapidamente um modelo na forma de uma linguagem específica do domínio (DSL). Você começa ao usar um editor especializado para definir um esquema ou sintaxe abstrata junto com uma notação gráfica. Dessa definição, o VMSDK gera:  
  
- Uma implementação de modelo com uma API fortemente tipada executada em um repositório baseado em transação.  
  
- Um gerenciador baseado em árvore.  
  
- Um editor gráfico no qual os usuários podem exibir o modelo ou partes dele que você definir.  
  
- Métodos de serialização que salvam seus modelos em XML legível.  
  
- Recursos para gerar código de programa e outros artefatos usando modelagem de texto.  
  
  Você pode personalizar e estender todos esses recursos. Suas extensões são integradas de tal forma que você ainda pode atualizar a definição de DSL e gerar novamente os recursos sem perder suas extensões.  
  
## <a name="samples-and-the-latest-information"></a>Exemplos e as informações mais recentes  
 [Baixe a modelagem do SDK para Visual Studio 2015](http://www.microsoft.com/download/details.aspx?id=48148)  
  
 [Exemplos de](http://go.microsoft.com/fwlink/?LinkId=186128) para o SDK de modelagem para Visual Studio.  
  
 Para obter orientação sobre técnicas avançadas e solução de problemas, visite [Fórum de extensibilidade de ferramentas de modelagem & de DSL do Visual Studio](http://go.microsoft.com/fwlink/?LinkID=186074).  
  
## <a name="in-this-section"></a>Nesta seção  
 [Introdução às linguagens específicas de domínio](../modeling/getting-started-with-domain-specific-languages.md)  
  
 [Noções básicas sobre modelos, classes e relações](../modeling/understanding-models-classes-and-relationships.md)  
  
 [Como definir uma linguagem específica de domínio](../modeling/how-to-define-a-domain-specific-language.md)  
  
 [Personalizando e estendendo uma linguagem específica de domínio](../modeling/customizing-and-extending-a-domain-specific-language.md)  
  
 [Validação em uma linguagem específica de domínio](../modeling/validation-in-a-domain-specific-language.md)  
  
 [Escrevendo código para personalizar uma linguagem específica de domínio](../modeling/writing-code-to-customise-a-domain-specific-language.md)  
  
 [Gerando código com base em uma linguagem específica de domínio](../modeling/generating-code-from-a-domain-specific-language.md)  
  
 [Noções básicas do código DSL](../modeling/understanding-the-dsl-code.md)  
  
 [Personalizando o armazenamento de arquivos e a serialização XML](../modeling/customizing-file-storage-and-xml-serialization.md)  
  
 [Implantando soluções de linguagem específica de domínio](../modeling/deploying-domain-specific-language-solutions.md)  
  
 [Criando uma linguagem específica de domínio baseada no Windows Forms](../modeling/creating-a-windows-forms-based-domain-specific-language.md)  
  
 [Criando uma linguagem específica de domínio baseada no WPF](../modeling/creating-a-wpf-based-domain-specific-language.md)  
  
 [Como estender o designer de linguagem específica de domínio](../modeling/how-to-extend-the-domain-specific-language-designer.md)  
  
 [Edições do Visual Studio com suporte pelo SDK de Visualização e Modelagem](../modeling/supported-visual-studio-editions-for-visualization-amp-modeling-sdk.md)  
  
 [Como migrar uma linguagem específica de domínio para uma nova versão](../modeling/how-to-migrate-a-domain-specific-language-to-a-new-version.md)  
  
 [Referência de API do SDK de Modelagem para Visual Studio](../modeling/api-reference-for-modeling-sdk-for-visual-studio.md)



