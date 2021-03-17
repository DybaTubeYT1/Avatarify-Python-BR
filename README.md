![mona](https://user-images.githubusercontent.com/80713813/111460108-5753fc80-86fa-11eb-8875-043a6c787623.gif)

<!-- Descarregar [Windows app (beta)](https://github.com/alievk/avatarify/wiki/Windows-App) -->

[![Abrir em Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/drive/1bElP9KQI9aQPiDfIE5kg1R4_kqATe8Pn?usp=sharing)

<!-- [<img src="https://img.shields.io/badge/slack-join-brightgreen?style=flat&logo=slack">](https://join.slack.com/t/avatarify/shared_invite/zt-dyoqy8tc-~4U2ObQ6WoxuwSaWKKVOgg) -->

:arrow_forward: [Demonstração](https://youtu.be/Q7LFDT-FRzs)

:arrow_forward: [AI-generaed Elon Musk](https://youtu.be/lONuXGNqLO0)

# Abrir Avatarify

Avatares fotorealistas para vídeo-conferência [aplicações](#configure-video-meeting-app). Democratizado.

Baseado em [First Order Motion Model](https://github.com/AliaksandrSiarohin/first-order-model).

**Open Avatarify não está afiliado à Avatarify Inc.**

## Notícias
- **14 de Dezembro de 2020.** Lançado o Windows GUI app beta. Veja [aqui](https://github.com/alievk/avatarify/wiki/Windows-App-(Beta)).
- **11 de Julho de 2020.** Adicionado suporte Docker. Agora pode correr Avatarify a partir do Docker em [Linux](#docker). Graças a [mikaelhg](https://github.com/mikaelhg) e [mintmaker](https://github.com/mintmaker) pela contribuição!
- **22 de Maio de 2020.** Adicionado o modo [Google Colab](https://colab.research.google.com/github/alievk/avatarify/blob/master/avatarify.ipynb). Agora pode correr o Avatarify em qualquer computador sem GPU!
- **7 de Maio de 2020.** Adicionado suporte de GPU remoto para todas as plataformas (baseado na solução [mynameisfiber's](https://github.com/mynameisfiber)). [Demo](https://youtu.be/3Dz_bUIPYFM). Implantação [instruções](https://github.com/alievk/avatarify/wiki/Remote-GPU). 
- **24 de Abril de 2020.** Adicionada a instalação do Windows [tutorial](https://www.youtube.com/watch?v=lym9ANVb120).
- **17 de Abril de 2020.** Criada a comunidade Slack. Junte-se por favor através do [link do convite](https://join.slack.com/t/avatarify/shared_invite/zt-dyoqy8tc-~4U2ObQ6WoxuwSaWKKVOgg).
- **15 de Abril de 2020.** Adicionados [StyleGAN-generated](https://www.thispersondoesnotexist.com) avatares. Basta premir `Q` e agora conduz-se uma pessoa que nunca existiu. Cada vez que carrega no botão - o novo avatar é amostrado.
- **13 de Abril de 2020.** Adicionado suporte Windows (kudos a [9of9](https://github.com/9of9)).

## Tabela de Conteúdos
- [Requisitos](#requisitos)
- [Instalar](#instalar)
    - [Baixar pesos de rede](#download-network-weights)
    - [Linux](#linux)
    - [Mac](#mac)
    - [Windows](#janelas)
    - [GPU Remoto](#remote-gpu)
    - [Docker](#docker)
- [Configuração de avatares](#setup-avatars)
- [Executar](#run)
    - [Linux](#linux-1)
    - [Mac](#mac-1)
    - [Windows](#windows-1)
- [Controlos](#controlos)
- [Conduzindo o seu avatar](#driving-seu-avatar)
- (#configure-video-meeting-app)
  - [Skype](#skype)
  - [Zoom](#zoom)
  - [Equipas](#teams)
  - [Slack](#slack)
- [Desinstalar](#uninstalar)
- [Contribuição](#contribuição)
- [FAQ](#faq)
- [Resolução de Problemas](#troubleshooting)

## Requisitos

Pode executar o Avatarify em dois modos: *localmente* e *remotely*.

Para executar o Avatarify *localmente* necessita de uma placa de vídeo com CUDA (NVIDIA). Caso contrário, ela irá voltar para o processador central e correr muito lentamente. Estas são métricas de desempenho para algum hardware:

- GeForce GTX 1080 Ti: **33 quadros por segundo***
- GeForce GTX 1070: **15 quadros por segundo***
- GeForce GTX 950: **9 quadros por segundo***

Também pode executar Avatarify *remotely* em [Google Colab](https://colab.research.google.com/github/alievk/avatarify/blob/master/avatarify.ipynb) (fácil) ou num [servidor dedicado](https://github.com/alievk/avatarify/wiki/Remote-GPU) com uma GPU (mais difícil). Não há requisitos especiais de PC para este modo, apenas uma ligação estável à Internet.

É claro que também é necessária uma webcam!

<!-- * [conda Python 3.7](https://docs.conda.io/en/latest/miniconda.html)
* [CUDA](https://developer.nvidia.com/cuda-downloads) -->

## Instalar

#### Descarregar pesos de rede
Descarregar os pesos do modelo a partir de [aqui](https://openavatarify.s3.amazonaws.com/weights/vox-adv-cpk.pth.tar) ou [aqui](https://yadi.sk/d/M0FWpz2ExBfgAA) ou [aqui](https://drive.google.com/file/d/1coUCdyRXDbpWnEkA99NLNY60mb9dQ_n3/view?usp=sharing) [228 MB, md5sum `8a45a24037871c045fbb8a6a8aa95ebc`]

#### Linux
Linux utiliza `v4l2loopback` para criar uma câmara fotográfica virtual.

<!--- 1. instalar [CUDA](https://developer.nvidia.com/cuda-downloads?target_os=Linux&target_arch=x86_64). --->
1. Descarregar [Miniconda Python 3.7](https://docs.conda.io/en/latest/miniconda.html#linux-installers) e instalar usando o comando:
```bash
bash Miniconda3-latest-Linux-x86_64.sh
```
2. Clonar `avatarify` e instalar as suas dependências (o privilégio de sudolege é exigido):
```bash
clone de git https://github.com/alievk/avatarify.git
cd avatarify
bash scripts/install.sh
```
3. [Baixar pesos de rede](#download-network-weights) e colocar o ficheiro `vox-adv-cpk.pth.tar` no directório `avatarify` (não o descompacte).


#### Mac
<!--
*(!) Nota*: descobrimos que nas versões após [v4.6.8 (23 de Março de 2020)](https://zoom.us/client/4.6.19178.0323/ZoomInstaller.pkg) Suporte para máquinas fotográficas virtuais com Zoom desactivado no Mac. Para utilizar o Avatarify no Zoom pode escolher entre 2 opções:
- Instalar [Zoom v4.6.8](https://zoom.us/client/4.6.19178.0323/ZoomInstaller.pkg), que é a última versão que suporta câmaras virtuais
- Utilizar a última versão do Zoom, mas desactivar a validação da biblioteca ao executar este comando em terminal:
```bash
codesign --remove-signature /Applications/zoom.us.app
```
-->
<!--*(!) Nota*: Para executar Avatarify em Mac é necessária uma ligação [GPU remota](https://github.com/alievk/avatarify/wiki/Remote-GPU).-->

Vamos utilizar [CamTwist](http://camtwiststudio.com) para criar uma câmara virtual para Mac.

1. Instalar [Miniconda Python 3.7](https://docs.conda.io/en/latest/miniconda.html#macosx-installers) ou utilizar *Casco Homebrew*: instalar --cask miniconda'.
2. [Descarregar](https://github.com/alievk/avatarify/archive/master.zip) e desempacotar o repositório ou utilizar o `git`:
```bash
git clone https://github.com/alievk/avatarify.git
cd avatarify
bash scripts/install_mac.sh
```
3. Descarregar e instalar [CamTwist](http://camtwiststudio.com) a partir de [aqui](http://camtwiststudio.com/download). É fácil.

#### Janelas

<!-- **Novo***: Veja o nosso [app](https://github.com/alievk/avatarify/wiki/Windows-App) com interface gráfica! -->

:arrow_forward: [Vídeo tutorial](https://youtu.be/lym9ANVb120)

Este guia é testado para Windows 10.

<!--- 1. instalar [CUDA](https://developer.nvidia.com/cuda-downloads?target_os=Windows&target_arch=x86_64&target_version=10&target_type=exenetwork). -->
1. Instalar [Miniconda Python 3.8](https://docs.conda.io/en/latest/miniconda.html#windows-installers).
2. Instalar [Git](https://git-scm.com/download/win).
3. Prima o botão Windows e escreva "miniconda". Executar o Anaconda Prompt sugerido.
4. Descarregar e instalar o Avatarify (por favor copie - cole estes comandos e não os altere):
```bash
clone de git https://github.com/alievk/avatarify.git
cd avatarify
scripts\install_windows.bat
```
5. [Baixar pesos de rede](#download-network-weights) e colocar o ficheiro `vox-adv-cpk.pth.tar` no directório `avatarify` (não o descompacte).
6. Executar `run_windows.bat`. Se a instalação foi bem sucedida, aparecerão duas janelas "cam" e "avatarify". Deixe estas janelas abertas para os próximos passos de instalação. <!-- Se existirem várias câmaras (incluindo as virtuais) no sistema, poderá ter de seleccionar a correcta. Abrir `scripts/settings_windows.bat` e editar a variável `CAMID`. `CAMID` é um número índice de câmara como 0, 1, 2, ...-->
7. Instalar [OBS Studio](https://obsproject.com/) para capturar a saída do Avatarify.
8. Instalar [VirtualCam plugin](https://obsproject.com/forum/resources/obs-virtualcam.539/). Escolher `Instalar e registar apenas 1 câmara virtual`.
9. Executar o OBS Studio.
10. Na secção Fontes, prima o botão Adicionar (sinal "+"), seleccione Windows Capture e prima OK. Na janela exibida, escolher "[python.exe]: avatarify" no menu suspenso Janela e premir OK. Depois seleccionar Edit -> Transform -> Fit to screen.
11. Em OBS Studio, vá a Ferramentas -> VirtualCam. Verifique AutoStart, defina Buffered Frames a 0 e carregue em Start.
12. Agora `OBS-Câmera` deve estar disponível em Zoom (ou outro software de videoconferência).

Os passos 10-11 são necessários apenas uma vez durante a configuração.

#### GPU remoto

Pode descarregar o trabalho pesado para [Google Colab](https://colab.research.google.com/github/alievk/avatarify/blob/master/avatarify.ipynb) ou um [servidor com uma GPU](https://github.com/alievk/avatarify/wiki/Remote-GPU) e utilizar o seu computador portátil apenas para comunicar o fluxo de vídeo. O servidor e o software cliente são nativos e estão disponíveis em docas.

### Docker
As imagens do Docker só estão disponíveis no Linux.

1. Instalar o Docker seguindo a [Documentação](https://docs.docker.com/engine/install/). Depois execute este [passo](https://docs.docker.com/engine/install/linux-postinstall/#manage-docker-as-a-non-root-user) para tornar o Docker disponível para o seu utilizador.
2. Para utilizar o gpu (dificilmente recomendado): Instale os controladores nvidia e [docker nvidia](https://github.com/NVIDIA/nvidia-docker#quickstart).
3. Clone `avatarify` e instale as suas dependências (módulo kernel v4l2loopback):
```bash
clone de git https://github.com/alievk/avatarify.git
cd avatarify
bash scripts/install_docker.sh
```
4. Construir o Dockerfile:
```bash
cd avatarify
construção portuária -t avatarify .
```
## Configuração de avatares
Avatarify vem com um conjunto padrão de avatares de pessoas famosas, mas pode estender este conjunto simplesmente copiando os seus avatares para a pasta "avatares".

Siga estes conselhos para uma melhor qualidade visual:
* Faça uma colheita quadrada da sua imagem de avatar.
* Cortar a cara do avatar para que não esteja muito perto nem muito longe. Use avatares padrão como referência.
* Prefira imagens com fundo uniforme. Vai diminuir os artefactos visuais.

## Correr
A sua câmara web deve estar ligada à corrente.

**Nota:** execute a sua aplicação de vídeo-conferência apenas após o Avatarify ser iniciado.

#### Linux
The run script will create virtual camera `/dev/video9`. You can change these settings in `scripts/settings.sh`.

<!-- Supõe-se que existe apenas uma câmara web ligada ao computador em `/dev/video0`.-->
Pode utilizar o comando `v4l2-ctl --list-devices' para listar todos os dispositivos do seu sistema.

Executar:
```bash
bash run.sh
```
Se não tiver instalado uma GPU, adicione a bandeira `--no-gpus'. Para utilizar o Docker, adicionar a bandeira `--docker'.

As janelas `cam` e `avatarify` irão aparecer. A janela "cam" é para controlar a sua posição facial e "avatarify" é para a pré-visualização da animação avatar. Por favor, siga estas [recomendações](#driving-your-avatar) para conduzir os seus avatares.

#### Mac
*Nota*: No Mac Avatarify corre apenas com [Google Colab](https://colab.research.google.com/github/alievk/avatarify/blob/master/avatarify.ipynb) ou um [servidor dedicado](https://github.com/alievk/avatarify/wiki/Remote-GPU) com GPU.

Por favor, encontre onde descarregou `avatarify` e o caminho substituto `/path/to/avatarify` abaixo.

<!--1. Abra o terminal e corra:
```bash
cd /caminho/para/avatarify
bash run_mac.sh --worker-hosting gpu_server_address
```-->
1. Para executar o Avatarify por favor siga as instruções para [Google Colab](https://colab.research.google.com/github/alievk/avatarify/blob/master/avatarify.ipynb) ou um [servidor dedicado](https://github.com/alievk/avatarify/wiki/Remote-GPU).
2. Ir para [CamTwist](http://camtwiststudio.com).
3. Escolha `Desktop+` e prima `Select`.
4. Na secção `Settings' escolha `Confine to Application Window' e seleccione `python (avatarify)` a partir do menu drop-down.

As janelas `cam` e `avatarify` irão aparecer. A janela `cam` serve para controlar a sua posição facial e `avatarify` serve para a pré-visualização da animação avatar. Por favor, siga estas [recomendações](#driving-your-avatar) para conduzir os seus avatares.

#### Janelas

<!--
Se existirem várias câmaras (incluindo virtuais) no seu sistema, poderá ter de seleccionar a câmara correcta em `scripts/settings_windows.bat`. Abra este ficheiro e edite a variável `CAMID`. A variável `CAMID` é um número de índice de câmaras como 0, 1, 2, ...
-->

1. No Anaconda Prompt:
```
cd C:\path paraavatarify
run_windows.bat
```
2. Gerir o estúdio OBS. Deverá iniciar automaticamente a transmissão de vídeo do Avatarify para o 'OBS-Camera'.

As janelas `cam` e `avatarify` irão aparecer. A janela "cam" é para controlar a sua posição facial e "avatarify" é para a pré-visualização da animação avatar. Por favor, siga estas [recomendações](#driving-your-avatar) para conduzir os seus avatares.

**Note:** Para reduzir a latência do vídeo, no OBS Studio clique com o botão direito na janela de pré-visualização e desmarque Activar Pré-visualização.

## Controlos


Chaves | Controlos
--- | ---
1-9 | Estes alternarão imediatamente entre os primeiros 9 avatares.
P | Liga o avatar gerado por StyleGAN. Cada vez que se prime o botão - o novo avatar é amostrado.
0 | Liga e desliga a exibição de avatares.
A/D | Avatar anterior/próximo avatar em pasta.
W/S | Ampliar/Desactivar câmara de zoom.
U/H/J/K | Traduzir câmara. `H` - esquerda, `K` - direita, `U` - cima, `J` - baixo por 5 pixels. Adicionar `Shift` para ajustar por 1 pixel.
Shift-Z | Reiniciar o zoom da câmara e a tradução
Z/C | Ajustar a opacidade de sobreposição de alvos de avatares.
X | Redefinir quadro de referência.
F | Alternar o modo de procura da moldura de referência.
R | Janela de referência do espelho.
T | Janela de saída de espelhos.
L | Recarregar avatares.
I | Mostrar FPS
O | Sobreposição da detecção facial.
ESC | Desistir

## Conduzindo o seu avatar

Estes são os princípios fundamentais para conduzir o seu avatar:

* Alinhe o seu rosto na janela da câmara o mais próximo possível em proporção e posição do avatar alvo. Use a função zoom in/out (teclas W/S) e a tradução para a esquerda, direita, para cima, para baixo (teclas U/H/J/K). Quando tiver alinhado, carregar em 'X' para usar este frame como referência para conduzir o resto da animação.
* Use a função de sobreposição de imagem (teclas Z/C) ou a função de sobreposição de detecção facial (tecla O) para combinar as suas expressões faciais e as do avatar o mais próximo possível

Em alternativa, pode clicar em 'F' para que o software tente encontrar um quadro de referência melhor. Isto irá abrandar o framerate, mas enquanto isto acontece, pode continuar a mover a sua cabeça: a janela de pré-visualização irá piscar a verde quando encontrar que a sua pose facial está mais próxima do avatar do que a que está a usar actualmente. Verá também dois números: o primeiro número é o quão perto está actualmente alinhado com o avatar, e o segundo número é o quão perto está alinhado o quadro de referência.

Pretende obter o primeiro número tão pequeno quanto possível - cerca de 10 é normalmente um bom alinhamento. Quando terminar, prima novamente 'F' para sair do modo de procura da moldura de referência.

Não precisa de ser exacto, e algumas outras configurações podem ainda produzir melhores resultados, mas é normalmente um bom ponto de partida.

## Configurar aplicação de reunião em vídeo

Avatarify suporta qualquer aplicação de vídeo-conferência onde a fonte de entrada de vídeo pode ser alterada (Zoom, Skype, Hangouts, Slack, ...). Aqui estão alguns exemplos de como configurar uma aplicação específica para utilizar o Avatarify.

#### Skype

Ir para Definições -> Áudio & Vídeo, escolher "avatarify" (Linux), "CamTwist" (Mac) ou "OBS-Câmera" (Windows) camera.

<img ![skype](https://user-images.githubusercontent.com/80713813/111460804-2c1ddd00-86fb-11eb-8e6f-d03e58db35e0.jpg)
 largura=600>

### Zoom

Ir para Definições -> Vídeo e escolher `avatarify` (Linux), `CamTwist` (Mac) ou `OBS-Camera` (Windows) no menu pendente Camera.

![zoom](https://user-images.githubusercontent.com/80713813/111461235-b6664100-86fb-11eb-9f05-ce6d5bf3b2c0.jpg)


### Equipas

Vá à sua foto de perfil -> Configurações -> Dispositivos e escolha `avatarify` (Linux), `CamTwist` (Mac) ou `OBS-Camera` (Windows) no menu pendente Camera.

![teams](https://user-images.githubusercontent.com/80713813/111460993-6dae8800-86fb-11eb-875e-d78088ff7ce7.jpg)

### Folga

Fazer uma chamada, permitir o browser utilizando câmaras, clicar no ícone Definições, escolher `avatarify` (Linux), `CamTwist` (Mac) ou `OBS-Camera` (Windows) no menu suspenso Definições de vídeo.

![slack](https://user-images.githubusercontent.com/80713813/111461289-c847e400-86fb-11eb-8e14-c2b26a1d4fb9.jpg)

## Desinstalar
Para remover o Avatarify e os seus programas relacionados siga as [instruções](https://github.com/alievk/avatarify/wiki/Removing-Avatarify) no Wiki.


## Contribuição

O nosso objectivo é democratizar os avatares fotorealistas para videoconferências. Para tornar a tecnologia ainda mais acessível, temos de resolver os seguintes problemas:

~~Adicionar suporte para mais plataformas (Linux e Mac já são suportados).~~
* ~~Poio a GPU de memória. Este é um trabalho em curso.~~~
*Portação para GPUs não-CUDA (GPUs Intel integradas, GPUs AMD, etc.) e optimização. O objectivo é executar Avatarify em tempo real (pelo menos 10FPS) em computadores portáteis modernos.

Por favor, faça pedidos de extracção se tiver quaisquer melhorias ou correcções de bugs.


## FAQ

P: **Preciso de algum conhecimento de programação para executar o Avatarify?**  
R: Na verdade não, mas precisa de algum conhecimento a nível de principiante sobre a linha de comando. Para Windows gravámos um vídeo [tutorial](https://www.youtube.com/watch?v=lym9ANVb120), por isso vai ser fácil de instalar.

P: **Por que funciona tão lentamente no meu Macbook?**  
R: O modelo utilizado no Avatarify requer uma GPU NVIDIA habilitada para CUDA para efectuar cálculos pesados. Os Macbooks não têm tais GPUs, e para processar utilizam CPU, que tem muito menos poder computacional para executar Avatarify sem problemas.

P: **Não tenho uma GPU NVIDIA, posso executá-la?**  
R: Ainda pode executá-la sem uma GPU NVIDIA, mas com um desempenho drasticamente reduzido (<1fps).

P: **Eu tenho uma GPU ATI (por exemplo, Radeon). Porque é que funciona tão lentamente?**  
R: Para executar a rede neural Avatarify usa a biblioteca PyTorch, que está optimizada para CUDA. Se a PyTorch não conseguir encontrar uma GPU com CUDA no seu sistema, ela irá voltar para a CPU. O desempenho na CPU será muito pior.

P: **Como adicionar um novo avatar?**  
R: É fácil. Tudo o que precisa é encontrar uma imagem do seu avatar e colocá-la na pasta 'avatares'. [Mais](https://github.com/alievk/avatarify#setup-avatars).

P: **O meu avatar parece distorcido.**  
R: Precisa de calibrar a sua posição facial. Por favor siga as [dicas](https://github.com/alievk/avatarify#driving-your-avatar) ou veja o vídeo [tutorial](https://youtu.be/lym9ANVb120?t=662).

P: **Posso usar uma GPU de nuvem?**  
R: Isto é um trabalho em curso. Ver a [discussão](https://github.com/alievk/avatarify/issues/115) relevante.

P: **Avatarify crashed, o que fazer?**  
R: Primeiro, tente encontrar o seu erro na secção [troubleshooting](https://github.com/alievk/avatarify#troubleshooting). Se não estiver lá, tente encontrá-lo na secção [questões](https://github.com/alievk/avatarify/issues). Se não encontrou o seu problema lá, por favor abra um novo utilizando o modelo de problema.

P: **Posso utilizar o Avatarify para fins comerciais?**  
R: Não. Avatarify e First Order Motion Model são licenciados sob licença Creative Commons Não-Comercial, que proíbe o uso comercial.

P: **Que aplicações de videoconferência é que o Avatarify suporta?**  
R: Avatarify cria uma câmara virtual que pode ser ligada a qualquer aplicação onde a fonte de entrada de vídeo pode ser alterada (Zoom, Skype, Hangouts, Slack, ...). 

P: **Onde posso discutir com a comunidade tópicos relacionados com Avatarify-?**  
R: Temos Slack. Por favor, junte-se: [<img src="https://img.shields.io/badge/slack-join-brightgreen?style=flat&logo=slack">](https://join.slack.com/t/avatarify/shared_invite/zt-dyoqy8tc-~4U2ObQ6WoxuwSaWKKVOgg)

## Troubleshooting

Por favor, siga a página [Wiki](https://github.com/alievk/avatarify/wiki/Troubleshooting).
