# Instalação Automatizada – Windows 10/11 Pro Lite (autounattend.xml)

## Introdução

Este repositório contém um arquivo `autounattend.xml` projetado para automatizar e otimizar a instalação do Windows 10/11 Pro a partir de uma imagem ISO oficial da Microsoft. O objetivo é replicar, da forma mais fiel possível, as otimizações de uma ISO customizada com NTLite, mas através de um método de configuração pós-instalação, ideal para quem deseja aplicar tweaks em uma instalação limpa sem modificar a imagem original.

As configurações focam em três pilares: **desempenho** (para jogos e desenvolvimento), **privacidade** (minimizando a telemetria) e uma **experiência de usuário limpa** (removendo bloatware e ajustando a interface).

> **Referência do Projeto Original:**
> Este projeto é a contraparte "unattended" de uma ISO customizada criada anteriormente com o NTLite. Para entender a fundo a filosofia e cada componente removido/alterado na ISO original, consulte o repositório e o relatório detalhado aqui:
> [Acessar Repositório NTLite-ISO-Windows-10-Lite](https://github.com/henrique-sdc/NTLite-ISO-Windows-10-Lite)

## Funcionalidades e Otimizações

Este arquivo `autounattend.xml` irá configurar a instalação do Windows para aplicar as seguintes mudanças automaticamente:

*   **Configuração de Usuário:** Cria um usuário local de administrador sem senha, forçando a definição de uma no primeiro login e evitando a vinculação com uma Conta Microsoft durante a instalação.
*   **Privacidade Aprimorada:** Desativa a telemetria, ID de publicidade, sugestões de aplicativos, resultados de pesquisa do Bing e outras funcionalidades de coleta de dados.
*   **Remoção de Bloatware:** Executa um script para desinstalar uma lista extensa de aplicativos pré-instalados e não essenciais (Cortana, Office Hub, Mail, Solitaire, etc.).
*   **Otimizações de Desempenho:**
    *   Aplica tweaks de registro para otimizar o agendador gráfico da GPU, a resolução de timers do sistema e prioridades de tarefas para jogos.
    *   Ativa o plano de energia de "Desempenho Máximo".
    *   Desativa a Inicialização Rápida e a Hibernação.
    *   Desativa a aceleração do mouse ("Aprimorar precisão do ponteiro").
*   **Interface Limpa e Funcional:**
    *   Define o tema escuro para o sistema e aplicativos.
    *   Remove todos os blocos dinâmicos do Menu Iniciar.
    *   Oculta ícones desnecessários da barra de tarefas (Pesquisa, Visão de Tarefas).
    *   Configura o Explorador de Arquivos para uma experiência de usuário avançado (mostrar arquivos ocultos, extensões, abrir em "Este PC").
*   **Instalação de Componentes Essenciais:**
    *   Baixa e instala silenciosamente o **Microsoft Visual C++ Redistributable (x64)**, um pré-requisito para muitos jogos e aplicativos.

## Como Usar

1.  **Baixe uma ISO Oficial:** Obtenha a imagem de instalação mais recente do Windows 10/11 Pro (x64) diretamente do [site da Microsoft](https://www.microsoft.com/pt-br/software-download/windows10).
2.  **Crie um Pendrive Bootável:** Utilize uma ferramenta como o [Rufus](https://rufus.ie/) ou [Ventoy](https://www.ventoy.net/) para gravar a imagem ISO em um pendrive.
3.  **Copie o Arquivo:** Após a criação do pendrive, copie o arquivo `autounattend.xml` deste repositório para a **raiz** do pendrive.
4.  **(Opcional) Papel de Parede Personalizado:**
    *   Na raiz do pendrive, crie a seguinte estrutura de pastas: `$OEM$\$$\System32\oobe\info\backgrounds\`
    *   Coloque seu arquivo de papel de parede dentro da pasta `backgrounds` e renomeie-o para `backgroundDefault.jpg`.
5.  **Inicie a Instalação:** Dê boot no computador a partir do pendrive. A instalação do Windows detectará o arquivo `autounattend.xml` e começará o processo automatizado.

**Atenção:** Este script está configurado para ser **interativo na etapa de particionamento**. Ele irá parar e pedir que você escolha em qual disco/partição instalar o Windows. Após essa etapa, o restante do processo é totalmente automático.

## Análise de Antivírus (Falso Positivo)

Softwares antivírus, como o Kaspersky, podem detectar este arquivo `autounattend.xml` como um "Trojan" (ex: `HEUR:Trojan.PowerShell.Generic`). **Isto é um falso positivo.**

O alerta ocorre porque o arquivo contém scripts PowerShell que realizam ações administrativas legítimas, mas que também são usadas por malwares, como:
*   Baixar e executar arquivos da internet (o instalador oficial do VC++ da Microsoft).
*   Modificar configurações de boot (`bcdedit`).
*   Alterar o Registro do Windows para aplicar tweaks.
*   Desinstalar aplicativos do sistema.

Cada linha de código neste arquivo foi gerada com base em seleções manuais e visa apenas otimizar a instalação. É seguro adicionar o arquivo às exceções do seu antivírus.

# Link completo do autounattend com as minhas alterações:
[Link para alterar o autounattend.xml](
https://schneegans.de/windows/unattend-generator/?LanguageMode=Unattended&UILanguage=pt-BR&Locale=pt-BR&Keyboard=00020409&GeoLocation=32&ProcessorArchitecture=amd64&HidePowerShellWindows=true&ComputerNameMode=Custom&ComputerName=PCdeHenrique&CompactOsMode=Never&TimeZoneMode=Implicit&PartitionMode=Interactive&DiskAssertionMode=Skip&WindowsEditionMode=Generic&WindowsEdition=pro&InstallFromMode=Automatic&PEMode=Default&UserAccountMode=Unattended&AccountName0=Henrique+S&AccountDisplayName0=&AccountPassword0=&AccountGroup0=Administrators&AutoLogonMode=Own&PasswordExpirationMode=Unlimited&LockoutMode=Default&HideFiles=HiddenSystem&ShowFileExtensions=true&LaunchToThisPC=true&ShowEndTask=true&TaskbarSearch=Hide&TaskbarIconsMode=Default&DisableWidgets=true&HideTaskViewButton=true&DisableBingResults=true&StartTilesMode=Empty&StartPinsMode=Empty&DisableFastStartup=true&DisableSystemRestore=true&DisableLastAccess=true&DisableAppSuggestions=true&PreventDeviceEncryption=true&HideEdgeFre=true&DisableEdgeStartupBoost=true&DisablePointerPrecision=true&EffectsMode=Custom&DWMAeroPeekEnabled=true&DWMSaveThumbnailEnabled=true&ListviewShadow=true&ThumbnailsOrIcon=true&DragFullWindows=true&FontSmoothing=true&DropShadow=true&DesktopIconsMode=Default&StartFoldersMode=Default&WifiMode=Skip&ExpressSettings=DisableAll&LockKeysMode=Skip&StickyKeysMode=Disabled&ColorMode=Custom&SystemColorTheme=Dark&AppsColorTheme=Dark&AccentColor=%23ffffff&WallpaperMode=Default&LockScreenMode=Default&Remove3DViewer=true&RemoveBingSearch=true&RemoveClipchamp=true&RemoveCopilot=true&RemoveCortana=true&RemoveWindowsHello=true&RemoveFamily=true&RemoveFeedbackHub=true&RemoveGetHelp=true&RemoveInternetExplorer=true&RemoveMailCalendar=true&RemoveMaps=true&RemoveMathInputPanel=true&RemoveNews=true&RemoveOffice365=true&RemoveOneNote=true&RemoveOneSync=true&RemoveOutlook=true&RemovePaint3D=true&RemovePeople=true&RemovePowerAutomate=true&RemoveQuickAssist=true&RemoveRecall=true&RemoveRdpClient=true&RemoveSkype=true&RemoveSolitaire=true&RemoveStepsRecorder=true&RemoveStickyNotes=true&RemoveTeams=true&RemoveGetStarted=true&RemoveToDo=true&RemoveWallet=true&RemoveWeather=true&RemoveFaxAndScan=true&RemoveWindowsMediaPlayer=true&RemoveYourPhone=true&SystemScript0=%24uri+%3D+%5Buri%5D%3A%3Anew%28+%27https%3A%2F%2Faka.ms%2Fvs%2F17%2Frelease%2Fvc_redist.x64.exe%27+%29%3B%0D%0A%24file+%3D+%22%24env%3ATEMP%5C%7B0%7D%22+-f+%24uri.Segments%5B-1%5D%3B%0D%0A%5BSystem.Net.WebClient%5D%3A%3Anew%28%29.DownloadFile%28+%24uri%2C+%24file+%29%3B%0D%0AStart-Process+-FilePath+%24file+-ArgumentList+%27%2Fquiet+%2Fnorestart%27+-Wait%3B%0D%0ARemove-Item+-LiteralPath+%24file+-ErrorAction+%27SilentlyContinue%27%3B&SystemScriptType0=Ps1&SystemScript1=%24out+%3D+%26+%22%24env%3Awindir%5CSystem32%5Cpowercfg.exe%22+%2FDuplicateScheme+%27e9a42b02-d5df-448d-aa00-03f14749eb61%27%3B%0D%0Aif%28+%24out+-match+%27%5Cs%28%5Ba-f0-9-%5D%7B36%7D%29%5Cs%27+%29+%7B%0D%0A++++%26+%22%24env%3Awindir%5CSystem32%5Cpowercfg.exe%22+%2FSetActive+%24Matches%5B1%5D%3B%0D%0A%7D+else+%7B%0D%0A++++%27Could+not+enable+Ultimate+Performance+power+scheme.%27+%7C+Write-Warning%3B%0D%0A%7D&SystemScriptType1=Ps1&SystemScript2=powercfg.exe+%2Fhibernate+off%0D%0Abcdedit+%2Fset+useplatformtick+yes%0D%0Abcdedit+%2Fset+disabledynamictick+yes%0D%0Abcdedit+%2Fdeletevalue+useplatformclock%0D%0Abcdedit+%2Fset+tscsyncpolicy+Enhanced&SystemScriptType2=Cmd&SystemScript3=Windows+Registry+Editor+Version+5.00%0D%0A%0D%0A%5BHKEY_LOCAL_MACHINE%5CSOFTWARE%5CMicrosoft%5CPolicyManager%5Cdefault%5CApplicationManagement%5CAllowGameDVR%5D%0D%0A%22value%22%3Ddword%3A00000000%0D%0A%0D%0A%5BHKEY_LOCAL_MACHINE%5CSYSTEM%5CCurrentControlSet%5CControl%5CSession+Manager%5Ckernel%5D%0D%0A%22GlobalTimerResolutionRequests%22%3Ddword%3A00000001%0D%0A%0D%0A%5BHKEY_LOCAL_MACHINE%5CSYSTEM%5CCurrentControlSet%5CControl%5CGraphicsDrivers%5CScheduler%5D%0D%0A%22EnablePreemption%22%3Ddword%3A00000000%0D%0A%0D%0A%5BHKEY_LOCAL_MACHINE%5CSOFTWARE%5CMicrosoft%5CWindows+NT%5CCurrentVersion%5CMultimedia%5CSystemProfile%5CTasks%5CGames%5D%0D%0A%22Scheduling+Category%22%3D%22High%22%0D%0A%22SFIO+Priority%22%3D%22High%22&SystemScriptType3=Reg&FirstLogonScript0=Windows+Registry+Editor+Version+5.00%0D%0A%0D%0A%5BHKEY_CURRENT_USER%5CControl+Panel%5CAccessibility%5CMouseKeys%5D%0D%0A%22Flags%22%3D%220%22%0D%0A%0D%0A%5BHKEY_CURRENT_USER%5CControl+Panel%5CAccessibility%5CStickyKeys%5D%0D%0A%22Flags%22%3D%220%22%0D%0A%0D%0A%5BHKEY_CURRENT_USER%5CControl+Panel%5CAccessibility%5CKeyboard+Response%5D%0D%0A%22Flags%22%3D%220%22%0D%0A%0D%0A%5BHKEY_CURRENT_USER%5CControl+Panel%5CAccessibility%5CToggleKeys%5D%0D%0A%22Flags%22%3D%220%22&FirstLogonScriptType0=Reg&WdacMode=Skip)

# Adicional - Marcar isso para Windows 11:

- Use classic context (right-click) menu in Windows 11
