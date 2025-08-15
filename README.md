# meu-primeiro-site
index.html
<!DOCTYPE html>
<html lang="pt-br">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>Meu Primeiro Site</title>
  <!-- Liga o CSS (certifique-se de que o arquivo se chama styles.css) -->
  <link rel="stylesheet" href="styles.css" />
</head>
<body>
  <main class="container">

    <!-- MENU no topo -->
    <nav class="menu">
      <a href="index.html" class="ativo">Início</a>
      <a href="about.html">Sobre</a>
    </nav>

    <!-- BLOCO HERO (duas colunas: texto + imagem) -->
    <section class="hero">
      <div class="hero-imagem">
  <img class="img-responsiva" src="img/paisagem.jpg" alt="Paisagem com céu azul e montanhas ao fundo">
</div>

        <h1>Olá, mundo!</h1>
        <p>Meu primeiro site agora tem <strong>layout responsivo</strong> 🎯</p>
        <a class="btn" href="#">Clique aqui</a>
      </div>

      <div class="hero-imagem">
        <!-- Se você RENOMEOU a imagem para paisagem.jpg, troque a linha de baixo pelo comentário seguinte -->
        <img class="img-responsiva" src="img/thought-catalog-o0Qqw21-0NI-unsplash.jpg" alt="Paisagem com céu azul e montanhas ao fundo" />
        <!-- <img class="img-responsiva" src="img/paisagem.jpg" alt="Paisagem com céu azul e montanhas ao fundo" /> -->
      </div>
    </section>

    <!-- FORMULÁRIO (conectado ao Formspree) -->
    <h2>Fale comigo</h2>
    <form class="form-contato" id="contato"
          action="https://formspree.io/f/mjkozjbz" method="POST">

      <label for="nome">Nome:</label>
      <input type="text" id="nome" name="nome" placeholder="Digite seu nome" required />

      <label for="email">E-mail:</label>
      <input type="email" id="email" name="email" placeholder="Digite seu e-mail" required />

      <label for="mensagem">Mensagem:</label>
      <textarea id="mensagem" name="mensagem" rows="4" placeholder="Escreva sua mensagem..." required></textarea>

      <!-- Opcional: assunto do e-mail -->
      <input type="hidden" name="_subject" value="Nova mensagem do site" />

      <!-- Opcional: anti-spam (honeypot). Se for preenchido, o script ignora. -->
      <input type="text" name="empresa" autocomplete="off" tabindex="-1"
             style="position:absolute; left:-9999px; opacity:0; height:0; width:0;">

      <button type="submit" class="btn">Enviar</button>

      <!-- Caixinha para mostrar sucesso/erro -->
      <div id="status" aria-live="polite" class="alert" style="display:none;"></div>
    </form>

    <!-- Link externo em nova aba -->
    <p>
      Veja meu
      <a href="https://developer.mozilla.org/pt-BR/docs/Web/HTML" target="_blank" rel="noopener noreferrer">
        guia rápido de HTML
      </a>.
    </p>

  </main>

  <!-- Script: envia para o Formspree sem sair da página e mostra sucesso/erro -->
  <script>
    // Pega o formulário e a caixinha de status
    const form = document.getElementById("contato");
    const statusBox = document.getElementById("status");

    // Intercepta o envio para mandar via internet sem trocar de página
    form.addEventListener("submit", async (e) => {
      e.preventDefault(); // não recarregar a página
      const fd = new FormData(form);

      // Honeypot: se o campo escondido "empresa" vier preenchido, ignorar (possível bot)
      if (fd.get("empresa")) return;

      try {
        const res = await fetch(form.action, {
          method: "POST",
          body: fd,
          headers: { "Accept": "application/json" }
        });

        if (res.ok) {
          form.reset();
          mostrar("Mensagem enviada com sucesso! ✅", true);
        } else {
          mostrar("Não foi possível enviar. Tente novamente. ❌", false);
        }
      } catch (err) {
        mostrar("Erro de conexão. Verifique sua internet. ⚠️", false);
      }
    });

    function mostrar(msg, ok) {
      statusBox.textContent = msg;
      statusBox.className = "alert " + (ok ? "success" : "error");
      statusBox.style.display = "block";
      setTimeout(() => { statusBox.style.display = "none"; }, 5000);
    }
  </script>
</body>
</html>
