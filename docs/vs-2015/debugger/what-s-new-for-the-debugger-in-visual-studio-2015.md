---
title: O que há de novo no depurador no Visual Studio 2015 | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-debug
ms.tgt_pltfrm: ''
ms.topic: article
dev_langs:
- FSharp
- VB
- CSharp
- C++
helpviewer_keywords:
- debugger, what's new
- what's new [debugger]
- debugging [Visual Studio], what's new
- what's new [Visual Studio], debugging
ms.assetid: 2aed9caa-2384-4e49-8595-82d8b06cf271
caps.latest.revision: 86
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 859233c1c79360f28e306dc0fca7df574cb39ccf
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51774881"
---
# <a name="whats-new-for-the-debugger-in-visual-studio-2015"></a>O que há de novo no depurador no Visual Studio 2015
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Para obter informações sobre tudo o que há de novas no Visual Studio 2015 atualização 1 depuração e diagnóstico, consulte [notas de versão do Visual Studio 2015 atualização 1](https://www.visualstudio.com/news/vs2015-update1-vs#debug).  
  
 Para obter informações sobre tudo o que há de novas no Visual Studio 2015 RTM depuração e diagnóstico, consulte [notas de versão do Visual Studio 2015](https://www.visualstudio.com/news/vs2015-vs#debug).  
  
## <a name="visual-studio-2015-update-1-changes"></a>Alterações do Visual Studio 2015 atualização 1  
 C++ editar e continuar dá suporte a mais recursos. Para obter mais informações, consulte [editar e continuar (Visual C++)](../debugger/edit-and-continue-visual-cpp.md).  
  
 Para depurar violações de acesso do Visual C++, uma nova caixa de diálogo de exceção especifica o ponteiro que causou a exceção. Para obter mais informações, consulte [como depurar uma violação de acesso?](../debugger/how-can-i-debug-an-access-violation-q.md) e [aperfeiçoamento em violações de acesso de depuração C++ no Visual Studio 2015 atualização 1](http://blogs.msdn.com/b/visualstudioalm/archive/2015/10/29/improvement-to-debugging-c-access-violations-in-visual-studio-2015-update-1.aspx)  
  
## <a name="visual-studio-2015-rtm-debugger-ui-and-hotkey-changes"></a>IU do depurador do Visual Studio 2015 RTM e alterações de tecla de acesso  
 Há alterações significativas de interface do usuário em exceções de interface do usuário e os pontos de interrupção.  
  
### <a name="breakpoints"></a>Pontos de interrupção  
 No Visual Studio 2015, há uma nova maneira de configurar os pontos de interrupção, que é o **configurações de ponto de interrupção** janela.  
  
 Aqui está um resumo das janelas de pontos de interrupção principais e as teclas de atalho:  
  
|Recurso|Localização do menu|Tecla de acesso|  
|-------------|-------------------|------------|  
|Novo ponto de interrupção, alternar ponto de interrupção|**Depurar / ativar/desativar ponto de interrupção**<br /><br /> menu de contexto no editor / **Inserir ponto de interrupção**<br /><br /> Clique na margem esquerda|F9|  
|Novo ponto de interrupção de função|**Depurar / novo ponto de interrupção de ponto de interrupção de função**|No Visual Studio 2015 RTM (com nenhuma atualização), use ALT + F9, B<br /><br /> No Visual Studio 2015 atualização 1 e posterior, use CTRL + B|  
|**Pontos de interrupção** janela|**Depurar / Windows / pontos de interrupção**|CTRL + ALT + B|  
|**Configurações de ponto de interrupção**, **condições**|menu de contexto no ponto de interrupção / **condições**|ALT + F9, C|  
|**Configurações de ponto de interrupção**, **ações**|menu de contexto no ponto de interrupção / **ações**|Nenhuma tecla de acesso|  
  
 Para obter mais informações, consulte os seguintes artigos:  
  
1.  [Usando pontos de interrupção](../debugger/using-breakpoints.md)  
  
2.  [Nova experiência de configuração de ponto de interrupção](http://blogs.msdn.com/b/visualstudioalm/archive/2014/10/06/new-breakpoint-configuration-experience.aspx)  
  
3.  [Experiência de configuração do ponto de interrupção](http://channel9.msdn.com/Events/Visual-Studio/Connect-event-2014/711)  
  
### <a name="exception-settings"></a>Configurações de exceção  
 O novo **configurações de exceção** janela permite que você especifique o tipo de tratamento de exceções, você deseja para exceções únicas ou categorias de exceções.  
  
|Recurso|Localização do menu|Tecla de acesso|  
|-------------|-------------------|------------|  
|**Configurações de exceção** janela|**Depurar / Windows / configurações de exceção**|CTRL + ALT + E|  
  
 Para obter mais informações, consulte os seguintes artigos:  
  
1.  [Gerenciando exceções com o depurador](../debugger/managing-exceptions-with-the-debugger.md)  
  
2.  [A nova janela de exceções](http://blogs.msdn.com/b/visualstudioalm/archive/2015/02/23/the-new-exception-settings-window-in-visual-studio-2015.aspx)  
  
### <a name="edit-and-continue"></a>Editar e continuar  
 No Visual Studio 2015, você pode definir o editar e continuar na **Ferramentas / opções / depuração / geral** página. Nas versões anteriores, essas configurações foram em uma categoria de opções separadas.  
  
### <a name="attach-to-process"></a>Anexar ao processo  
 No Visual Studio 2015 a anexar ao processo de comando está disponível somente no menu Depurar. Na versão anterior tinha sido disponível no menu Ferramentas. O CTRL + ALT + P teclas de atalho funciona em todas as versões.  
  
## <a name="see-also"></a>Consulte também  
 [Depurando no Visual Studio](../debugger/debugging-in-visual-studio.md)



