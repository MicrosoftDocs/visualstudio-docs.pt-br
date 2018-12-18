---
title: Isento da Proteção de Informações do Windows
ms.date: 06/01/2018
ms.prod: visual-studio-dev15
ms.technology: vs-ide-general
ms.topic: conceptual
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 1a1b38e6e30a816382da72ef8280868fa68dfb10
ms.sourcegitcommit: ce154aee5b403d5c1c41da42302b896ad3cf8d82
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/07/2018
ms.locfileid: "34845899"
---
# <a name="configure-visual-studio-as-a-wip-exempt-app"></a>Configurar o Visual Studio como um aplicativo da isento da WIP

A [WIP](/windows/security/information-protection/windows-information-protection/protect-enterprise-data-using-wip) (Proteção de Informações do Windows) ajuda a proteger os dados empresariais contra perda causada por aplicativos, como email, mídia social e nuvem pública, que estão fora do controle da empresa. A WIP ajuda a proteger contra perda de dados acidental em dispositivos corporativos e pessoais, sem exigir alterações em seu ambiente ou outros aplicativos.

Os aplicativos *esclarecidos* para WIP devem impedir que os dados empresariais cheguem a locais de rede desprotegidos e evitar a criptografia de dados pessoais. O Visual Studio não é um aplicativo esclarecido, portanto, ele não funciona em ambientes habilitados para WIP, a menos que você o isente. Siga as etapas neste artigo para habilitar o Visual Studio para funcionar em um computador habilitado para WIP.

## <a name="configure-vs-as-a-wip-exempt-app"></a>Configurar o VS como um aplicativo isento da WIP

Você pode isentar o Visual Studio das restrições da WIP, mas ainda permitir que ele use dados empresariais. Os aplicativos isentos da WIP podem se conectar aos recursos de nuvem da empresa usando um endereço IP ou um nome de host. Não é aplicada nenhuma criptografia e o aplicativo pode acessar arquivos locais.

Para isentar o Visual Studio da WIP, execute as [etapas para isentar um aplicativo da área de trabalho](/windows/security/information-protection/windows-information-protection/create-wip-policy-using-intune-azure#exempt-apps-from-a-wip-policy).

## <a name="create-a-wip-exempt-applocker-policy-file"></a>Crie um arquivo de política do AppLocker isento da WIP

Como o Visual Studio inclui vários binários, [crie um arquivo de política do AppLocker isento da WIP](/windows/security/threat-protection/windows-defender-application-control/applocker/run-the-automatically-generate-rules-wizard). O AppLocker permite gerar regras automaticamente para todos os arquivos dentro de uma pasta.

## <a name="add-appcompat-to-the-enterprise-cloud-resource-policy"></a>Adicionar o AppCompat à política de recursos de nuvem empresariais

Para especificar onde o Visual Studio pode acessar dados empresariais em sua rede, siga estas [etapas para definir onde seus aplicativos protegidos podem localizar e enviar dados empresariais](/windows/security/information-protection/windows-information-protection/create-wip-policy-using-intune-azure#choose-where-apps-can-access-enterprise-data). Para impedir que o Windows bloqueie as conexões aos recursos de nuvem por meio de um endereço IP, adicione a cadeia de caracteres /\*AppCompat\*/ à configuração.

## <a name="see-also"></a>Consulte também

- [Comportamento do aplicativo com WIP](/windows/security/information-protection/windows-information-protection/app-behavior-with-wip)