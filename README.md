<p align="center">
  <img src="./build/icon.png" alt="Ícone do Assistant" width="104">
</p>

<h1 align="center">Assistant</h1>

<p align="center">
  Gerenciador de ações manuais para Windows com perfis por aplicativo, sequências de teclado e mouse, repetição controlada, cooldowns e HUD transparente.
</p>

<p align="center">
  <img alt="Versão" src="https://img.shields.io/badge/versão-0.4.1-2563eb?style=flat-square">
  <img alt="Plataforma" src="https://img.shields.io/badge/plataforma-Windows-0078d4?style=flat-square&logo=windows11&logoColor=white">
  <img alt="Electron" src="https://img.shields.io/badge/Electron-43-47848f?style=flat-square&logo=electron&logoColor=white">
  <img alt="React" src="https://img.shields.io/badge/React-19-149eca?style=flat-square&logo=react&logoColor=white">
  <img alt="Licença" src="https://img.shields.io/badge/licença-MIT-16a34a?style=flat-square">
</p>

---

## Sobre o projeto

O **Assistant** permite transformar um acionamento manual em uma sequência organizada de entradas de teclado e mouse. As ações ficam separadas por perfil, conjunto e aplicativo alvo, permitindo manter configurações diferentes para jogos, programas e rotinas de acessibilidade.

O projeto foi desenvolvido com foco em:

- configuração visual, sem editar arquivos manualmente;
- execução previsível e fácil de interromper;
- HUD discreto que não bloqueia a tela;
- dados armazenados localmente;
- reutilização dos mesmos atalhos em aplicativos diferentes;
- proteção contra entradas presas e execuções fora de contexto.

> [!IMPORTANT]
> O Assistant não lê memória, pixels, vida, inventário, inimigos ou qualquer estado interno do aplicativo alvo. Ele não injeta código em outros processos e não procura contornar sistemas de proteção. Todas as ações partem de um comando configurado pelo usuário.

## Sumário

- [Principais recursos](#principais-recursos)
- [Requisitos](#requisitos)
- [Instalação para usuários](#instalação-para-usuários)
- [Primeiros passos](#primeiros-passos)
- [Repetição da sequência](#repetição-da-sequência)
- [Cooldowns e cargas](#cooldowns-e-cargas)
- [Overlay e menu radial](#overlay-e-menu-radial)
- [Execução pelo código-fonte](#execução-pelo-código-fonte)
- [Gerar instalador](#gerar-instalador)
- [Dados, backup e privacidade](#dados-backup-e-privacidade)
- [Solução de problemas](#solução-de-problemas)
- [Limites operacionais](#limites-operacionais)
- [Estrutura do projeto](#estrutura-do-projeto)
- [Contribuição](#contribuição)
- [Licença](#licença)

## Principais recursos

### Perfis e conjuntos

- Perfis associados ao executável de cada jogo ou programa.
- Detecção automática do aplicativo em primeiro plano.
- Uso do mesmo atalho em perfis diferentes.
- Conjuntos independentes dentro de um perfil, úteis para classes, personagens, builds ou contextos de trabalho.
- Atalhos próprios para alternar conjuntos sem abrir a janela principal.

### Acionamentos

O Assistant reconhece:

- teclado e combinações com modificadores;
- Mouse 4 e Mouse 5;
- roda do mouse para cima e para baixo;
- controle XInput experimental;
- botões A, B, X, Y, LB, RB, LT, RT, direcional, Start, Back, L3 e R3.

Modos disponíveis:

| Modo | Comportamento |
|---|---|
| Ao pressionar | Executa quando o botão é pressionado. |
| Ao soltar | Executa quando o botão é liberado. |
| Duplo toque | Exige dois acionamentos dentro do intervalo configurado. |
| Pressionamento longo | Executa após manter o botão pressionado pelo tempo definido. |
| Enquanto segura | Repete somente enquanto o botão físico permanecer pressionado. |

### Editor de ações

Cada ação pode combinar etapas de:

- pressionar uma tecla;
- aguardar um intervalo;
- clicar ou segurar botões do mouse;
- usar Mouse 4 ou Mouse 5;
- rolar a roda do mouse;
- executar outra ação como subação reutilizável;
- reproduzir um aviso sonoro.

Também estão disponíveis:

- captura visual de teclas e botões;
- reordenação e duplicação de etapas;
- gravador de sequência finita;
- variáveis de tecla e tempo por perfil;
- estimativa da duração de cada ciclo;
- diagnóstico de entradas, bloqueios e execuções.

### Repetição controlada

- Quantidade definida entre `1` e `9.999` ciclos.
- Valor `-1` para repetição contínua.
- Intervalo configurável entre os ciclos.
- Interrupção ao pressionar novamente o mesmo atalho.
- Botão **Parar execução** na interface.
- Parada automática opcional ao perder o foco do aplicativo alvo.
- Progresso exibido no editor e no overlay.

### Cooldowns, grupos e cargas

- Cooldown individual por ação.
- Início do cooldown ao começar ou ao finalizar a execução completa.
- Grupos de cooldown compartilhado.
- Até dez cargas por ação.
- Recarga individual de cada carga.
- Reset e reinício manual do contador.
- Valores fixos ou vinculados a variáveis do perfil.

### Overlay transparente

- HUD sempre acima do aplicativo alvo.
- Fundo da janela totalmente transparente.
- Modos **Minimalista**, **Micro HUD** e **Barra horizontal**.
- Exibição de tecla, nome, estado, repetição, cargas e cooldown.
- Opacidade e escala configuráveis.
- Opção para mostrar somente ações em atividade.
- Ocultação automática fora do perfil associado.
- Modo de passagem de cliques para não interferir no jogo.
- Reposicionamento livre com posição salva automaticamente.

### Menu radial

- Até oito ações por conjunto.
- Acionamento por teclado ou mouse.
- Seleção pela direção do cursor.
- Zona central para cancelar.
- Janela transparente e sem captura permanente do foco.

### Organização e operação

- Busca por nome, descrição ou tecla.
- Fila opcional quando outra ação já está em execução.
- Bandeja do Windows.
- Inicialização automática opcional.
- Pausa global do motor.
- Parada de emergência em `Ctrl + Shift + F12`.
- Importação e exportação de perfis.
- Backup completo das configurações.
- Migração automática de versões anteriores.

## Requisitos

### Para usar o aplicativo instalado

| Requisito | Observação |
|---|---|
| Sistema operacional | Windows 10 ou Windows 11, 64 bits. |
| PowerShell | Windows PowerShell disponível no sistema; já vem instalado normalmente no Windows. |
| Permissões | O Assistant e o aplicativo alvo devem usar o mesmo nível de permissão. |
| Modo de exibição | Para o overlay, prefira modo janela ou janela sem bordas. |
| Controle | Opcional; deve ser compatível com XInput. |

A versão instalada não exige VS Code, Node.js ou npm.

### Para desenvolver ou compilar

- Windows 10 ou Windows 11, 64 bits;
- Node.js 22 LTS ou 24;
- npm;
- Git, opcional;
- VS Code, opcional, mas recomendado.

## Instalação para usuários

1. Abra a área **Releases** deste repositório.
2. Baixe o instalador da versão mais recente, com nome semelhante a:

```text
Assistant-0.4.1-x64.exe
```

3. Execute o instalador.
4. Escolha a pasta de instalação.
5. Abra o **Assistant** pelo menu Iniciar ou pelo atalho da área de trabalho.

Na primeira execução, o Assistant prepara localmente o componente responsável pelas entradas do Windows. Esse processo pode levar alguns segundos.

> [!NOTE]
> O projeto ainda pode ser distribuído sem assinatura digital. Nesse caso, o Windows SmartScreen ou um antivírus pode solicitar confirmação. Verifique se o arquivo foi obtido das Releases oficiais ou compile diretamente pelo código-fonte.

> [!TIP]
> Caso o jogo seja executado como administrador, abra o Assistant como administrador também. Um programa sem elevação normalmente não consegue enviar entradas para outro processo elevado.

## Primeiros passos

### 1. Configure o perfil

1. Selecione ou crie um perfil.
2. Abra o jogo ou programa desejado.
3. Clique em **Detectar**.
4. Mude para a janela alvo e aguarde a detecção.
5. Confirme o nome do executável.

### 2. Crie uma ação

1. Clique em **Nova ação**.
2. Escolha o conjunto ao qual ela pertence.
3. Defina o acionamento, como `F7`, `Ctrl + Q` ou `Mouse 4`.
4. Escolha o modo de acionamento.
5. Adicione uma ou mais etapas.
6. Ative a ação e salve.

Exemplo:

```text
Acionamento: F7

1. Pressionar tecla 1 por 40 ms
2. Aguardar 150 ms
3. Pressionar tecla 2 por 40 ms
4. Aguardar 180 ms
5. Pressionar tecla 3 por 40 ms
```

### 3. Faça um teste seguro

Antes de usar em um jogo:

1. abra o Bloco de Notas;
2. desative temporariamente a exigência de primeiro plano ou associe um perfil ao Bloco de Notas;
3. configure uma ação que envie uma tecla simples;
4. confirme se a quantidade, os intervalos e a interrupção funcionam como esperado.

## Repetição da sequência

A repetição envolve a sequência completa da ação.

### Quantidade definida

```text
Quantidade: 10
Intervalo: 500 ms
```

A sequência será executada dez vezes. O intervalo é aplicado entre os ciclos, sem espera adicional após o último.

### Repetição contínua

```text
Quantidade: -1
Intervalo: 500 ms
```

A execução continua até uma destas condições:

- o mesmo atalho ser pressionado novamente;
- o botão **Parar execução** ser acionado;
- a parada de emergência ser usada;
- o motor ser pausado;
- o aplicativo alvo perder o foco, quando essa proteção estiver ativada;
- o Assistant ser encerrado.

> [!WARNING]
> Use intervalos adequados. No modo contínuo, o intervalo mínimo efetivo é de 50 ms. O modo **Enquanto segura** possui repetição própria e não pode ser combinado com a repetição da sequência.

## Cooldowns e cargas

O cooldown do Assistant é um contador local. Ele não lê o cooldown real do jogo ou programa.

É possível escolher quando o contador começa:

- **Ao iniciar:** começa no primeiro ciclo.
- **Ao finalizar:** começa após a última repetição ou após uma interrupção já iniciada.

As cargas e cooldowns são consumidos uma vez por acionamento da ação, não uma vez por ciclo.

Os grupos compartilhados permitem que várias ações usem o mesmo bloqueio. Um exemplo comum é um grupo para poções, no qual usar uma ação bloqueia temporariamente as demais.

## Overlay e menu radial

### Reposicionar o overlay

1. Abra **Preferências**.
2. Clique em **Reposicionar overlay**.
3. Arraste pela alça exibida no HUD.
4. Clique em **Concluir**.

A posição é salva automaticamente. O mesmo comando também está disponível no menu da bandeja.

### Evitar que o HUD atrapalhe

Configuração recomendada para jogos:

```text
Ocultar fora do perfil: ativado
Mostrar somente ativos: ativado
Ignorar cliques: ativado
Opacidade: 0,80 a 0,90
Escala: 0,85 a 1,00
```

Caso o overlay não apareça sobre um jogo em tela cheia, use **janela sem bordas** ou **modo janela**.

## Execução pelo código-fonte

Clone ou baixe este repositório e abra o terminal na pasta do projeto.

```bash
npm install
npm run dev
```

No Windows, também é possível executar:

```text
INICIAR.bat
```

O terminal deve permanecer aberto somente durante o modo de desenvolvimento.

### Scripts disponíveis

| Comando | Função |
|---|---|
| `npm run dev` | Inicia Vite e Electron em modo de desenvolvimento. |
| `npm run build` | Gera a interface de produção na pasta `dist`. |
| `npm run preview` | Visualiza o build do Vite localmente. |
| `npm run dist` | Gera o instalador NSIS para Windows. |
| `npm run dist:portable` | Gera uma versão portátil. |

## Gerar instalador

Execute:

```text
GERAR_INSTALADOR.bat
```

Ou use o terminal:

```bash
npm install
npm run dist
```

O instalador será criado na pasta:

```text
release/
```

Para gerar a versão portátil:

```bash
npm run dist:portable
```

## Dados, backup e privacidade

Na versão atual:

- as configurações permanecem no computador do usuário;
- não é necessário criar conta;
- não há telemetria ou sincronização online;
- o funcionamento normal não depende de internet após a instalação.

A pasta de dados pode ser aberta por:

```text
Preferências → Abrir pasta de dados
```

No Windows, ela normalmente corresponde a:

```text
%APPDATA%\Assistant\
```

O arquivo principal é:

```text
assistant-config.json
```

Use os recursos de **Exportar backup** e **Exportar perfil** antes de atualizar manualmente arquivos do projeto.

## Solução de problemas

### A entrada é capturada, mas a ação não executa

Verifique:

- se **Ação ativa** está habilitada;
- se o executável do perfil está configurado corretamente;
- se o conjunto correto está ativo;
- se a janela alvo está em primeiro plano;
- se a ação está em cooldown ou sem cargas;
- se o motor está pausado;
- se outra ação está executando e o modo atual bloqueia novas ações;
- se o Assistant e o aplicativo alvo usam o mesmo nível de permissão.

### O overlay não aparece

- Ative o overlay em **Preferências**.
- Confirme se a ação está marcada para aparecer no overlay.
- Desative temporariamente **Mostrar somente ativos**.
- Confirme se o perfil foi identificado.
- Teste com **Ocultar fora do perfil** desativado.
- Use modo janela ou janela sem bordas.

### O overlay não pode ser arrastado

- Use **Preferências → Reposicionar overlay**.
- Durante o reposicionamento, arraste pela alça exibida.
- Clique em **Concluir** para restaurar a passagem de cliques.

### O jogo está como administrador

Feche o Assistant e abra-o usando **Executar como administrador**. O nível de permissão precisa ser igual ao do aplicativo alvo.

### O antivírus sinalizou o componente de entrada

Ferramentas que capturam atalhos globais e enviam entradas podem receber análise adicional de antivírus. Baixe somente das Releases oficiais, confira o código-fonte ou compile localmente.

### O CMD fica aberto

Isso ocorre apenas com `INICIAR.bat` ou `npm run dev`. Instale o aplicativo gerado por `npm run dist` para usá-lo sem terminal.

### Mouse ou controle não foi reconhecido

- Abra o diagnóstico e confirme se o motor está pronto.
- Use a opção de recompilar o componente nativo.
- Para controle, confirme que o dispositivo é reconhecido como XInput pelo Windows.
- O suporte a controle ainda é experimental.

## Limites operacionais

| Item | Limite atual |
|---|---:|
| Etapas autorais por ação | 30 |
| Etapas após expansão de subações | 60 |
| Duração máxima de cada ciclo | 20 segundos |
| Repetições finitas | 1 a 9.999 |
| Intervalo mínimo no modo contínuo | 50 ms |
| Cargas por ação | 1 a 10 |
| Itens no menu radial | Até 8 |
| Variáveis por perfil | Até 40 |
| Tamanho máximo da fila | Até 10 ações |

A parada de emergência padrão é:

```text
Ctrl + Shift + F12
```

Ela interrompe execuções, repetições, fila, timers e libera entradas mantidas pelo Assistant.

## Escopo e uso responsável

O Assistant foi projetado como uma ferramenta local de atalhos, acessibilidade e qualidade de vida. O projeto não oferece:

- leitura de memória de outros processos;
- reconhecimento de tela ou análise de pixels;
- seleção automática de alvos;
- movimentação autônoma;
- coleta automática;
- injeção de código;
- ocultação do processo;
- evasão de anti-cheat.

Cada jogo ou serviço possui regras próprias. Verifique os termos de uso do aplicativo alvo antes de utilizar sequências de entrada, especialmente repetições contínuas.

## Estrutura do projeto

```text
Assistant/
├── build/                    # Ícones do aplicativo e da bandeja
├── electron/
│   ├── main.cjs              # Processo principal, execução e janelas
│   ├── preload.cjs           # Ponte segura entre Electron e React
│   └── windows/
│       ├── AssistantInputHelper.cs
│       └── build-helper.ps1
├── src/
│   ├── App.jsx               # Interface principal, overlay e menu radial
│   ├── main.jsx              # Entrada do React
│   └── styles.css            # Sistema visual
├── GERAR_INSTALADOR.bat
├── INICIAR.bat
├── package.json
└── vite.config.js
```

### Tecnologias

- Electron;
- React;
- Vite;
- JavaScript;
- C# e Win32 para captura e envio de entradas;
- NSIS por meio do electron-builder.

## Contribuição

Contribuições são bem-vindas.

1. Faça um fork do repositório.
2. Crie uma branch para sua alteração:

```bash
git checkout -b feature/minha-melhoria
```

3. Instale as dependências e teste localmente.
4. Faça commits objetivos.
5. Abra um Pull Request explicando o problema, a solução e como validar a mudança.

Ao contribuir com o motor de entrada, preserve os princípios do projeto: execução iniciada pelo usuário, interrupção confiável, ausência de leitura interna do aplicativo alvo e nenhuma tentativa de evasão de mecanismos de proteção.

## Licença

Distribuído sob a licença [MIT](./LICENSE).

Copyright © Daniel.
