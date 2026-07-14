# SMAX Toolkit - TJSP

Conjunto de ferramentas de automação e aprimoramento de interface para o sistema SMAX do Tribunal de Justiça de São Paulo.

**Versão atual:** 2.91

---

## Scripts disponíveis

| Script | Descrição |
|--------|-----------|
| `SMAX Toolkit - TJSP.user.js` | Triagem, respostas em lote, scripts de solução e discussão, consulta eProc e mais |

---

## 1. Pré-requisito: instalar o Tampermonkey

1. Instale a extensão **Tampermonkey** na loja do seu navegador (Chrome, Edge ou Firefox)
2. Vá em **Gerenciar Extensões** e ative o **Modo do desenvolvedor**
3. No Tampermonkey → **Painel de Controle** → **Configurações**, marque:
   - Permitir scripts de usuário
   - Permitir acesso a abas
   - Permitir requisições remotas

---

## 2. Instalação

Clique no link abaixo para instalar diretamente pelo Tampermonkey:

**[Instalar SMAX Toolkit - TJSP](https://github.com/rsalvessap/SMAX-TOOLS/raw/refs/heads/master/SMAX/SMAX%20Toolkit%20-%20TJSP.user.js)**

> O Tampermonkey abrirá uma aba de confirmação. Clique em **Instalar**.

Um único script cobre tanto o SMAX quanto o eProc — não é necessário instalar nada separado.

---

## 3. Configuração inicial

Ao abrir o SMAX na tela de chamados, uma **engrenagem** aparecerá no canto inferior direito. Clique nela para abrir o painel de configurações.

### 3.1 Identificação

No campo **"Quem é você?"** (aba Geral), busque e selecione seu próprio nome. Isso vincula suas ações ao seu usuário.

### 3.2 Equipes e roteamento

Na aba **Equipes**:

1. Clique em **+ Nova Equipe** para criar uma equipe (ex: JEC)
2. Defina as regras de roteamento:
   - **GSE:** grupos de suporte que pertencem a esta equipe
   - **Local de Divulgação:** termos regex que identificam chamados da equipe
3. Adicione os membros da equipe:
   - Use a busca para encontrar atendentes
   - Configure os **Dígitos Finais** de cada um (ex: `00-05, 10-15`)
   - Marque **Ausente** para quem não deve receber chamados
4. Configure a **assinatura da equipe** (HTML que será inserido nas respostas)

> A equipe **GERAL** é padrão e captura tudo que não se enquadrar nas regras específicas.

### 3.3 Escritas reais

Por padrão as escritas reais estão **ativadas**. Para testar sem gravar no SMAX, desative na aba Geral.

---

## 4. Módulos

### 4.1 HUD de Triagem

Acesse via **Configurações → Triagem → Abrir Triagem**.

Painel de tela inteira para triagem rápida de chamados:

- **Filtro por dígitos finais** — processa apenas chamados cujo ID termine nos dígitos configurados
- **Seletor de GSE** — alterna entre filas de atendimento
- **Navegação** — setas `< >` para avançar entre chamados
- **Classificação de urgência** — Baixa / Média / Alta / Crítica (define urgência e calcula responsável automaticamente)
- **Editor de resposta** — editor rico com formatação completa (negrito, itálico, listas, links, cores, tamanhos)
- **Seletor de assinaturas** — insere assinatura da equipe ou pessoal
- **Vinculação a Mudança Global** — campo para informar o ID da mudança global
- **Discussões** — exibe todas as discussões do chamado no painel lateral
- **Números de processo CNJ** — detectados e linkificados automaticamente na descrição

### 4.2 HUD de Respostas (ResponseHUD)

Acesse via **Configurações → Respostas → Abrir ResponseHUD**.

Painel completo para atendimento e respostas em lote:

#### Painel esquerdo — Filtros e lista

- **Filtro por equipes** — pills com indicador azul (GSE na API) ou amarelo (regex local)
- **Filtro por Status Operacional** — pills gerados automaticamente a partir dos chamados carregados
- **Filtro por Status** — Em Andamento, Pronto, Pendente, etc.
- **Filtro por Especialista** — mostra apenas chamados de um atendente específico
- **Filtro de texto** — busca em tempo real por descrição, solicitante ou localização
- **Presets salvos** — salve combinações de filtros para reutilizar. Preset fixo "Rejeitados" sempre disponível
- **Ordenação** — por ID, data, status ou especialista (ascendente/descendente)
- **Busca por número** — localiza qualquer chamado pelo ID, mesmo fora dos filtros
- **Seleção em lote** — checkbox "Selecionar todos" para operações em massa
- **Scroll virtual** — renderiza apenas itens visíveis (suporta listas grandes)

#### Painel direito — Detalhe e ações

**Cabeçalho:**
- ID do chamado (link para o SMAX), badges VIP e Global, solicitante, localização, número do processo CNJ, data de criação

**Barra de ações (chips):**

| Chip | Função |
|------|--------|
| GSE | Alterar grupo de suporte. Opção "Com encaminhamento" posta discussão interna com texto configurável |
| Especialista | Designar atendente. Busca por nome |
| Status | Alterar status do chamado (16 opções) |
| Status Operacional | Alterar situação operacional (35+ opções TJSP) |
| Seguidor | Adicionar/remover seguidores do chamado |
| Seguir | Adicionar a si mesmo como seguidor |
| Recebimento | Postar discussão pública para o solicitante (texto editável nas configurações) |
| Escalar | Transição do chamado de Validação para Atendimento |

**Editor de solução:**
- Editor rico completo: negrito, itálico, sublinhado, tachado, listas, links, cores, tamanhos de fonte, limpeza de formatação
- Seletor de assinaturas (equipe e pessoais)
- Seletor de scripts de solução (locais + compartilhados)
- Código de finalização: Atendido Offline, Suporte ao Vivo, Incidente Resolvido

**Painel de discussões:**
- Lista de todas as discussões do chamado com badges de privacidade (PUBLIC/INTERNAL)
- Botão "Replicar" copia conteúdo para o editor de solução
- Modal de expansão com navegação entre discussões
- **Nova discussão:** editor próprio com seletor de destinatário (Agente/Usuário/Fornecedor) e objetivo (Atualização/Acompanhamento/Resolução/etc.)
- Seletor de scripts de discussão com preenchimento automático de destinatário e objetivo

**Anexos:**
- Chips de anexos do chamado. Imagens abrem em modal com navegação por teclado. PDFs abrem em nova aba.

**Envio (ENVIAR):**
- Chamado único: executa diretamente
- Lote: exibe painel de confirmação com tabela detalhada por chamado
- Grava: solução, GSE, especialista, status, status operacional, escalação, encaminhamento, recebimento, seguidores

### 4.3 Scripts/Templates

Acesse via **Configurações → Scripts**.

- **Duas abas:** Solução e Discussão
- Crie, edite e exclua scripts localmente
- Scripts de discussão aceitam campos opcionais: "Para" e "Objetivo"
- **Sincronização:** importa scripts do Gerenciador de Chamados (Supabase) ou do SharedConfig (GitHub)
- **Exportar/Importar:** backup e restauração em JSON
- Scripts compartilhados aparecem com badge "Compartilhado" e não podem ser editados localmente

### 4.4 Assinaturas

Acesse via **Configurações → Assinaturas**.

- **Assinaturas pessoais:** criar/editar/excluir com pré-visualização em tempo real
- **Assinaturas por equipe:** configuradas na aba Equipes (uma por equipe)
- Inseridas no editor via botão ✒️ (disponível tanto no HUD de Triagem quanto no ResponseHUD)

### 4.5 Destaque de Solicitantes

Acesse via **Configurações → Destaque**.

- Busca qualquer pessoa no SMAX (não limitado a membros de equipe)
- Adicione solicitantes à lista de destaque para identificá-los rapidamente

### 4.6 Relatório de Atividades

Acesse via **ResponseHUD → botão 📊** ou **Configurações → Triagem/Respostas**.

- Gera relatório por período (data início/fim)
- Resumo: chamados respondidos, vinculados, transferidos, designados, alterações de status
- Tabela detalhada com cada ação realizada
- Exportação em CSV
- Sincronização automática com Supabase

### 4.7 Consulta de Processos no eProc

Números de processo no formato CNJ são detectados automaticamente em descrições e discussões.

**Formatos reconhecidos:**
- Formatado: `4000439-14.2026.8.26.0201`
- Bruto (20 dígitos): `40004391420268260201`

Clique no número → nova aba do eProc abre já com a pesquisa executada (requer eProc aberto e logado).

### 4.8 Mensagem de Recebimento

Acesse a configuração via **Configurações → Geral → Mensagem de Recebimento**.

- Texto editável pelo usuário (sem necessidade de HTML)
- Cada linha do texto vira um parágrafo no envio
- Enviado como discussão pública para o solicitante
- Funciona em lote (mesmo texto para todos os chamados selecionados)
- Ativado pelo botão **📨 Recebimento** no ResponseHUD

---

## 5. Temas

Três temas disponíveis, alternados pelo botão no canto superior do HUD:

| Tema | Descrição |
|------|-----------|
| Light | Fundo claro, texto escuro |
| Dark | Fundo escuro, texto claro |
| Gray | Tons neutros com acentos dourados |

A preferência é salva e persiste entre sessões.

---

## 6. Configuração compartilhada (SharedConfig)

Na aba **Geral**, configure a **URL do SharedConfig** para sincronizar automaticamente:
- Equipes e regras de roteamento
- Scripts de solução e discussão
- Configurações de grupos e ausências

O JSON é hospedado no GitHub e atualizado via botão "Publicar para a equipe" (requer token GitHub).

---

## 7. Atalhos de teclado

| Tecla | Ação |
|-------|------|
| ESC | Fecha o painel ativo (Triagem ou Respostas) |
| ← → | Navega entre imagens no visualizador de anexos |
| Enter | No campo de busca por número, executa a pesquisa |

---

## 8. Dicas

- Mantenha o cadastro de ausências atualizado — chamados são redistribuídos automaticamente
- Se um chamado cair na equipe errada, revise as regras de GSE e Local de Divulgação
- O script atualiza automaticamente pelo Tampermonkey quando há nova versão no repositório
- Use o preset "Rejeitados" no ResponseHUD para localizar rapidamente chamados devolvidos
- O botão "Escalar" recoloca chamados rejeitados na fila de atendimento
