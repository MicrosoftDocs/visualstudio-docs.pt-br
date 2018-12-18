---
title: Visão geral de supressão de origem | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-devops-test
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- source suppression, code analysis
- code analysis, source suppression
ms.assetid: f1a2dc6a-a9eb-408c-9078-2571e57d207d
caps.latest.revision: 42
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: 844681d079e5565aab9eceadb73f7d8a61cbb2c6
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49209034"
---
# <a name="in-source-suppression-overview"></a>Visão geral de supressão na origem
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Supressão do código-fonte é a capacidade para suprimir ou ignorar violações de análise de código em código gerenciado, adicionando a **SuppressMessage** de atributo para os segmentos de código que fazem com que as violações. O **SuppressMessage** é um atributo condicional que está incluído nos metadados de IL do seu assembly de código gerenciado somente se o símbolo de compilação CODE_ANALYSIS for definido em tempo de compilação.  
  
 No C + + / CLI, use as macros CA_SUPPRESS_MESSAGE ou CA_GLOBAL_SUPPRESS_MESSAGE no arquivo de cabeçalho, para adicionar o atributo.  
  
 Você não deve usar supressões de código-fonte em builds de versão para impedir que os metadados de supressão na origem de envio acidentalmente. Devido ao custo de processamento de supressão de código-fonte, o desempenho do seu aplicativo também pode ser degradado, incluindo os metadados de supressão na origem.  
  
> [!NOTE]
>  Você não tem manualmente código esses atributos por conta própria. Para obter mais informações, consulte [como: suprimir avisos usando o Item de Menu](../code-quality/how-to-suppress-warnings-by-using-the-menu-item.md). O item de menu não está disponível para código C++.  
  
## <a name="suppressmessage-attribute"></a>Atributo SuppressMessage  
 Quando você com o botão direito em um aviso de análise de código a **lista de erros** e, em seguida, clique em **suprimir mensagem (NS)**, um **SuppressMessage** atributo é adicionado em seu código ou para o arquivo de supressões globais do projeto.  
  
 O **SuppressMessage** atributo tem o seguinte formato:  
  
```vb  
<Scope:SuppressMessage("Rule Category", "Rule Id", Justification = "Justification", MessageId = "MessageId", Scope = "Scope", Target = "Target")>  
```  
  
```csharp  
[Scope:SuppressMessage("Rule Category", "Rule Id", Justification = "Justification", MessageId = "MessageId", Scope = "Scope", Target = "Target")]  
  
```  
  
 [C++]  
  
```  
CA_SUPPRESS_MESSAGE("Rule Category", "Rule Id", Justification = "Justification", MessageId = "MessageId", Scope = "Scope", Target = "Target")  
  
```  
  
 Sendo que:  
  
-   **Categoria de regra** -a categoria na qual a regra é definida. Para obter mais informações sobre categorias de regras de análise de código, consulte [análise de código para avisos de código gerenciado](../code-quality/code-analysis-for-managed-code-warnings.md).  
  
-   **Id da regra** -o identificador da regra. O suporte inclui tanto um nome curto e longo para o identificador de regra. O nome curto é CAXXXX; o nome longo é CAXXXX:FriendlyTypeName.  
  
-   **Justificação** -o texto que é usado para documentar o motivo para suprimir a mensagem.  
  
-   **Id da mensagem** -identificador exclusivo de um problema para cada mensagem.  
  
-   **Escopo** -o de destino no qual o aviso está sendo suprimido. Se o destino não for especificado, ele é definido como o destino do atributo. Escopos com suporte incluem o seguinte:  
  
    -   Módulo  
  
    -   Namespace  
  
    -   Recurso  
  
    -   Tipo  
  
    -   Membro  
  
-   **Destino** – um identificador que é usado para especificar o destino no qual o aviso está sendo suprimido. Ele deve conter um nome totalmente qualificado de item.  
  
## <a name="suppressmessage-usage"></a>Uso de SuppressMessage  
 Avisos da análise de código são suprimidos no nível ao qual uma instância das **SuppressMessage** atributo é aplicado. O objetivo é acoplar rigidamente as informações de supressão para o código onde ocorre a violação.  
  
 A forma geral de supressão inclui a categoria de regra e um identificador de regra que contém uma representação legível por humanos opcional do nome da regra. Por exemplo,  
  
 `[SuppressMessage("Microsoft.Design", "CA1039:ListsAreStrongTyped")]`  
  
 Se houver motivos de desempenho estrito para minimizar os metadados de supressão na origem, o nome da regra pode ser removido. A categoria de regra e a sua ID de regra juntos, constituem um identificador de regra suficientemente exclusivo. Por exemplo,  
  
 `[SuppressMessage("Microsoft.Design", "CA1039")]`  
  
 Esse formato não é recomendado devido a questões de facilidade de manutenção.  
  
## <a name="suppressing-multiple-violations-within-a-method-body"></a>Suprimindo várias violações dentro de um corpo de método  
 Atributos só podem ser aplicados a um método e não podem ser incorporados dentro do corpo do método. No entanto, você pode especificar o identificador como a ID da mensagem para distinguir várias ocorrências de uma violação de dentro de um método.  
  
 [!code-cpp[InSourceSuppression#1](../snippets/cpp/VS_Snippets_CodeAnalysis/InSourceSuppression/cpp/insourcesuppression.cpp#1)]
 [!code-csharp[InSourceSuppression#1](../snippets/csharp/VS_Snippets_CodeAnalysis/InSourceSuppression/cs/InSourceSuppression.cs#1)]
 [!code-vb[InSourceSuppression#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/InSourceSuppression/vb/InSourceSuppression.vb#1)]  
  
## <a name="generated-code"></a>Código gerado  
 Compiladores de código gerenciado e algumas ferramentas de terceiros geram código para facilitar o desenvolvimento rápido de código. Código gerado pelo compilador que aparece nos arquivos de origem geralmente é marcado com o **GeneratedCodeAttribute** atributo.  
  
 Você pode escolher se deseja suprimir avisos de análise de código e erros de código gerado. Para obter informações sobre como suprimir esses avisos e erros, consulte [como: suprimir avisos para o código gerado pelo](../code-quality/how-to-suppress-code-analysis-warnings-for-generated-code.md).  
  
 Observe que a análise de código ignora **GeneratedCodeAttribute** quando ele é aplicado a um assembly inteiro ou um único parâmetro. Nessas situações ocorrerem raramente.  
  
## <a name="global-level-suppressions"></a>Supressões no nível global  
 A ferramenta de análise de código gerenciado examina **SuppressMessage** atributos que são aplicados no nível do assembly, módulo, tipo, membro ou parâmetro. Também é acionado violações em relação a recursos e namespaces. Essas violações deve ser aplicadas no nível global no escopo e são direcionadas. Por exemplo, a seguinte mensagem suprime uma violação de namespace:  
  
 `[module: SuppressMessage("Microsoft.Design", "CA1020:AvoidNamespacesWithFewTypes", Scope = "namespace", Target = "MyNamespace")]`  
  
> [!NOTE]
>  Quando você suprime um aviso com escopo de namespace, ele suprime o aviso em relação ao namespace em si. Ele não suprime o aviso em relação aos tipos no namespace.  
  
 Qualquer supressão pode ser expressos com a especificação de um escopo explícito. Esses supressões devem residir no nível global. Você não pode especificar a supressão de nível de membro decorando um tipo.  
  
 Supressões no nível global são a única maneira de suprimir as mensagens que se referem ao código gerado pelo compilador que não é mapeado para a fonte de usuário fornecido explicitamente. Por exemplo, o código a seguir suprime uma violação em relação a um construtor emitidos pelo compilador:  
  
 `[module: SuppressMessage("Microsoft.Design", "CA1055:AbstractTypesDoNotHavePublicConstructors", Scope="member", Target="Microsoft.Tools.FxCop.Type..ctor()")]`  
  
> [!NOTE]
>  Destino sempre contém o nome do item totalmente qualificado.  
  
## <a name="global-suppression-file"></a>Arquivo de supressão global  
 O arquivo de supressão global mantém supressões supressões no nível global ou supressões que não especificam um destino. Por exemplo, supressões de violações no nível de assembly são armazenadas nesse arquivo. Além disso, alguns supressões de ASP.NET são armazenados nesse arquivo, porque as configurações de nível de projeto não estão disponíveis para o código por trás de um formulário. Uma supressão global é criada e adicionada ao seu projeto na primeira vez que você seleciona os **no arquivo de supressão do projeto** opção do **suprimir mensagem (NS)** comando na janela lista de erros. Para obter mais informações, consulte [como: suprimir avisos usando o Item de Menu](../code-quality/how-to-suppress-warnings-by-using-the-menu-item.md).  
  
## <a name="see-also"></a>Consulte também  
 <xref:System.Diagnostics.CodeAnalysis>



