---
title: Habilitar o acesso ao VBA para criar ou abrir um Visual Studio Tools para o projeto do Microsoft Office system
decsprition: You must explicitly enable access to the Office VBA project system before you can create or open a Visual Studio Tools for Office system project
ms.custom: ''
ms.date: 02/02/2017
ms.technology: office-development
ms.prod: visual-studio-dev15
ms.topic: conceptual
f1_keywords:
- vst.project.vbawrongversion
- VST.Project.VBASecurityGenericError
- VST.Project.VBASecurityPermissions
- VST.SelectDocWizard.MissingCOM
- VST.Project.VBASecurityNotSet
dev_langs:
- VB
- CSharp
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: f17c4e1481e7f33034e16d1e60a285b25c6f8230
ms.sourcegitcommit: 1466ac0f49ebf7448ea4507ae3f79acb25d51d3e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/22/2018
ms.locfileid: "34448985"
---
# <a name="enable-access-to-vba-to-create-or-open-a-visual-studio-tools-for-the-microsoft-office-system-project"></a>Habilitar o acesso ao VBA para criar ou abrir um Visual Studio Tools para o projeto do Microsoft Office system

Você deve habilitar explicitamente o acesso para o Visual Basic para o sistema de projeto Applications (VBA) no Microsoft Office antes de criar ou abrir um Visual Studio Tools para o projeto do Microsoft Office system.

 Projetos de desenvolvimento do Microsoft Office exigem acesso ao Visual Basic para o sistema de projeto Applications (VBA) no Microsoft Office Word e Microsoft Office Excel, mesmo que os projetos não usar o Visual Basic para aplicativos. O suporte em tempo de design de controles em projetos do Visual Basic e C# depende do sistema de projeto do Visual Basic for Applications.

 Alguns vírus de macro do Microsoft Office tentam automatizar o sistema de projeto do Visual Basic for Applications como um meio de propagação. Ao permitir o acesso ao sistema de projeto do Visual Basic for Applications, você remove uma proteção que ajuda a impedir a propagação de vírus de macro. No entanto, a segurança normal de macro permanece ativada, de modo que o nível de segurança da macro e da lista de editores confiáveis que você mantém nos aplicativos do Office determinará se alguma macro é executada ou não em seu computador.

> [!NOTE]
> Isso só se aplica ao computador de desenvolvimento. Computadores de usuários finais não é necessário para esta opção habilitada para executar soluções do Office.

 É importante observar que desabilitar o acesso ao sistema de projeto do Visual Basic for Applications por conta própria não o protege contra vírus, isso simplesmente ajuda a interromper a disseminação de alguns vírus para outros documentos se o seu computador já estiver infectado com um vírus de macro. A opção é desabilitada por padrão como uma camada adicional de proteção ao computador, mas habilitá-la não torna seu computador mais suscetível a vírus se você estiver seguindo as práticas recomendadas de segurança.

 A melhor proteção contra vírus de macro é a execução do Office no nível de segurança alta ou muito alta, confiar somente macros de verificado, fontes conhecidas, do Office e permaneçam atualizados com patches de segurança e de antivírus.

 Para obter mais informações sobre como proteger seu computador contra vírus e outros programas mal-intencionados, consulte [ http://www.microsoft.com/protect ](http://www.microsoft.com/protect).

 Você pode habilitar ou desabilitar a opção **confiança acesso ao projeto do Visual Basic** manualmente.

 Você pode reparar a instalação do Office se vir erros de VBA ou COM.

## <a name="to-enable-or-disable-access-to-visual-basic-projects"></a>Para habilitar ou desabilitar o acesso a projetos do Visual Basic

1. Clique o **arquivo** guia.

2. Clique em **opções**.

3. Clique em **Central de confiabilidade**e, em seguida, clique em **definições**.

4. No **Central de confiabilidade**, clique em **configurações de Macro**.

5. Marque ou desmarque **confiar no acesso ao modelo de objeto do projeto do VBA** para habilitar ou desabilitar o acesso a projetos do Visual Basic.

6. Clique em **OK**.

### <a name="to-enable-or-disable-access-to-visual-basic-projects-with-the-2007-microsoft-office-system"></a>Para habilitar ou desabilitar o acesso a projetos do Visual Basic com o Microsoft Office 2007

1. Sobre o **ferramentas** menu do Word ou Excel, aponte para **Macro**e, em seguida, clique em **segurança**.

2. No **segurança** caixa de diálogo, clique o **editores confiáveis** guia.

3. Selecione para habilitar ou desmarque para desabilitar, **confiança acesso ao projeto do Visual Basic**.

4. Clique em **OK**.

## <a name="to-set-your-office-macro-security-level"></a>Para definir o nível de segurança de macro do Office

1. Clique o **arquivo** guia.

2. Clique em **opções**.

3. Clique em **Central de confiabilidade**e, em seguida, clique em **definições**.

4. No **Central de confiabilidade**, clique em **configurações de Macro**.

5. No **configurações de Macro** seção, selecione a configuração desejada.

6. Clique em **OK**.

### <a name="to-set-your-office-macro-security-level-with-the-2007-microsoft-office-system"></a>Para definir o nível de segurança de macro do Office com o Microsoft Office 2007

1. Sobre o **ferramentas** menu do Word ou Excel, aponte para **Macro**e, em seguida, clique em **segurança**.

2. Sobre o **nível de segurança** , selecione a configuração desejada.

    O **nível de segurança** guia contém detalhes sobre cada nível. Para mais informações, consulte o tópico "Níveis de segurança de macro" na Ajuda do Office.

### <a name="to-install-vba-with-the-2007-microsoft-office-system"></a>Para instalar o VBA com o sistema Microsoft Office 2007

1. No painel de controle, execute **adicionar ou remover programas** ou **programas e recursos**.

2. Selecione o escritório no **programas instalados** lista.

3. Clique em **Alterar**.

4. Selecione **adicionar ou remover recursos**e, em seguida, clique em **continuar**.

5. Selecione **escolha a personalização avançada de aplicativos**e, em seguida, clique em **próximo**.

6. Expanda **recursos compartilhados do Office** no **escolher opções de atualização para aplicativos e ferramentas** lista.

7. Abra o menu suspenso próximo a **Visual Basic for Applications**e, em seguida, clique em **executar de Meu computador**.

8. Clique em **Continue**.

9. Clique em **Fechar**.

## <a name="to-repair-your-installation-of-office"></a>Para reparar a instalação do Office

1. No painel de controle, execute **adicionar ou remover programas** ou **programas e recursos**.

2. Selecione a versão do Office no **programas instalados** lista.

3. Clique em **Alterar**.

4. Selecione **reinstalar ou reparar**e, em seguida, clique em **próximo**.

5. Selecione **detectar e reparar erros na instalação do Office**e, em seguida, clique em **instalar**.

## <a name="see-also"></a>Consulte também

 [Proteger as soluções do Office](../vsto/securing-office-solutions.md)