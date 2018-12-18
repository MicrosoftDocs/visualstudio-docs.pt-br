---
title: Adicionar parâmetro a uma ação rápida de método
ms.date: 09/28/2018
ms.prod: visual-studio-dev15
ms.technology: vs-ide-general
ms.topic: reference
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- dotnet
ms.openlocfilehash: 0337f9869764f544f5248d4da717af849457b8e8
ms.sourcegitcommit: 6672a1e9d135d7e5cca3cceea07c6fe5a0871475
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/28/2018
ms.locfileid: "47443705"
---
# <a name="add-a-parameter-to-a-method-using-a-quick-action"></a>Adicionar um parâmetro a um método usando uma Ação Rápida

Esta geração de código aplica-se a:

- C#

- Visual Basic

**O que:** permite adicionar automaticamente um parâmetro a um método com base no uso.

**Quando:** você precisa adicionar um parâmetro a um método e deseja declará-lo automaticamente.

**Motivo:** você poderia adicionar o parâmetro para a declaração do método antes de chamá-lo, no entanto, esse recurso adiciona o parâmetro automaticamente com base na chamada de método.

## <a name="how-to-use-it"></a>Como usá-lo

1. Adicione um argumento extra a uma chamada de método.

   Uma linha vermelha "ondulada" aparece sob o nome do método onde você o chama.

2. Coloque o ponteiro sobre a linha vermelha "ondulada" até aparecer o menu Ações rápidas. Selecione a **seta para baixo** no menu Ações Rápidas e, em seguida, selecione **Adicionar parâmetro ao [método]**.

   ![Adicionar parâmetro a ação rápida de método no Visual Studio](media/add-parameter-to-method.png)

   > [!TIP]
   > Também é possível acessar o menu Ações Rápidas colocando o cursor na linha de chamada de método e, em seguida, pressionando a tecla **Ctrl**+**.** ou selecionando o ícone de lâmpada na margem de arquivo.

   O Visual Studio adiciona o novo parâmetro à declaração de método.

> [!NOTE]
> Se você tiver outras chamadas para o método, elas podem produzir erros depois de usar essa Ação Rápida porque não especificam um argumento para o parâmetro recém-adicionado.

## <a name="see-also"></a>Consulte também

- [Adicionar parâmetro ao construtor](generate-constructor.md#addparameter)