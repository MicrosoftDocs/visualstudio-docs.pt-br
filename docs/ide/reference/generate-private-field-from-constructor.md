---
title: Gerar campo privado e Propriedade do Construtor
ms.date: 06/20/2020
ms.topic: reference
author: mikadumont
ms.author: midumont
manager: jillfra
dev_langs:
- CSharp
- VB
ms.workload:
- dotnet
ms.openlocfilehash: 56bd361d2bffb4ff17b03ac6743837032d1934e1
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/23/2020
ms.locfileid: "85283717"
---
# <a name="generate-private-field-and-property-from-constructor"></a>Gerar campo privado e Propriedade do Construtor

Esta refatoração aplica-se a: 

- C# 

**O que:** Gerar um campo ou propriedade particular de um construtor. 

**Quando:** Você deseja adicionar e inicializar rapidamente um campo ou propriedade particular de um construtor.

**Por que:** Escrever campos e propriedades particulares pode ser demorado e repetitivo. O uso dessa refatoração é rápido e torna o programa mais robusto.

## <a name="how-to"></a>Como fazer 

1. Coloque o cursor no nome do parâmetro dentro do construtor.

2. Pressione **Ctrl** + **.** para acionar o menu **Ações e Refatorações Rápidas**.
   
3. Em seguida, selecione de um dos seguintes:

- **Criar e inicializar campo** ou **criar e inicializar Propriedade**.

   ![Gerar campo particular do construtor](media/generate-private-field-from-constructor.png)

## <a name="see-also"></a>Veja também 

- [Refatoração](../refactoring-in-visual-studio.md)
