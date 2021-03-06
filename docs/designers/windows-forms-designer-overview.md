---
title: Criar aplicativos do Windows Forms
description: Saiba mais sobre o Designer de Formulários do Windows no Visual Studio, que fornece uma solução rápida de desenvolvimento para a criação de aplicativos baseados em Windows Forms.
ms.custom: SEO-VS-2020
ms.date: 08/09/2019
ms.topic: overview
helpviewer_keywords:
- Windows Forms Designer
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.openlocfilehash: 768c19f78102bf19346867beda967a069c1d182e
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2021
ms.locfileid: "99844951"
---
# <a name="windows-forms-designer-overview"></a>Visão geral do Designer de Formulários do Windows

O Designer de Formulários do Windows no Visual Studio fornece uma solução rápida de desenvolvimento para criar aplicativos baseados no Windows Forms. O Designer de Formulários do Windows possibilita adicionar controles facilmente a um formulário, organizá-los e escrever código para seus eventos. Para saber mais sobre o Windows Forms, confira [Visão geral do Windows Forms](/dotnet/framework/winforms/windows-forms-overview).

## <a name="functionality"></a>Funcionalidade

Usando o designer, é possível:

- Adicionar componentes, controles de dados ou controles baseados no Windows a um formulário.

- Clicar duas vezes no formulário no designer e escrever o código no evento `Load` desse formulário, ou clicar duas vezes em um controle no formulário e escrever o código para o evento padrão do controle.

- Editar a propriedade Text de um controle selecionando-o e digitando um nome.

- Ajustar o posicionamento do controle selecionado movendo-o com o mouse ou as teclas de direção. Da mesma forma, é possível ajustar o posicionamento com mais precisão usando as teclas Ctrl e de direção. Por fim, é possível ajustar o tamanho do controle usando as teclas Shift e de direção.

- Selecionar vários controles usando as teclas **Shift** ou **Ctrl** enquanto clica. Ao usar **Shift**+clique, o primeiro controle selecionado é o controle dominante ao alinhar ou manipular o tamanho. Ao usar **Ctrl**+clique, o último controle selecionado é dominante, portanto, o controle dominante é alterado com cada novo controle adicionado. Como alternativa, você pode selecionar vários controles arrastando um retângulo de seleção ao redor dos controles que deseja selecionar.

> [!NOTE]
> Use o Designer de Formulários do Windows, e não o Editor de Recursos, para fazer alterações no arquivo de recurso de um formulário (*.resx*). Se você editar um arquivo .resx baseado em formulário, verá um aviso de que poderá perder as alterações feitas no Editor de Recursos. Isso ocorre porque o Designer de Formulários do Windows gera o arquivo .resx.

## <a name="see-also"></a>Consulte também

- [Visão geral de Windows Forms](/dotnet/framework/winforms/windows-forms-overview)
- [Controles de formulários do Windows](/dotnet/framework/winforms/controls/)
- [Entrada do usuário no Windows Forms](/dotnet/framework/winforms/user-input-in-windows-forms)
- [Associação de dados no Windows Forms](/dotnet/framework/winforms/windows-forms-data-binding)
- [Aprimorar aplicativos do Windows Forms](/dotnet/framework/winforms/advanced/)
- <xref:System.Windows.Forms?displayProperty=fullName> Referência de API
