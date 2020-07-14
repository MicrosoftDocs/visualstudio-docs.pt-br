---
title: A pasta de trabalho usada para criar este projeto contém controles ActiveX que o designer não pode carregar
ms.date: 02/02/2017
ms.topic: error-reference
f1_keywords:
- VST.SelectDocWizard.ContainsActiveXControls
dev_langs:
- VB
- CSharp
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 4485489b48c4d1b03b608c6072cfc859e8bc8f59
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85537339"
---
# <a name="the-workbook-used-to-create-this-project-contains-activex-controls-that-the-designer-cannot-load"></a>A pasta de trabalho usada para criar este projeto contém controles ActiveX que o designer não pode carregar
  Esse erro aparece quando você adiciona um controle a um documento do Word ou a uma planilha do Excel de forma programática, salva o documento ou a pasta de trabalho e, em seguida, cria uma nova solução de nível de documento com base no documento ou na pasta de trabalho.

 As informações que descrevem o tipo gerenciado do controle não são salvas junto com o documento ou a pasta de trabalho. Quando você cria uma nova solução com base no documento ou pasta de trabalho, o Visual Studio não tem informações suficientes para carregar o controle no designer de item de host.

## <a name="to-correct-this-error"></a>Para corrigir este erro

1. Abra o documento ou pasta de trabalho.

2. Remova os controles que foram adicionados em tempo de execução. Você pode fazer isso selecionando-os no documento ou na pasta de trabalho e pressionando a tecla **delete** .

3. Crie uma solução de nível de documento com base no documento ou na pasta de trabalho.

## <a name="see-also"></a>Confira também
- [Como: criar projetos do Office no Visual Studio](../vsto/how-to-create-office-projects-in-visual-studio.md)
- [Adicionar controles a documentos do Office em tempo de execução](../vsto/adding-controls-to-office-documents-at-run-time.md)
