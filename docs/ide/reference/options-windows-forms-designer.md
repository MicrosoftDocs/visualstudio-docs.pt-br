---
title: Opções, Designer de Formulários do Windows, Geral
ms.date: 08/09/2019
ms.topic: reference
f1_keywords:
- VS.ToolsOptionsPages.WindowsFormsDesigner.General
helpviewer_keywords:
- Windows Forms Designer options
- Options dialog box, Windows Forms Designer
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 6166c2f0fcdd8c99c459559a699f7b8704aff647
ms.sourcegitcommit: 6b0503ed8d25454d6e39a8e606910b3fa58cf1d2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/13/2019
ms.locfileid: "68981692"
---
# <a name="options-dialog-box-windows-forms-designer"></a>Caixa de diálogo Opções: Designer de Formulários do Windows

A página de opções do Designer de Formulários do Windows possibilita definir preferências para as grades e outros recursos no Visual Studio. Abra a caixa de diálogo **Opções** no menu **Ferramentas**.

## <a name="code-generation-settings"></a>Configurações de geração de código

**Geração de Código Otimizada**\
Permite a geração de código otimizada. Alguns controles podem não ser compatíveis com esse modo. Para que essa alteração tenha efeito, o Visual Studio deve ser fechado e reaberto.

## <a name="high-dpi-support"></a>Suporte a DPI alto

**Notificações de Ajuste de DPI**\
Mostrar uma mensagem no Designer de Formulários do Windows que pode reiniciar o Visual Studio com 100% de ajuste. Para saber mais, confira [Desativar o reconhecimento de DPI no Visual Studio](/dotnet/framework/winforms/disable-dpi-awareness-visual-studio).

## <a name="layout-settings"></a>Configurações de layout

**Tamanho da Célula de Grade Padrão**\
Define o espaçamento, em pixels, entre linhas de grade horizontais e verticais no designer. O tamanho padrão é 8, 8. O tamanho máximo é 200, 200.

**Modo de Layout**\
Especifica o sistema de alinhamento a ser usado para o layout. Você pode escolher SnapToGrid ou Snaplines.

**Mostrar Grade**\
Especifica se os designers exibem a grade de dimensionamento. Por padrão, a grade está ativada.

**Ajustar à Grade**\
Determina se os designers encaixam objetos e controles à grade. Em outras palavras, o redimensionamento e o movimento de elementos no designer são restritos ao incremento GridSize quando esse recurso está ativado. Com o SnapToGrid ativado, é mais fácil alinhar os diversos aspectos da interface do usuário com precisão, mas isso limita a liberdade com a qual é possível encaixar controles. Por padrão, o SnapToGrid está ativado.

## <a name="object-bound-smart-tag-settings"></a>Configurações de Marcas Inteligentes Associadas a Objetos

**Abrir Automaticamente as Marcas Inteligentes**\
Determina se os controles e componentes exibem marcas inteligentes. Nem todos os controles e componentes dão suporte a marcas inteligentes.

## <a name="refactoring"></a>Refatoração

**Habilitar Refatoração ao Renomear**\
Quando definida como `true`, uma operação de refatoração de renomeação é executada ao renomear um componente da janela Propriedades ou da janela Estrutura de Tópicos do Documento.

## <a name="toolbox"></a>Caixa de Ferramentas

**Preencher Automaticamente a Caixa de Ferramentas**\
Determina se a janela Caixa de Ferramentas é preenchida automaticamente com componentes e controles criados pelo projeto.