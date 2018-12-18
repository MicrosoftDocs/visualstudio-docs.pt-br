---
title: IntelliSense de hospedagem | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], legacy - IntelliSense hosting
ms.assetid: 20c61f8a-d32d-47e2-9c67-bf721e2cbead
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 28fc8ca212574c054add28e69a409fde4f58308a
ms.sourcegitcommit: 06db1892fff22572f0b0a11994dc547c2b7e2a48
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/08/2018
ms.locfileid: "39638828"
---
# <a name="intellisense-hosting"></a>IntelliSense de hospedagem
O Visual Studio permite a hospedagem de IntelliSense. IntellSense hospedagem permite que você fornece o IntelliSense para código não é hospedado pelo editor de texto do Visual Studio.  
  
## <a name="intellisense-hosting-usage"></a>Uso de hospedagem do IntelliSense  
 No Visual Studio, qualquer código que tenha acesso a um conjunto de conclusão e um buffer de texto pode obter IntelliSense windows de qualquer lugar na interface do usuário (IU). Alguns cenários de exemplo disso são o preenchimento na **inspeção** janela ou no campo de condição de uma janela de propriedades do ponto de interrupção.  
  
### <a name="implementation-interfaces"></a>Interfaces de implementação  
  
#### <a name="ivsintellisensehost"></a>IVsIntellisenseHost  
 Qualquer componente de interface do usuário que hospeda as janelas pop-up do IntelliSense deve oferecer suporte a <xref:Microsoft.VisualStudio.TextManager.Interop.IVsIntellisenseHost> interface. A exibição de texto do editor de núcleo padrão inclui um estoque <xref:Microsoft.VisualStudio.TextManager.Interop.IVsIntellisenseHost> implementação para manter a funcionalidade IntelliSense atual da interface. Geralmente, os métodos do <xref:Microsoft.VisualStudio.TextManager.Interop.IVsIntellisenseHost> representam um subconjunto do que é implementado de interface a <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView> interface. O subconjunto inclui tratamento de UI IntelliSense, cursor e manipulação de seleção e funcionalidade de substituição de texto simples. Além disso, o <xref:Microsoft.VisualStudio.TextManager.Interop.IVsIntellisenseHost> interface permite separado IntelliSense "subject" e "contexto" para que o IntelliSense pode ser fornecido para entidades que não existem diretamente no buffer de texto que está sendo usado para contexto.  
  
#### <a name="ivsintellisensehostgethostflags"></a>IVsIntellisenseHost.GetHostFlags  
 Uma <xref:Microsoft.VisualStudio.TextManager.Interop.IVsIntellisenseHost> provedor de interface deve implementar o <xref:Microsoft.VisualStudio.TextManager.Interop.IVsIntellisenseHost.GetHostFlags%2A> dá suporte ao método para permitir que um cliente determinar que tipo de IntelliSense apresenta o host.  
  
 Os sinalizadores de host definidos em [IntelliSenseHostFlags](../extensibility/intellisensehostflags.md), são resumidas abaixo.  
  
|Sinalizador de Host do IntelliSense|Descrição|  
|----------------------------|-----------------|  
|IHF_READONLYCONTEXT|A configuração desta sinalizador significa que o buffer de contexto é somente leitura e edição ocorrem somente dentro do texto de assunto.|  
|IHF_NOSEPERATESUBJECT|Definir esse sinalizador significa que existe não é nenhum assunto separado do IntelliSense. A entidade existe no buffer de contexto, como os tradicionais <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView> sistema IntelliSense.|  
|IHF_SINGLELINESUBJECT|A configuração desta sinalizador significa que a entidade não for compatível com, como em uma edição de linha única em várias linhas, o **inspeção** janela.|  
|IHF_FORCECOMMITTOCONTEXT|Se esse sinalizador estiver definido e o buffer de contexto deve ser atualizado, o host permite que o sinalizador somente leitura no buffer de contexto a ser ignorada e as edições para continuar.|  
|IHF_OVERTYPE|Edição (no assunto ou contexto) deve ser feito no modo sobrescrever.|  
  
#### <a name="ivsintellisensehostbeforecompletorcommit-and-ivsintellisensehostaftercompletorcommit"></a>IVsIntellisenseHost.BeforeCompletorCommit e IVsIntellisenseHost.AfterCompletorCommit  
 Esses métodos de retorno de chamada são chamados pela janela de conclusão antes e depois que o texto é confirmado, para habilitar o processamento pré e pós-processamento.  
  
#### <a name="ivsintellisensecompletor"></a>IVsIntellisenseCompletor  
 O <xref:Microsoft.VisualStudio.TextManager.Interop.IVsIntellisenseCompletor> interface é uma versão que pode ser criada junto da janela de preenchimento padrão que é usada pelo ambiente de desenvolvimento integrado (IDE). Qualquer <xref:Microsoft.VisualStudio.TextManager.Interop.IVsIntellisenseHost> interface pode implementar o IntelliSense ao usar essa interface completor rapidamente.  
  
## <a name="see-also"></a>Consulte também  
 <xref:Microsoft.VisualStudio.TextManager.Interop>