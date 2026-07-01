# Núcleo

Uma plataforma de IA **100% gratuita e de código aberto** para ler arquivos, responder perguntas com apoio de busca na web, e crescer com contribuições de qualquer pessoa — no mesmo espírito do Linux: nasce pequena, funcional, e aberta para o mundo construir em cima.

## O que já funciona nesta versão (MVP)

- Cadastro e login de usuários (o primeiro usuário criado vira admin automaticamente).
- Upload e leitura de arquivos: `.txt`, `.pdf` (imagens são aceitas mas ainda não analisadas visualmente — veja "Próximos passos").
- Pergunta livre + leitura do arquivo enviado, respondida por um modelo de IA **rodando localmente e de graça** via [Ollama](https://ollama.com).
- Busca automática na web (DuckDuckGo, gratuito, sem chave de API) para complementar a resposta com informação atual.
- Histórico de análises por usuário.
- Criação de "objetos" (projetos/agentes/bases de conhecimento) — base para o sistema multiusuário crescer.
- Painel para admins listarem usuários.

Tudo isso roda **sem nenhuma chave de API paga**.

## Como rodar na sua máquina

### 1. Pré-requisitos
- [Node.js](https://nodejs.org) 18 ou superior.
- [Ollama](https://ollama.com) instalado (gratuito, open source) — é o que dá "vida" às respostas de IA.

### 2. Instalar o Ollama e baixar um modelo aberto
```bash
# depois de instalar o Ollama:
ollama pull llama3
ollama serve
```
Isso deixa um servidor de IA rodando em `http://localhost:11434`, de graça, no seu computador.

### 3. Instalar e rodar o Núcleo
```bash
npm install
node server.js
```
Acesse `http://localhost:3000` no navegador.

### 4. Primeiro acesso
Crie sua conta na tela "Criar conta" — o primeiro cadastro vira automaticamente **admin**.

## Arquitetura (para quem for contribuir)

```
server.js     → rotas da API (auth, upload, análise, histórico, objetos)
ai.js         → integração com Ollama (IA local) e busca web (DuckDuckGo)
db.js         → armazenamento simples em JSON (trocar por Postgres/SQLite quando escalar)
public/       → frontend (uma página, sem framework, fácil de mexer)
```

Propositalmente simples: sem build step, sem framework pesado, para que qualquer pessoa consiga ler o código em minutos e propor mudanças.

## Próximos passos (contribuições bem-vindas)

- [ ] Análise de imagem real com modelo multimodal (ex.: LLaVA via Ollama).
- [ ] Leitura e resumo de vídeo (extração de frames + transcrição via Whisper, ambos open source).
- [ ] Geração de imagens com modelos abertos (Stable Diffusion via ComfyUI/Automatic1111).
- [ ] Suporte a MCP (Model Context Protocol) para plugar novas ferramentas de forma padronizada.
- [ ] Integração com redes sociais via APIs oficiais (o usuário conecta a própria conta via OAuth — não há acesso a perfis de terceiros sem autorização).
- [ ] Trocar `db.json` por PostgreSQL para uso em produção com mais usuários.
- [ ] Permissões mais finas por objeto (compartilhar um projeto com outro usuário).

## Por que gratuito e aberto

A ideia não é competir com plataformas de IA fechadas — é entregar uma base honesta, funcional e sem custo, que qualquer pessoa pode rodar no próprio computador ou servidor, entender de ponta a ponta, e modificar sem pedir permissão a ninguém. Cresce se for útil; e é útil porque é simples o suficiente para alguém entrar e mexer.

## Licença

MIT — use, modifique e redistribua livremente. Veja [LICENSE](./LICENSE).
