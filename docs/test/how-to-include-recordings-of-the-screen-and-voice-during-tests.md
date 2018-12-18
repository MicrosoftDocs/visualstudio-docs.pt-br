---
title: Tela de registro e de voz durante testes
ms.date: 10/03/2016
ms.topic: conceptual
helpviewer_keywords:
- test settings, recording desktop video
ms.assetid: 2cefe8c2-430a-4cb4-bbe0-f3edb2e5bc03
author: gewarren
ms.author: gewarren
manager: douge
ms.prod: visual-studio-dev15
ms.technology: vs-ide-test
ms.openlocfilehash: 1470ab88cb21a7a80fa46f57f944ec5df21d544f
ms.sourcegitcommit: ae46be4a2b2b63da7e7049e9ed67cd80897c8102
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/05/2018
ms.locfileid: "52894407"
---
# <a name="how-to-include-recordings-of-the-screen-and-voice-during-tests-using-test-settings"></a>Como incluir gravações da tela e de voz durante testes usando as configurações de teste

No editor de configuração do Visual Studio, é possível configurar o adaptador de dados de diagnóstico que grava a tela e a voz do usuário que está executando o teste. Esse adaptador de dados de diagnóstico salva uma gravação de voz e tela da sessão da área de trabalho durante o teste. A gravação é salva com o resultado do teste ou pode ser anexada a um bug. Outros membros da equipe podem usar a gravação para isolar defeitos no aplicativo que sejam difíceis de reproduzir.

> [!WARNING]
> As gravações de tela e voz não dão suporte a várias configurações de monitor.

O gravador de tela e voz pode ser usado com testes manuais ou automatizados. Por exemplo, se executar um teste de IU codificado remotamente, você talvez queira gravar a área de trabalho para ver o teste de IU codificado à medida que ele é executado. Para obter informações sobre como capturar uma gravação de tela e de voz remotamente, confira [Como configurar o agente de teste para executar testes que interagem com a área de trabalho](../test/how-to-set-up-your-test-agent-to-run-tests-that-interact-with-the-desktop.md).

[!INCLUDE [web-load-test-deprecated](includes/web-load-test-deprecated.md)]

## <a name="to-configure-screen-and-voice-recording-for-your-test-settings"></a>Para configurar a gravação de voz e tela para suas configurações de teste

1.  Abra as configurações de teste que você deseja definir para registrar a tela e a voz. Para obter mais informações, confira [Coletar dados de diagnóstico durante o teste (Azure Test Plans)](/azure/devops/test/collect-diagnostic-data?view=vsts) ou [Coletar informações de diagnóstico usando configurações de teste](../test/collect-diagnostic-information-using-test-settings.md).

2.  Nas configurações de teste, selecione a **Função** a ser usada para gravar a tela e a voz.

    > [!NOTE]
    > Para testes manuais e testes automatizados, essa seria a máquina que executa os testes.

3.  Selecione **Gravador de Tela e Voz** e escolha **Configurar**.

     A caixa de diálogo **Configurar Adaptador de Dados de Diagnóstico – Gravador de Tela e Voz** é exibida.

     ![Configuração de vídeo](../test/media/testsettingvideoconfiggdr.png)

4.  (Opcional) Selecione **Habilitar registro de voz** para capturar o conteúdo de áudio em sua gravação.

5.  (Opcional) Marque a caixa de seleção ao lado de **Salvar a gravação se o caso de teste passar** para especificar que a tela e as gravações de voz sejam salvas independentemente dos testes serem aprovados ou reprovados.

    > [!WARNING]
    > Se você selecionar **Salvar a gravação se o caso de teste passar**, a gravação será armazenada com os resultados de teste, o que usará espaço de armazenamento no servidor. Use a ferramenta **Limpeza de Anexo de Teste** para limpar esses anexos.

6.  Em **Qualidade de Gravação da Tela**, configure as seguintes opções da lista suspensa:

    1.  **Taxa de quadros:** especifique quantos quadros por segundo você deseja usar na gravação de voz e tela. O valor padrão é 4 quadros por segundo. Valores entre 2 e 20 podem ser especificados.

    2.  **Taxa de bits:** especifique quantos quilobytes serão usados por segundo na gravação de voz e tela. O valor padrão é 512. Valores entre 512 e 10.000 podem ser especificados.

    3.  **Qualidade (1-100):** você pode especificar a qualidade da gravação de voz e tela selecionando um intervalo entre 1 e 100. O padrão é 50 (intermediário).

7.  Escolha **OK**. As configurações do coletor de rastreamento de diagnóstico agora estão definidas e salvas em suas configurações de teste.

    > [!TIP]
    > Para redefinir a configuração desse adaptador de dados de diagnóstico, escolha **Restaurar configuração padrão** para o Visual Studio e **Redefinir como padrão** para o Microsoft Test Manager.

## <a name="see-also"></a>Consulte também

- [Coletar dados de diagnóstico durante testes (Azure Test Plans)](/azure/devops/test/collect-diagnostic-data?view=vsts)
- [Coletar dados de diagnóstico em testes manuais (Azure Test Plans)](/azure/devops/test/mtm/collect-more-diagnostic-data-in-manual-tests?view=vsts)
- [Coletar informações de diagnóstico usando configurações de teste](../test/collect-diagnostic-information-using-test-settings.md)
- [Executar testes manuais (Azure Test Plans)](/azure/devops/test/run-manual-tests?view=vsts)