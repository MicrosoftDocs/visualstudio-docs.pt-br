---
title: Avisos e Erros XAML
ms.date: 03/06/2018
ms.prod: visual-studio-dev15
ms.technology: vs-ide-designers
ms.topic: conceptual
ms.assetid: 34eac8a0-7ec5-4c40-b97a-0126ed367931
author: karann-msft
ms.author: karann
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 09251f13cafa320e2736e9c61135283bb9e9739d
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49844179"
---
# <a name="xaml-errors-and-warnings"></a>Avisos e erros de XAML

Ao criar XAML, o Visual Studio analisa o código conforme você digita. Um rabisco aparece em uma linha de código quando um erro é detectado. Se você passar o mouse sobre o rabisco, verá mais informações sobre o erro ou aviso. Em alguns erros e avisos, uma lâmpada de Ação rápida é exibida. Ela também aparece ao pressionar **Ctrl**+**.** o atalho de teclado exibe as opções para corrigir o problema.

## <a name="error-types"></a>Tipos de erro

Em segundo plano, várias ferramentas analisam o XAML em paralelo. Erros de XAML são categorizados em um dos três seguintes tipos, com base na ferramenta que detectou o erro:

|**Erro detectado por**|**Formato do código de erro**|
| - |-----------------|
|Serviço de linguagem XAML (Editor XAML)|XLSxxxx|
|XAML Designer|XDGxxxx|
|Editar e Continuar em XAML|XECxxxx|

> [!Note]
> Nem todos os erros ou avisos têm um código correspondente. Geralmente, esses erros são do XAML Designer.


## <a name="suppress-xaml-designer-errors"></a>Suprimir erros do XAML Designer

Abra a caixa de diálogo **Opções** selecionando **Ferramentas > Opções** e, em seguida, selecione **Editor de Texto > XAML > Diversos**.

Desmarque a caixa de seleção **Mostrar erros detectados pelo XAML Designer**.

![Suprimir erros do XAML Designer](../designers/media/suppress_xaml_designer_errors.png)


