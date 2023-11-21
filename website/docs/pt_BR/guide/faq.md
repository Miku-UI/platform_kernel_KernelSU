# FAQ

## KernelSU oferece suporte ao meu dispositivo?

Primeiro, seu dispositivo deve ser capaz de desbloquear o bootloader. Se não, então não há suporte.

Em seguida, instale o app gerenciador do KernelSU em seu dispositivo e abra-o, se mostrar `Sem suporte` então seu dispositivo não pode ser suportado imediatamente, mas você pode construir a fonte do kernel e integrar o KernelSU para fazê-lo funcionar ou usar [Dispositivos com suporte não oficial](unofficially-support-devices).

## Para usar o KernelSU precisa desbloquear o bootloader?

Certamente, sim.

## KernelSU suporta módulos?

Sim, mas está na versão inicial, pode apresentar bugs. Por favor, aguarde até que fique estável.

## KernelSU suporta Xposed?

Sim, [Dreamland](https://github.com/canyie/Dreamland) e [TaiChi](https://taichi.cool) funcionam agora. Para o LSPosed, você pode fazê-lo funcionar usando [ZygiskNext](https://github.com/Dr-TSNG/ZygiskNext).

## KernelSU suporta Zygisk?

KernelSU não tem suporte integrado ao Zygisk, mas você pode usar [ZygiskNext](https://github.com/Dr-TSNG/ZygiskNext).

## KernelSU é compatível com o Magisk?

O sistema de módulos do KernelSU está em conflito com a montagem mágica do Magisk, se houver algum módulo habilitado no KernelSU, então todo o Magisk não funcionaria.

Mas se você usar apenas o `su` do KernelSU, então funcionará bem com o Magisk. KernelSU modifica o `kernel` e o Magisk modifica o `ramdisk`, eles podem trabalhar juntos.

## KernelSU substituirá o Magisk?

Achamos que não e esse não é o nosso objetivo. O Magisk é bom o suficiente para solução root do espaço do usuário e terá uma longa vida. O objetivo do KernelSU é fornecer uma interface de kernel aos usuários, não substituindo o Magisk.

## KernelSU oferece suporte a dispositivos não GKI?

É possível. Mas você deve baixar o código-fonte do kernel e integrar o KernelSU à árvore do código-fonte e compilar o kernel você mesmo.

## KernelSU oferece suporte a dispositivos abaixo do Android 12?

É o kernel do dispositivo que afeta a compatibilidade do KernelSU e não tem nada a ver com a versão do Android. A única restrição é que os dispositivos lançados com Android 12 devem ser kernel 5.10+ (dispositivos GKI). Então:

1. Os dispositivos lançados com Android 12 devem ser compatíveis.
2. Dispositivos com kernel antigo (alguns dispositivos Android 12 também têm o kernel antigo) são compatíveis (você mesmo deve construir o kernel).

## KernelSU suporta kernel antigo?

É possível, o KernelSU é portado para o kernel 4.14 agora, para o kernel mais antigo, você precisa fazer o backport manualmente e PRs são sempre bem-vindas!

## Como integrar o KernelSU para o kernel antigo?

Por favor, consulte a guia [Como integrar o KernelSU para kernels não GKI](how-to-integrate-for-non-gki).

## Por que a minha versão do Android é 13 e o kernel mostra “android12-5.10”?

A versão do Kernel não tem nada a ver com a versão do Android, se você precisar fazer o flash do kernel, use sempre a versão do kernel, a versão do Android não é tão importante.

## Existe algum namespace de montagem --mount-master/global no KernelSU?

Não existe agora (talvez no futuro), mas há muitas maneiras de mudar manualmente para o namespace de montagem global, como:

1. `nsenter -t 1 -m sh` para obter um shell no namespace de montagem global.
2. Adicione `nsenter --mount=/proc/1/ns/mnt` ao comando que você deseja executar, o comando será executado no namespace de montagem global. O KernelSU também está [usando desta forma](https://github.com/tiann/KernelSU/blob/77056a710073d7a5f7ee38f9e77c9fd0b3256576/manager/app/src/main/java/me/weishu/kernelsu/ui/util/KsuCli.kt#L115).

## Eu sou GKI1.0, posso usar isso?

GKI1 é completamente diferente do GKI2, você deve compilar o kernel sozinho.