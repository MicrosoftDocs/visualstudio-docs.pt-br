---
title: Política de modelo e na janela Propriedades | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- Properties window, template policy
ms.assetid: 1d8019d3-5e57-47ba-b358-526b0796a63b
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 8cf24f6f769ea9344d2a7716856e3c84fdf122de
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49816320"
---
# <a name="template-policy-and-the-properties-window"></a>Política de modelo e a janela Propriedades
Quando um projeto está contido dentro de um projeto de modelo da empresa, esse projeto de modelo empresarial pode impor a política. Política de modelo se torna um sistema de restrição que pode ser usado para definir valores padrão para propriedades, ocultar propriedades, adicionar propriedades e assim por diante.  
  
 Usando a diretiva de modelo para controlar a exibição das informações na **propriedades** janela é diferente da implementação do <xref:Microsoft.VisualStudio.Shell.Interop.IVsPerPropertyBrowsing>. <xref:Microsoft.VisualStudio.Shell.Interop.IVsPerPropertyBrowsing> lida com propriedades do objeto no nível do componente, enquanto a política de modelo pode ser usada para restringir as propriedades do objeto no nível da solução ou projeto. Em outras palavras  
  
- Implementar os métodos em <xref:Microsoft.VisualStudio.Shell.Interop.IVsPerPropertyBrowsing> para determinar o que é exibido o **propriedades** janela para objetos específicos  
  
- Usar a diretiva de modelo no nível de solução e projeto para determinar o que é exibido o **propriedades** janela de objetos especificadas anteriormente  
  
  Usando a diretiva de modelo para restringir seletivamente propriedades específicas na **propriedades** janela quando um item de projeto de um tipo especificado está selecionada no **Gerenciador de soluções** pode ser útil para todos os membros de a equipe de desenvolvimento trabalhando em um projeto. Por exemplo, usando a política de modelo, você pode configurar todas as informações de cadeia de caracteres de conexão em um banco de dados para desenvolvedores e verifique a cadeia de conexão somente leitura. Dessa forma, você pode fornecer uma maneira simples de garantir que cada desenvolvedor usa o caminho correto para acesso a dados.  
  
## <a name="see-also"></a>Consulte também  
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPerPropertyBrowsing>   
 [Estender as propriedades](../../extensibility/internals/extending-properties.md)