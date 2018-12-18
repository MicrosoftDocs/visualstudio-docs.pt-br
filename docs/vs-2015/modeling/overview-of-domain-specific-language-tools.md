---
title: Visão geral das ferramentas de linguagem específica do domínio | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-tfs-dev14
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Domain-Specific Language
ms.assetid: 50d93ea2-8c88-4522-853b-40ab194953db
caps.latest.revision: 56
author: gewarren
ms.author: gewarren
manager: douge
ms.openlocfilehash: c01116ee4a4b0edc43a6277db7725e8d962bd607
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49839317"
---
# <a name="overview-of-domain-specific-language-tools"></a>Visão geral das Ferramentas de Linguagem Específica do Domínio
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Ferramentas de linguagem específica do domínio (ferramentas DSL), que são hospedados no [!INCLUDE[vsprvs](../includes/vsprvs-md.md)], permitem que você criar uma linguagem específica de domínio e, em seguida, gerar tudo o que os usuários devem ter para criar modelos que são baseados na linguagem.  
  
 As ferramentas a seguir estão incluídas nas ferramentas de DSL:  
  
-   Assistente de projeto que usa modelos de solução diferentes para ajudá-lo a começar a desenvolver sua linguagem específica do domínio.  
  
-   Um designer gráfico para criar e editar sua definição de linguagem específica do domínio.  
  
-   Um mecanismo de validação que verifica se a definição de linguagem específica de domínio está bem formada e exibe os erros e avisos se houver problemas.  
  
-   Um gerador de código que usa uma definição de linguagem específica de domínio como entrada e produz o código-fonte como saída.  
  
## <a name="the-dsl-tools-solution"></a>A solução de ferramentas DSL  
 O Assistente de Designer específica de domínio fornece os seguintes modelos de solução:  
  
- Fluxo de tarefas  
  
- Diagramas de classe  
  
- Linguagem mínima  
  
- Modelos do componente  
  
- WPF mínima  
  
- Windows. Forms mínima  
  
- Biblioteca de DSL  
  
  Para obter mais informações, consulte [escolhendo um modelo de solução de linguagem específica do domínio](../modeling/choosing-a-domain-specific-language-solution-template.md).  
  
  O assistente cria um [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] solução que tem os seguintes projetos:  
  
- DSL  
  
   O projeto de Dsl define a linguagem específica de domínio e suas ferramentas de edição e de processamento.  
  
- **DslPackage**  
  
   Projeto DslPackage determina como as ferramentas de linguagem integram [!INCLUDE[vsprvs](../includes/vsprvs-md.md)].  
  
## <a name="the-dsl-tools-graphical-interface"></a>A Interface gráfica de ferramentas DSL  
 Você pode usar a interface gráfica de ferramentas DSL para adicionar elementos e relações para sua linguagem específica do domínio. Depois que você adicionou os elementos, você pode definir sua aparência, mapeando-os para as formas, personalizar cores e adicionar os decoradores. Você também pode adicionar elementos à caixa de ferramentas.  
  
## <a name="validation-in-dsl-tools"></a>Validação em ferramentas DSL  
 DSL fornece um nível de validação para certificar-se de que o modelo de domínio atende aos requisitos básicos para geração de código. Normalmente, quando você cria sua própria linguagem específica de domínio, você adicionaria sua própria validação para expressar suas regras de lógica de negócios. Para obter mais informações sobre a validação personalizada, consulte [validação em uma linguagem específica do domínio](../modeling/validation-in-a-domain-specific-language.md).  
  
 É recomendável que você valide sua linguagem específica do domínio com frequência quando você criá-lo. Se sua linguagem específica do domínio tem erros de validação, você não pode gerar o código-fonte. O processo de geração de código-fonte dos modelos é executado clicando **transformar todos os modelos** na barra de ferramentas do Gerenciador de soluções. Sempre que você modificar a definição de linguagem, certifique-se **transformar todos os modelos**. Para obter mais informações, consulte [como: criar uma solução de linguagem específica do domínio](../modeling/how-to-create-a-domain-specific-language-solution.md).  
  
## <a name="customization-of-dsl-tools"></a>Personalização das ferramentas DSL  
 Você pode fornecer código adicional para refinar o comportamento do modelo e definir restrições em seu idioma. Se necessário, você pode fazer alterações significativas, modificando os modelos de texto.  
  
## <a name="distributing-your-dsl-solution"></a>Distribuir sua solução DSL  
 Ferramentas DSL gera um pacote que está hospedado em [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]. O pacote exibe uma caixa de ferramentas, um Gerenciador de DSL e outros elementos de interface do usuário que permitem aos usuários criar modelos usando sua linguagem específica do domínio.  
  
 Quando você compila e executa a solução de ferramentas DSL [!INCLUDE[vsprvs](../includes/vsprvs-md.md)], uma segunda instância do [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] mostra a aparência de sua linguagem específica do domínio para o usuário da linguagem. Depois de verificar se tudo está funcionando corretamente, você pode distribuir o `.vsix` arquivo que você encontrará na pasta de compilação do projeto DslPackage. Esse arquivo pode ser usado para instalar a DSL como uma [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] extensão em outros computadores.  Para obter mais informações, consulte [implantar soluções de linguagem específica do domínio](../modeling/deploying-domain-specific-language-solutions.md).  
  
## <a name="see-also"></a>Consulte também  
 [A instância Experimental](../extensibility/the-experimental-instance.md)   
 [Glossário de ferramentas de linguagem específica do domínio](http://msdn.microsoft.com/en-us/ca5e84cb-a315-465c-be24-76aa3df276aa)



