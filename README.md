# BRN Automação — Site Institucional

> Site institucional completo para a **BRN Automação**, empresa especializada em segurança eletrônica e instalações elétricas em São Paulo. Desenvolvido como uma **single-page application** em HTML/CSS/JS puro, sem dependências externas de framework.

---

## 📋 Sumário

- [Visão Geral](#visão-geral)
- [Funcionalidades](#funcionalidades)
- [Estrutura do Arquivo](#estrutura-do-arquivo)
- [Painel Administrativo](#painel-administrativo)
- [Personalização](#personalização)
- [Serviços Cobertos](#serviços-cobertos)
- [Tecnologias Utilizadas](#tecnologias-utilizadas)
- [Deploy](#deploy)

---

## Visão Geral

O site da BRN Automação é uma landing page institucional de página única (`index.html`) que apresenta os serviços da empresa, galeria de projetos, depoimentos de clientes, formulário de agendamento e informações de contato — tudo gerenciável via painel admin embutido, sem necessidade de backend.

---

## Funcionalidades

### Seções Públicas
| Seção | Descrição |
|---|---|
| **Hero** | Banner principal com chamada para ação e badge de status ativo |
| **Stats Bar** | Indicadores numéricos (anos de experiência, clientes, projetos etc.) |
| **Serviços** | Cards com os serviços oferecidos (ícone, título, descrição) |
| **Galeria** | Grid de fotos de projetos com lightbox e legenda |
| **Quem Somos** | Apresentação da empresa com foto da equipe e diferenciais |
| **Depoimentos** | Cards de avaliações de clientes com estrelas |
| **Agendamento** | Formulário + mini calendário interativo para solicitar visita |
| **Contato** | Telefone, endereço e botão de WhatsApp |
| **Rodapé** | Logo, links rápidos e redes sociais |

### Recursos de UX
- **Loading screen** animado com logo
- **Navegação sticky** com scroll indicator e link ativo automático
- **Animações de entrada** (fade-up) com Intersection Observer
- **Botão "Voltar ao topo"** que aparece após rolagem
- **Lightbox** nativo para ampliação de fotos da galeria
- **Calendário mini** interativo para agendamento
- **Design responsivo** para mobile e desktop

---

## Estrutura do Arquivo

O site é um único arquivo `index.html` auto-contido:

```
index.html
├── <head>
│   ├── Meta tags (SEO, Open Graph)
│   ├── Google Fonts (Plus Jakarta Sans + Instrument Serif)
│   └── <style> — todo o CSS inline (~700 linhas)
│
└── <body>
    ├── .page-loading        ← Tela de carregamento
    ├── <nav>                ← Navegação sticky
    ├── .hero                ← Banner principal
    ├── .stats-bar           ← Barra de estatísticas
    ├── #servicos            ← Grid de serviços
    ├── #galeria             ← Galeria de fotos + lightbox
    ├── #quem-somos          ← Sobre a empresa
    ├── #avaliacoes          ← Depoimentos
    ├── #agendar             ← Formulário de agendamento
    ├── #contato             ← Informações de contato
    ├── <footer>             ← Rodapé
    ├── .admin-overlay       ← Painel administrativo (oculto)
    └── <script>             ← Toda a lógica JS inline (~600 linhas)
```

---

## Painel Administrativo

O site possui um **painel admin embutido** acessível via atalho de teclado ou área clicável discreta.

### Acesso
- Senha padrão: definida na constante `ADMIN_PWD_DEFAULT` no script
- A senha é armazenada no `localStorage` do navegador após a primeira alteração

### O que pode ser editado via admin

| Aba | Campos editáveis |
|---|---|
| **Geral** | Hero (título, subtítulo, badge), estatísticas, contato (telefone, endereço) |
| **Serviços** | Nome, emoji/ícone, descrição de cada card; foto do serviço (upload base64) |
| **Galeria** | Upload de fotos (base64, máx. 2MB cada), legenda por foto, exclusão |
| **Quem Somos** | Título, textos, badge de destaque, foto da equipe, até 4 diferenciais (ícone + título + subtítulo) |
| **Avaliações** | Texto, nome do cliente e número de estrelas de cada depoimento |
| **Agendamento** | Dias da semana disponíveis (toggle on/off) e horários por dia |
| **Logo** | Upload de imagem personalizada (substitui o SVG padrão em toda a página) |
| **Senha** | Alteração da senha do painel admin |

### Persistência de Dados
Todos os dados são salvos no **`localStorage`** do navegador. Isso significa:
- ✅ Sem servidor ou banco de dados necessário
- ⚠️ Os dados ficam apenas no navegador onde foram salvos
- ⚠️ Limpar o cache/dados do site apaga as configurações

> **Para ambiente de produção com múltiplos dispositivos**, recomenda-se integrar uma solução de persistência como Firebase Realtime Database ou um endpoint de API simples.

---

## Personalização

### Cores (CSS Variables)
Edite as variáveis no bloco `:root` no início do `<style>`:

```css
:root {
  --blue-900: #071d36;  /* Fundo hero, textos principais */
  --blue-800: #0d2d5e;  /* Títulos */
  --blue-600: #185fa5;  /* Cor primária (botões, destaques) */
  --blue-500: #2272c3;  /* Links, foco */
  --red-600:  #c0303f;  /* Ações de exclusão */
}
```

### Dados Iniciais (siteData)
Os conteúdos padrão estão no objeto `siteData` no `<script>`. Edite os valores diretamente para alterar os textos que aparecem antes de qualquer edição via admin:

```javascript
const siteData = {
  hero: { titulo: "...", subtítulo: "...", badge: "..." },
  stats: [...],
  servicos: [...],
  galeria: [...],
  quemsomos: { ... },
  avaliacoes: [...],
  agendamento: { dias: {...}, horarios: {...} },
  contato: { telefone: "...", endereco: "..." }
};
```

### Logo
- **Padrão**: SVG inline com texto "brn / AUTOMAÇÃO"
- **Personalizado**: Upload via painel admin (PNG/JPG, máx. 2MB)
- O logo é aplicado automaticamente no nav, footer e loading screen

---

## Serviços Cobertos

A BRN Automação oferece os seguintes serviços, configuráveis pelo painel admin:

- 📷 **CFTV** — Câmeras de segurança e monitoramento
- 🚨 **Alarme** — Sistemas de alarme residencial e comercial
- ⚡ **Cerca Elétrica** — Instalação e manutenção de cercas elétricas
- 🔌 **Instalação Elétrica** — Elétrica residencial e comercial
- 🌐 **Cabeamento Estruturado** — Redes de dados e telefonia
- 🔒 **Controle de Acesso** — Fechaduras, catracas e porteiros

---

## Tecnologias Utilizadas

| Tecnologia | Uso |
|---|---|
| HTML5 semântico | Estrutura da página |
| CSS3 (variáveis, grid, flexbox, animações) | Estilo e layout |
| JavaScript ES6+ (vanilla) | Interatividade e lógica do admin |
| Google Fonts | Tipografia (Plus Jakarta Sans + Instrument Serif) |
| localStorage API | Persistência dos dados do admin |
| Intersection Observer API | Animações de entrada ao rolar |
| FileReader API | Upload de imagens no admin |

**Zero dependências externas de JavaScript** — não utiliza jQuery, React, Vue ou qualquer framework.

---

## Deploy

Por ser um único arquivo estático, o site pode ser hospedado em qualquer plataforma:

```bash
# GitHub Pages
# Basta fazer o commit do index.html na branch main/gh-pages

# Netlify / Vercel
# Faça upload direto do arquivo ou conecte o repositório

# Servidor tradicional (Apache/Nginx)
# Coloque o index.html na pasta pública (public_html / www)
```

### Recomendações para Produção
1. Adicionar arquivo `robots.txt` e sitemap XML
2. Configurar HTTPS (obrigatório para Google ranking)
3. Adicionar Google Analytics ou similar para métricas
4. Considerar CDN para as fontes do Google Fonts se houver restrição de privacidade
5. Para persistência de dados multi-dispositivo, integrar backend (Firebase, Supabase, etc.)

---

## Licença

Desenvolvido para uso exclusivo da **BRN Automação**. Todos os direitos reservados.
