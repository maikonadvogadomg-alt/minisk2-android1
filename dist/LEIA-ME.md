# Mini SK — editor modular ao vivo

Abra o **index.html**: no computador, com dois cliques; no celular, pelo navegador ou hospedado de graça (GitHub Pages ou Netlify).
Ele não usa Replit nem servidor. Também não depende de nenhuma biblioteca de fora: são só HTML, CSS e JavaScript.

## O que tem

| Botão | Para quê |
|---|---|
| ☰ | Árvore de arquivos. Cria arquivo ou pasta (＋📄 ＋📁). Importa arquivos, uma pasta inteira ou um .zip (⤒). Baixa o projeto em .zip (⤓). |
| ⋯ ao lado de cada arquivo (ou segurar o dedo) | Abrir, ver no preview, renomear, duplicar, mover, baixar, copiar o caminho, **analisar com a IA** e apagar. |
| Preview (embaixo) | Mostra o resultado ao vivo enquanto você digita (⚡). Para mudar o tamanho, arraste a barrinha ou use ▁ ▔. O botão ▤ abre o console de erros. Funciona com CSS, JS, imagens, módulos (`import`) e `fetch('dados.json')`. |
| 🔍 Buscar | Procura em todos os arquivos e destaca o que achou em amarelo. Tocar num resultado abre o arquivo no ponto certo. Também troca tudo de uma vez. |
| 🤖 IA | Aceita chave do Groq, Gemini (a antiga `AIza…` e a nova `AQ.…`), OpenRouter, Claude, OpenAI, xAI e outras. Quando o código vem com o nome do arquivo, o botão **Aplicar** grava direto nele. Tem 🎤 ditado e 🔊 voz. |
| 📸 Voltar | Checkpoints, que são fotos do projeto inteiro. Antes de apagar, importar, trocar tudo ou aplicar código da IA, ele tira uma foto sozinho. Na lista, você pode voltar, ver o que mudou ou baixar o .zip. |
| 🐙 GitHub | Com o seu token: importa um repositório, envia (commit), cria um repositório novo e publica o site grátis (Pages). |
| 🧪 API | Testa o **servidor do projeto** rodando no seu PC (ex.: `http://localhost:8080`).<br>• **Procurar rotas:** lê o código e lista as rotas do servidor e as chamadas que a tela faz. Marca **"rota não achada"** quando a tela chama algo que o servidor não tem, que é o jeito de achar onde quebrou.<br>• **Enviar** (GET/POST/…) mostra o status, o tempo e a resposta.<br>• **Testar todas as GET** testa uma por uma (✅/❌).<br>• **🤖 Perguntar à IA** manda o resultado para a IA explicar. |
| 📦 APK | Gera um **APK de verdade**: o HTML vai **dentro** do app e funciona sem internet. Não é a "casca" TWA.<br>1. **Preparar arquivos** cria `apk.config.json`, a pasta `android/` e `.github/workflows/apk.yml`.<br>2. **Enviar e gerar** envia ao GitHub e manda montar.<br>3. O painel acompanha cada passo (✅ ❌ ⏳). Se der certo, mostra o botão de baixar; se der erro, mostra o motivo e o botão **🤖 Explicar com a IA**.<br>A chave de assinatura fica guardada, então o APK novo instala por cima do antigo. |
| 🧬 Raio-X | Lê **todos** os package.json, inclusive dos projetos da Replit com vários projetos dentro (monorepo).<br>• Explica cada dependência em português: para que serve, se é obrigatória ou só para montar, se é coisa da Replit.<br>• Gera o **plano completo** (baixar .md, copiar ou salvar), o package.json unificado e as pastas vazias em .bat.<br>• **📦 Pacote para a IA:** junta os arquivos importantes num .txt para mandar no chat.<br>• **⤵ Montar:** cola um texto com `===== ARQUIVO: caminho =====` e ele cria os arquivos. |
| 📱 PWA | **🎨 Ícone:** o seu Gerador de Ícones PRO, agora com a versão *maskable* (que o Android recorta sem cortar o desenho), SVG, favicon.ico e apple-touch-icon. Grava em `icons/` ou baixa em .zip.<br>**📲 Instalável:** escolha a página. Ele cria o que faltar (ícones, manifest e service worker com a lista de arquivos feita sozinha) e arruma o `<head>` sem duplicar nada.<br>**🧭 Hub:** acha todas as páginas .html do projeto, sem você digitar endereço, e **gera o index do Hub já montado**, com a lista gravada dentro. Instalou uma vez, está tudo lá, em qualquer celular. |
| 🗂 Projetos | Vários projetos: abrir um .zip como projeto novo, renomear e apagar. Também mostra o espaço usado e os atalhos. |

## Cérebro da IA (para ela não se perder)
Cada projeto tem uma pasta `.sk/` com dois arquivos:
- `.sk/diario.md` é o resumo do projeto: o objetivo, o que já funciona e o que falta. A IA lê esse arquivo em toda mensagem e o atualiza quando termina algo.
- `.sk/memoria.json` guarda a conversa daquele projeto.

O medidor de tokens mostra quanto está sendo enviado. Quando passa do limite escolhido, as mensagens antigas ficam de fora, mas o diário continua sendo enviado.

## Codificação e tipos
Ao importar, ele reconhece UTF-8, UTF-16 e Windows-1252 (o "Latin-1" de arquivos antigos do Windows), para os acentos não virem lixo. Arquivos binários, como imagens, PDF e APK, são guardados intactos. A barra de baixo do editor mostra o tipo do arquivo (HTML, JS, Java, JSON…), a codificação e o tamanho.

## Onde ficam os arquivos
Os projetos ficam **no navegador deste aparelho** (IndexedDB) e continuam lá quando você fecha.
Para não perder nada:
- baixe o .zip (⤓) de vez em quando, **ou**
- envie para o GitHub (🐙).

Limpar os dados do navegador apaga os projetos.

## Links entre páginas no preview
Se uma página tem link para outra do projeto (ex.: `<a href="peticao/index.html">`), clicar no preview abre essa outra página ali mesmo.

## Atalhos (no computador)
| Atalho | Faz |
|---|---|
| Ctrl+S | Salvar |
| Ctrl+B | Abrir ou fechar os arquivos |
| Ctrl+Shift+F | Buscar |
| Ctrl+J | IA |
| Ctrl+G | Ir para uma linha |
| Ctrl+Enter | Enviar para a IA |
| Alt+P | Aumentar ou diminuir o preview |

## Módulos (pasta `js/`)
Cada arquivo faz uma coisa. Eles conversam por eventos (`SK.on` / `SK.emit`), então dá para trocar um módulo sem quebrar os outros.

| Arquivo | Cuida de |
|---|---|
| 00-core.js | base, avisos, janelas, banco do navegador |
| 10-fs.js | arquivos, pastas, projetos, codificação, importar e exportar |
| 20-zip.js | ler e criar .zip (sem biblioteca) |
| 30-highlight.js | cores do código |
| 40-editor.js | editor e abas |
| 50-tree.js | árvore de arquivos |
| 60-preview.js | preview ao vivo e console |
| 70-search.js | buscar e trocar |
| 80-ai.js | IA, chaves, memória, tokens |
| 85-checkpoints.js | checkpoints |
| 90-github.js | GitHub |
| 95-pwa.js | ícones, instalar como app, Hub |
| 96-apk.js | APK Android pelo GitHub (projeto Android em Java + receita) |
| 97-analise.js | Raio-X: dependências, plano, pacote para IA, montar de texto |
| 98-api.js | Testar a API do projeto (rotas, chamadas, pedidos) |
| 99-app.js | junta tudo e monta a tela |

## Próximos passos planejados
- Entrar com o playground jurídico como um projeto.
- Painel do Supabase (login, banco e chaves guardadas com segurança).
