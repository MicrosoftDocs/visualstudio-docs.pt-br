---
title: Usando o Emulator Express para executar e depurar um serviço de nuvem do Azure em um computador local | Microsoft Docs
description: Usando o Emulator Express para executar e depurar um serviço de nuvem em um computador local
author: mikejo5000
manager: douge
ms.assetid: 73108f98-a552-4817-b7a1-551367b71906
ms.topic: conceptual
ms.workload: azure-vs
ms.date: 03/06/2017
ms.author: mikejo
ms.prod: visual-studio-dev14
ms.technology: vs-azure
ms.openlocfilehash: 28dd59e3d691df0199afffe93d68d60668c6afe4
ms.sourcegitcommit: e481d0055c0724d20003509000fd5f72fe9d1340
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/05/2018
ms.locfileid: "51001142"
---
# <a name="using-emulator-express-to-run-and-debug-an-azure-cloud-service-on-a-local-machine"></a>Usando o Emulator Express para executar e depurar um serviço de nuvem do Azure em um computador local
Usando o Emulator Express, você pode testar e depurar um serviço de nuvem sem executar o Visual Studio como administrador. Você pode definir as configurações de projeto para usar o Emulator Express ou o emulador completo, dependendo dos requisitos do serviço de nuvem. Para obter mais informações sobre o emulador completo, consulte [executar um aplicativo do Azure no emulador de computação](/azure/storage/common/storage-use-emulator).

## <a name="using-emulator-express-in-visual-studio"></a>Usando o Emulator Express no Visual Studio
Quando você cria um projeto do Azure no Azure SDK 2.3 ou posterior, o Emulator Express é usado automaticamente. Para projetos existentes que foram criados com uma versão anterior do SDK do Azure, use as etapas a seguir para selecionar o Emulator Express:

1. Crie ou abra um projeto de serviço de nuvem do Azure no Visual Studio.

1. Na **Gerenciador de soluções**, clique com botão direito no projeto e, no menu de contexto, selecione **propriedades**.

1. Nas páginas de propriedades de projetos, selecione o **Web** guia.

    ![Propriedades de um projeto de serviço de nuvem do Azure](./media/vs-azure-tools-emulator-express-debug-run/web-properties.png)

1. Sob **Development Server Local**, selecione **opção de usar o IIS Express**.

1. Sob **emulador**, selecione **usar o Emulator Express**.
   
1. Para iniciar o Emulator Express, execute o seguinte comando no prompt de comando: 

    ```
    csrun.exe /useemulatorexpress
    ```

## <a name="emulator-express-limitations"></a>Limitações do Emulator Express
Os seguintes problemas são limitações conhecidos do Emulator Express: 

- O Emulator Express não é compatível com o servidor Web do IIS.
- O serviço de nuvem pode conter várias funções, mas cada função é limitada a uma instância.
- Você não pode acessar números de porta abaixo de 1000. Se você usar um provedor de autenticação que normalmente usa uma porta abaixo de 1000, talvez você precise alterar esse valor para um número de porta acima de 1000.
- As limitações que se aplicam ao emulador de computação do Azure também se aplicam ao Emulator Express. Por exemplo, você não pode ter mais de 50 instâncias de função por implantação. Para obter mais informações sobre o emulador de computação do Azure, consulte [executar um aplicativo do Azure no emulador de computação](http://go.microsoft.com/fwlink/p/?LinkId=623050).

## <a name="next-steps"></a>Próximas etapas
[Depurando serviços de nuvem do Azure](https://msdn.microsoft.com/library/azure/ee405479.aspx)
