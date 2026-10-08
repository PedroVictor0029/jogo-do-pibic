# jogo-do-pibic

[index-atualizado.html](https://github.com/user-attachments/files/33215153/index-atualizado.html)

<!doctype html>
<html lang="pt-BR">
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width, initial-scale=1, maximum-scale=1, user-scalable=no">
<title>Plantão Pixel — Hospital da Vila</title>
<style>
  * { box-sizing: border-box; }
  body {
    margin: 0; min-height: 100vh; padding: 14px;
    display: grid; place-items: center;
    color: #fff4d6; background: #11172d;
    font: 14px ui-monospace, Consolas, monospace;
  }
  main { width: min(100%, 980px); text-align: center; }
  h1 { color: #adf1ff; letter-spacing: 3px; text-shadow: 3px 3px #394f92; }
  #frame {
    position: relative; overflow: hidden;
    border: 6px solid #f7dfad; border-radius: 7px;
    background: #83cbbb; box-shadow: 0 0 0 5px #39405e;
  }
  canvas {
    display: block; width: 100%; height: auto;
    image-rendering: pixelated; touch-action: none;
  }
  .overlay {
    position: absolute; inset: 0; display: grid; place-items: center;
    padding: 16px; background: #11172ddd;
  }
  .card {
    max-width: 460px; max-height: calc(100% - 8px); overflow-y: auto; padding: 20px; text-align: left;
    line-height: 1.6; background: #202747; border: 3px solid #f7dfad;
    box-shadow: 6px 6px #10142a;
  }
  .card h2 { color: #a7f2e1; margin-top: 0; }
  #dialog {
    position: absolute; display: none; inset: auto 4% 4%;
    min-height: 100px; padding: 12px; text-align: left;
    line-height: 1.5; background: #171c35f5; border: 3px solid #f7dfad;
  }
  #dialog strong { color: #9ef4d5; }
  #dialog small { display: block; margin-top: 6px; text-align: right; color: #aebbe0; }
  button {
    padding: 9px 12px; color: #fff4d6; background: #303958;
    border: 2px solid #f7dfad; border-radius: 5px;
    font: inherit; touch-action: manipulation;
  }
  button:active { transform: translateY(2px); }
  .card button { display: block; margin: 12px auto 0; background: #317888; }
  .hud { display: flex; justify-content: space-between; align-items: center; gap: 8px; flex-wrap: wrap; margin: 12px 0; }
  .hint { color: #b9c5e5; }
  .touch { display: none; justify-content: space-between; max-width: 520px; margin: 14px auto; }
  .pad { display: grid; grid-template: 44px 44px 44px / 48px 48px 48px; gap: 3px; }
  .pad button { padding: 0; }
  .up { grid-column: 2; }
  .left { grid-column: 1; grid-row: 2; }
  .down { grid-column: 2; grid-row: 2; }
  .right { grid-column: 3; grid-row: 2; }
  .actions { display: flex; gap: 12px; align-items: center; }
  .actions button { width: 62px; height: 62px; border-radius: 50%; font-size: 22px; font-weight: bold; }
  .actions .a { background: #b84c70; }
  .actions .b { background: #347eb2; }
  @media (max-width: 700px), (pointer: coarse) { .touch { display: flex; } }
.choices{display:grid;gap:8px;margin:14px 0}.choices button{text-align:left;background:#303958}.feedback{min-height:24px;text-align:center;color:#a7f2e1}.mini-title{color:#a7f2e1}
.wash-game{padding-top:4px}.wash-count{color:#9ef4d5;font-size:12px;text-align:center}.wash-visual{margin:8px auto 10px;max-width:360px;border:2px solid #66819a;border-radius:8px;background:linear-gradient(#e5f7ef 0 72%,#c0e5df 72%);overflow:hidden}.wash-visual svg{display:block;width:100%;height:auto}.skin{fill:#efb995;stroke:#805b56;stroke-width:3;stroke-linejoin:round}.nail{fill:none;stroke:#d88d83;stroke-width:2;stroke-linecap:round}.tap{fill:#768fa1}.water-drops,.soap-bubbles,.towel-icon{display:none}.water-drops path{fill:#56bce0;animation:waterfall .7s ease-in infinite alternate}.water-drops path:nth-child(2){animation-delay:.2s}.water-drops path:nth-child(3){animation-delay:.35s}.soap-bubbles circle{fill:#fff;stroke:#80cde0;stroke-width:2;animation:bubble .9s ease-in-out infinite alternate}.towel-icon path{fill:#fff7df;stroke:#c2a983;stroke-width:3;stroke-linejoin:round}.towel-icon path+path{fill:none;stroke:#d5bf9b;stroke-width:2}.wash-visual[data-step="0"] .water-drops,.wash-visual[data-step="6"] .water-drops{display:block}.wash-visual[data-step="1"] .soap-bubbles,.wash-visual[data-step="2"] .soap-bubbles,.wash-visual[data-step="3"] .soap-bubbles,.wash-visual[data-step="4"] .soap-bubbles,.wash-visual[data-step="5"] .soap-bubbles{display:block}.wash-visual[data-step="7"] .towel-icon{display:block}.wash-visual[data-step="2"] #washHandA,.wash-visual[data-step="4"] #washHandA{translate:-8px 0}.wash-visual[data-step="2"] #washHandB,.wash-visual[data-step="4"] #washHandB{translate:8px 0}.wash-visual[data-step="3"] #washHandA{translate:9px -2px}.wash-visual[data-step="3"] #washHandB{translate:-9px 2px}.wash-visual[data-step="5"] #washHandA{rotate:-8deg}.wash-visual[data-step="5"] #washHandB{rotate:8deg}.wash-hand{transform-box:fill-box;transform-origin:center;transition:translate .35s ease,rotate .35s ease}.wash-game h3{margin:6px 0;color:#a7f2e1}.wash-game p{min-height:42px;margin:4px 0 10px;line-height:1.45}.wash-controls{display:flex;justify-content:space-between;gap:8px}.wash-controls button{flex:1}.wash-controls button:disabled{opacity:.45;cursor:default}@keyframes waterfall{from{translate:0 -2px;opacity:.45}to{translate:0 5px;opacity:1}}@keyframes bubble{from{scale:.8;opacity:.6}to{scale:1.15;opacity:1}}
.brush-game{max-width:420px;margin:8px auto;padding:10px;background:#293858;border:2px solid #66819a;border-radius:8px;text-align:center}.brush-instruction{margin:2px 0 8px;line-height:1.4;color:#fff4d6}.brush-status{margin:4px 0 8px;color:#9ef4d5;font-weight:bold}#brushProgress{display:block;width:100%;height:12px;margin:0 auto 8px;accent-color:#9ef4d5}#toothBoard{display:block;width:100%;height:auto;border:2px solid #a9c8ca;border-radius:8px;touch-action:none;cursor:none;user-select:none}.row-label{font: bold 10px ui-monospace,Consolas,monospace;fill:#52727a}.brush-help{margin:7px 0 0;color:#dce9ff;font-size:12px}.tooth{fill:#fffdf0;stroke:#b3c8c9;stroke-width:2;filter:drop-shadow(1px 2px 0 #c8d9d5)}.plaque{fill:#f4c84d;stroke:#ba8d22;stroke-width:1.5}.plaque.cleaned{transform:scale(.2);opacity:0;transition:transform .18s,opacity .18s}.brush-status.done{color:#ffe680;font-size:16px} .nutrition-game{max-width:420px;margin:8px auto;padding:10px;background:#293858;border:2px solid #66819a;border-radius:8px;text-align:center}.nutrition-instruction,.nutrition-tip{margin:5px 0;color:#fff4d6;line-height:1.4}.nutrition-progress{color:#9ef4d5;font-weight:bold;margin:7px}.food-tray{display:grid;grid-template-columns:1fr 1fr;gap:6px;padding:10px;background:#e9d7ae;border:3px solid #ad8b59;border-radius:18px}.tray-slot{min-height:44px;padding:6px 3px;display:grid;place-items:center;background:#fff7e3;border:2px dashed #c6b48f;border-radius:12px;color:#43516b;font-size:11px}.tray-slot.filled{background:#d5f0d8;border-style:solid;border-color:#76b681}.food-choices{display:grid;grid-template-columns:repeat(2,1fr);gap:6px;margin:9px 0}.food-choices button{margin:0!important;padding:10px 5px;background:#394968;min-height:48px;transition:transform .16s,background .16s,box-shadow .16s}.food-choices button:hover:not(:disabled){transform:translateY(-3px) scale(1.03);background:#4d6482;box-shadow:0 4px 0 #18213b}.food-tray.celebrate{animation:platePop .55s ease}.nutrition-cheer{min-height:25px;color:#ffe680;font-weight:bold}@keyframes platePop{50%{transform:scale(1.04) rotate(-1deg)}}.food-choices button:disabled{opacity:.55;border-color:#9ef4d5}.soap-instruction{margin:5px 0;line-height:1.45;color:#fff4d6}.soap-step,.soap-progress{margin:7px;color:#9ef4d5;font-weight:bold}#soapBoard{display:block;width:100%;max-width:400px;height:auto;margin:6px auto;border:2px solid #a9c8ca;border-radius:10px;touch-action:none;user-select:none}.soap-target{fill:#fff8d055;stroke:#e6b941;stroke-width:3;stroke-dasharray:4 3;transition:fill .2s,stroke .2s}.soap-target.active{fill:#76d8bb88;stroke:#168969;stroke-width:4;stroke-dasharray:none;filter:drop-shadow(0 0 5px #71e5bb)}.soap-target.cleaned{fill:#78c994;stroke:#287d55;stroke-dasharray:none}.soap-phase-next{margin:8px auto!important;background:#317888!important}.soap-target.active{animation:targetPulse .8s ease-in-out infinite alternate}@keyframes targetPulse{to{filter:drop-shadow(0 0 8px #71e5bb);transform:scale(1.12)}}.soap-target.cleaned::after{content:"✓"} .award-card{text-align:center!important;max-width:520px!important;background:linear-gradient(180deg,#263457,#202747);border-color:#ffe7a5}.award-medal{position:relative;width:78px;height:78px;margin:8px auto 14px;display:grid;place-items:center;border:5px solid #ffe486;border-radius:50%;background:#e5a640;box-shadow:0 0 0 5px #8f642e,5px 7px 0 #12192e;animation:medalBounce 1.4s ease-in-out infinite}.award-medal:before,.award-medal:after{content:"";position:absolute;top:63px;width:20px;height:30px;background:#d85e78;border:3px solid #8f3f62;z-index:-1}.award-medal:before{left:11px;transform:rotate(13deg)}.award-medal:after{right:11px;transform:rotate(-13deg);background:#58aeca;border-color:#34758f}.award-medal span{font-size:31px;color:#fff8d9;text-shadow:2px 2px #9a612f}.award-medal b{position:absolute;right:8px;top:8px;color:#fff5bf;font-size:13px}.award-confetti{color:#ffe680;font-size:20px;letter-spacing:7px;animation:confettiFloat 1.8s ease-in-out infinite alternate}.award-list{display:grid;gap:6px;margin:12px 0;padding:10px;background:#18223e;border:2px dashed #8295bd;text-align:left}.award-label{display:block;margin:12px 0 4px;color:#ccefe7;font-size:12px}.award-card input{width:100%;padding:10px;border:2px solid #8facc7;border-radius:4px;background:#fff7e3;color:#283452;font:inherit}.certificate{margin:14px 0;padding:14px 10px;background:#fff3ce;color:#40506c;border:5px double #c49d51;box-shadow:4px 4px #11172d;animation:certificateIn .45s ease}.certificate span,.certificate strong,.certificate p,.certificate b{display:block}.certificate span{font-size:11px;letter-spacing:2px}.certificate strong{margin:8px 0;color:#386e70;font-size:22px;overflow-wrap:anywhere}.certificate p{margin:6px}.award-message{color:#ffe680;min-height:18px}@keyframes medalBounce{50%{transform:translateY(-5px) rotate(3deg)}}@keyframes confettiFloat{to{transform:translateY(4px);filter:brightness(1.3)}}@keyframes certificateIn{from{opacity:0;transform:scale(.9)}to{opacity:1;transform:scale(1)}}@media(prefers-reduced-motion:reduce){.award-medal,.award-confetti{animation:none}}</style>
</head>
<body>
<main>
  <h1>✚ PLANTÃO PIXEL ✚</h1>

  <div id="frame">
    <canvas id="game" width="720" height="450" aria-label="Mapa pixel art do hospital"></canvas>

    <div id="dialog">
      <strong id="speaker"></strong>
      <div id="message"></div>
      <small>A ou Espaço para continuar</small>
    </div>

    <section class="overlay" id="intro">
      <div class="card">
        <h2>Hospital da Vila</h2>
        <p>Uma aventura sobre cuidar! Converse com os pacientes e aprenda sobre alimentação saudável, higiene das mãos e escovação dental.</p>
        <p><b>Teclado:</b> setas ou WASD para andar; Espaço para conversar.<br>
        <b>Celular:</b> use o direcional e os botões A e B.</p>
        <button id="start">COMEÇAR O PLANTÃO</button>
      </div>
    </section>

    <section class="overlay" id="ending" style="display:none">
      <div class="card award-card">
        <span class="badge">PLANTÃO CONCLUÍDO</span>
        <div class="award-confetti" aria-hidden="true">✦　✧　✦　✧　✦</div>
        <div class="award-medal" aria-hidden="true"><span>✚</span><b>★</b></div>
        <h2>Medalha Guardião da Saúde!</h2>
        <p>Você espalhou cuidado pelo hospital. Confira tudo o que aprendeu:</p>
        <div class="award-list"><div>🥗 <b>Nutrição:</b> escolher alimentos variados</div><div>🫧 <b>Higiene:</b> ensaboar, enxaguar e secar</div><div>🦷 <b>Sorriso:</b> escovar com cuidado</div></div>
        <label class="award-label" for="awardName">Seu nome no certificado (opcional)</label>
        <input id="awardName" maxlength="24" placeholder="Digite seu nome" autocomplete="off">
        <button id="claimAward">RECEBER MEU CERTIFICADO ✨</button>
        <div class="certificate" id="certificate" style="display:none"><span>CERTIFICADO DE CUIDADO</span><strong id="certificateName">Pequeno(a) Guardião(ã)</strong><p>Concluiu as missões de saúde do Hospital da Vila!</p><b>🥗　🫧　🦷</b></div>
        <p class="award-message" id="awardMessage" aria-live="polite"></p>
        <button onclick="location.reload()">JOGAR DE NOVO</button>
      </div>
    </section>
    <section class="overlay" id="challenge" style="display:none"><div class="card"><span class="badge" id="topic"></span><h2 id="challengeTitle" style="color:#a7f2e1"></h2><p id="question"></p><div id="washGame" class="wash-game" style="display:none">
  <div class="wash-count" id="washCount"></div>
  <div class="wash-visual" id="washVisual" data-step="0">
    <svg viewBox="0 0 300 125" role="img" aria-label="Ilustração animada de duas mãos sendo lavadas">
      <g id="washHandA" class="wash-hand">
        <path class="skin" d="M64 105V60c0-8 12-8 12 0V36c0-9 12-9 12 0v23V29c0-9 12-9 12 0v30V35c0-9 12-9 12 0v39c9-10 18-5 14 5l-10 23c-3 8-9 12-19 12H77c-8 0-13-4-13-9Z"/>
        <path class="nail" d="M79 42v11m12-18v12m12-12v12m12-6v12"/>
      </g>
      <g id="washHandB" class="wash-hand" transform="translate(300 0) scale(-1 1)">
        <path class="skin" d="M64 105V60c0-8 12-8 12 0V36c0-9 12-9 12 0v23V29c0-9 12-9 12 0v30V35c0-9 12-9 12 0v39c9-10 18-5 14 5l-10 23c-3 8-9 12-19 12H77c-8 0-13-4-13-9Z"/>
        <path class="nail" d="M79 42v11m12-18v12m12-12v12m12-6v12"/>
      </g>
      <g class="water-drops"><path d="M146 12c0 0-7 9-7 14a7 7 0 0 0 14 0c0-5-7-14-7-14m-20 8c0 0-4 6-4 9a4 4 0 0 0 8 0c0-3-4-9-4-9m40-1c0 0-4 6-4 9a4 4 0 0 0 8 0c0-3-4-9-4-9"/></g>
      <g class="soap-bubbles"><circle cx="141" cy="52" r="7"/><circle cx="157" cy="66" r="4"/><circle cx="149" cy="39" r="3"/><circle cx="129" cy="69" r="3"/></g>
      <g class="towel-icon"><path d="M126 44h48v49h-48z"/><path d="M134 54h32m-32 9h32m-32 9h24"/></g>
      <path class="tap" d="M137 18h27v6h-8v7h-7v-7h-12z"/>
    </svg>
  </div>
  <h3 id="washStepTitle"></h3><p id="washStepText"></p>
  <div class="wash-controls"><button id="washPrev">← VOLTAR</button><button id="washNext">PRÓXIMA ETAPA →</button></div>
<div class="choices" id="choices"></div><div class="feedback" id="feedback"></div><button class="primary" id="returnHospital" style="display:none">VOLTAR AO HOSPITAL</button></div></section>
    <section class="overlay" id="brushChallenge" style="display:none"><div class="card"><span class="badge">ESCOVAÇÃO DENTAL</span><h2 style="color:#a7f2e1">Vamos limpar todos os dentinhos!</h2><div id="brushGame" class="brush-game"><p class="brush-instruction">🪥 Arraste a escova pelas manchas amarelas até limpar os dentinhos!</p><div class="brush-status" id="brushStatus"></div><progress id="brushProgress" max="28" value="0" aria-label="Progresso da escovação"></progress><svg id="toothBoard" viewBox="0 0 360 190" aria-label="Escove os dentes"><rect width="360" height="190" rx="12" fill="#fff3ed"/><path d="M16 29 Q180 12 344 29 L344 39 Q180 32 16 39Z M16 143 Q180 151 344 143 L344 154 Q180 164 16 154Z" fill="#ef9eae"/><text x="180" y="20" text-anchor="middle" fill="#765362" font-size="10" font-weight="bold">SORRISO SAUDÁVEL</text><g id="toothLayer"></g><g id="brushCursor" visibility="hidden" pointer-events="none"><rect x="-5" y="-2" width="10" height="39" rx="5" fill="#398ca4" stroke="#24566e" stroke-width="2"/><path d="M-2 4v25M2 4v25" stroke="#85d9dc" stroke-width="2"/><rect x="-13" y="-15" width="26" height="13" rx="5" fill="#ffd66e" stroke="#8c6d3a" stroke-width="2"/><path d="M-9 -14v-5m6 5v-6m6 6v-6m6 6v-5" stroke="#fff" stroke-width="2" stroke-linecap="round"/></g></svg><p class="brush-help">Segure e esfregue com mouse ou dedo. Passe por todos os dentinhos! ⭐</p></div><div class="feedback" id="brushFeedback"></div><button class="primary" id="brushReturn" style="display:none">VOLTAR AO HOSPITAL</button></div></section>
    <section class="overlay" id="nutritionChallenge" style="display:none"><div class="card"><span class="badge">NUTRIÇÃO SAUDÁVEL</span><h2 style="color:#a7f2e1">Monte uma bandeja colorida!</h2><div id="nutritionGame" class="nutrition-game"><p class="nutrition-instruction">Escolha uma opção de cada grupo para completar a bandeja.</p><div class="nutrition-cheer" id="nutritionCheer">🌟 Ajude Lia a preparar uma bandeja campeã!</div><div class="nutrition-progress" id="nutritionProgress">0 de 4 grupos escolhidos</div><div class="food-tray" id="foodTray"><div class="tray-slot" data-group="colorido">🍎 Fruta ou legume</div><div class="tray-slot" data-group="energia">🍚 Arroz ou tubérculo</div><div class="tray-slot" data-group="feijao">🫘 Feijão ou ovo</div><div class="tray-slot" data-group="agua">💧 Água</div></div><div class="food-choices" id="foodChoices"></div><p class="nutrition-tip">Dica: variar os alimentos ajuda a incluir diferentes nutrientes.</p></div><div class="feedback" id="nutritionFeedback"></div><button class="primary" id="nutritionReturn" style="display:none">VOLTAR AO HOSPITAL</button></div></section>    <section class="overlay" id="soapChallenge" style="display:none"><div class="card"><span class="badge">MISSÃO DAS MÃOS LIMPAS</span><h2 style="color:#a7f2e1">Passe o sabonete por cada parte!</h2><p class="soap-instruction">Arraste a espuma até o círculo brilhante. Vamos limpar as palmas, dedos, unhas e punhos!</p><div class="soap-step" id="soapStep">1 de 6 · Palmas</div><svg id="soapBoard" viewBox="0 0 360 170" aria-label="Arraste a espuma azul pelas mãos"><rect width="360" height="170" rx="12" fill="#e7f8f2"/><path d="M71 145V83c0-8 13-8 13 0V54c0-9 13-9 13 0V44c0-9 13-9 13 0v8c0-9 13-9 13 0v42c8-9 19-3 15 7l-12 29c-3 7-9 11-18 11H88c-10 0-17-5-17-15Z" fill="#efb995" stroke="#805b56" stroke-width="3"/><path d="M71 145V83c0-8 13-8 13 0V54c0-9 13-9 13 0V44c0-9 13-9 13 0v8c0-9 13-9 13 0v42c8-9 19-3 15 7l-12 29c-3 7-9 11-18 11H88c-10 0-17-5-17-15Z" transform="translate(360 0) scale(-1 1)" fill="#efb995" stroke="#805b56" stroke-width="3"/><g id="soapTargets"><circle class="soap-target active" data-zone="0" cx="104" cy="101" r="16"/><circle class="soap-target" data-zone="1" cx="256" cy="101" r="16"/><circle class="soap-target" data-zone="2" cx="108" cy="60" r="16"/><circle class="soap-target" data-zone="3" cx="252" cy="60" r="16"/><circle class="soap-target" data-zone="4" cx="82" cy="128" r="16"/><circle class="soap-target" data-zone="5" cx="278" cy="128" r="16"/></g><g id="soapDrag" transform="translate(180 143)" style="cursor:grab"><circle r="17" fill="#80d9ee" stroke="#347eaa" stroke-width="3"/><circle cx="-5" cy="-5" r="5" fill="#efffff"/><text x="0" y="5" text-anchor="middle" font-size="15">🫧</text></g></svg><div class="soap-progress" id="soapProgress">0 de 6 partes limpas</div><div class="feedback" id="soapFeedback"></div><button class="primary soap-phase-next" id="soapPhaseNext" style="display:none">ENXAGUAR AS MÃOS →</button><button class="primary" id="soapReturn" style="display:none">VOLTAR AO HOSPITAL</button></div></section>      </div>

  <div class="hud">
    <span id="score">✚ Médico · 0/3 cuidados</span>
    <button id="music">♫ Música ligada</button>
  </div>
  <p class="hint" id="hint">Explore o hospital e encontre os pacientes</p>

  <div class="touch">
    <div class="pad">
      <button class="up" data-key="ArrowUp">▲</button>
      <button class="left" data-key="ArrowLeft">◀</button>
      <button class="down" data-key="ArrowDown">▼</button>
      <button class="right" data-key="ArrowRight">▶</button>
    </div>
    <div class="actions">
      <button class="a" id="buttonA">A</button>
      <button class="b" id="buttonB">B</button>
    </div>
  </div>
  <p class="hint">A: conversar/avançar · B: saber sobre objetos, sentar/levantar ou sair do minigame.</p>
</main>

<script>
(() => {
  const canvas = document.querySelector("#game");
  const ctx = canvas.getContext("2d");
  const keys = new Set();
  const W = 576, H = 360, SCALE = canvas.width / W;

  const player = { x: 310, y: 125, vx: 0, vy: 0 };
  let lastMoveTime = performance.now();
  let lastFrameTime = performance.now(), walkPhase = 0, walking = false;
  let started = false, dialogue = null, lineIndex = 0, nearby = null, nearbyProp = null, isSitting = false;
  let audio = null, musicOn = true, victoryPlayed = false;

  const patients = [
    {
      x: 352, y: 49, name: "Lia · Nutrição", color: "#e888b1", done: false,
      lines: [
        "Oi, doutor(a)! Nosso corpo precisa de energia e nutrientes para brincar, estudar e crescer.",
        "Uma alimentação saudável fica mais colorida com frutas, verduras, legumes e alimentos variados.",
        "Água também é importante! Sempre que puder, escolha água para matar a sede. Cada pessoa tem necessidades diferentes."
      ]
    },
    {
      x: 322, y: 110, name: "Bento · Higiene", color: "#e3ad78", done: false,
      lines: [
        "Olá! Lavar as mãos é uma atitude simples que ajuda a proteger você e outras pessoas.",
        "Use água e sabão. Esfregue as palmas, o dorso das mãos, entre os dedos e embaixo das unhas.",
        "Lave as mãos antes de comer e depois de usar o banheiro. Na dúvida, peça orientação a um adulto ou profissional."
      ]
    },
    {
      x: 108, y: 110, name: "Nina · Dentista", color: "#9b8de0", done: false,
      lines: [
        "Escovar os dentes ajuda a remover restos de alimentos e placa.",
        "Use uma escova macia e creme dental com flúor. Faça movimentos suaves em todas as faces dos dentes.",
        "A língua também merece cuidado. Peça ajuda a um adulto e visite o dentista regularmente."
      ]
    },
    {x:472,y:130,name:"Davi · Sala de espera",color:"#78b5c9",done:false,figure:true,role:"patient",lines:["Oi! Estou esperando minha consulta. Aqui tem cadeiras para todo mundo descansar.","Quando chamam meu nome, eu vou com um adulto até a sala indicada."]},
    {x:28,y:51,name:"Dra. Rosa · Consultório",color:"#87bd91",done:false,figure:true,role:"doctor",lines:["Olá! No consultório eu converso com cada pessoa para saber como ela está.","É importante contar ao profissional de saúde o que você está sentindo."]},
    {x:91,y:193,name:"Enf. Bia · Triagem",color:"#e3aa72",done:false,figure:true,role:"nurse",lines:["Bem-vindo à triagem! Eu pergunto como a pessoa está e verifico alguns sinais de saúde.","Assim, a equipe consegue organizar o atendimento com cuidado."]},
    {x:193,y:285,name:"Luz · Recepção",color:"#d58da8",done:false,figure:true,role:"reception",lines:["Oi! Na recepção eu ajudo as pessoas a encontrar o lugar certo.","Se estiver perdido, pode pedir ajuda a um adulto ou à equipe do hospital."]},
    {x:391,y:294,name:"Téo · Paciente",color:"#85b9ca",done:false,figure:true,role:"patient",pose:"lying",lines:["Estou recebendo cuidado nos dentes. A equipe explicou cada passo para eu ficar tranquilo.","No dentista, podemos fazer perguntas e avisar se algo incomodar."]},
    {x:438,y:292,name:"Dr. Caio · Dentista",color:"#8fbf9a",done:false,figure:true,role:"surgeon",lines:["Estamos cuidando dos dentes do Téo com atenção e instrumentos limpos.","No consultório odontológico, o dentista explica o que vai fazer e trabalha com segurança."]},
    {x:489,y:306,name:"Malu · Auxiliar",color:"#d59da7",done:false,figure:true,role:"nurse",lines:["Sou auxiliar da equipe. Organizo os materiais e ajudo o paciente durante o atendimento.","Cada instrumento é preparado com muito cuidado antes de ser usado."]}
  ];

  const interactables = [
    {kind:"medicine",x:425,y:60,name:"Soro fisiológico",range:25,lines:["O soro fisiológico é uma solução de água e sal usada para alguns cuidados, conforme o tipo de produto.","Ele pode ajudar a limpar ou umedecer algumas regiões. Cada produto tem um uso próprio.","Medicamentos e produtos de saúde só devem ser usados com orientação de um adulto responsável ou profissional."]},
    {kind:"medicine",x:471,y:60,name:"Xarope",range:25,lines:["Existem xaropes diferentes para sintomas diferentes.","Um xarope não serve para todo tipo de tosse ou para todas as pessoas.","Só um adulto responsável ou profissional de saúde pode decidir se deve usar e qual produto escolher."]},
    {kind:"medicine",x:517,y:60,name:"Pomada",range:25,lines:["Há pomadas para cuidados diferentes, como alguns problemas de pele.","A embalagem e a orientação profissional explicam para que serve cada uma.","Não passe uma pomada sem pedir ajuda a um adulto responsável."]},
    ...[423,458,493].map((x,i)=>({kind:"seat",x,y:158,name:"Poltrona da sala de espera",range:21})),
    ...[95,114].map(x=>({kind:"seat",x,y:189,name:"Banco da triagem",range:19})),
    ...[174,198,222,246].map(x=>({kind:"seat",x,y:300,name:"Cadeira da recepção",range:20}))
  ];

  const walls = [
    {x:0,y:0,w:576,h:12}, {x:0,y:0,w:12,h:360},
    // Paredes das salas: aberturas alinhadas às portas desenhadas.
    {x:17,y:23,w:116,h:4},{x:17,y:68,w:116,h:4},{x:17,y:23,w:4,h:49},{x:129,y:23,w:4,h:13},{x:129,y:58,w:4,h:14},
    {x:252,y:23,w:116,h:4},{x:252,y:68,w:116,h:4},{x:364,y:23,w:4,h:49},{x:252,y:23,w:4,h:13},{x:252,y:58,w:4,h:14},
    {x:17,y:77,w:116,h:4},{x:17,y:135,w:116,h:4},{x:17,y:77,w:4,h:61},{x:129,y:77,w:4,h:15},{x:129,y:116,w:4,h:19},
    {x:252,y:77,w:116,h:4},{x:252,y:135,w:116,h:4},{x:364,y:77,w:4,h:61},{x:252,y:77,w:4,h:15},{x:252,y:116,w:4,h:19},
    {x:17,y:139,w:116,h:4},{x:17,y:224,w:116,h:4},{x:17,y:139,w:4,h:85},{x:129,y:139,w:4,h:16},{x:129,y:181,w:4,h:43},
    {x:252,y:139,w:116,h:4},{x:252,y:224,w:116,h:4},{x:364,y:139,w:4,h:85},{x:252,y:139,w:4,h:16},{x:252,y:181,w:4,h:43},
    // Paredes da recepção e odontologia com portas voltadas ao corredor sul.
    {x:22,y:249,w:144,h:4},{x:220,y:249,w:52,h:4},{x:22,y:330,w:250,h:4},{x:22,y:249,w:4,h:85},{x:268,y:249,w:4,h:85},
    {x:300,y:249,w:76,h:4},{x:430,y:249,w:122,h:4},{x:300,y:330,w:252,h:4},{x:300,y:249,w:4,h:85},{x:548,y:249,w:4,h:85},
    {x:564,y:0,w:12,h:360}, {x:0,y:348,w:576,h:12},
    {x:139,y:15,w:8,h:17}, {x:139,y:58,w:8,h:19},
    {x:245,y:15,w:8,h:17}, {x:245,y:58,w:8,h:19},
    {x:139,y:77,w:8,h:12}, {x:139,y:116,w:8,h:19},
    {x:245,y:77,w:8,h:12}, {x:245,y:116,w:8,h:19},
    {x:139,y:139,w:8,h:16}, {x:245,y:139,w:8,h:16},
    {x:380,y:14,w:8,h:74}, {x:380,y:110,w:8,h:118},
    {x:390,y:88,w:45,h:6}, {x:456,y:88,w:100,h:6},
    {x:12,y:238,w:154,h:8}, {x:220,y:238,w:156,h:8}, {x:430,y:238,w:134,h:8},
    {x:282,y:249,w:8,h:29}, {x:282,y:300,w:8,h:34},
    // Balcão da farmácia: barreira sólida alinhada à prateleira desenhada.
    {x:398,y:71,w:148,h:7}
  ];

  function rect(x, y, w, h, color) {
    ctx.fillStyle = color;
    ctx.fillRect(Math.round(x), Math.round(y), w, h);
  }

  function label(text, x, y, color = "#344362", size = 8) {
    ctx.fillStyle = color;
    ctx.font = "bold " + size + "px monospace";
    ctx.textAlign = "center";
    ctx.fillText(text, x, y);
  }

  function drawRoomWalls() {
    const wall='#d8c69d', edge='#9e896c', light='#fff0d0';
    function h(x,y,w){rect(x,y,w,4,edge);rect(x+1,y,w-2,2,wall);rect(x+1,y,w-2,1,light)}
    function v(x,y,hg){rect(x,y,4,hg,edge);rect(x+1,y+1,2,hg-2,wall);rect(x+1,y+1,1,hg-2,light)}
    // Consultório e nutrição: aberturas centrais levam ao corredor.
    h(17,23,116);h(17,68,116);v(17,23,49);v(129,23,10);v(129,58,10);
    h(252,23,116);h(252,68,116);v(364,23,49);v(252,23,10);v(252,58,10);
    // Enfermaria e banheiro.
    h(17,77,116);h(17,135,116);v(17,77,61);v(129,77,12);v(129,116,19);
    h(252,77,116);h(252,135,116);v(364,77,61);v(252,77,12);v(252,116,19);
    // Recepção e odontologia.
    h(17,139,116);h(17,224,116);v(17,139,85);v(129,139,16);v(129,181,43);
    h(252,139,116);h(252,224,116);v(364,139,85);v(252,139,16);v(252,181,43);
    // Divisórias do corredor, com passagens alinhadas às portas.
    v(137,15,17);v(137,58,19);v(137,77,12);v(137,116,19);v(137,139,16);
    v(243,15,17);v(243,58,19);v(243,77,12);v(243,116,19);v(243,139,16);
  }
  function drawMap() {
    rect(0, 0, W, H, "#83cbbb");
    for (let x = 12; x < W-12; x += 24) {
      for (let y = 12; y < H-12; y += 24) {
        rect(x, y, 23, 23, (x + y) % 3 ? "#8bd4c1" : "#7ec4b5"); rect(x+3,y+4,2,2,"#a4e2d1");rect(x+18,y+17,2,2,"#72b8ae");if((x+y)%48===0)rect(x+10,y+11,3,2,"#91d1c3");
      }
    }

    // Paredes externas e corredor
    rect(12, 12, W-24, 7, "#e8e0c8");
    rect(12, H-22, W-24, 10, "#e8e0c8");
    rect(12, 12, 3, H-24, "#e8e0c8");
    rect(W-15, 12, 3, H-24, "#e8e0c8");
    // Corredor de ligação e passagem para a ala nova.
    rect(12,238,154,4,"#9e896c"); rect(12,239,154,2,"#d8c69d");
    rect(220,238,156,4,"#9e896c"); rect(220,239,156,2,"#d8c69d"); rect(430,238,134,4,"#9e896c"); rect(430,239,134,2,"#d8c69d");
    rect(380,14,4,74,"#9e896c"); rect(381,15,2,72,"#d8c69d");
    rect(380,110,4,118,"#9e896c"); rect(381,111,2,116,"#d8c69d");

    // Salas
    const rooms = [
      [18,26,112,42,"#b4dfd2","CONSULTÓRIO"],
      [254,26,112,42,"#c8e2c3","NUTRIÇÃO"],
      [18,80,112,55,"#b8d9e7","ENFERMARIA"],
      [254,80,112,55,"#edd0d9","BANHEIRO"],
      [18,142,112,82,"#e1dcc0","TRIAGEM"],
      [254,142,112,82,"#d1dfec","CONSULTA"]
    ];
    rooms.forEach(([x,y,w,h,color,name]) => {
      rect(x,y,w,h,color);
      for(let tx=x+5;tx<x+w-4;tx+=14) for(let ty=y+19;ty<y+h-4;ty+=13) {
        rect(tx,ty,2,2,"#ffffff18");
        if(((tx+ty)/2)%3===0) rect(tx+5,ty+5,2,2,"#52627a18");
      }
      rect(x+2,y+h-4,w-4,2,"#718d91"); rect(x+3,y+h-4,w-6,1,"#e7eee0");
      rect(x+(w-Math.min(w-8,name.length*6+12))/2,y+3,Math.min(w-8,name.length*6+12),13,"#334360");
      label(name, x + w/2, y + 13, "#fff4d6", 8);
    });

    drawRoomWalls();

    // Móveis e detalhes
    rect(39,43,40,12,"#eee4ca"); rect(41,45,36,8,"#a4cecf");
    rect(270,43,52,10,"#e8dac1");
    ["#e88770","#77bf8b","#f2cc6b"].forEach((color,i) => rect(300+i*15,45,8,6,color));
    [27,63].forEach(x => {
      rect(x,101,30,16,"#f8f0dc"); rect(x+2,103,26,9,"#f8fbf2");
      rect(x+3,102,9,5,"#edb3a5"); rect(x,116,30,3,"#739bb0");
    });
    rect(267,102,35,21,"#faf3e5"); rect(270,104,15,17,"#b9dce0");
    rect(31,168,49,14,"#9a886d"); rect(34,165,43,12,"#bdab8c");
    rect(300,169,39,20,"#f7f1e5"); rect(304,171,31,6,"#a7c7cb");
    for (let x = 128; x < 257; x += 16) rect(x,113,9,4,"#a4d8c9");
    rect(173,194,38,24,"#8c7781");
    // Mobiliário adicional nas salas ampliadas.
    rect(83,45,39,18,'#f8f0dc');rect(86,47,33,10,'#b3d4d2');rect(86,57,4,7,'#718896');rect(115,48,9,15,'#c0a988');
    rect(330,47,10,16,'#fff0db');rect(332,49,6,5,'#f0b867');rect(332,56,6,5,'#83bd87');
    rect(340,103,17,12,'#f5f2e8');rect(343,105,11,6,'#a9d3d6');rect(344,98,9,3,'#89afbb');
    [87,106].forEach(x=>{rect(x,184,16,9,'#728e9a');rect(x+2,193,12,3,'#526b78')});
    rect(347,179,8,3,'#8398aa');rect(350,172,3,12,'#8398aa');rect(344,169,14,4,'#f4df9e');
    // Letreiro retangular vertical encostado à parede lateral da sala de espera.
    rect(368,153,12,48,"#85745f");rect(370,155,8,44,"#334360");
    ctx.save();ctx.translate(374,177);ctx.rotate(-Math.PI/2);label("SAÍDA",0,2,"#fff5db",7);ctx.restore();
    drawNewWing();
  }

  function drawNewWing() {
    // Farmácia na ala leste.
    rect(392,24,160,62,"#d5e8d2"); rect(395,27,154,56,"#c7e1c5");
    rect(407,30,130,13,"#334360"); label("FARMÁCIA",472,40,"#fff4d6",9);
    label("MEDICAMENTOS",472,47,"#43566c",6);
    rect(400,49,144,21,"#8c755e");rect(402,50,140,18,"#e9dfc5");
    const medicines=[
      {name:"SORO",color:"#8ed5e5",cap:"#f4f2e5"},
      {name:"XAROPE",color:"#b67852",cap:"#ecd38a"},
      {name:"POMADA",color:"#e4a078",cap:"#f4e9cf"}
    ];
    medicines.forEach((medicine,i)=>{const x=404+i*46;rect(x,51,42,18,"#fff8e6");rect(x+15,52,12,2,medicine.cap);rect(x+13,54,16,8,medicine.color);rect(x+15,62,12,2,"#7c8793");rect(x+18,56,6,4,"#ffffff88");label(medicine.name,x+21,68,"#344362",5.5)});
    rect(398,71,148,7,"#765d47");rect(399,71,146,2,"#c9a778");rect(400,75,144,2,"#a88762");
    label("USE SÓ COM UM ADULTO",472,84,"#35445d",5);
    // Sala de espera ampla, com janelas, poltronas e plantas.
    rect(390,88,45,4,"#9e896c");rect(391,89,43,2,"#d8c69d");rect(456,88,100,4,"#9e896c");rect(457,89,98,2,"#d8c69d");
    rect(392,98,160,126,"#c5dfdc"); rect(395,101,154,120,"#b7d7d2");
    rect(405,107,40,20,"#93d4e2"); rect(408,110,34,14,"#d8f4e9");rect(424,110,2,14,"#8cb8c0");
    label("ESPERA",493,113,"#42516c",9);
    [410,445,480].forEach((x,i)=>{rect(x,151,27,17,'#465574');rect(x+3,146,21,10,['#df8292','#e6be71','#7bb7c6'][i]);rect(x+5,168,4,5,'#34415f');rect(x+20,168,4,5,'#34415f')});
    rect(519,175,15,22,'#9a7056');rect(516,164,21,17,'#66a777');rect(520,159,13,12,'#8cc885');rect(522,156,8,8,'#a2d58e');
    rect(391,232,174,3,'#9e896c');rect(392,233,172,2,'#d8c69d');
    // Ala sul: duas salas conectadas pelo corredor central.
    rect(22,250,250,84,'#e1e6cf');rect(25,253,244,78,'#d7e1c5');rect(34,257,226,13,'#334360');label("RECEPÇÃO AMPLIADA",147,267,"#fff4d6",9);
    // Balcão amplo e assentos distribuídos pela recepção.
    rect(43,284,104,20,'#8d7059');rect(47,281,96,7,'#c4a783');rect(48,292,94,4,'#9fb9b2');
    rect(59,275,15,7,'#394765');rect(61,276,11,4,'#8bc7d0');rect(112,275,15,7,'#394765');rect(114,276,11,4,'#8bc7d0');
    [166,190,214,238].forEach((x,i)=>{rect(x,294,17,9,['#6f91a0','#d88d98','#d3ad61','#78a886'][i]);rect(x+2,303,13,4,'#536789')});
    rect(162,281,16,28,'#8b6e5c');rect(158,275,24,10,'#6eaf79');rect(164,269,13,10,'#89c984');
    rect(300,250,252,84,'#d9e1ed');rect(303,253,246,78,'#ccd9e8');rect(315,257,222,13,'#334360');label("ODONTOLOGIA AMPLIADA",426,267,"#fff4d6",9);
    // Contornos visíveis das salas inferiores; as portas ficam alinhadas às colisões.
    const lowerWalls=[[22,249,144,4],[220,249,52,4],[22,330,250,4],[22,249,4,85],[268,249,4,85],[300,249,76,4],[430,249,122,4],[300,330,252,4],[300,249,4,85],[548,249,4,85]];
    lowerWalls.forEach(([x,y,w,h])=>{rect(x,y,w,h,"#9e896c");if(w>h)rect(x+1,y+1,w-2,h-2,"#d8c69d");else rect(x+1,y+1,w-2,h-2,"#d8c69d")});
    rect(357,289,68,17,'#678b9d');rect(362,283,58,12,'#f0d4d7');rect(367,278,26,8,'#fff4e7');rect(410,294,8,18,'#647c91');
    rect(391,274,3,17,'#8499aa');rect(384,272,17,3,'#8499aa');rect(386,269,13,5,'#f5df9b');
    rect(446,284,74,8,'#96795e');rect(450,280,66,5,'#c7aa84');rect(457,292,9,13,'#8eb7bf');rect(470,292,9,13,'#d9959b');rect(497,293,18,19,'#b8c9cc');
    rect(462,286,19,23,'#986e58');rect(458,276,27,13,'#6da777');rect(464,270,16,11,'#91cb83');
    rect(282,249,4,29,'#9e896c');rect(283,250,2,27,'#d8c69d');rect(282,300,4,34,'#9e896c');rect(283,301,2,32,'#d8c69d');
  }

  function drawLyingPatient(x,y) {
    rect(x-16,y+7,32,4,"#9fb8bc");
    rect(x-15,y-2,25,9,"#77aebb");rect(x-13,y-1,21,5,"#a8d2d2");
    rect(x+8,y-4,9,11,"#efc09e");rect(x+8,y-6,9,4,"#634d62");
    rect(x+12,y,2,1,"#28334c");rect(x+10,y+2,4,2,"#fff2df");
    rect(x-15,y+1,5,5,"#d8e9e3");rect(x-11,y+2,2,2,"#e35e6c");rect(x-12,y+1,4,1,"#fff7e7");
  }
  function drawPerson(x, y, color, isPlayer = false, role = "patient", sitting = false) {
    const step = isPlayer && walking && !sitting ? Math.round(Math.sin(walkPhase * 2) * 2) : 0;
    const bob = isPlayer && walking && !sitting ? Math.round(Math.sin(walkPhase * 4)) : 0;
    y += bob;
    // Sombra, botas y uniforme com contorno pixelado.
    rect(x-9,y+10,18,4,"#548b83");rect(x-7,y+10,14,2,"#72a99a");
    if(!sitting){rect(x-6,y+5+step,5,6,"#27324c");rect(x+1,y+5-step,5,6,"#27324c");}
    rect(x-7,y-5,14,12,"#293450");rect(x-8,y-3,2,7,"#293450");rect(x+6,y-3,2,7,"#293450");
    const coat = isPlayer ? "#f6f5e9" : role === "nutrition" ? "#eaa17b" : role === "hygiene" ? "#75b7c9" : role === "doctor" ? "#f2f0e2" : role === "nurse" ? "#69adc0" : role === "reception" ? "#d7839f" : role === "surgeon" ? "#68aeb0" : role === "patient" ? color : "#b9a6e8";
    rect(x-6,y-4,12,10,coat);rect(x-6,y+4,12,2,isPlayer?"#d9d9cf":"#55647c");rect(x-1,y-3,2,9,"#fff9e9");
    rect(x-4,y-1,2,2,"#e9d6b0"); rect(x+2,y-1,2,2,"#e9d6b0");
    if(isPlayer&&sitting){rect(x-5,y+4,6,3,"#27324c");rect(x,y+5,7,3,"#27324c");rect(x+4,y+7,5,2,"#27324c");rect(x-5,y+2,2,3,"#d7e4ed");}
    // Cabeça, orelhas, cabelo e expressões.
    rect(x-6,y-15,12,10,"#293450"); rect(x-5,y-14,10,9,"#f0bf9e");
    rect(x-7,y-12,2,4,"#f0bf9e"); rect(x+5,y-12,2,4,"#f0bf9e");
    if (isPlayer) {
      rect(x-6,y-16,12,4,"#373047"); rect(x-4,y-18,8,3,"#373047");
      rect(x-5,y-10,4,3,"#33415e"); rect(x+1,y-10,4,3,"#33415e");
      rect(x-4,y-9,2,1,"#fff"); rect(x+2,y-9,2,1,"#fff");
      rect(x-2,y-2,4,4,"#d64e68"); rect(x-1,y-1,2,2,"#fff"); // cruz do médico
      rect(x+5,y-3,2,7,"#4d6a86"); rect(x+4,y+3,4,2,"#4d6a86"); // estetoscópio
      rect(x-5,y-4,2,3,"#d7e4ed");rect(x+3,y-4,2,3,"#d7e4ed");rect(x-5,y+5,3,1,"#9bc7c4");rect(x+2,y+5,3,1,"#9bc7c4");
    } else {
      const hair = role === "nutrition" ? "#8d514e" : role === "hygiene" ? "#60473d" : role === "doctor" ? "#544653" : role === "nurse" ? "#5d485a" : role === "reception" ? "#6a4554" : role === "surgeon" ? "#38485d" : "#574a83";
      rect(x-6,y-16,12,4,hair); rect(x-5,y-18,5,3,hair); rect(x+2,y-17,4,3,hair);
      rect(x-3,y-10,2,2,"#28334c"); rect(x+2,y-10,2,2,"#28334c");
      rect(x-2,y-7,4,1,"#bd6e76");
      rect(x-5,y-8,2,2,"#e89c91");rect(x+4,y-8,2,2,"#e89c91");
      rect(x-4,y-4,2,3,"#fff2e3");rect(x+3,y-4,2,3,"#fff2e3");
      if (role === "nutrition") { rect(x+5,y-15,4,3,"#74b86e"); rect(x+7,y-17,2,3,"#498c5e"); }
      if (role === "hygiene") { rect(x-7,y-19,14,4,"#f5f3e9"); rect(x-2,y-20,4,2,"#84d5df"); }
      if (role === "dentist") { rect(x-7,y-17,14,3,"#f8f5e9"); rect(x-1,y-16,2,2,"#df6a86"); }
      if (role === "doctor" || role === "surgeon") { rect(x-2,y-2,4,4,"#d64e68");rect(x-1,y-1,2,2,"#fff"); }
      if (role === "surgeon") { rect(x-7,y-19,14,4,"#426b80");rect(x-5,y-17,10,3,"#9fd3d0");rect(x-4,y-7,8,3,"#e8f2e7");rect(x-3,y-6,6,1,"#91bdbe"); }
      if (role === "nurse") { rect(x-7,y-19,14,4,"#f7f4e6");rect(x-2,y-20,4,2,"#e3a6bd"); }
    }
  }

  function updateNearby() {
    nearby = null; nearbyProp = null;
    let closest = 25;
    for (const patient of patients) {
      const distance = Math.hypot(patient.x-player.x, patient.y-player.y);
      if (distance < closest) {
        closest = distance;
        nearby = patient;
      }
    }
    for(const prop of interactables){const distance=Math.hypot(prop.x-player.x,prop.y-player.y);if(distance<closest&&distance<prop.range){closest=distance;nearby=null;nearbyProp=prop}}
    document.querySelector("#hint").textContent = isSitting
      ? "Aperte B para levantar"
      : nearbyProp?.kind==="medicine" ? "Aperte B para saber sobre: "+nearbyProp.name
      : nearbyProp?.kind==="seat" ? "Aperte B para sentar"
      : nearby ? "Aproxime-se: " + nearby.name
      : "Explore o hospital e encontre os pacientes";
  }

  function drawDecorations() {
    // Placas educativas e objetos decorativos em pixels.
    function poster(x,y,accent,kind) {
      rect(x,y,17,19,"#8b765f");rect(x+1,y+1,15,16,"#fff3d9");
      rect(x+3,y+3,11,2,"#b7c6c0");rect(x+3,y+6,11,1,"#d8d0bb");
      if(kind==="apple"){rect(x+6,y+10,6,5,accent);rect(x+8,y+8,2,2,"#4c8b59");rect(x+10,y+9,2,2,"#70aa63")}
      if(kind==="soap"){rect(x+6,y+10,6,5,accent);rect(x+8,y+8,2,2,"#f4ffff");rect(x+12,y+7,2,2,"#8bd9eb")}
      if(kind==="tooth"){rect(x+6,y+9,6,5,"#fff");rect(x+7,y+13,2,2,"#fff");rect(x+10,y+13,2,2,"#fff");rect(x+5,y+8,8,2,accent)}
      rect(x+1,y+17,15,2,"#715c50");
    }
    function plant(x,y) {
      rect(x+4,y+9,11,9,"#946c55");rect(x+3,y+8,13,3,"#bf9270");
      rect(x+8,y+3,3,7,"#43845d");rect(x+3,y+4,6,4,"#6ab779");rect(x+11,y+1,6,5,"#83c77b");rect(x+7,y,5,5,"#5eaa70");rect(x+1,y+7,6,3,"#8bd08b");
    }
    function lamp(x,y) {
      rect(x,y,20,4,"#f8df99");rect(x+2,y+1,16,2,"#fff7cf");rect(x+3,y+4,14,2,"#ad956b");
      if(Math.sin(performance.now()/900+x)>-.35) rect(x+4,y+6,12,1,"#ffedab55");
    }
    poster(22,43,"#e98a73","apple");poster(344,43,"#78cbe1","soap");poster(22,188,"#e8879a","tooth");poster(351,188,"#e1b761","tooth");
    plant(115,85);plant(342,203);plant(524,205);
    lamp(54,25);lamp(298,25);lamp(50,140);lamp(296,140);lamp(430,91);
    // Relógio, caixa de primeiros socorros e marcas no corredor.
    rect(187,29,17,17,"#85745f");rect(189,31,13,13,"#fff4d6");rect(195,33,1,5,"#44516c");rect(195,37,4,1,"#d65f67");rect(194,36,2,2,"#44516c");
    rect(178,143,14,12,"#f8f0dc");rect(180,145,10,8,"#d86670");rect(184,146,2,6,"#fff7e7");rect(182,148,6,2,"#fff7e7");
    [152,168,224,240,390,454].forEach((x,i)=>{rect(x,244,8,2,i%2?"#eac879":"#8fd2c5");rect(x+2,246,4,1,"#fff1cc")});

    rect(26,41,18,14,'#fff1cb'); rect(29,44,12,2,'#df8b8d'); rect(29,48,8,2,'#74b998'); rect(29,52,10,1,'#9ab0ba');
    rect(92,46,7,7,'#68a875'); rect(89,51,13,4,'#ba8065'); rect(192,25,14,14,'#f5e9c9'); rect(198,27,2,5,'#dd716f'); rect(198,33,4,2,'#536789');
    rect(29,92,12,5,'#fff3d8'); rect(31,94,8,1,'#a5c7c1'); rect(337,108,12,5,'#fff3d8'); rect(339,110,8,1,'#a5c7c1');
    rect(27,213,11,12,'#fff1cb'); rect(30,216,5,2,'#e78b91'); rect(30,220,5,2,'#70b783');
    rect(231,107,18,3,'#f6e3ad'); rect(234,108,12,1,'#fff8dc'); rect(165,24,10,3,'#f6df9a'); rect(305,24,10,3,'#f6df9a');
  }
  function draw(timestamp) {
    const now = timestamp || performance.now();
    const frameDelta = Math.min((now - lastFrameTime) / 1000, 0.05);
    lastFrameTime = now;
    move(now);
    walking = Math.hypot(player.vx, player.vy) > 8;
    if (walking) walkPhase += frameDelta * 12;
    ctx.setTransform(SCALE,0,0,SCALE,0,0);
    drawMap();
    drawDecorations();
    for (const patient of patients) {
      const role = patient.role || (patient.name.includes("Lia") ? "nutrition" : patient.name.includes("Bento") ? "hygiene" : "dentist");
      if(patient.pose==="lying") drawLyingPatient(patient.x,patient.y); else drawPerson(patient.x, patient.y, patient.color, false, role);
      if(patient.figure){if(nearby===patient)label(patient.name.split(" · ")[0],patient.x,patient.y-22,"#263653",7)}else label(patient.name.split(" · ")[0], patient.x, patient.y+22, "#263653", 8);
      if (patient.done && !patient.figure) label("✓", patient.x+10, patient.y-20, "#28734d", 9);
    }
    drawPerson(player.x, player.y, "#f5f4ed", true, "patient", isSitting);

    if (nearby && !dialogue) {
      rect(nearby.x-2, nearby.y-20, 5, 5, "#fff4d0");
      label("!", nearby.x, nearby.y-16, "#d85570");
    }
    if(nearbyProp&&!dialogue)label("B",nearbyProp.x,nearbyProp.y-17,"#d85570",8);

    const panel = document.querySelector("#dialog");
    if (dialogue) {
      panel.style.display = "block";
      document.querySelector("#speaker").textContent = dialogue.name;
      document.querySelector("#message").textContent = dialogue.lines[lineIndex];
    } else {
      panel.style.display = "none";
    }
    requestAnimationFrame(draw);
  }

  const miniGames = [
    {topic:'NUTRIÇÃO SAUDÁVEL',title:'Monte uma bandeja colorida',question:'Qual opção combina melhor variedade e equilíbrio?',answers:['Só doces e refrigerante','Arroz, feijão, legumes e uma fruta','Pular o almoço'],correct:1,success:'Isso! Variar os alimentos ajuda a incluir diferentes nutrientes. Água também é uma ótima escolha para matar a sede.'},
    {topic:'HIGIENE BÁSICA',title:'Desafio das mãos limpas',question:'Quando é especialmente importante lavar as mãos?',answers:['Antes de comer e depois de usar o banheiro','Só quando parecem sujas','Uma vez por semana'],correct:0,success:'Muito bem! Água e sabão, esfregando todas as partes das mãos, ajudam a remover sujeira e micróbios.'},
    {topic:'ESCOVAÇÃO DENTAL',title:'Escolha o kit do sorriso',question:'Qual combinação ajuda no cuidado diário dos dentes?',answers:['Escova macia e creme dental com flúor','Escova dura sem creme dental','Só enxaguar com água'],correct:0,success:'Acertou! Escove com cuidado e peça orientação a um adulto e ao dentista.'}
  ];
  const washSteps=[
    ['Molhe as mãos','Passe as mãos por água corrente. Molhe palmas, dorsos e entre os dedos.'],
    ['Aplique sabonete','Use sabonete suficiente para cobrir toda a superfície das mãos.'],
    ['Palma com palma','Junte as palmas e esfregue em movimentos circulares.'],
    ['Dorso das mãos','Esfregue a palma sobre o dorso da outra mão. Troque de lado.'],
    ['Entre os dedos','Entrelace os dedos e esfregue bem os espaços.'],
    ['Polegares, pontas e unhas','Esfregue cada polegar. Friccione pontas e unhas na palma, inclua os punhos e faça isso por cerca de 20 segundos no total.'],
    ['Enxágue bem','Enxágue em água corrente até retirar todo o sabonete.'],
    ['Seque com cuidado','Seque por completo com toalha limpa ou papel-toalha. Pronto!']
  ];
  let washIndex=0, activePatient=null;
  function renderWashStep(){const s=washSteps[washIndex];document.querySelector('#washCount').textContent=`ETAPA ${washIndex+1} DE ${washSteps.length}`;document.querySelector('#washStepTitle').textContent=s[0];document.querySelector('#washStepText').textContent=s[1];document.querySelector('#washVisual').dataset.step=washIndex;document.querySelector('#washPrev').disabled=washIndex===0;document.querySelector('#washNext').textContent=washIndex===washSteps.length-1?'MISSÃO DA ESPUMA →':'PRÓXIMA ETAPA →';}
  let plaqueSpots=[],brushActive=false,brushPatient=null;
  function startBrushGame(patient){brushPatient=patient;brushActive=false;plaqueSpots=[];const layer=document.querySelector('#toothLayer'),brush=document.querySelector('#brushCursor');layer.innerHTML='';brush.setAttribute('visibility','hidden');for(let r=0;r<2;r++)for(let c=0;c<7;c++){const x=25+c*45,y=r?98:35,t=document.createElementNS('http://www.w3.org/2000/svg','rect');t.setAttribute('x',x);t.setAttribute('y',y);t.setAttribute('width',36);t.setAttribute('height',48);t.setAttribute('rx',12);t.setAttribute('class','tooth');layer.appendChild(t);for(let m=0;m<2;m++){const d=document.createElementNS('http://www.w3.org/2000/svg','circle'),dx=x+12+m*13,dy=y+17+m*14;d.setAttribute('cx',dx);d.setAttribute('cy',dy);d.setAttribute('r',5);d.setAttribute('class','plaque');layer.appendChild(d);plaqueSpots.push({x:dx,y:dy,node:d})}}document.querySelector('#brushStatus').textContent=`Manchinhas restantes: ${plaqueSpots.length}`;document.querySelector('#brushProgress').value=0;document.querySelector('#brushStatus').classList.remove('done');document.querySelector('#brushReturn').style.display='none';document.querySelector('#brushFeedback').textContent=''}
  function brushAt(e){const b=document.querySelector('#toothBoard'),pt=b.createSVGPoint();pt.x=e.clientX;pt.y=e.clientY;const p=pt.matrixTransform(b.getScreenCTM().inverse()),brush=document.querySelector('#brushCursor');brush.setAttribute('transform',`translate(${p.x} ${p.y}) rotate(-25)`);brush.setAttribute('visibility','visible');plaqueSpots=plaqueSpots.filter(s=>{if(Math.hypot(p.x-s.x,p.y-s.y)<19){s.node.remove();return false}return true});const st=document.querySelector('#brushStatus');st.textContent=`Manchinhas restantes: ${plaqueSpots.length}`;document.querySelector('#brushProgress').value=28-plaqueSpots.length;if(!plaqueSpots.length&&!st.classList.contains('done')){st.classList.add('done');st.textContent='✨ Sorriso brilhante! ✨';if(brushPatient&&!brushPatient.done){brushPatient.done=true;document.querySelector('#score').textContent=`✚ Médico · ${patients.filter(p=>!p.figure&&p.done).length}/3 cuidados`;document.querySelector('#brushFeedback').textContent='Muito bem! Escove com movimentos suaves e peça ajuda a um adulto.';document.querySelector('#brushReturn').style.display='block'}}}
  const nutritionOptions=[{label:'🍎 Maçã · fruta',group:'colorido'},{label:'🥕 Cenoura · legume',group:'colorido'},{label:'🍚 Arroz · energia',group:'energia'},{label:'🥔 Batata · energia',group:'energia'},{label:'🫘 Feijão · proteína',group:'feijao'},{label:'🥚 Ovo · proteína',group:'feijao'},{label:'💧 Água',group:'agua'},{label:'🍭 Doce',group:'doce'}];
  function startNutritionGame(patient){const selected=new Set(),choices=document.querySelector('#foodChoices'),slots=document.querySelectorAll('#foodTray .tray-slot'),status=document.querySelector('#nutritionProgress');choices.innerHTML='';slots.forEach(slot=>{slot.classList.remove('filled');slot.textContent=slot.dataset.group==='colorido'?'🍎 Fruta ou legume':slot.dataset.group==='energia'?'🍚 Arroz ou tubérculo':slot.dataset.group==='feijao'?'🫘 Feijão ou ovo':'💧 Água'});status.textContent='0 de 4 grupos escolhidos';document.querySelector('#nutritionReturn').style.display='none';document.querySelector('#nutritionFeedback').textContent='';document.querySelector('#nutritionCheer').textContent='🌟 Ajude Lia a preparar uma bandeja campeã!';nutritionOptions.forEach(food=>{const button=document.createElement('button');button.type='button';button.textContent=food.label;button.addEventListener('click',()=>{if(!food.group||food.group==='doce'){document.querySelector('#nutritionFeedback').textContent='Escolha um alimento dos grupos pedidos para completar a bandeja.';return}if(selected.has(food.group)){document.querySelector('#nutritionFeedback').textContent='Esse grupo já está na bandeja! Escolha outro para variar.';return}selected.add(food.group);const slot=document.querySelector(`#foodTray [data-group="${food.group}"]`);slot.textContent=food.label;slot.classList.add('filled');button.disabled=true;status.textContent=`${selected.size} de 4 grupos escolhidos`;document.querySelector('#nutritionCheer').textContent=['⭐ Boa escolha!','🌈 Sua bandeja está ganhando cores!','✨ Que escolha esperta!','👏 Mais um passo para a bandeja campeã!'][selected.size-1];document.querySelector('#foodTray').classList.remove('celebrate');void document.querySelector('#foodTray').offsetWidth;document.querySelector('#foodTray').classList.add('celebrate');document.querySelector('#nutritionFeedback').textContent='Continue escolhendo um alimento diferente para cada espaço.';if(selected.size===4){patient.done=true;status.textContent='🌈 Bandeja colorida completa!';document.querySelector('#nutritionFeedback').textContent='Muito bem! Fruta ou legume, arroz ou tubérculo, feijão ou ovo e água formam uma combinação variada.';document.querySelector('#score').textContent=`✚ Médico · ${patients.filter(p=>!p.figure&&p.done).length}/3 cuidados`;document.querySelector('#nutritionReturn').style.display='block';choices.querySelectorAll('button').forEach(b=>b.disabled=true)}});choices.appendChild(button)})}  const soapParts=['Palmas','Dorso das mãos','Entre os dedos','Polegares','Pontas dos dedos e unhas','Punhos'];
  const soapPhases=[{name:'ENSABOAR',next:'ENXAGUAR AS MÃOS →'},{name:'ENXAGUAR',next:'SECAR AS MÃOS →'},{name:'SECAR',next:''}];
  let soapIndex=0,soapPhase=0,soapDragging=false;
  function resetSoapQuest(){soapIndex=0;soapPhase=0;soapDragging=false;document.querySelectorAll('.soap-target').forEach((t,i)=>{t.classList.toggle('active',i===0);t.classList.remove('cleaned')});document.querySelector('#soapDrag').setAttribute('transform','translate(180 143)');document.querySelector('#soapDrag circle').setAttribute('fill','#80d9ee');document.querySelector('#soapDrag text').textContent='🫧';document.querySelector('#soapStep').textContent='MISSÃO 1/3 · ENSABOAR · 1/6 Palmas';document.querySelector('#soapProgress').textContent='Ensaboe cada parte das mãos';document.querySelector('#soapFeedback').textContent='';document.querySelector('#soapPhaseNext').style.display='none';document.querySelector('#soapPhaseNext').textContent=soapPhases[0].next;document.querySelector('#soapReturn').style.display='none'}
  function advanceSoapPhase(){if(soapPhase>=2)return;soapPhase++;soapIndex=0;document.querySelectorAll('.soap-target').forEach((t,i)=>{t.classList.remove('cleaned','active');if(i===0)t.classList.add('active')});document.querySelector('#soapDrag').setAttribute('transform','translate(180 143)');document.querySelector('#soapPhaseNext').style.display='none';document.querySelector('#soapPhaseNext').textContent=soapPhases[soapPhase].next;const soapCircle=document.querySelector('#soapDrag circle');soapCircle.setAttribute('fill',soapPhase===0?'#80d9ee':soapPhase===1?'#78c9f2':'#fff1c9');document.querySelector('#soapDrag text').textContent=soapPhase===0?'🫧':soapPhase===1?'💧':'🧻';document.querySelector('#soapStep').textContent='MISSÃO '+(soapPhase+1)+'/3 · '+soapPhases[soapPhase].name+' · 1/6 '+soapParts[0];document.querySelector('#soapProgress').textContent=soapPhase===1?'Agora tire todo o sabonete com água!':'Agora seque cada parte com uma toalha limpa!';document.querySelector('#soapFeedback').textContent=soapPhase===1?'Passe por todas as partes mais uma vez, como se a água estivesse levando a espuma.':'Última missão! Passe a toalha por todos os pontos.'}
  function moveSoap(e){const board=document.querySelector('#soapBoard'),pt=board.createSVGPoint();pt.x=e.clientX;pt.y=e.clientY;const p=pt.matrixTransform(board.getScreenCTM().inverse());document.querySelector('#soapDrag').setAttribute('transform','translate('+p.x+' '+p.y+')');const target=document.querySelector('.soap-target[data-zone="'+soapIndex+'"]');if(target&&Math.hypot(p.x-Number(target.getAttribute('cx')),p.y-Number(target.getAttribute('cy')))<23){target.classList.remove('active');target.classList.add('cleaned');soapIndex++;document.querySelector('#soapProgress').textContent=soapIndex+' de '+soapParts.length+' partes · '+soapPhases[soapPhase].name.toLowerCase();if(soapIndex===soapParts.length){if(soapPhase<2){document.querySelector('#soapStep').textContent='✨ '+soapPhases[soapPhase].name+' completo!';document.querySelector('#soapFeedback').textContent=soapPhase===0?'Espuma em todos os cantinhos! Agora vamos enxaguar.':'Sabonete removido! Agora vamos secar direitinho.';document.querySelector('#soapPhaseNext').style.display='block'}else{document.querySelector('#soapStep').textContent='🏆 Mãos limpas, enxaguadas e sequinhas!';document.querySelector('#soapProgress').textContent='3 missões completas · 18 partes cuidadas';document.querySelector('#soapFeedback').textContent='Mandou muito bem! Lavar, enxaguar e secar ajuda a cuidar da saúde.';if(activePatient&&!activePatient.done){activePatient.done=true;document.querySelector('#score').textContent='✚ Médico · '+patients.filter(p=>!p.figure&&p.done).length+'/3 cuidados';document.querySelector('#soapReturn').style.display='block'}}}else{document.querySelector('.soap-target[data-zone="'+soapIndex+'"]').classList.add('active');document.querySelector('#soapStep').textContent='MISSÃO '+(soapPhase+1)+'/3 · '+soapPhases[soapPhase].name+' · '+(soapIndex+1)+'/6 '+soapParts[soapIndex]}}}
  document.querySelector('#soapPhaseNext').addEventListener('click',advanceSoapPhase);
  const soapBoard=document.querySelector('#soapBoard'),soapDrag=document.querySelector('#soapDrag');soapDrag.addEventListener('pointerdown',e=>{e.preventDefault();soapDragging=true;soapBoard.setPointerCapture(e.pointerId);moveSoap(e)});soapBoard.addEventListener('pointermove',e=>{if(soapDragging)moveSoap(e)});['pointerup','pointercancel','lostpointercapture'].forEach(t=>soapBoard.addEventListener(t,()=>soapDragging=false));  const toothBoard=document.querySelector('#toothBoard');toothBoard.addEventListener('pointerdown',e=>{e.preventDefault();brushActive=true;toothBoard.setPointerCapture(e.pointerId);brushAt(e)});toothBoard.addEventListener('pointermove',e=>{if(brushActive)brushAt(e)});['pointerup','pointercancel','lostpointercapture'].forEach(t=>toothBoard.addEventListener(t,()=>brushActive=false));  function openMiniGame(patient) {
    activePatient=patient;const isNutrition=patient.name.includes("Nutrição"),isWash=patient.name.includes("Higiene"),isBrush=patient.name.includes("Dentista")||patient.name.includes("Odontologia"),game=miniGames[isWash?1:isBrush?2:0];
    if(isNutrition){document.querySelector("#nutritionGame").style.display="block";startNutritionGame(patient);document.querySelector("#challenge").style.display="none";document.querySelector("#nutritionChallenge").style.display="grid";return;}
    if(isBrush){document.querySelector("#brushGame").style.display="block";startBrushGame(patient);document.querySelector("#challenge").style.display="none";document.querySelector("#brushChallenge").style.display="grid";return;}
    document.querySelector('#topic').textContent=game.topic;document.querySelector('#challengeTitle').textContent=isNutrition?'Monte uma bandeja colorida!':isWash?'Lave as mãos passo a passo':isBrush?'Escove todos os dentinhos!':game.title;document.querySelector('#question').textContent=game.question;document.querySelector('#question').style.display=(isNutrition||isWash||isBrush)?'none':'block';document.querySelector('#feedback').textContent='';document.querySelector('#returnHospital').style.display='none';document.querySelector('#choices').style.display=(isNutrition||isWash||isBrush)?'none':'grid';document.querySelector('#washGame').style.display=isWash?'block':'none';document.querySelector('#brushGame').style.setProperty('display',isBrush?'block':'none','important');document.querySelector('#nutritionGame').style.display=isNutrition?'block':'none';
    if(isNutrition)startNutritionGame(patient);
    if(isWash){washIndex=0;document.querySelector('#washPrev').disabled=false;document.querySelector('#washNext').disabled=false;renderWashStep();}
    if(isBrush){startBrushGame(patient);document.querySelector('#toothBoard').style.display='block';}
    const list=document.querySelector('#choices');list.innerHTML='';if(!isNutrition&&!isWash&&!isBrush)game.answers.forEach((answer,index)=>{const button=document.createElement('button');button.textContent='▸ '+answer;button.onclick=()=>{const feedback=document.querySelector('#feedback');if(index!==game.correct){feedback.textContent='Quase! Pense no cuidado mais completo e tente outra opção.';button.style.borderColor='#ff91a8';return}feedback.textContent=game.success;patient.done=true;const count=patients.filter(p=>!p.figure&&p.done).length;document.querySelector('#score').textContent=`✚ Médico · ${count}/3 cuidados`;document.querySelector('#returnHospital').style.display='block';for(const choice of list.querySelectorAll('button'))choice.disabled=true};list.appendChild(button)});document.querySelector('#challenge').style.display='grid';
  }
  function actionB(){
    const soapChallenge=document.querySelector('#soapChallenge');if(soapChallenge.style.display==='grid'){const back=document.querySelector('#soapReturn');if(back.style.display!=='none'){back.click();return;}soapChallenge.style.display='none';soapDragging=false;updateNearby();return;}
    const nutritionChallenge=document.querySelector('#nutritionChallenge');if(nutritionChallenge.style.display==='grid'){const back=document.querySelector('#nutritionReturn');if(back.style.display!=='none'){back.click();return;}nutritionChallenge.style.display='none';updateNearby();return;}
    const brushChallenge=document.querySelector('#brushChallenge');
    if(brushChallenge.style.display==='grid'){const back=document.querySelector('#brushReturn');if(back.style.display!=='none'){back.click();return;}brushChallenge.style.display='none';brushActive=false;updateNearby();return;}
    const challenge=document.querySelector('#challenge');
    if(challenge.style.display==='grid'){
      const returnButton=document.querySelector('#returnHospital');
      if(returnButton.style.display!=='none'){returnButton.click();return;}
      document.querySelector('#brushCursor').setAttribute('visibility','hidden');
      challenge.style.display='none';brushActive=false;dialogue=null;lineIndex=0;updateNearby();return;
    }
    talk();
  }  function talk() {
    if (!started || (document.querySelector('#challenge').style.display === 'grid'||document.querySelector('#brushChallenge').style.display === 'grid'||document.querySelector('#nutritionChallenge').style.display === 'grid'||document.querySelector('#soapChallenge').style.display === 'grid')) return;
    if(isSitting){isSitting=false;player.vx=0;player.vy=0;updateNearby();return;}
    if (dialogue) { lineIndex++; if (lineIndex >= dialogue.lines.length) { const patient=dialogue; dialogue=null; lineIndex=0; if(!patient.figure&&!patient.done) openMiniGame(patient); } return; }
    updateNearby();
    if(nearbyProp){if(nearbyProp.kind==="seat"){isSitting=true;player.x=nearbyProp.x;player.y=nearbyProp.y;player.vx=0;player.vy=0;updateNearby();return;}dialogue={...nearbyProp,figure:true};lineIndex=0;return;}
    if (nearby && (!nearby.done || nearby.figure)) { dialogue=nearby; lineIndex=0; }
  }
  function move(now = performance.now()) {
    const dt = Math.min((now - lastMoveTime) / 1000, 0.04);
    lastMoveTime = now;
    let dx = 0, dy = 0;
    const canMove = started && !dialogue && !isSitting && document.querySelector('#challenge').style.display !== 'grid'&&document.querySelector('#brushChallenge').style.display !== 'grid'&&document.querySelector('#nutritionChallenge').style.display !== 'grid'&&document.querySelector('#soapChallenge').style.display !== 'grid';
    if (canMove) {
      if (keys.has('ArrowLeft') || keys.has('a')) dx--;
      if (keys.has('ArrowRight') || keys.has('d')) dx++;
      if (keys.has('ArrowUp') || keys.has('w')) dy--;
      if (keys.has('ArrowDown') || keys.has('s')) dy++;
    }
    if (dx && dy) { dx *= Math.SQRT1_2; dy *= Math.SQRT1_2; }
    const response=1-Math.exp(-10*dt),speed=100;
    player.vx+=(dx*speed-player.vx)*response;player.vy+=(dy*speed-player.vy)*response;
    const collides=(x,y)=>{
      // Hitbox compacta deixa atravessar portas estreitas sem remover as paredes.
      const box={x:x-3.5,y:y-4,w:7,h:8};
      return walls.some(w=>box.x<w.x+w.w&&box.x+box.w>w.x&&box.y<w.y+w.h&&box.y+box.h>w.y)||patients.some(p=>Math.hypot(p.x-x,p.y-y)<8.5);
    };
    const distance=Math.max(Math.abs(player.vx*dt),Math.abs(player.vy*dt)),steps=Math.max(1,Math.ceil(distance/2)),stepTime=dt/steps;
    for(let i=0;i<steps;i++){
      const nextX=player.x+player.vx*stepTime;if(!collides(nextX,player.y))player.x=nextX;else player.vx=0;
      const nextY=player.y+player.vy*stepTime;if(!collides(player.x,nextY))player.y=nextY;else player.vy=0;
    }
    updateNearby();
  }

  // Melodia original simples, sintetizada no navegador.
  function startMusic() {
    if (!audio) audio = new (window.AudioContext || window.webkitAudioContext)();
    const notes = [392,440,523,440,349,392,440,330,392,494,440,392,330,349,392,262];
    let i = 0;
    function playNote() {
      if (!musicOn) return;
      const osc = audio.createOscillator();
      const gain = audio.createGain();
      const time = audio.currentTime;
      osc.type = "square";
      osc.frequency.value = notes[i++ % notes.length];
      gain.gain.setValueAtTime(0.0001, time);
      gain.gain.exponentialRampToValueAtTime(0.035, time + 0.015);
      gain.gain.exponentialRampToValueAtTime(0.0001, time + 0.19);
      osc.connect(gain).connect(audio.destination);
      osc.start(time);
      osc.stop(time + 0.2);
      setTimeout(playNote, 220);
    }
    playNote();
  }

  function playVictoryTune() {
    if (!musicOn || !audio || victoryPlayed) return;
    victoryPlayed = true;
    audio.resume();
    const notes=[523.25,659.25,783.99,1046.5,783.99,880,1046.5,1318.5,1046.5];
    const start=audio.currentTime+0.08;
    notes.forEach((frequency,index)=>{
      const osc=audio.createOscillator(),gain=audio.createGain(),time=start+index*0.17;
      osc.type="square";osc.frequency.setValueAtTime(frequency,time);
      gain.gain.setValueAtTime(0.0001,time);gain.gain.exponentialRampToValueAtTime(0.045,time+0.015);gain.gain.exponentialRampToValueAtTime(0.0001,time+0.15);
      osc.connect(gain).connect(audio.destination);osc.start(time);osc.stop(time+0.16);
    });
  }
  function showEnding() {
    document.querySelector('#ending').style.display='grid';
    playVictoryTune();
  }

  document.addEventListener("keydown", event => {
    const focusedControl=event.target instanceof HTMLElement&&(event.target.matches('input,textarea,select,button')||event.target.isContentEditable);
    if(focusedControl)return;
    if ([" ","ArrowUp","ArrowDown","ArrowLeft","ArrowRight"].includes(event.key)) event.preventDefault();
    if (event.key === " " || event.key === "Enter") { talk(); return; }
    if (event.key.toLowerCase() === "b") { event.preventDefault(); actionB(); return; }
    keys.add(event.key.toLowerCase());
  });
  document.addEventListener("keyup", event => keys.delete(event.key.toLowerCase()));

  document.querySelectorAll("[data-key]").forEach(button => {
    const key = button.dataset.key;
    button.addEventListener("pointerdown", event => { event.preventDefault(); keys.add(key); });
    ["pointerup","pointerleave","pointercancel"].forEach(type =>
      button.addEventListener(type, () => keys.delete(key))
    );
  });

  document.querySelector("#buttonA").addEventListener("click", talk);
  document.querySelector("#buttonB").addEventListener("click", actionB);

  document.querySelector('#soapReturn').addEventListener('click',()=>{document.querySelector('#soapChallenge').style.display='none';if(patients.filter(p=>!p.figure).every(p=>p.done))setTimeout(showEnding,350);else updateNearby();});
  document.querySelector('#nutritionReturn').addEventListener('click',()=>{document.querySelector('#nutritionChallenge').style.display='none';if(patients.filter(p=>!p.figure).every(p=>p.done))setTimeout(showEnding,350);else updateNearby();});
  document.querySelector('#brushReturn').addEventListener('click',()=>{document.querySelector('#brushChallenge').style.display='none';if(patients.filter(p=>!p.figure).every(p=>p.done))setTimeout(showEnding,350);else updateNearby();});
  document.querySelector('#washPrev').addEventListener('click',()=>{if(washIndex>0){washIndex--;renderWashStep();}});
    document.querySelector('#washNext').addEventListener('click',()=>{
    if(washIndex<washSteps.length-1){washIndex++;renderWashStep();return;}
    document.querySelector('#challenge').style.display='none';resetSoapQuest();document.querySelector('#soapChallenge').style.display='grid';
  });document.querySelector('#returnHospital').addEventListener('click', () => {
    document.querySelector('#challenge').style.display='none';
    if (patients.filter(p=>!p.figure).every(p=>p.done)) setTimeout(showEnding,350);
    else updateNearby();
  });
  document.querySelector("#claimAward").addEventListener("click",()=>{
    const name=document.querySelector("#awardName").value.trim();
    document.querySelector("#certificateName").textContent=name||"Pequeno(a) Guardião(ã)";
    document.querySelector("#certificate").style.display="block";
    document.querySelector("#awardName").style.display="none";
    document.querySelector("#claimAward").style.display="none";
    document.querySelector("#awardMessage").textContent="Certificado conquistado! Que bom cuidar da saúde!";
  });
  document.querySelector("#start").addEventListener("click", () => {
    started = true;
    document.querySelector("#intro").style.display = "none";
    startMusic();
  });

  document.querySelector("#music").addEventListener("click", event => {
    musicOn = !musicOn;
    event.currentTarget.textContent = "♫ Música " + (musicOn ? "ligada" : "desligada");
    if (audio) {
      if (musicOn) { audio.resume(); startMusic(); }
      else audio.suspend();
    }
  });

  updateNearby();
  draw();
})();
</script>
</body>
</html>




















