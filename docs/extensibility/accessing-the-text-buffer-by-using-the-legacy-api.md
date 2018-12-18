---
title: Acessando o Buffer de texto usando a API herdada | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], legacy - text buffers
ms.assetid: cd6cf4ae-fff5-4e23-b293-7cbafdb8aed2
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 3347fc2fd03a2eb6b466145672d3aebb77ad71a6
ms.sourcegitcommit: 8ee7efb70a1bfebcb6dd9855b926a4ff043ecf35
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/17/2018
ms.locfileid: "39078008"
---
# <a name="access-the-text-buffer-by-using-the-legacy-api"></a>Acessar o buffer de texto, usando a API herdada
O texto é responsável por gerenciar os fluxos de texto e persistência de arquivo. Embora o buffer pode ler ou gravar outros formatos, toda a comunicação comum com o buffer é executada usando o Unicode. Nas APIs herdadas, o buffer de texto pode usar aquele - ou um sistema de coordenadas bidimensional para identificar os locais de caractere no buffer.  
  
## <a name="one--and-two-dimension-coordinate-systems"></a>Dimensão de um e dois sistemas de coordenadas  
 Uma posição de coordenadas unidimensional baseia-se a posição de um caractere a partir do primeiro caractere no buffer, como 147. Você usa o <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextStream> interface para acessar um unidimensional local no buffer. Um sistema de coordenadas bidimensional é baseado em pares de linha e índice. Por exemplo, um caractere no buffer em 43, 5 seria na linha 43, cinco caracteres à direita do primeiro caractere na linha. Você acessa um local bidimensional no buffer usando o <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextLines> interface. Tanto a <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextLines> e o <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextStream> interfaces são implementadas pelo objeto de buffer de texto (<xref:Microsoft.VisualStudio.TextManager.Interop.VsTextBuffer>) e pode ser acessado entre si usando `QueryInterface`. O diagrama a seguir mostra essas e outras interfaces principais em <xref:Microsoft.VisualStudio.TextManager.Interop.VsTextBuffer>.  
  
 ![Objeto de Buffer de texto](../extensibility/media/vstextbuffer.gif "vsTextBuffer")  
Objeto de buffer de texto  
  
 Embora o sistema de coordenadas funcione no buffer de texto, ele é otimizado para usar coordenadas bidimensionais. Um sistema de coordenadas unidimensional pode criar sobrecarga de desempenho. Portanto, use o sistema de coordenadas bidimensional sempre que possível.  
  
 O responsabilidade de segundo do buffer de texto é a persistência de arquivo. Para fazer isso, o objeto de buffer de texto implementa <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistDocData2> e atua como o componente de objeto de dados de documentos para itens de projeto e outros componentes do ambiente envolvidos na persistência. Para obter mais informações, consulte [abrindo e salvando itens de projeto](../extensibility/internals/opening-and-saving-project-items.md).  
  
## <a name="in-this-section"></a>Nesta seção  
 [Alterar as configurações de exibição usando a API herdada](../extensibility/changing-view-settings-by-using-the-legacy-api.md)  
 Explica como alterar as configurações de exibição usando a API herdada.  
  
 [Use o Gerenciador de texto para monitorar as configurações globais](../extensibility/using-the-text-manager-to-monitor-global-settings.md)  
 Explica como usar o Gerenciador de texto para monitorar as configurações globais.  
  
## <a name="see-also"></a>Consulte também  
 [Dentro do editor de núcleo](../extensibility/inside-the-core-editor.md)