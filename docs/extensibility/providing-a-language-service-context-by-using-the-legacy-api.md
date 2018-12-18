---
title: Fornecer um contexto de serviço de linguagem, usando a API herdada | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], legacy - language service context
ms.assetid: daa2df22-9181-4bad-b007-a7d40302bce1
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 67ff7d911ef0cdd3debd920ac85e9e3265a619e3
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49909952"
---
# <a name="provide-a-language-service-context-by-using-the-legacy-api"></a>Fornecer um contexto de serviço de linguagem, usando a API herdada
Há duas opções para um serviço de linguagem fornecer o contexto de usuário usando o [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] editor de núcleo: fornecer um contexto de marcador de texto, ou fornecer todo o contexto de usuário. As diferenças entre cada são descritas aqui.  
  
 Para obter mais informações sobre como fornecer contexto para um serviço de linguagem que está conectado ao seu próprio editor, consulte [como: fornecer contexto para editores](../extensibility/how-to-provide-context-for-editors.md).  
  
## <a name="provide-text-marker-context-to-the-editor"></a>Fornecer o contexto de marcador de texto no Editor  
 Para fornecer contexto para erros do compilador indicados por marcadores de texto na [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] editor de núcleo, implemente o <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextMarkerContextProvider> interface. Nesse cenário, o serviço de linguagem fornece contexto somente quando o cursor estiver sobre um marcador de texto. Isso permite que o editor fornecer a palavra-chave na posição do cursor para o **ajuda dinâmica** janela sem atributos.  
  
## <a name="provide-all-user-context-to-the-editor"></a>Fornecer todo o contexto de usuário para o editor  
 Se você estiver criando um serviço de linguagem e estiver usando o [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] principais editor, em seguida, você pode implementar o <xref:Microsoft.VisualStudio.TextManager.Interop.IVsLanguageContextProvider> interface para fornecer contexto para o serviço de linguagem.  
  
 Para a implementação de `IVsLanguageContextProvider`, um recipiente de contexto (coleção) está anexado ao editor, o que é responsável por atualizar o recipiente de contexto. Quando o **ajuda dinâmica** janela chamadas a <xref:Microsoft.VisualStudio.Shell.Interop.IVsUserContext.Update%2A> interface no recipiente contexto no tempo ocioso, o recipiente de contexto consultará o editor para uma atualização. O editor, em seguida, notifica o serviço de linguagem que ele deve atualizar o editor e passa um ponteiro para o recipiente de contexto. Isso é feito chamando o <xref:Microsoft.VisualStudio.TextManager.Interop.IVsLanguageContextProvider.UpdateLanguageContext%2A> método do editor para o serviço de linguagem. Usando o ponteiro para o recipiente de contexto, o serviço de linguagem pode agora adicionar e remover atributos e palavras-chave. Para obter mais informações, consulte <xref:Microsoft.VisualStudio.TextManager.Interop.IVsLanguageContextProvider>.  
  
 Há duas maneiras diferentes para implementar `IVsLanguageContextProvider`:  
  
- Fornecer uma palavra-chave para o recipiente de contexto  
  
   Quando o editor é chamado para atualizar o recipiente de contexto, passe os atributos e palavras-chave apropriadas e, em seguida, retornar `S_OK`. Esse valor de retorno instrui o editor para manter seu contexto de palavra-chave e atributo em vez de fornecer a palavra-chave na posição do cursor ao recipiente de contexto.  
  
- Obter a palavra-chave da palavra-chave na posição do cursor  
  
   Quando o editor é chamado para atualizar o recipiente de contexto, passe os atributos apropriados e, em seguida, retornar `E_FAIL`. Esse valor de retorno instrui o editor para manter seus atributos no recipiente de contexto, mas atualize o recipiente de contexto com a palavra-chave na posição do cursor.  
  
  O diagrama a seguir demonstra como o contexto é fornecido para um serviço de linguagem que implementa `IVsLanguageContextProvider`.  
  
  ![Gráfico de LangServiceImplementation2](../extensibility/media/vslanguageservice2.gif "vsLanguageService2")  
  Contexto para um serviço de linguagem  
  
  Como você pode ver no diagrama, o [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] principal editor de texto tem um recipiente de contexto anexado a ele. Esse recipiente de contexto aponta para três recipientes de subcontexto separado: serviço de linguagem, o editor padrão e o marcador de texto. Os recipientes language service e o texto marcador subcontexto contêm atributos e palavras-chave para o serviço de linguagem, se o <xref:Microsoft.VisualStudio.TextManager.Interop.IVsLanguageContextProvider> interface é implementada, os marcadores de texto e se o <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextMarkerContextProvider> interface é implementada. Se você não implementar qualquer uma dessas interfaces, o editor fornece contexto para a palavra-chave na posição do cursor no recipiente de subcontexto de editor padrão.  
  
## <a name="context-guidelines-for-editors-and-designers"></a>Diretrizes de contexto para editores e designers  
 Designers e editores devem fornecer uma palavra-chave geral para o editor ou a janela do designer. Isso é feito para que um tópico de ajuda genérico, mas apropriado, será exibido para o designer ou editor quando um usuário pressiona **F1**. Um editor deve, além disso, forneça a palavra-chave atual na posição do cursor ou fornecer um termo-chave com base na seleção atual. Isso é feito para garantir que um tópico da Ajuda para o texto ou um elemento de interface do usuário apontado ou selecionado exibe quando o usuário pressiona **F1**. Um designer fornece contexto para um item selecionado em um designer, como um botão em um formulário. Editores e designers também devem se conectar a um serviço de linguagem conforme descrito na [fundamentos do serviço de linguagem herdado](../extensibility/internals/legacy-language-service-essentials.md).