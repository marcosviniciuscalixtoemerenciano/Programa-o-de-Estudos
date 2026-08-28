# 📚 StudyFlow - Cronograma de Estudos Interativo

O **StudyFlow** é uma aplicação web simples e dinâmica desenvolvida para ajudar estudantes a organizarem sua rotina de aprendizado com foco, disciplina e equilíbrio. 

A ferramenta permite personalizar todo o plano de estudos em tempo real através de um painel de edição integrado.

---

## 🚀 Funcionalidades

- **Personalização em Tempo Real:** Edite títulos, links de imagem, dias da semana e matérias diretamente pela interface.
- **Formatação Automática de Listas:** Converte automaticamente linhas com `:` em itens destacados (ex: `Segunda: Matemática` vira **Segunda:** Matemática).
- **Design Responsivo:** Adaptado para navegação em computadores, tablets e dispositivos móveis.
- **Interface Moderna:** Layout limpo em tons de azul, focado na usabilidade e legibilidade.

---

## 🛠️ Tecnologias Utilizadas

- **HTML5:** Estruturação semântica do conteúdo.
- **CSS3:** Estilização, variáveis CSS, Flexbox, CSS Grid e responsividade.
- **JavaScript (ES6+):** Manipulação do DOM e lógica de atualização dinâmica da página.

---

## 📦 Como Executar o Projeto

Como o projeto utiliza apenas tecnologias front-end padrão, não é necessário instalar dependências.

1. Clone este repositório ou baixe o arquivo `.html`.
2. Abra o arquivo `index.html` em qualquer navegador web.

---

## 📌 Próximos Passos (Melhorias Futuras)

- [ ] Implementar `localStorage` para salvar as alterações do usuário no navegador.
- [ ] Adicionar suporte a Modo Escuro (Dark Mode).
- [ ] Permitir exportação do cronograma em formato PDF.




<!DOCTYPE html>
<html lang="pt-BR">
  <head>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Lista de estudo diário</title>
    <style>
      :root {
        --bg: #f3f7ff;
        --panel: #ffffff;
        --primary: #2f6fed;
        --primary-dark: #214bb3;
        --secondary: #dfe9ff;
        --text: #20314d;
        --muted: #5b6d87;
        --border: #dfe7f3;
      }

      * {
        box-sizing: border-box;
      }

      body {
        margin: 0;
        font-family: Arial, sans-serif;
        background: linear-gradient(180deg, #eef4ff 0%, #f9fbff 100%);
        color: var(--text);
      }

      .container {
        max-width: 1200px;
        margin: 0 auto;
        padding: 24px;
      }

      .site-header {
        background: rgba(255, 255, 255, 0.9);
        border: 1px solid var(--border);
        border-radius: 16px;
        padding: 18px 22px;
        box-shadow: 0 10px 25px rgba(46, 85, 170, 0.08);
        display: flex;
        justify-content: space-between;
        align-items: center;
        margin-bottom: 24px;
      }

      .brand {
        font-size: 1.5rem;
        font-weight: bold;
        color: var(--primary-dark);
      }

      .nav {
        display: flex;
        gap: 18px;
        flex-wrap: wrap;
      }

      .nav a {
        text-decoration: none;
        color: var(--text);
        font-weight: 600;
      }

      .hero {
        background: var(--panel);
        border: 1px solid var(--border);
        border-radius: 22px;
        padding: 28px;
        margin-bottom: 24px;
        display: grid;
        grid-template-columns: 1.2fr 1fr;
        gap: 24px;
        align-items: center;
        box-shadow: 0 12px 28px rgba(42, 86, 174, 0.08);
      }

      .hero-copy h1 {
        margin: 0 0 12px;
        font-size: clamp(2rem, 4vw, 3rem);
        color: var(--primary-dark);
      }

      .hero-copy p {
        margin: 0;
        color: var(--muted);
        font-size: 1.05rem;
        line-height: 1.6;
      }

      .hero-image img {
        width: 100%;
        max-height: 350px;
        object-fit: cover;
        border-radius: 18px;
        display: block;
      }

      .editor {
        background: var(--panel);
        border: 1px solid var(--border);
        border-radius: 18px;
        padding: 20px;
        margin-bottom: 28px;
        box-shadow: 0 10px 20px rgba(28, 53, 108, 0.05);
      }

      .editor h3 {
        margin: 0 0 16px;
        color: var(--primary-dark);
        font-size: 1.3rem;
      }

      form {
        display: grid;
        grid-template-columns: repeat(auto-fit, minmax(240px, 1fr));
        gap: 15px;
      }

      label {
        display: flex;
        flex-direction: column;
        font-weight: bold;
        color: var(--text);
        gap: 6px;
      }

      input, textarea, button {
        font: inherit;
        padding: 10px 12px;
        border-radius: 10px;
        border: 1px solid #cbd8ee;
        background: #f9fbff;
      }

      textarea {
        min-height: 120px;
        resize: vertical;
        grid-column: 1 / -1;
      }

      button {
        background: var(--primary);
        color: white;
        border: none;
        cursor: pointer;
        font-weight: bold;
        transition: 0.2s ease;
        box-shadow: 0 8px 18px rgba(47, 111, 237, 0.2);
      }

      button:hover {
        background: var(--primary-dark);
      }

      .content {
        background: var(--panel);
        border: 1px solid var(--border);
        border-radius: 20px;
        padding: 20px;
        box-shadow: 0 10px 22px rgba(40, 74, 140, 0.06);
      }

      .content h2 {
        text-align: center;
        color: var(--primary-dark);
        margin: 0 0 18px;
      }

      table {
        width: 100%;
        max-width: 900px;
        margin: 0 auto;
        border-collapse: collapse;
        background: #fff;
        border-radius: 12px;
        overflow: hidden;
      }

      th, td {
        border: 1px solid var(--border);
        padding: 14px 16px;
        text-align: left;
      }

      th {
        background: var(--secondary);
        color: var(--primary-dark);
      }

      ul {
        margin: 0;
        padding-left: 18px;
        line-height: 1.7;
      }

      @media (max-width: 760px) {
        .site-header {
          flex-direction: column;
          gap: 12px;
          text-align: center;
        }

        .hero {
          grid-template-columns: 1fr;
        }
      }
    </style>
  </head>
  <body>
    <div class="container">
      <header class="site-header">
        <div class="brand">StudyFlow</div>
        <nav class="nav">
          <a href="#">Início</a>
          <a href="#">Cronograma</a>
          <a href="#">Matérias</a>
          <a href="#">Metas</a>
        </nav>
      </header>

      <section class="hero">
        <div class="hero-copy">
          <h1 id="tituloPagina">Programação de estudo</h1>
          <p>
            Organize sua rotina de aprendizado com foco, disciplina e equilíbrio.
            Este cronograma ajuda a dividir o tempo entre teoria, prática e revisão.
          </p>
        </div>

        <div class="hero-image">
          <img id="imagemPagina" src="https://images.unsplash.com/photo-1522202176988-66273c2fd55f?auto=format&fit=crop&w=1200&q=80" alt="Estudos">
        </div>
      </section>

      <div class="editor">
        <h3>Editar informações</h3>
        <form id="formEdicao">
          <label>
            Título
            <input id="tituloInput" type="text" value="Programação de estudo">
          </label>

          <label>
            Imagem
            <input id="imagemInput" type="url" value="https://images.unsplash.com/photo-1522202176988-66273c2fd55f?auto=format&fit=crop&w=1200&q=80">
          </label>

          <label>
            Texto do cabeçalho
            <input id="cabecalhoInput" type="text" value="Cronograma de estudo">
          </label>

          <label>
            Dias da semana
            <input id="diasInput" type="text" value="Segunda a Sexta-feira">
          </label>

          <textarea id="rotinaInput">1. Teoria (45 min): Foque na matéria do dia (videoaula ou leitura).&#10;2. Intervalo (15 min): Descanse a mente e tome água.&#10;3. Prática (45 min): Resolva questões do assunto estudado.&#10;4. Correção (20 min): Analise os erros e anote os pontos principais.</textarea>

          <textarea id="materiasInput">Segunda: Matemática&#10;Terça: Português e Redação&#10;Quarta: História e Geografia&#10;Quinta: Física e Química&#10;Sexta: Biologia, Filosofia e Sociologia</textarea>

          <textarea id="fimSemanaInput">Sábado: Revisão geral das anotações (1h) + Simulado de questões mistas (1h).&#10;Domingo: Descanso total e 15 minutos à noite para organizar a semana seguinte.</textarea>

          <button type="submit">Atualizar informações</button>
        </form>
      </div>

      <main class="content">
        <h2 id="tituloPaginaSecundario">Cronograma de estudo</h2>

        <table>
          <tr>
            <th colspan="2"><strong id="cabecalhoPagina">Cronograma de estudo</strong></th>
          </tr>

          <tr>
            <th colspan="2" id="diasPagina">Segunda a Sexta-feira</th>
          </tr>

          <tr>
            <td colspan="2">
              <ul id="rotinaPagina">
                <li><strong>1. Teoria (45 min):</strong> Foque na matéria do dia (videoaula ou leitura).</li>
                <li><strong>2. Intervalo (15 min):</strong> Descanse a mente e tome água.</li>
                <li><strong>3. Prática (45 min):</strong> Resolva questões do assunto estudado.</li>
                <li><strong>4. Correção (20 min):</strong> Analise os erros e anote os pontos principais.</li>
              </ul>
            </td>
          </tr>

          <tr>
            <th colspan="2">Distribuição das matérias</th>
          </tr>

          <tr>
            <td colspan="2">
              <ul id="materiasPagina">
                <li><strong>Segunda:</strong> Matemática</li>
                <li><strong>Terça:</strong> Português e Redação</li>
                <li><strong>Quarta:</strong> História e Geografia</li>
                <li><strong>Quinta:</strong> Física e Química</li>
                <li><strong>Sexta:</strong> Biologia, Filosofia e Sociologia</li>
              </ul>
            </td>
          </tr>

          <tr>
            <th colspan="2">Fim de semana</th>
          </tr>

          <tr>
            <td colspan="2">
              <ul id="fimSemanaPagina">
                <li><strong>Sábado:</strong> Revisão geral das anotações (1h) + Simulado de questões mistas (1h).</li>
                <li><strong>Domingo:</strong> Descanso total e 15 minutos à noite para organizar a semana seguinte.</li>
              </ul>
            </td>
          </tr>
        </table>
      </main>
    </div>

    <script>
      const formEdicao = document.getElementById('formEdicao');
      const tituloPagina = document.getElementById('tituloPagina');
      const tituloPaginaSecundario = document.getElementById('tituloPaginaSecundario');
      const imagemPagina = document.getElementById('imagemPagina');
      const cabecalhoPagina = document.getElementById('cabecalhoPagina');
      const diasPagina = document.getElementById('diasPagina');
      const rotinaPagina = document.getElementById('rotinaPagina');
      const materiasPagina = document.getElementById('materiasPagina');
      const fimSemanaPagina = document.getElementById('fimSemanaPagina');

      function converterLista(texto) {
        return texto
          .split('\n')
          .map(item => item.trim())
          .filter(item => item !== '')
          .map(item => {
            const [titulo, ...resto] = item.split(':');
            if (resto.length > 0) {
              return `<li><strong>${titulo}:</strong> ${resto.join(':').trim()}</li>`;
            }
            return `<li>${item}</li>`;
          })
          .join('');
      }

      function atualizarPagina(event) {
        event.preventDefault();

        const novoTitulo = document.getElementById('tituloInput').value || 'Programação de estudo';
        tituloPagina.textContent = novoTitulo;
        tituloPaginaSecundario.textContent = novoTitulo;

        const imagem = document.getElementById('imagemInput').value;
        if (imagem) {
          imagemPagina.src = imagem;
          imagemPagina.alt = 'Imagem de estudo';
        }

        const novoCabecalho = document.getElementById('cabecalhoInput').value || 'Cronograma de estudo';
        cabecalhoPagina.textContent = novoCabecalho;
        tituloPaginaSecundario.textContent = novoCabecalho;

        diasPagina.textContent = document.getElementById('diasInput').value || 'Segunda a Sexta-feira';
        rotinaPagina.innerHTML = converterLista(document.getElementById('rotinaInput').value);
        materiasPagina.innerHTML = converterLista(document.getElementById('materiasInput').value);
        fimSemanaPagina.innerHTML = converterLista(document.getElementById('fimSemanaInput').value);
      }

      formEdicao.addEventListener('submit', atualizarPagina);
    </script>
  </body>
</html>

