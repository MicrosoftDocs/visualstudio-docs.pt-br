---
title: 'Como: adicionar marcadores de texto padrão | Microsoft Docs'
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], legacy - standard text markers
ms.assetid: a39fca69-0014-474c-933f-51f0e9b9617e
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 4dd34b14b89c78d01f1d4acab57f33014860d7ba
ms.sourcegitcommit: 06db1892fff22572f0b0a11994dc547c2b7e2a48
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/08/2018
ms.locfileid: "39638811"
---
# <a name="how-to-add-standard-text-markers"></a>Como: adicionar marcadores de texto padrão
Use o procedimento a seguir para criar um dos tipos de marcador de texto padrão fornecidos com o [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] editor de núcleo.  
  
## <a name="to-create-a-text-marker"></a>Para criar um marcador de texto  
  
1.  Dependendo se você estiver usando um sistema de coordenadas de um ou bidimensional, chame o <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextLines.CreateLineMarker%2A> método ou o <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextStream.CreateStreamMarker%2A> método para criar um marcador de texto novo.  
  
     Nessa chamada de método, especifique um tipo de marcador, um intervalo de texto para criar o marcador de failover e um <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextMarkerClient> interface. Esse método, em seguida, retorna um ponteiro para o marcador de texto criado recentemente. Tipos de marcador são tirados o <xref:Microsoft.VisualStudio.TextManager.Interop.MARKERTYPE> enumeração. Especifique um <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextMarkerClient> interface se você quiser ser informado sobre eventos de marcador.  
  
    > [!NOTE]
    >  Crie marcadores de texto no thread da interface do usuário principal somente. O editor de núcleo depende do conteúdo do buffer de texto para criar marcadores de texto e o buffer de texto não é thread-safe.  
  
## <a name="add-a-custom-command"></a>Adicionar um comando personalizado  
 Implementando o `IVsTextMarkerClient` aprimora a interface e fornecer um ponteiro para ele de um marcador de comportamento de marcador de várias maneiras. Em primeiro lugar, isso permite que você forneça dicas para o marcador e executar comandos. Isso também permite que você deseja receber notificações de evento de marcadores individuais e para criar um menu de contexto sobre o marcador. Use o procedimento a seguir para adicionar um comando personalizado para o menu de contexto do marcador.  
  
### <a name="to-add-a-custom-command-to-the-context-menu"></a>Para adicionar um comando personalizado ao menu de contexto  
  
1.  Antes do menu de contexto é exibido, o ambiente chama o <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextMarkerClient.GetMarkerCommandInfo%2A> método e passa a você um ponteiro para o marcador de texto afetado e o número do item de comando no menu de contexto.  
  
     Por exemplo, os comandos de ponto de interrupção específico no menu de contexto incluem **remover o ponto de interrupção** por meio **novo ponto de interrupção**, conforme mostrado na seguinte captura de tela.  
  
     ![Menu de contexto de marcador](../extensibility/media/vsmarkercontextmenu.gif "vsMarkercontextmenu")  
  
2.  Devolver um texto que identifica o nome do comando personalizado. Por exemplo, **remover o ponto de interrupção** pode ser um comando personalizado se o ambiente não já forneceu-lo. Você também passa novamente se o comando está com suporte, disponível e habilitado, e/ou uma alternância de ligado / desligado. O ambiente usa essas informações para exibir o comando personalizado no menu de contexto da forma correta.  
  
3.  Para executar o comando, o ambiente chama o <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextMarkerClient.ExecMarkerCommand%2A> método, passando um ponteiro para o marcador de texto e o número do comando selecionado do menu de contexto.  
  
     Use essas informações desta chamada para executar qualquer ação que o marcador de texto determina de seu comando personalizado.  
  
## <a name="see-also"></a>Consulte também  
 [Usar marcadores de texto com a API herdada](../extensibility/using-text-markers-with-the-legacy-api.md)   
 [Como: implementar o marcador de erros](../extensibility/how-to-implement-error-markers.md)   
 [Como: criar marcadores de texto personalizado](../extensibility/how-to-create-custom-text-markers.md)   
 [Como: usar marcadores de texto](../extensibility/how-to-use-text-markers.md)