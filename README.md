<!doctype html>
<html lang="es">
<head>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Generador de Tipografías</title>

  <!-- Google Fonts -->
  <link href="https://fonts.googleapis.com/css2?family=Great+Vibes&family=Pinyon+Script&family=Poppins:wght@300;600&family=Playfair+Display:wght@400;700&family=Lobster&family=Dancing+Script&family=Pacifico&family=Sacramento&family=Kaushan+Script&family=Satisfy&family=Courgette&family=Cookie&family=Marck+Script&family=Parisienne&family=Alex+Brush&family=Allura&family=Italianno&family=Herr+Von+Muellerhoff&display=swap" rel="stylesheet">

  <style>
    /* Fuentes locales */
    @font-face {
      font-family: 'Last Christmas PERSONAL USE';
      src: url('fonts/LastChristmasPERSONALUSE-Regular.woff2') format('woff2');
    }
    @font-face {
      font-family: 'Baby Garland';
      src: url('fonts/BabyGarland.woff2') format('woff2');
    }

    /* Reset y base */
    * { box-sizing: border-box; margin: 0; padding: 0; }

    body { font-family: Poppins, sans-serif; padding: 20px; transition: background 0.3s, color 0.3s; }

    body.light { background: #f8fafc; color: #0f172a; }
    body.dark { background: #0f172a; color: #f8fafc; }

    h1 { text-align: center; margin-bottom: 5px; font-weight: 700; font-size: 2.5rem; transition: color 0.3s; }
    body.light h1 { color: #1e293b; }
    body.dark h1 { color: #facc15; }

    h2.subtitle { text-align: center; margin-bottom: 20px; font-weight: 400; font-size: 1rem; transition: color 0.3s; }
    body.light h2.subtitle { color: #0f172a; }
    body.dark h2.subtitle { color: #ffffff; }

    .wrap { max-width: 1000px; margin: 0 auto; }
    .controls { display: flex; flex-direction: column; gap: 15px; margin-bottom: 30px; }
    label { font-weight: 600; transition: color 0.3s; }
    body.light label { color: #1e293b; }
    body.dark label { color: #f8fafc; }

    input[type=text] { width: 100%; padding: 12px 15px; font-size: 1.1rem; border-radius: 10px; border: 1px solid #cbd5e1; transition: background 0.3s, color 0.3s; }
    body.light input[type=text] { background: #fff; color: #0f172a; }
    body.dark input[type=text] { background: #1e293b; color: #f8fafc; border: 1px solid #334155; }

    input[type=range] { width: 100%; }

    #font-list { display: grid; grid-template-columns: repeat(auto-fit, minmax(250px, 1fr)); gap: 20px; }

    .font-sample { padding: 20px; border-radius: 15px; text-align: center; transition: transform 0.2s, box-shadow 0.2s, background 0.3s; position: relative; }
    .font-sample:hover { transform: translateY(-5px); }

    body.light .font-sample { background: #fff; box-shadow: 0 6px 12px rgba(0,0,0,0.1), 0 0 10px gold; }
    body.dark .font-sample { background: #1e293b; box-shadow: 0 6px 12px rgba(0,0,0,0.5), 0 0 10px gold; }

    .font-name { font-weight: 700; font-size: 1.3rem; margin-bottom: 10px; position: relative; transition: color 0.3s; }
    .font-name::before, .font-name::after { content: '💎'; margin: 0 5px; }
    body.light .font-name { color: #1e293b; }
    body.dark .font-name { color: #facc15; }

    .sample-text { font-size: 2.5rem; word-break: break-word; margin-top: 10px; transition: color 0.3s; }
    body.light .sample-text { color: #1e293b; }
    body.dark .sample-text { color: #f8fafc; }

    @media (max-width: 600px) { .sample-text { font-size: 2rem; } }

    .toggle-btn { margin-bottom: 20px; padding: 10px 20px; font-size: 1rem; border-radius: 10px; cursor: pointer; border: none; font-weight: 600; transition: background 0.3s, color 0.3s; }
    body.light .toggle-btn { background: #1e293b; color: #f8fafc; }
    body.dark .toggle-btn { background: #facc15; color: #0f172a; }
  </style>
</head>
<body>
  <h1>Generador de Tipografías</h1>
  <h2 class="subtitle">Web Fabricado en Joyería Esmeralda</h2>

  <div class="wrap">
    <button class="toggle-btn" id="toggle-mode">Cambiar Modo</button>

    <div class="controls">
      <label for="text-input">Escribe aquí</label>
      <input id="text-input" type="text" placeholder="Ej. Braian Acuña" value="Braian Acuña">

      <label for="size-range">Tamaño</label>
      <input id="size-range" type="range" min="18" max="180" value="48">
    </div>

    <div id="font-list"></div>
  </div>

  <script>
    if(window.matchMedia && window.matchMedia('(prefers-color-scheme: dark)').matches){
      document.body.classList.add('dark');
    } else {
      document.body.classList.add('light');
    }

    const toggleBtn = document.getElementById('toggle-mode');
    toggleBtn.addEventListener('click', () => {
      document.body.classList.toggle('light');
      document.body.classList.toggle('dark');
    });

    const fonts = [
      {name: "Baby Garland", css: "'Baby Garland', cursive"},
      {name: "Last Christmas PERSONAL USE", css: "'Last Christmas PERSONAL USE', cursive"},
      {name: "Alex Brush", css: "'Alex Brush', cursive"},
      {name: "Allura", css: "Allura, cursive"},
      {name: "Italianno", css: "Italianno, cursive"},
      {name: "Herr Von Muellerhoff", css: "'Herr Von Muellerhoff', cursive"},
      {name: "Poppins", css: "Poppins, sans-serif"},
      {name: "Playfair Display", css: "Playfair Display, serif"},
      {name: "Lobster", css: "Lobster, cursive"},
      {name: "Great Vibes", css: "Great Vibes, cursive"},
      {name: "Pinyon Script", css: "Pinyon Script, cursive"},
      {name: "Dancing Script", css: "'Dancing Script', cursive"},
      {name: "Pacifico", css: "Pacifico, cursive"},
      {name: "Sacramento", css: "Sacramento, cursive"},
      {name: "Kaushan Script", css: "'Kaushan Script', cursive"},
      {name: "Satisfy", css: "Satisfy, cursive"},
      {name: "Courgette", css: "Courgette, cursive"},
      {name: "Cookie", css: "Cookie, cursive"},
      {name: "Marck Script", css: "'Marck Script', cursive"},
      {name: "Parisienne", css: "Parisienne, cursive"}
    ];

    const fontList = document.getElementById('font-list');
    const input = document.getElementById('text-input');
    const sizeRange = document.getElementById('size-range');

    fonts.forEach(font => {
      const container = document.createElement('div');
      container.className = 'font-sample';

      const title = document.createElement('div');
      title.className = 'font-name';
      title.textContent = font.name;
      title.style.fontFamily = font.css;

      const sample = document.createElement('div');
      sample.className = 'sample-text';
      sample.textContent = input.value;
      sample.style.fontFamily = font.css;
      sample.style.fontSize = sizeRange.value + 'px';

      container.appendChild(title);
      container.appendChild(sample);
      fontList.appendChild(container);

      font.sampleElement = sample;
    });

    function updateSamples() {
      const text = input.value || 'Escribe algo...';
      const size = sizeRange.value + 'px';
      fonts.forEach(font => {
        font.sampleElement.textContent = text;
        font.sampleElement.style.fontSize = size;
      });
    }

    input.addEventListener('input', updateSamples);
    sizeRange.addEventListener('input', updateSamples);
  </script>
</body>
</html>
