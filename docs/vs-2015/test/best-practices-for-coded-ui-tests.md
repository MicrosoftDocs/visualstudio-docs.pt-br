---
title: Melhores práticas para testes de IU codificados | Microsoft Docs
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
- coded UI tests, best practices
ms.assetid: d5aef766-a24c-4f1f-ac9b-e5462b6627d4
caps.latest.revision: 41
ms.author: gewarren
manager: douge
ms.openlocfilehash: 1a067751662895f99f4caf95d487dc8c8a4672f3
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49903576"
---
# <a name="best-practices-for-coded-ui-tests"></a>Práticas recomendadas para testes de IU codificados
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Este tópico descreve as melhores práticas a seguir ao desenvolver testes de IU codificados.  
  
 **Requisitos**  
  
-   Visual Studio Enterprise  
  
## <a name="best-practices"></a>Práticas recomendadas  
 Use as orientações a seguir para criar um teste de IU codificado flexível.  
  
- Use o **Construtor de Teste de IU Codificado** sempre que possível.  
  
- Não modifique o arquivo `UIMap.designer.cs` diretamente. Se fizer isso, as alterações no arquivo serão substituídas.  
  
- Crie o teste como uma sequência de métodos registrados. Para saber mais sobre como registrar um método, consulte [Criando Testes de IU Codificados](../test/use-ui-automation-to-test-your-code.md#VerifyingCodeUsingCUITCreate).  
  
- Cada método registrado deve agir em uma única página, formulário ou caixa de diálogo. Crie um novo método de teste para cada nova página, formulário ou caixa de diálogo.  
  
- Ao criar um método, use um nome de método significativo em vez do nome padrão. Um nome significativo ajuda a identificar a finalidade do método.  
  
- Quando possível, limite cada método registrado a menos de 10 ações. Essa abordagem modular torna mais fácil substituir um método se a interface do usuário for alterada.  
  
- Crie cada asserção usando o **Construtor de Teste de IU Codificado**, que adiciona automaticamente um método de asserção ao arquivo `UIMap.Designer.cs`.  
  
- Se a interface do usuário (IU) for alterada, registre novamente os métodos de teste, os métodos de asserção ou as seções afetadas de um método de teste existente.  
  
- Crie um arquivo <xref:Microsoft.VisualStudio.TestTools.UITest.Common.UIMap.UIMap> separado para cada módulo em seu aplicativo em teste. Para obter mais informações, consulte [Testar um Aplicativo Grande com Vários Mapas de Interface do Usuário](../test/testing-a-large-application-with-multiple-ui-maps.md).  
  
- No aplicativo em teste, use nomes significativos ao criar os controles de interface do usuário. Isso confere mais significado e usabilidade aos nomes de controle gerados automaticamente.  
  
- Caso esteja criando asserções por meio de codificação com a API, crie um método para cada asserção na parte da classe <xref:Microsoft.VisualStudio.TestTools.UITest.Common.UIMap.UIMap> que está no arquivo `UIMap.cs`. Chame esse método do seu método de teste para executar a asserção.  
  
- Se estiver codificando diretamente com a API, use as propriedades e métodos nas classes geradas no arquivo `UIMap.Designer.cs` do código o tanto quanto for possível. Essas classes tornarão o trabalho mais fácil e confiável e aumentarão a produtividade.  
  
  Os testes de IU codificados se adaptam automaticamente a várias alterações na interface do usuário. Se, por exemplo, a posição ou cor de um elemento da interface do usuário forem alteradas, na maioria das vezes, o teste de IU codificado ainda encontrará o elemento correto.  
  
  Durante uma execução de teste, os controles de interface do usuário são localizados pela estrutura de teste por meio de um conjunto de propriedades de pesquisa aplicadas a cada classe de controle nas definições criadas pelo **Construtor de Teste de IU Codificado** no arquivo `UIMap.Designer.cs`. As propriedades de pesquisa contêm pares nome-valor de nomes e valores da propriedade que podem ser usados para identificar o controle, como as propriedades <xref:Microsoft.VisualStudio.TestTools.UITesting.UITestControl.FriendlyName%2A>, <xref:Microsoft.VisualStudio.TestTools.UITesting.UITestControl.Name%2A> e <xref:Microsoft.VisualStudio.TestTools.UITesting.UITestControl.ControlType%2A> do controle. Se as propriedades de pesquisa não forem alteradas, o teste de IU codificado encontrará o controle na interface do usuário com êxito. Se as propriedades de pesquisa forem alteradas, o teste de IU codificado terá um algoritmo de correspondência inteligente que aplica a heurística para encontrar controles e janelas na interface do usuário. Quando a interface do usuário é alterada, pode ser possível modificar as propriedades de pesquisa dos elementos identificados anteriormente para garantir que eles sejam encontrados.  
  
## <a name="what-to-do-if-your-user-interface-changes"></a>O que fazer se a interface do usuário for alterada  
 Interfaces do usuário mudam frequentemente durante o desenvolvimento. Aqui estão algumas maneiras de reduzir o efeito dessas alterações:  
  
- Localize o método registrado que faz referência a esse controle e use o **Construtor de Teste de IU Codificado** para registrar as ações desse método. É possível usar o mesmo nome para que o método substitua as ações existentes.  
  
- Se um controle tiver uma asserção inválida:  
  
  -   Exclua o método que contém a asserção.  
  
  -   Remova a chamada para esse método do método de teste.  
  
  -   Adicione uma nova asserção arrastando o botão de fios para o controle de interface do usuário, abra o mapa da interface do usuário e adicione a nova asserção.  
  
  Para saber mais sobre como registrar testes de IU codificados, consulte [Usar a Automação de Interface do Usuário para Testar o Código](../test/use-ui-automation-to-test-your-code.md).  
  
## <a name="what-to-do-if-a-background-process-needs-to-complete-before-the-test-can-continue"></a>O que fazer se um processo de segundo plano precisar ser concluído antes de continuar o teste  
 Talvez seja necessário esperar até que o processo seja concluído para continuar com a próxima ação de interface do usuário. Para fazer isso, você pode usar <xref:Microsoft.VisualStudio.TestTools.UITesting.PlaybackSettings.WaitForReadyLevel%2A> para esperar para que o teste continue, como no exemplo a seguir.  
  
```  
// Set the playback to wait for all threads to finish  
Playback.PlaybackSettings.WaitForReadyLevel = WaitForReadyLevel.AllThreads;  
  
// Press the submit button  
this.UIMap.ClickSubmit();  
  
// Reset the playback to wait only for the UI thread to finish  
Playback.PlaybackSettings.WaitForReadyLevel = WaitForReadyLevel.UIThreadOnly;  
```  
  
## <a name="see-also"></a>Consulte também  
 <xref:Microsoft.VisualStudio.TestTools.UITest.Common.UIMap.UIMap>   
 <xref:Microsoft.VisualStudio.TestTools.UITesting>   
 [Usar a automação de interface do usuário para testar o código](../test/use-ui-automation-to-test-your-code.md)   
 [Criando testes de IU codificados](../test/use-ui-automation-to-test-your-code.md#VerifyingCodeUsingCUITCreate)   
 [Testando um aplicativo grande com vários mapas de interface do usuário](../test/testing-a-large-application-with-multiple-ui-maps.md)   
 [Configurações e plataformas com suporte para testes de IU codificados e gravações das ações](../test/supported-configurations-and-platforms-for-coded-ui-tests-and-action-recordings.md)



