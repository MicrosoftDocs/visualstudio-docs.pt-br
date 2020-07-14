---
title: Como criar um diretório de saída comum
ms.date: 11/04/2016
ms.technology: vs-ide-compile
ms.topic: how-to
helpviewer_keywords:
- output directory
- builds [Visual Studio], common directory
- common directory
ms.assetid: 1fcc2c48-07cb-4c4f-9556-36945e7dfc4e
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 9a499b5ca5ea64dd9ded10f82b1af43258f346d3
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/23/2020
ms.locfileid: "85284770"
---
# <a name="how-to-build-to-a-common-output-directory"></a>Como criar um diretório de saída comum

Por padrão, [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] compila cada projeto em uma solução em sua própria pasta dentro da solução. É possível alterar os caminhos de saída do build dos seus projetos para forçar todas as saídas a serem colocadas na mesma pasta.

## <a name="to-place-all-solution-outputs-in-a-common-directory"></a>Para colocar todas as saídas de solução em um diretório comum

1. Clique em um projeto na solução.

2. No menu **Projeto** , clique em **Propriedades**.

3. Dependendo do tipo de projeto, clique na guia **Compilar** ou na guia **Build** e defina o **Caminho de saída** para uma pasta usar para todos os projetos na solução.

4. Repita as etapas 1 a 3 para todos os projetos na solução.

## <a name="see-also"></a>Veja também

- [Compilação e construção](../ide/compiling-and-building-in-visual-studio.md)
- [Como alterar o diretório de saída do build](../ide/how-to-change-the-build-output-directory.md)