---
title: Depurar um serviço WCF do Self-Hosted | Microsoft Docs
description: Saiba como depurar um serviço WCF auto-hospedado. A maneira mais fácil (mas nem sempre possível) é configurar o Visual Studio para iniciar o cliente e o servidor.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- debugging, WCF
- WCF, self-hosted service
- WCF, debugging
ms.assetid: 288922be-ba3f-411e-af50-bba39c9529cc
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 3cd11966347cd90576eb78a59f6c7eb96cc697ef
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102155075"
---
# <a name="how-to-debug-a-self-hosted-wcf-service"></a>Como depurar um serviço WCF auto-hospedado
Um *serviço auto-hospedado* é um serviço WCF que não é executado dentro do IIS, do Host de Serviço WCF ou do [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] Development Server. A maneira mais fácil de depurar um WCF auto-hospedado é configurar o [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] para iniciar o cliente e o servidor quando você escolher **Iniciar Depuração** no menu **Depurar**.

 Se o serviço WCF está sendo auto-hospedado internamente ou é um processo que não pode ser iniciado dessa maneira, como serviço do NT, você não pode usar este método. Em vez disso, execute um destes procedimentos:

- Anexe manualmente o depurador ao processo de hospedagem. Para obter mais informações, consulte [anexar a processos em execução](../debugger/attach-to-running-processes-with-the-visual-studio-debugger.md).

     — ou —

- Inicie a depuração do cliente e inspecione uma chamada para o serviço. Isso requer que você habilite a depuração no arquivo app.config. Para obter mais informações, [limitações na depuração do WCF](../debugger/limitations-on-wcf-debugging.md).

### <a name="to-start-both-client-and-host-from-visual-studio"></a>Para iniciar o cliente e o host do Visual Studio

1. Crie uma solução do [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] que contém os projetos de cliente e de servidor.

2. Configure a solução para iniciar os processos do cliente e do servidor quando você escolhe **Iniciar** no menu **Depurar**.

   1. No **Gerenciador de Soluções**, clique com o botão direito do mouse no nome da solução.

   2. Clique em **Definir Projetos de Inicialização**.

   3. Na caixa de diálogo **\<name> Propriedades da solução** , selecione **vários projetos de inicialização**.

   4. Na grade **Vários Projetos de Inicialização**, na linha que corresponde ao projeto do servidor, clique em **Ação** e escolha **Iniciar**.

   5. Na linha que corresponde ao projeto de cliente, clique em **Ação** e escolha **Iniciar**.

   6. Clique em **OK**.

## <a name="see-also"></a>Confira também
- [Depurando serviços WCF](../debugger/debugging-wcf-services.md)
- [Limitações na depuração do WCF](../debugger/limitations-on-wcf-debugging.md)
- [Como: entrar em serviços WCF](../debugger/how-to-step-into-wcf-services.md)
