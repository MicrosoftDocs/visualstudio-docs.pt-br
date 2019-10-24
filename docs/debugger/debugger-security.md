---
title: Segurança do depurador | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- debugging [Visual Studio], security
- debugger, security
- security [Visual Studio], debugging best practices
ms.assetid: d4fc3c43-e844-419c-8dbb-551cc2a9b09e
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: d8d2e951bb62cb3ac8010029b76971662d07b898
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/22/2019
ms.locfileid: "72738313"
---
# <a name="debugger-security"></a>Segurança do depurador
A capacidade de depurar outro processo oferece poderes extremamente amplos que você não teria de outra forma, especialmente ao depurar remotamente. Um depurador mal-intencionado pode impor danos extensivos no computador que está sendo depurado.

 Porém, muitos desenvolvedores não percebem que a ameaça à segurança também pode fluir na direção oposta. É possível que o código mal-intencionado no processo a ser depurado possa comprometer a segurança do computador de depuração: há várias explorações de segurança das quais você deve se proteger.

## <a name="security-best-practices"></a>Práticas recomendadas de segurança
 Há uma relação de confiança implícita entre o código que você está depurando e o depurador. Se você estiver disposto a depurar algo, também deverá estar disposto a executá-lo. Ou seja, você deve ser capaz de confiar no que está depurando. Se você não puder confiar, não deverá depurar, ou deverá depurar de um computador com recursos que possam ser comprometidos e em um ambiente isolado.

 Para reduzir a superfície de ataque potencial, a depuração deverá ser desabilitada em computadores de produção. Pelo mesmo motivo, a depuração nunca deve ser habilitada indefinidamente.

### <a name="managed-debugging-security"></a>Segurança de depuração gerenciada
 Aqui estão algumas recomendações gerais que se aplicam a todas as depurações gerenciadas.

- Tenha cuidado ao anexar ao processo de um usuário não confiável: quando você faz isso, pressupõe que ele seja confiável. Quando você tenta anexar a um processo de usuário não confiável, uma caixa de diálogo de confirmação de aviso de segurança será exibida perguntando se você deseja anexar ao processo. Os "usuários confiáveis" incluem você e um conjunto de usuários padrão, comumente definidos em computadores que tenham o .NET Framework instalado, por exemplo, **aspnet**, **localsystem**, **networkservice** e **localservice**. Para obter mais informações, consulte [aviso de segurança: Anexar a um processo pertencente a um usuário não confiável pode ser perigoso. Se as informações a seguir parecerem suspeitas ou, se você não tiver certeza, não anexe a esse processo](../debugger/security-warning-attaching-to-a-process-owned-by-an-untrusted-user.md).

- Tenha cuidado ao baixar um projeto fora da Internet e carregá-lo no [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]. Isso é muito arriscado de fazer mesmo sem depuração. Quando você fizer isso, estará supondo que o projeto e o código que contém sejam confiáveis.

  Para obter mais informações, consulte [Depurando código gerenciado](../debugger/debugging-managed-code.md).

### <a name="remote-debugging-security"></a>Segurança de depuração remota
 A depuração local é geralmente mais segura do que a depuração remota. A depuração remota aumenta a área da superfície total que pode ser analisada.

 O Monitor de Depuração Remota do Visual Studio (msvsmon.exe) é usado na depuração remota e há várias recomendações de segurança para configurá-lo. O modo preferido de configurar o modo de autenticação é a autenticação do Windows, pois Modo Sem Autenticação não é seguro.

 ![Diálogo de erro](../debugger/media/dbg_err_remotepermissionschanged.png "DBG_ERR_RemotePermissionsChanged")

 Ao usar o Modo de Autenticação do Windows, lembre-se de que a concessão de uma permissão de usuário não confiável para se conectar a msvsmon é perigosa, porque o usuário recebe todas as permissões no computador.

 Não depure um processo desconhecido em um computador remoto: há explorações potenciais que podem afetar o computador que executa o depurador ou que podem comprometer o msvsmon.exe, o Monitor de Depuração Remota do Visual Studio. Se for absolutamente necessário depurar um processo desconhecido, tente depurá-lo localmente e use um firewall para manter todas as ameaças potenciais localizadas.

 Para obter mais informações, consulte [depuração remota](../debugger/remote-debugging.md).

### <a name="web-services-debugging-security"></a>Segurança de depuração de serviços Web
 É mais seguro depurar localmente, mas como você provavelmente não terá o [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] instalado no servidor Web, a depuração local não poderá ser prática. Em geral, depurar serviços Web é feito remotamente, exceto durante o desenvolvimento, de modo que as recomendações para a segurança de depuração remota também se aplicarão à depuração de serviços Web. Aqui estão algumas práticas recomendadas adicionais. Para obter mais informações, consulte [DEBUGGING XML Web Services](https://msdn.microsoft.com/library/c900b137-9fbd-4f59-91b5-9c2c6ce06f00).

- Não habilite a depuração em um servidor Web que tenha sido comprometido.

- Verifique se você sabe que o servidor Web está seguro antes de depurá-lo. Se você não tiver certeza se ele está seguro, não o depure.

- Tenha um cuidado especial se estiver depurando um serviço Web que está exposto na Internet.

### <a name="external-components"></a>Componentes externos
 Conheça o status de confiança de componentes externos com os quais seu programa interage, especialmente se você não escreveu o código. Esteja ciente também dos componentes que o [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] ou o depurador podem usar.

### <a name="symbols-and-source-code"></a>Símbolos e código-fonte
 As duas ferramentas do [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] que demandam preocupações com segurança são as seguintes:

- O Servidor de Origem, que fornece versões do código-fonte de um repositório de códigos-fonte. É útil quando você não tem a versão atual do código-fonte de um programa. [Aviso de segurança: o depurador deve executar o comando não confiável](../debugger/security-warning-debugger-must-execute-untrusted-command.md)

- O servidor do símbolo, que é usado para fornecer os símbolos necessárias para depurar uma falha durante uma chamada do sistema.

  Confira [Especificar arquivos de símbolo (.pdb) e de origem](../debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger.md)

## <a name="see-also"></a>Consulte também
- [Preparação e configurações do depurador](../debugger/debugger-settings-and-preparation.md)
- [Introdução ao depurador](../debugger/debugger-feature-tour.md)
- [Aviso de segurança Anexar a um processo pertencente a um usuário não confiável pode ser perigoso. Se as informações a seguir parecerem suspeitas ou você não tiver certeza, não anexe a esse processo](../debugger/security-warning-attaching-to-a-process-owned-by-an-untrusted-user.md)
- [Aviso de segurança: o depurador deve executar o comando não confiável](../debugger/security-warning-debugger-must-execute-untrusted-command.md)