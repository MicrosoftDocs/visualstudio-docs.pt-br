---
title: Caixa de diálogo Opções, Projetos e Soluções, Compilar e Executar
ms.date: 07/14/2017
ms.prod: visual-studio-dev15
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- VS.ToolsOptionsPages.Projects.Build_and_Run
helpviewer_keywords:
- builds [Visual Studio], setting up
- run actions
- debugger, run options
ms.assetid: c884976e-c0df-4c6d-8e3a-856ea2bd547c
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 1b2d047201214e3a7cd4c14c61baa041840decd8
ms.sourcegitcommit: 1abb9cf4c3ccb90e3481ea8079272c98aad12875
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/26/2018
ms.locfileid: "50143314"
---
# <a name="options-dialog-box-projects-and-solutions-build-and-run"></a>Caixa de diálogo Opções, Projetos e Soluções, Compilar e Executar

Nesta caixa de diálogo, você pode especificar o número máximo de projetos do Visual C++ ou do C# que podem ser compilados ao mesmo tempo, determinados comportamentos de build padrão e algumas configurações de log de build. Para acessar essas opções, selecione **Ferramentas > Opções**, expanda **Projetos e Soluções** e selecione **Compilar e executar**.

**Número máximo de builds paralelos de projetos**

Especifica o número máximo de projetos do Visual C++ e do C# que podem ser compilados ao mesmo tempo. Para otimizar o processo de build, o número máximo de compilações paralelas de projetos é automaticamente definido como o número de CPUs do seu computador. O máximo é de 32.

**Somente compilar dependências e projetos de inicialização ao Executar**

Compila o projeto de inicialização e suas dependências quando você usa a tecla F5 e seleciona o comando de menu **Depurar > Iniciar** ou os comandos aplicáveis no menu **Compilar**. Se ficar desmarcado, todos os projetos e dependências serão compilados.

**Ao Executar, quando os projetos estiverem desatualizados**

*Aplica-se somente a projetos [!INCLUDE[vcprvc](../../code-quality/includes/vcprvc_md.md)].*

Ao executar um projeto com F5 ou com o comando **Depurar > Iniciar**, a configuração padrão **Avisar para compilar** exibe uma mensagem se uma configuração do projeto estiver desatualizada. Selecione **Compilar sempre** para compilar o projeto sempre que ele for executado. Selecione **Nunca compilar** para suprimir todos os builds automáticos quando um projeto for executado.

**Ao Executar, quando ocorrerem erros de build ou implantação**

*Aplica-se somente a projetos [!INCLUDE[vcprvc](../../code-quality/includes/vcprvc_md.md)].*

Ao executar um projeto com F5 ou com o comando **Depurar > Iniciar**, a configuração padrão **Solicitar inicialização** exibe uma mensagem se o projeto dever ser executado mesmo que o build tenha falhado. Selecione **Iniciar versão antiga** para iniciar automaticamente a última compilação boa, o que pode resultar em incompatibilidades entre o código em execução e o código-fonte. Selecione **Não iniciar** para suprimir a mensagem.

**Para novas soluções, use o projeto selecionado atualmente como o projeto de inicialização**

Quando essa opção é definida, novas soluções usam o projeto selecionado atualmente como o projeto de inicialização.

**Detalhamento da saída de build do projeto no MSBuild**

Determina quanta informação aparece na Janela de **Saída** para o build.

**Detalhamento do arquivo de log de build do projeto no MSBuild**

*Aplica-se somente a projetos [!INCLUDE[vcprvc](../../code-quality/includes/vcprvc_md.md)].*

Determina quanta informação é gravada no arquivo de log de build, que está localizado em \\...\\*ProjectName*\Debug\\*ProjectName*.log.

## <a name="see-also"></a>Consulte também

- [Compilando e criando](../../ide/compiling-and-building-in-visual-studio.md)
- [Caixa de diálogo Opções, Projetos e Soluções](projects-and-solutions-options-dialog-box.md)
- [Caixa de diálogo Opções, Projetos e Soluções, Projetos Web](options-dialog-box-projects-and-solutions-web-projects.md)