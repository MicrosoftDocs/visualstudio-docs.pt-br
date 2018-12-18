---
title: Grade de propriedades de exibição | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- properties [Visual Studio SDK], grid
ms.assetid: 318e41b0-acf5-4842-b85e-421c9d5927c5
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 52bda19b6b4acf02b70963ab52431334d2f1f1fc
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49836665"
---
# <a name="properties-display-grid"></a>Grade de exibição de propriedades
O **propriedades** janela exibe os campos dentro de uma grade. A coluna esquerda contém os nomes de propriedade; a coluna à direita contém os valores de propriedade.  
  
## <a name="working-with-the-grid"></a>Trabalhar com a grade  
 A lista de duas colunas mostra as propriedades de configuração independente que podem ser alteradas em tempo de design e suas configurações atuais. Observe que todas as propriedades não podem ser mostradas. Uma propriedade pode ser definida como oculta, por exemplo, Implementando o <xref:Microsoft.VisualStudio.Shell.Interop.IVsPerPropertyBrowsing.HideProperty%2A> método. Especificamente, para ocultar propriedades que têm propriedades filho:  
  
1. Defina as `pfDisplay` parâmetro no <xref:Microsoft.VisualStudio.Shell.Interop.IVsPerPropertyBrowsing.DisplayChildProperties%2A> para `FALSE`.  
  
2. Defina as `pfHide` parâmetro no <xref:Microsoft.VisualStudio.Shell.Interop.IVsPerPropertyBrowsing.HideProperty%2A> para `TRUE`.  
  
   Informações de envio por push para o **propriedades** janela, o IDE usa <xref:Microsoft.VisualStudio.Shell.Interop.ISelectionContainer>. <xref:Microsoft.VisualStudio.Shell.Interop.ISelectionContainer> é chamado pelo VSPackages para cada janela que contém objetos selecionáveis com propriedades relacionadas a serem exibidos na **propriedades** janela. **Gerenciador de soluções**da implementação de <xref:Microsoft.VisualStudio.Shell.Interop.ISelectionContainer> chamadas `GetProperty` usando <xref:Microsoft.VisualStudio.Shell.Interop.__VSHPROPID> em sua hierarquia do projeto para adquirir os objetos navegáveis na hierarquia.  
  
   Se não der suporte o VSPackage <xref:Microsoft.VisualStudio.Shell.Interop.__VSHPROPID>, o IDE tenta usar <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy.GetProperty%2A> usando o valor para <xref:Microsoft.VisualStudio.Shell.Interop.__VSHPROPID> que forneçam o item de hierarquia ou itens.  
  
   Seu projeto de VSPackage não precisa criar <xref:Microsoft.VisualStudio.Shell.Interop.ISelectionContainer> porque o pacote de janela fornecida pelo IDE que o implementa (por exemplo, **Gerenciador de soluções**) constrói <xref:Microsoft.VisualStudio.Shell.Interop.ISelectionContainer> em seu nome.  
  
   <xref:Microsoft.VisualStudio.Shell.Interop.ISelectionContainer> consiste em três métodos que são chamados pelo IDE:  
  
- <xref:Microsoft.VisualStudio.Shell.Interop.ISelectionContainer.CountObjects%2A> contém o número de objetos selecionados a serem exibidos na **propriedades** janela.  
  
- <xref:Microsoft.VisualStudio.Shell.Interop.ISelectionContainer.GetObjects%2A> Retorna o `IDispatch` objetos que estão selecionados a serem exibidos na **propriedades** janela.  
  
- <xref:Microsoft.VisualStudio.Shell.Interop.ISelectionContainer.SelectObjects%2A> permite que qualquer um dos objetos retornados por <xref:Microsoft.VisualStudio.Shell.Interop.ISelectionContainer.GetObjects%2A> a ser selecionado pelo usuário. Isso permite que o VSPackage visualmente atualizar a seleção exibida para o usuário na interface do usuário.  
  
  O **propriedades** janela extrai informações do `IDispatch` objetos para recuperar as propriedades que está sendo procuradas. O navegador de propriedades usa `IDispatch` peça o objeto quais propriedades ele dá suporte a consultando `ITypeInfo`, que é obtida da `IDispatch::GetTypeInfo`. O navegador usa esses valores para preencher a **propriedades** janela e alterar os valores para propriedades individuais são exibidos na grade. As informações de propriedades são mantidas dentro do próprio objeto.  
  
  Porque dá suporte a objetos retornados `IDispatch`, o chamador pode obter informações como o nome do objeto com uma chamada a `IDispatch::Invoke` ou `ITypeInfo::Invoke` com um identificador de expedição predefinidos (DISPID) que representa as informações desejadas. Os DISPIDs declarados são negativos para garantir que eles não entrem em conflito com os identificadores definidos pelo usuário.  
  
  O **propriedades** janela exibe diferentes tipos de campos, dependendo dos atributos de propriedades específicas de um objeto selecionado. Esses campos incluem caixas de edição, listas suspensas e links para caixas de diálogo do editor personalizado.  
  
- Contido em uma lista enumerada de valores são recuperados por um <xref:Microsoft.VisualStudio.Shell.Interop.ISelectionContainer.GetObjects%2A> consultar para `IDispatch`. Os valores obtidos de uma lista enumerada podem ser alterados na grade de propriedades clicando duas vezes no nome do campo, ou clicando no valor e selecionando o novo valor na lista suspensa. Para propriedades que têm configurações de listas enumeradas predefinidas, duas vezes no nome da propriedade na lista de propriedades percorre as opções disponíveis. Para propriedades predefinidas com apenas duas opções, como verdadeiro/falso, clique duas vezes o nome da propriedade para alternar entre as opções.  
  
- Se <xref:Microsoft.VisualStudio.Shell.Interop.IVsPerPropertyBrowsing.HasDefaultValue%2A> é `false`, indicando que o valor foi alterado, o valor é exibido em negrito. <xref:Microsoft.VisualStudio.Shell.Interop.IVsPerPropertyBrowsing.CanResetPropertyValue%2A> é usado para determinar se o valor pode ser redefinido para o valor original. Se assim, você pode alterar para o padrão clicando duas vezes o valor e escolhendo **redefinir** no menu exibido. Caso contrário, você precisará alterar o valor para o padrão manualmente. <xref:Microsoft.VisualStudio.Shell.Interop.IVsPerPropertyBrowsing> também permite que você localizar e ocultar os nomes das propriedades exibidas durante o tempo de design, mas não afeta os nomes de propriedade exibidos durante o tempo de execução.  
  
- Clicar no botão de reticências (...) exibe uma lista de valores de propriedade na qual o usuário pode selecionar (por exemplo, um seletor de cor ou uma lista de fontes). <xref:Microsoft.VisualStudio.Shell.Interop.IProvidePropertyBuilder> fornece esses valores.  
  
## <a name="see-also"></a>Consulte também  
 [Estender as propriedades](../../extensibility/internals/extending-properties.md)