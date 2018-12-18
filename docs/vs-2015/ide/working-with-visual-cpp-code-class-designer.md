---
title: Trabalhando com código do Visual C++ (Designer de Classe) | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-general
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- vs.classdesigner.cpplimitation
helpviewer_keywords:
- Visual C++, Class Designer
- Class Designer, Visual C++ support
- Class Designer, limitations
- Class Designer, tasks in Visual C++
- Visual C++, class diagrams
- C++, class diagrams
- C++, Class Designer
ms.assetid: f5b40921-2ef7-4de0-b595-45b44c79ffa6
caps.latest.revision: 27
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: f777c9bdd0cf2ea300d2df8e7cbfbc8900c25c2a
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49929524"
---
# <a name="working-with-visual-c-code-class-designer"></a>Trabalhando com código do Visual C++ (Designer de Classe)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

O Designer de Classe exibe uma superfície de design visual chamada um *diagrama de classe* que fornece uma representação visual dos elementos de código no projeto. É possível usar diagramas de classe para criar e visualizar classes e outros tipos em um projeto.  
  
 O Designer de Classe dá suporte aos seguintes elementos de código C++:  
  
-   Classe (semelhante a uma forma de classe gerenciada, com exceção de que ela pode ter vários relacionamentos de herança)  
  
-   Classe anônima (exibe o nome gerado do Modo de Exibição de Classe para o tipo anônimo)  
  
-   Classe de modelo  
  
-   Estrutura  
  
-   Enum  
  
-   Macro (exibe a exibição pós-processada da macro)  
  
-   DefTipo  
  
> [!NOTE]
>  Isso não é o mesmo que o diagrama de classe UML, que pode ser criado em um Projeto de Modelagem. Para obter mais informações, consulte [Diagramas de classe UML: Referência](../modeling/uml-class-diagrams-reference.md).  
  
## <a name="troubleshooting-type-resolution-and-display-issues"></a>Solucionando problemas de exibição e resolução de tipo  
  
### <a name="location-of-source-files"></a>Local dos arquivos de origem  
 O Designer de Classe não mantém controle sobre a localização dos arquivos de origem. Portanto, se você modificar a estrutura do projeto ou mover os arquivos de origem no projeto, o Designer de Classe pode perder o controle do tipo (especialmente, o tipo de origem de um typedef, classes base ou tipos de associação). É possível receber um erro como **O Designer de Classe não pode exibir este tipo**. Se você fizer isso, arraste o código-fonte realocado ou modificado para o diagrama de classe, para exibi-lo novamente.  
  
### <a name="update-and-performance-issues"></a>Problemas de atualização e desempenho  
 Para projetos do Visual C++, pode levar de 30 a 60 segundos para que uma alteração no arquivo de origem seja exibida no diagrama de classe. Esse atraso também pode fazer com que o Designer de Classe gere o erro **Nenhum tipo foi encontrado na seleção**. Se você receber um erro como esse, clique em **Cancelar** na mensagem de erro e aguarde até que o elemento de código seja exibido no Modo de Exibição de Classe. Depois de fazer isso, o Designer de Classe deverá exibir o tipo.  
  
 Se um diagrama de classe não for atualizado com as alterações feitas no código, talvez seja necessário fechar o diagrama e abri-lo novamente.  
  
### <a name="type-resolution-issues"></a>Problemas de resolução de tipo  
 O Designer de Classe poderá não resolver tipos pelos seguintes motivos:  
  
- O tipo está em um projeto ou assembly que não é referenciado no projeto que contém o diagrama de classe. Para corrigir esse erro, adicione uma referência ao projeto ou ao assembly que contém o tipo. Para obter mais informações, consulte [NIB: Como adicionar ou remover referências usando a caixa de diálogo Adicionar Referência](http://msdn.microsoft.com/en-us/3bd75d61-f00c-47c0-86a2-dd1f20e231c9).  
  
- O tipo não está no escopo correto e, portanto, o Designer de Classe não pode localizá-lo. Verifique se o código não tem uma declaração `using`, `imports` ou `#include` ausente. Além disso, verifique se você não moveu o tipo (ou um tipo relacionado) para fora do namespace em que ele estava originalmente localizado.  
  
- O tipo não existe (ou foi comentado). Para corrigir esse erro, verifique se você não comentou nem excluiu o tipo.  
  
- O tipo está localizado em uma biblioteca referenciada por uma diretiva #import. Uma possível solução alternativa é adicionar o código gerado (o arquivo .tlh) manualmente a uma diretiva #include no arquivo de cabeçalho.  
  
  O erro que provavelmente você receberá para um problema de resolução de tipo é **O código não pôde ser encontrado em uma ou mais formas no diagrama de classe '\<element>'**. Essa mensagem de erro não indica necessariamente que o código tem um erro. Ela indica apenas que o designer de classe não pôde exibir o código. Tente as medidas a seguir.  
  
- Verifique se o tipo existe. Verifique se você não comentou nem excluiu o código-fonte acidentalmente.  
  
- Verifique se o Designer de Classe dá suporte ao tipo inserido. Consulte [Limitações de elementos de código C++](#limitations).  
  
- Tente resolver o tipo. O tipo pode estar em um projeto ou assembly que não é referenciado no projeto que contém o diagrama de classe. Para corrigir esse erro, adicione uma referência ao projeto ou ao assembly que contém o tipo. Para obter mais informações, consulte [NIB: Como adicionar ou remover referências usando a caixa de diálogo Adicionar Referência](http://msdn.microsoft.com/en-us/3bd75d61-f00c-47c0-86a2-dd1f20e231c9).  
  
- Verifique se o tipo está no escopo correto para que o Designer de Classe possa localizá-lo. Verifique se o código não tem uma declaração `using`, `imports` ou `#include` ausente. Além disso, verifique se você não moveu o tipo (ou um tipo relacionado) para fora do namespace em que ele estava originalmente localizado.  
  
### <a name="troubleshooting-other-error-messages"></a>Solucionando problemas de outras mensagens de erro  
 Você pode obter ajuda com a solução de erros e avisos nos fóruns públicos do Microsoft Developer Network (MSDN). Visite o [Fórum do Designer de Classe do Visual Studio](http://go.microsoft.com/fwlink/?linkid=160754).  
  
##  <a name="limitations"></a> Limitações de elementos de código C++  
  
-   Quando um projeto do Visual C++ é carregado, o Designer de Classe funciona em modo somente leitura. É possível alterar o diagrama de classe, mas não é possível salvar alterações do diagrama de classe de volta no código-fonte.  
  
-   O Designer de Classe dá suporte somente à semântica nativa do C++. Para projetos do Visual C++ compilados em código gerenciado, o Designer de Classe visualizará apenas elementos de código que são tipos nativos. Portanto, é possível adicionar um diagrama de classe a um projeto, mas o Designer de Classe não permitirá a visualização de elementos nos quais a propriedade `IsManaged` está definida como `true` (ou seja, tipos de valor e tipos de referência).  
  
-   Para projetos do Visual C++, o Designer de Classe lê somente a definição do tipo. Por exemplo, suponha que você defina um tipo em um arquivo de cabeçalho (.h) e defina seus membros em um arquivo de implementação (.cpp). Se você invocar “Exibir Diagrama de Classe” no arquivo de implementação (.cpp), o Designer de Classe não exibirá nada. Como outro exemplo, se você invocar “Exibir Diagrama de Classe” em um arquivo .cpp que usa uma instrução `#include` para incluir outros arquivos, mas que não contém nenhuma definição de classe real, o Designer de Classe não exibirá nada novamente.  
  
-   Arquivos IDL (.idl), que definem interfaces COM e bibliotecas de tipo, não exibem diagramas, a menos que sejam compilados para o código C++ nativo.  
  
-   O Designer de Classe não dá suporte a funções globais e variáveis.  
  
-   O Designer de Classe não dá suporte a uniões. Esse é um tipo especial de classe no qual a memória alocada é apenas a quantidade necessária para o maior membro de dados da união.  
  
-   O Designer de Classe não exibe tipos de dados básicos como `int` e `char`.  
  
-   O Designer de Classe não exibe tipos que são definidos fora do projeto atual se o projeto não tem referências corretas para esses tipos.  
  
-   O Designer de Classe pode exibir tipos aninhados, mas não os relacionamentos entre um tipo aninhado e outros tipos.  
  
-   O Designer de Classe não pode exibir tipos que são nulos ou que derivam de um tipo nulo.  
  
## <a name="see-also"></a>Consulte também  
 [Projetando e exibindo classes e tipos](../ide/designing-and-viewing-classes-and-types.md)   
 [Trabalhando com classes e outros tipos (Designer de Classe)](../ide/working-with-classes-and-other-types-class-designer.md)   
 [Trabalhando com diagramas de classe (Designer de Classe)](../ide/working-with-class-diagrams-class-designer.md)   
 [Projetando classes e tipos (Designer de Classe)](../ide/designing-classes-and-types-class-designer.md)   
 [Informações adicionais sobre erros do Designer de Classe](../ide/additional-information-about-class-designer-errors.md)   
 [Classes do Visual C++ no Designer de Classe](../ide/visual-cpp-classes-in-class-designer.md)   
 [Estruturas do Visual C++ no Designer de Classe](../ide/visual-cpp-structures-in-class-designer.md)   
 [Enumerações do Visual C++ no Designer de Classe](../ide/visual-cpp-enumerations-in-class-designer.md)   
 [Typedefs do Visual C++ no Designer de Classe](../ide/visual-cpp-typedefs-in-class-designer.md)



