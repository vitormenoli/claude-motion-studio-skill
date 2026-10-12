# Claude Motion Studio Skill 🤖🎬

Repositório contendo as diretrizes avançadas de engenharia de prompt e Motion Design (baseadas nas regras Motion Studio Rules) para instruir o **Claude Opus 5.5** a atuar como um estúdio de animação profissional nativo.

## ✨ Como Funciona?
Este repositório foi construído utilizando o conceito de arquivos de configuração automática do Claude. Ao clonar este repositório ou mover o arquivo `CLAUDE.md` para a pasta onde você desenvolve seus vídeos de motion utilizando o **Claude Code**, a IA lerá as regras e assumirá a persona de diretor de arte automaticamente antes de aceitar seus comandos.

## 🚀 Como Utilizar no seu Ambiente Local

1. Crie uma pasta para o seu novo projeto de vídeo.
2. Baixe ou copie o arquivo `CLAUDE.md` deste repositório e cole-o na raiz da sua pasta de trabalho.
3. Abra o seu terminal do **Claude Code** dentro dessa pasta.
4. Envie o seu briefing de forma simples no final, pois o Claude já estará sob o comando das regras restritas. 

**Exemplo de Prompt para usar no terminal:**
```text
Detalhes sobre o vídeo: Crie um vídeo dinâmico de 15 segundos para o lançamento do meu novo aplicativo de finanças. Use tons escuros e dourado. Aqui está o site para capturar telas: https://meusite.com. Use como referência de ritmo o estilo deste post: https://x.com
```

## 🛠️ Tecnologias Utilizadas pela IA nas Regras
- **HTML Canvas / WebGL Puro** (Sem frameworks pesados externos)
- **Playwright Headless** (Para capturar telas reais do produto e renderizar frames)
- **FFmpeg** (Para compilar os frames gerados em arquivos MP4 fluidos com H.264)
- **Grid de Batidas (BPM)** (Para travar a sincronização perfeita de áudio e vídeo)
