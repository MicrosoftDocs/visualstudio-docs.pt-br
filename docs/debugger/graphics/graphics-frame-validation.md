---
title: Validação de quadros de gráficos | Microsoft Docs
ms.date: 03/02/2017
ms.topic: conceptual
f1_keywords:
- vs.graphics.FrameValidation
ms.assetid: 1e639182-1301-4e28-9c1e-b5df732f3f1b
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: ce283e5cbab30b612a02ec447113ad11e206a7f3
ms.sourcegitcommit: 53aa5a413717a1b62ca56a5983b6a50f7f0663b3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59655368"
---
# <a name="graphics-frame-validation"></a>Validação de quadro de gráficos
<!-- VERSIONLESS -->
Visual Studio 2017 e maior suporte a **validação de quadro** ferramenta.  A janela de validação de quadro exibe erros e avisos associados com a lista de eventos.  Para exibir essa janela, selecione a **Exibir > validação de quadro** menu.

![Validação de quadro](media/gfx_diag_frame_validation.png)

Clique o **executar a validação** botão no canto superior esquerdo para iniciar a análise.  Pode levar vários minutos para ser concluída dependendo da complexidade do quadro.  Os dados que aparece aqui é uma combinação de duas fontes: as mensagens que D3D em si emite quando [camadas de SDK](/windows/desktop/direct3d11/overviews-direct3d-11-devices-layers) estiver habilitado e os dados coletados do estado interno da ferramenta de controle. Uma vez concluído, você verá várias colunas de dados:

| **Coluna** | **Descrição** |
|------------| - |
| ID do evento | ID que é mapeado para uma entrada na [lista de eventos](graphics-event-list.md) janela. |
| Severidade | Corrupção, erro, aviso, informações ou mensagem. |
| Categoria | Aplicativo definido, diverso, inicialização, limpeza, compilação, criação do estado, configuração de estado, obtenção de estado, execução, manipulação de recursos, sombreador, redundante e não utilizado. |
| Mensagem | A mensagem associada ao evento. |
| evento | O evento associado com o erro ou aviso. |

## <a name="see-also"></a>Consulte também
[Diagnóstico de gráficos (depuração de gráficos DirectX)](visual-studio-graphics-diagnostics.md)
<!-- /VERSIONLESS -->