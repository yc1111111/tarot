# tarot
[index.html](https://github.com/user-attachments/files/24352158/index.html)
<!doctype html>
<html lang="zh-CN">
<head>
<meta charset="utf-8"/>
<meta name="viewport" content="width=device-width,initial-scale=1"/>
<title>Jungian Tarot Mentor · RWS 78 · Professional Single-File Prototype</title>

<style>
:root{
  --bg:#0b0f14;
  --panel:#111826;
  --panel2:#0f1723;
  --text:#e6edf6;
  --muted:#9fb0c3;
  --accent:#7dd3fc;
  --accent2:#a78bfa;
  --ok:#34d399;
  --warn:#fbbf24;
  --border:rgba(255,255,255,.12);
  --border2:rgba(255,255,255,.08);
  --radius:16px;

  --cardW:114px;
  --cardH:192px;

  --shadow:0 10px 30px rgba(0,0,0,.35);
}

*{box-sizing:border-box}
html,body{height:100%}
body{
  margin:0;background:
    radial-gradient(1100px 600px at 10% 0%, rgba(125,211,252,.10), transparent 55%),
    radial-gradient(900px 520px at 90% 20%, rgba(167,139,250,.10), transparent 55%),
    var(--bg);
  color:var(--text);
  font-family:system-ui,-apple-system,"PingFang SC","Microsoft YaHei",Segoe UI,Roboto,Helvetica,Arial;
  letter-spacing:.2px;
}

a{color:inherit}
h1,h2,h3{margin:0}
small{color:var(--muted)}
kbd{
  font-family:ui-monospace,SFMono-Regular,Menlo,Monaco,Consolas,"Liberation Mono","Courier New",monospace;
  font-size:12px;
  padding:2px 6px;
  border:1px solid var(--border);
  border-bottom-color:rgba(255,255,255,.06);
  border-radius:8px;
  background:rgba(255,255,255,.04);
}

main{
  max-width:1280px;
  margin:auto;
  padding:18px;
  display:grid;
  grid-template-columns: 420px 1fr;
  gap:14px;
}
@media(max-width:1020px){
  main{grid-template-columns:1fr}
}

.panel{
  background:linear-gradient(180deg, rgba(255,255,255,.03), transparent 35%), var(--panel);
  border:1px solid var(--border);
  border-radius:var(--radius);
  padding:14px;
  box-shadow:var(--shadow);
}

.header{
  display:flex;
  align-items:flex-start;
  justify-content:space-between;
  gap:10px;
}
.brandTitle{
  font-size:16px;
  font-weight:800;
  line-height:1.2;
}
.brandSub{
  margin-top:6px;
  font-size:12px;
  color:var(--muted);
  line-height:1.55;
}

.langSwitch{display:flex; gap:8px; align-items:center;}
.langSwitch button{
  width:auto;
  padding:8px 10px;
  border-radius:10px;
  border:1px solid var(--border);
  background:rgba(255,255,255,.04);
  color:var(--text);
  cursor:pointer;
}
.langSwitch button.active{
  border-color:rgba(125,211,252,.45);
  background:rgba(125,211,252,.12);
}

label{
  display:block;
  font-size:12px;
  color:var(--muted);
  margin-top:12px;
}

textarea,select,button,input{
  width:100%;
  margin-top:6px;
  padding:10px 10px;
  background:var(--panel2);
  color:var(--text);
  border:1px solid var(--border);
  border-radius:12px;
  outline:none;
}
textarea{min-height:76px; resize:vertical; line-height:1.5;}
select{cursor:pointer}
button{
  cursor:pointer;
  transition:transform .05s ease, background .15s ease, border-color .15s ease;
}
button:active{transform:translateY(1px)}
button.primary{border-color:rgba(125,211,252,.45); background:rgba(125,211,252,.12);}
button.secondary{border-color:rgba(167,139,250,.45); background:rgba(167,139,250,.10);}
button.good{border-color:rgba(52,211,153,.35); background:rgba(52,211,153,.10);}
button:disabled{opacity:.55; cursor:not-allowed;}

.row2{display:grid; grid-template-columns:1fr 1fr; gap:10px;}
.row3{display:grid; grid-template-columns:1fr 1fr 1fr; gap:10px;}

.hint{
  margin-top:10px;
  border:1px solid var(--border2);
  border-radius:12px;
  padding:10px;
  background:rgba(255,255,255,.03);
  color:var(--muted);
  font-size:12px;
  line-height:1.65;
}
.hint b{color:rgba(230,237,246,.95)}
.hr{height:1px;background:rgba(255,255,255,.08); margin:10px 0;}

.badgePill{
  display:inline-flex; align-items:center; gap:6px;
  font-size:11px; color:rgba(230,237,246,.9);
  padding:4px 8px; border-radius:999px;
  border:1px solid rgba(255,255,255,.14);
  background:rgba(255,255,255,.04);
}
.dot{width:8px; height:8px; border-radius:999px; background:rgba(125,211,252,.8); display:inline-block;}
.dot.ok{background:rgba(52,211,153,.85)}
.dot.warn{background:rgba(251,191,36,.85)}

.boardTitleRow{
  display:flex; align-items:center; justify-content:space-between; gap:10px;
  margin-bottom:10px;
}
.boardTitle{font-size:14px; font-weight:800;}
.boardMeta{font-size:12px; color:var(--muted); line-height:1.4;}

.board{
  position:relative;
  height:720px;
  border:1px dashed rgba(255,255,255,.18);
  border-radius:var(--radius);
  background:
    radial-gradient(420px 420px at 50% 50%, rgba(255,255,255,.04), transparent 70%),
    radial-gradient(600px 420px at 30% 20%, rgba(125,211,252,.06), transparent 60%),
    radial-gradient(600px 420px at 70% 80%, rgba(167,139,250,.05), transparent 60%);
  overflow:hidden;
}
@media(max-width:1020px){.board{height:660px}}

.slot{
  position:absolute;
  width:var(--cardW);
  height:var(--cardH);
  transform:translate(-50%,-50%);
}

.card{
  width:100%;
  height:100%;
  border-radius:14px;
  overflow:hidden;
  border:1px solid rgba(255,255,255,.18);
  background:#000;
  box-shadow:0 14px 30px rgba(0,0,0,.45);
  cursor:pointer;
  position:relative;
}
.card.empty{
  background:linear-gradient(180deg, rgba(255,255,255,.04), rgba(255,255,255,.02));
  border-style:solid;
  cursor:default;
}
.card img{width:100%; height:100%; object-fit:cover; display:block;}
.rev img{transform:rotate(180deg)}
.badge{
  position:absolute;
  top:8px; left:8px;
  font-size:11px;
  padding:4px 8px;
  border:1px solid rgba(255,255,255,.18);
  border-radius:999px;
  background:rgba(0,0,0,.35);
  color:rgba(230,237,246,.92);
  backdrop-filter: blur(6px);
}

.slotLabel{
  position:absolute;
  width:170%;
  left:50%;
  transform:translateX(-50%);
  bottom:-34px;
  text-align:center;
  font-size:11px;
  color:var(--muted);
  white-space:nowrap;
}
.slotMeaning{
  position:absolute;
  width:190%;
  left:50%;
  transform:translateX(-50%);
  bottom:-52px;
  text-align:center;
  font-size:10px;
  color:rgba(159,176,195,.88);
  white-space:nowrap;
  opacity:.85;
}

.analysisGrid{display:grid; grid-template-columns: 1fr; gap:10px; margin-top:8px;}
.interpItem{
  border:1px solid var(--border2);
  border-radius:14px;
  padding:10px 10px;
  background:rgba(255,255,255,.02);
}
.interpHead{
  display:flex;
  align-items:flex-start;
  justify-content:space-between;
  gap:10px;
}
.interpHead b{font-size:13px; line-height:1.35}
.tag{
  font-size:11px;
  color:rgba(230,237,246,.85);
  padding:3px 8px;
  border-radius:999px;
  border:1px solid rgba(255,255,255,.14);
  background:rgba(255,255,255,.04);
}
.kv{
  margin-top:8px;
  font-size:12px;
  line-height:1.65;
}
.kv .k{
  color:var(--muted);
  display:inline-block;
  min-width:130px;
}
.sep{height:1px; background:rgba(255,255,255,.08); margin:10px 0;}

textarea.readonly{
  min-height:240px;
  font-family:ui-monospace,SFMono-Regular,Menlo,Monaco,Consolas,"Liberation Mono","Courier New",monospace;
  font-size:12px;
  line-height:1.55;
}

.toast{
  position:fixed;
  bottom:18px; left:50%;
  transform:translateX(-50%);
  background:rgba(15,23,35,.92);
  border:1px solid rgba(255,255,255,.14);
  color:rgba(230,237,246,.95);
  padding:10px 12px;
  border-radius:14px;
  box-shadow:0 14px 30px rgba(0,0,0,.45);
  font-size:12px;
  opacity:0;
  pointer-events:none;
  transition:opacity .2s ease, transform .2s ease;
}
.toast.show{opacity:1; transform:translateX(-50%) translateY(-2px);}

.noteBox{
  border:1px solid rgba(255,255,255,.10);
  border-radius:14px;
  padding:10px;
  background:rgba(255,255,255,.03);
  margin-top:10px;
}
.noteBox h3{font-size:13px; margin:0 0 6px 0;}
.noteBox p{margin:0; color:var(--muted); font-size:12px; line-height:1.65;}
</style>
</head>

<body>
<main>

  <!-- LEFT -->
  <section class="panel">
    <div class="header">
      <div>
        <div class="brandTitle" id="brandTitle">Jungian Tarot Mentor</div>
        <div class="brandSub" id="brandSub">
          以荣格心理学为底层：塔罗作为投射性符号系统，用于意义建构、补偿机制识别与可执行反思（不做宿命论预测）。
        </div>
      </div>
      <div class="langSwitch">
        <button id="btnZh" onclick="setLang('zh')" class="active">中文</button>
        <button id="btnEn" onclick="setLang('en')">EN</button>
      </div>
    </div>

    <div style="display:flex; gap:8px; flex-wrap:wrap; margin-top:10px">
      <span class="badgePill"><span class="dot ok"></span><span id="pillDeck">RWS 78</span></span>
      <span class="badgePill"><span class="dot"></span><span id="pillJung">Jungian</span></span>
      <span class="badgePill"><span class="dot warn"></span><span id="pillNoFate">No-fatalism</span></span>
    </div>

    <label id="l_intent">咨询主题 / 意图</label>
    <textarea id="intent" placeholder="例：我在关系里反复陷入同一种模式，我想知道我在回避什么，以及下一步可以怎么做。"></textarea>

    <label id="l_spread">牌阵</label>
    <select id="spreadSelect"></select>

    <div class="row2">
      <div>
        <label id="l_orientMode">正/逆位规则</label>
        <select id="orientMode">
          <option value="random">随机正逆（推荐）</option>
          <option value="upright">全部正位（教学/训练）</option>
          <option value="none">不显示正逆（只看图像）</option>
        </select>
      </div>
      <div>
        <label id="l_drawPolicy">抽牌策略</label>
        <select id="drawPolicy">
          <option value="withoutReplacement">无放回（专业标准）</option>
          <option value="withReplacement">可放回（占卜实验用）</option>
        </select>
      </div>
    </div>

    <div class="hr"></div>

    <label id="l_ritual">导师式流程（洗牌 → 切牌 → 抽牌）</label>
    <div class="row3" style="margin-top:8px">
      <button class="primary" onclick="startShuffle()" id="b_shuffle">1) 洗牌</button>
      <button onclick="startCut()" id="cutBtn" disabled>2) 切牌</button>
      <button class="good" onclick="drawAll()" id="drawBtn" disabled>3) 抽牌</button>
    </div>

    <div class="row2" style="margin-top:10px">
      <button class="secondary" onclick="resetSession()" id="resetBtn">重置</button>
      <button onclick="copyPrompt()" id="copyBtn" disabled>复制 AI Prompt</button>
    </div>

    <div class="hint" id="hintBox">
      <div><b id="hintTitle">使用方式（导师版）</b></div>
      <div id="hintBody" style="margin-top:6px">
        1) 先写“意图”：用一句话定义你想理解的心理张力；2) 洗牌：把注意力放在主题上（不是祈求结果）；3) 切牌：象征把无意识材料“分层”；4) 抽牌：让牌位成为一个结构化镜子；5) 解牌：关注原型动力、补偿机制、阴影/礼物与可执行行动。
      </div>
      <div style="margin-top:8px">
        <span id="hintHotkey">提示：</span>
        <kbd>Click</kbd> <span id="hintClick">点击牌面可切换正/逆位（用于探索角度，不代表吉凶）。</span>
      </div>
      <div style="margin-top:8px">
        <span class="badgePill"><span class="dot"></span><span id="sessionPill">会话未开始</span></span>
      </div>
    </div>

    <div class="noteBox" id="cutBox" style="display:none">
      <h3 id="cutTitle">切牌（象征“分层”）</h3>
      <p id="cutBody">请选择切牌方式：把牌堆分成三叠，然后选择你直觉要作为“起点”的那一叠。系统会据此重组牌堆。</p>
      <div class="row3" style="margin-top:10px">
        <button onclick="chooseCut(0)" id="cutA">左</button>
        <button onclick="chooseCut(1)" id="cutB">中</button>
        <button onclick="chooseCut(2)" id="cutC">右</button>
      </div>
      <p style="margin-top:10px" id="cutNote"><small>提示：切牌不是“选幸运”，而是让你参与把主题从无意识带入结构。</small></p>
    </div>

  </section>

  <!-- RIGHT -->
  <section>
    <div class="panel">
      <div class="boardTitleRow">
        <div>
          <div class="boardTitle" id="spreadTitle">—</div>
          <div class="boardMeta" id="spreadMeta">—</div>
        </div>
        <div class="boardMeta" id="sessionMeta">—</div>
      </div>

      <div class="board" id="board" aria-label="Tarot board"></div>
    </div>

    <div class="panel" style="margin-top:12px">
      <div class="boardTitleRow">
        <div class="boardTitle" id="l_analysis">导师级解析（逐位 + 总结整合）</div>
        <div class="boardMeta" id="analysisMeta">Structured · Jungian</div>
      </div>

      <div class="analysisGrid" id="interp"></div>

      <div class="sep"></div>

      <label id="l_prompt">AI Prompt（可直接用于大模型）</label>
      <textarea id="aiPrompt" class="readonly" readonly></textarea>
    </div>
  </section>

</main>

<div class="toast" id="toast">Copied</div>

<script>
/* =========================================================
   I18N
========================================================= */
let LANG = "zh";

const I18N = {
  zh: {
    brandTitle: "Jungian Tarot Mentor（荣格塔罗导师）",
    brandSub: "以荣格心理学为底层：塔罗作为投射性符号系统，用于意义建构、补偿机制识别与可执行反思（不做宿命论预测）。",
    pills: { deck:"RWS 78", jung:"荣格取向", noFate:"非宿命论" },

    intent: "咨询主题 / 意图",
    intentPH: "例：我在关系里反复陷入同一种模式，我想知道我在回避什么，以及下一步可以怎么做。",
    spread: "牌阵",
    orientMode: "正/逆位规则",
    drawPolicy: "抽牌策略",

    ritual: "导师式流程（洗牌 → 切牌 → 抽牌）",
    shuffle: "1) 洗牌",
    cut: "2) 切牌",
    draw: "3) 抽牌",
    reset: "重置",
    copy: "复制 AI Prompt",

    usage: "使用方式（导师版）",
    usageBody: "1) 写清“意图”：一句话定义你要理解的心理张力；2) 洗牌：把注意力放在主题上（不是祈求结果）；3) 切牌：象征把无意识材料分层；4) 抽牌：让牌位成为结构化镜子；5) 解牌：关注原型动力、补偿机制、阴影/礼物与可执行行动。",
    hint: "提示：",
    click: "点击牌面可切换正/逆位（用于探索角度，不代表吉凶）。",
    sessionIdle: "会话未开始",
    sessionShuffled: "已洗牌",
    sessionCut: "已切牌",
    sessionDrawn: "已抽牌",
    orientationUpright: "正位",
    orientationReversed: "逆位",
    orientationNone: "不显示正逆",

    analysis: "导师级解析（逐位 + 总结整合）",
    analysisMeta: "结构化 · 荣格框架",
    prompt: "AI Prompt（可直接用于大模型）",

    cutTitle:"切牌（象征“分层”）",
    cutBody:"请选择切牌方式：把牌堆分成三叠，然后选择你直觉要作为“起点”的那一叠。系统会据此重组牌堆。",
    cutLeft:"左", cutMid:"中", cutRight:"右",
    cutNote:"提示：切牌不是“选幸运”，而是让你参与把主题从无意识带入结构。",

    spreadMetaTpl:(n)=>`RWS 78 · ${n} 位置 · （点击牌切换正/逆位）`,
    sessionMetaTpl:(time, state)=>`${time} · ${state}`,

    fields:{
      posMeaning:"牌位含义",
      cardLayer:"牌义层（符号 → 心理）",
      archetype:"核心原型",
      dynamics:"心理动力",
      compensation:"可能的补偿",
      shadowGift:"阴影 / 礼物",
      practice:"行动练习",
      question:"反思问题",
      suitRank:"结构信息"
    },

    synthesisTitle:"整合总结（导师视角）",
    synthesisFocus:"主题焦点",
    synthesisPattern:"可能的重复模式",
    synthesisShadow:"阴影与礼物",
    synthesisPlan:"行动计划（24h / 7d / 30d）",

    promptRole:"Role",
    promptContext:"Context",
    promptCards:"Cards (Positioned)",
    promptConstraints:"Constraints",
    promptOutput:"Output Format",

    suits:{
      Wands:"权杖（意志/行动）",
      Cups:"圣杯（情感/关系）",
      Swords:"宝剑（认知/冲突）",
      Pentacles:"星币（现实/价值）"
    }
  },
  en: {
    brandTitle: "Jungian Tarot Mentor",
    brandSub: "Tarot (RWS) as a projective symbolic tool: meaning-making, compensation patterns, shadow integration, and actionable reflection (no fatalistic prediction).",
    pills: { deck:"RWS 78", jung:"Jungian", noFate:"No-fatalism" },

    intent: "Consultation Topic / Intent",
    intentPH: "Example: I repeat the same pattern in relationships. What am I avoiding, and what can I do next?",
    spread: "Spread",
    orientMode: "Orientation rule",
    drawPolicy: "Draw policy",

    ritual: "Mentor flow (Shuffle → Cut → Draw)",
    shuffle: "1) Shuffle",
    cut: "2) Cut",
    draw: "3) Draw",
    reset: "Reset",
    copy: "Copy AI Prompt",

    usage: "How to use (mentor style)",
    usageBody: "1) Write a clear intent (one sentence); 2) Shuffle while holding attention on the theme (not outcomes); 3) Cut to symbolize layering unconscious material; 4) Draw into a structured mirror (the spread); 5) Interpret via archetypes, compensation, shadow/gift, and concrete actions.",
    hint: "Tip:",
    click: "Click a card to toggle upright/reversed (explore angles; not good/bad).",
    sessionIdle: "Session not started",
    sessionShuffled: "Shuffled",
    sessionCut: "Cut complete",
    sessionDrawn: "Drawn",
    orientationUpright: "Upright",
    orientationReversed: "Reversed",
    orientationNone: "Hidden",

    analysis: "Mentor Analysis (per-position + synthesis)",
    analysisMeta: "Structured · Jungian",
    prompt: "AI Prompt (ready for LLMs)",

    cutTitle:"Cut (symbolic layering)",
    cutBody:"Choose a cut: split into three piles and select the pile that feels like the 'start'. The deck will be reassembled accordingly.",
    cutLeft:"Left", cutMid:"Middle", cutRight:"Right",
    cutNote:"Tip: Cutting is not luck-picking; it is your participation in structuring the material.",

    spreadMetaTpl:(n)=>`RWS 78 · ${n} positions · (click card to toggle orientation)`,
    sessionMetaTpl:(time, state)=>`${time} · ${state}`,

    fields:{
      posMeaning:"Position meaning",
      cardLayer:"Card layer (symbol → psyche)",
      archetype:"Archetype",
      dynamics:"Dynamics",
      compensation:"Compensation",
      shadowGift:"Shadow / Gift",
      practice:"Practice",
      question:"Reflection",
      suitRank:"Structure"
    },

    synthesisTitle:"Synthesis (mentor lens)",
    synthesisFocus:"Core focus",
    synthesisPattern:"Likely repeating pattern",
    synthesisShadow:"Shadow & gift",
    synthesisPlan:"Action plan (24h / 7d / 30d)",

    promptRole:"Role",
    promptContext:"Context",
    promptCards:"Cards (Positioned)",
    promptConstraints:"Constraints",
    promptOutput:"Output Format",

    suits:{
      Wands:"Wands (will/action)",
      Cups:"Cups (emotion/relating)",
      Swords:"Swords (mind/conflict)",
      Pentacles:"Pentacles (reality/value)"
    }
  }
};

function setLang(l){
  LANG = l;
  const t = I18N[l];

  document.getElementById("btnZh").classList.toggle("active", l==="zh");
  document.getElementById("btnEn").classList.toggle("active", l==="en");

  document.getElementById("brandTitle").innerText = t.brandTitle;
  document.getElementById("brandSub").innerText = t.brandSub;

  document.getElementById("pillDeck").innerText = t.pills.deck;
  document.getElementById("pillJung").innerText = t.pills.jung;
  document.getElementById("pillNoFate").innerText = t.pills.noFate;

  document.getElementById("l_intent").innerText = t.intent;
  document.getElementById("intent").placeholder = t.intentPH;

  document.getElementById("l_spread").innerText = t.spread;
  document.getElementById("l_orientMode").innerText = t.orientMode;
  document.getElementById("l_drawPolicy").innerText = t.drawPolicy;

  document.getElementById("l_ritual").innerText = t.ritual;
  document.getElementById("b_shuffle").innerText = t.shuffle;
  document.getElementById("cutBtn").innerText = t.cut;
  document.getElementById("drawBtn").innerText = t.draw;
  document.getElementById("resetBtn").innerText = t.reset;
  document.getElementById("copyBtn").innerText = t.copy;

  document.getElementById("hintTitle").innerText = t.usage;
  document.getElementById("hintBody").innerText = t.usageBody;
  document.getElementById("hintHotkey").innerText = t.hint;
  document.getElementById("hintClick").innerText = t.click;

  document.getElementById("l_analysis").innerText = t.analysis;
  document.getElementById("analysisMeta").innerText = t.analysisMeta;
  document.getElementById("l_prompt").innerText = t.prompt;

  document.getElementById("cutTitle").innerText = t.cutTitle;
  document.getElementById("cutBody").innerText = t.cutBody;
  document.getElementById("cutA").innerText = t.cutLeft;
  document.getElementById("cutB").innerText = t.cutMid;
  document.getElementById("cutC").innerText = t.cutRight;
  document.getElementById("cutNote").innerText = t.cutNote;

  hydrateSpreadSelect();
  renderSpreadHeader();
  renderSlots(true);
  renderInterp();
  updatePrompt();
}

/* =========================================================
   Helpers
========================================================= */
function nowStamp(){
  const d = new Date();
  const pad = (n)=>String(n).padStart(2,"0");
  return `${d.getFullYear()}-${pad(d.getMonth()+1)}-${pad(d.getDate())} ${pad(d.getHours())}:${pad(d.getMinutes())}`;
}

function toast(msg){
  const el = document.getElementById("toast");
  el.textContent = msg;
  el.classList.add("show");
  setTimeout(()=>el.classList.remove("show"), 1100);
}

function imgUrl(filename, width=340){
  // Stable Wikimedia access without knowing hash folder
  // width parameter helps performance; Special:FilePath supports it.
  return `https://commons.wikimedia.org/wiki/Special:FilePath/${encodeURIComponent(filename)}?width=${width}`;
}

/* =========================================================
   Spreads (24+)
   Each position has: id, label, meaning, x, y
========================================================= */
function circlePositions(n, radiusPct, offsetRad=-Math.PI/2){
  return Array.from({length:n}).map((_,i)=>{
    const theta = (i/n)*2*Math.PI + offsetRad;
    return { x:50 + radiusPct*Math.cos(theta), y:50 + radiusPct*Math.sin(theta) };
  });
}

function linePositions(n, x0, y, dx){
  return Array.from({length:n}).map((_,i)=>({ x:x0 + i*dx, y }));
}

function gridPositions(cols, rows, x0, y0, dx, dy){
  const out=[];
  let id=1;
  for(let r=0;r<rows;r++){
    for(let c=0;c<cols;c++){
      out.push({ id:id++, x:x0 + c*dx, y:y0 + r*dy });
    }
  }
  return out;
}

const SPREADS = [
  // 1) Single Card
  {
    key:"one",
    name:{zh:"单牌镜像（当下焦点）", en:"Single Card Mirror (Now)"},
    meta:{zh:"快速聚焦：用一张牌照见当下最重要的心理动力。", en:"Fast focus: one card mirrors the key dynamic now."},
    positions:[
      {id:1, label:{zh:"焦点", en:"Focus"}, meaning:{zh:"此刻最需要被看见的核心主题。", en:"The core theme that needs to be seen now."}, x:50, y:48}
    ]
  },

  // 2) Two Cards: Problem / Resource
  {
    key:"two_resource",
    name:{zh:"二牌：张力与资源", en:"Two Cards: Tension & Resource"},
    meta:{zh:"把问题从“纠结”变成“结构”：张力在哪里？资源在哪里？", en:"Turn confusion into structure: where is tension and where is resource?"},
    positions:[
      {id:1, label:{zh:"张力", en:"Tension"}, meaning:{zh:"拉扯/冲突/卡住点是什么？", en:"Where is the pull/conflict/stuckness?"}, x:42, y:48},
      {id:2, label:{zh:"资源", en:"Resource"}, meaning:{zh:"你已有但未充分使用的资源。", en:"A resource you have but underuse."}, x:58, y:48}
    ]
  },

  // 3) Classic 3
  {
    key:"three_ppf",
    name:{zh:"三牌：过去-现在-走向", en:"Three Cards: Past–Present–Direction"},
    meta:{zh:"适合梳理阶段性脉络（非宿命“未来预测”）。", en:"Good for stage narrative (not fatalistic prediction)."},
    positions:[
      {id:1,label:{zh:"过去",en:"Past"},meaning:{zh:"形成当前局面的关键背景/旧模式。",en:"Background/old pattern shaping the current."},x:36,y:48},
      {id:2,label:{zh:"现在",en:"Present"},meaning:{zh:"当前最主要的心理动力与现实处境。",en:"Main dynamic & context now."},x:50,y:48},
      {id:3,label:{zh:"走向",en:"Direction"},meaning:{zh:"若维持现有方式，最可能的发展方向。",en:"Likely direction if current pattern continues."},x:64,y:48}
    ]
  },

  // 4) Jung 3: Ego / Unconscious / Compensation
  {
    key:"three_jung",
    name:{zh:"三牌：意识-无意识-补偿", en:"Three Cards: Ego–Unconscious–Compensation"},
    meta:{zh:"荣格式读法：意识立场、无意识材料、以及补偿性表达。", en:"Jungian read: ego stance, unconscious material, compensatory expression."},
    positions:[
      {id:1,label:{zh:"意识立场",en:"Ego stance"},meaning:{zh:"你当下的主观立场/自我叙事。",en:"Your current conscious stance/narrative."},x:36,y:48},
      {id:2,label:{zh:"无意识材料",en:"Unconscious"},meaning:{zh:"被压下/未被承认的内容。",en:"What is repressed/unacknowledged."},x:50,y:48},
      {id:3,label:{zh:"补偿",en:"Compensation"},meaning:{zh:"心理为平衡而采取的替代路径（症状/冲动/幻想）。",en:"How the psyche compensates to restore balance."},x:64,y:48}
    ]
  },

  // 5) 4 Card: Situation / Challenge / Advice / Outcome
  {
    key:"four_saco",
    name:{zh:"四牌：处境-阻碍-建议-结果", en:"Four Cards: Situation–Challenge–Advice–Outcome"},
    meta:{zh:"通用且清晰，适合大多数具体问题。", en:"General-purpose clarity for most concrete questions."},
    positions:[
      {id:1,label:{zh:"处境",en:"Situation"},meaning:{zh:"事情现在的真实样子。",en:"What it is right now."},x:34,y:44},
      {id:2,label:{zh:"阻碍",en:"Challenge"},meaning:{zh:"阻力/盲点/防御。",en:"Resistance/blind spot/defense."},x:50,y:44},
      {id:3,label:{zh:"建议",en:"Advice"},meaning:{zh:"更成熟的下一步。",en:"A mature next move."},x:66,y:44},
      {id:4,label:{zh:"结果",en:"Outcome"},meaning:{zh:"若采纳建议，最可能的走向。",en:"Likely outcome if advice is applied."},x:50,y:66}
    ]
  },

  // 6) Horseshoe 7
  {
    key:"horseshoe7",
    name:{zh:"马蹄铁 7 张（情境推进）", en:"Horseshoe 7 (Progression)"},
    meta:{zh:"从背景到建议：适合需要“看全局推进”的议题。", en:"From background to advice: a full progression view."},
    positions:(()=>{
      const coords = circlePositions(7, 34, -Math.PI/1.1);
      const labels = [
        ["背景","Background"],["现在","Present"],["隐秘影响","Hidden influence"],["障碍","Obstacle"],
        ["他人/环境","Others/Environment"],["建议","Advice"],["走向","Direction"]
      ];
      return coords.map((p,i)=>({
        id:i+1,
        label:{zh:labels[i][0],en:labels[i][1]},
        meaning:{
          zh:[
            "形成当前局面的关键背景。",
            "当下主要动力。",
            "你未看见的影响。",
            "最主要阻力与盲点。",
            "外界变量：他人/环境。",
            "更成熟的行动建议。",
            "若继续现状的可能走向。"
          ][i],
          en:[
            "Key background shaping now.",
            "Main dynamic now.",
            "Unseen influence.",
            "Main obstacle/blind spot.",
            "External variable: others/environment.",
            "Mature advice/action.",
            "Likely direction if pattern continues."
          ][i]
        },
        x:p.x, y:p.y
      }));
    })()
  },

  // 7) Celtic Cross 10
  {
    key:"celtic10",
    name:{zh:"凯尔特十字（10 张）", en:"Celtic Cross (10)"},
    meta:{zh:"经典全景牌阵：适合复杂议题与多维影响。", en:"Classic panoramic spread for complex issues."},
    positions:[
      {id:1,label:{zh:"核心处境",en:"Core"},meaning:{zh:"事情的核心与当下状态。",en:"Core situation now."},x:36,y:52},
      {id:2,label:{zh:"交叉影响",en:"Crossing"},meaning:{zh:"阻碍/助力（最强对抗或支持）。",en:"Crossing influence (challenge/support)."},x:36,y:52, overlay:true},
      {id:3,label:{zh:"意识/目标",en:"Conscious"},meaning:{zh:"你想达成的、意识所认同的方向。",en:"Conscious aim/goal."},x:36,y:30},
      {id:4,label:{zh:"潜意识/根基",en:"Unconscious"},meaning:{zh:"更深层动机、恐惧、根基。",en:"Unconscious root/motive."},x:36,y:74},
      {id:5,label:{zh:"过去影响",en:"Past"},meaning:{zh:"刚刚发生/仍在影响的过去。",en:"Recent past shaping now."},x:20,y:52},
      {id:6,label:{zh:"临近未来",en:"Near future"},meaning:{zh:"如果继续当前路径，短期走向。",en:"Short-term direction if unchanged."},x:52,y:52},
      {id:7,label:{zh:"自我立场",en:"Self"},meaning:{zh:"你的姿态、策略、角色。",en:"Your stance/role."},x:72,y:74},
      {id:8,label:{zh:"环境/他人",en:"Environment"},meaning:{zh:"外部条件、他人反应。",en:"External conditions/others."},x:72,y:58},
      {id:9,label:{zh:"希望/恐惧",en:"Hopes/Fears"},meaning:{zh:"你最深的期待与最怕的。",en:"Deep hopes and fears."},x:72,y:42},
      {id:10,label:{zh:"总结/走向",en:"Outcome"},meaning:{zh:"整合后的可能走向（非宿命）。",en:"Integrated direction (non-fatalistic)."},x:72,y:26}
    ]
  },

  // 8) Relationship 6
  {
    key:"relationship6",
    name:{zh:"关系 6 张（我/你/关系）", en:"Relationship 6 (Me/You/Us)"},
    meta:{zh:"适合关系议题：立场、需求、盲点、修复路径。", en:"For relationships: stance, needs, blind spots, repair."},
    positions:[
      {id:1,label:{zh:"我表面",en:"Me (surface)"},meaning:{zh:"你外显的立场/行为。",en:"Your outward stance/behavior."},x:30,y:40},
      {id:2,label:{zh:"我真实需要",en:"Me (need)"},meaning:{zh:"你更深的需要/恐惧。",en:"Your deeper need/fear."},x:30,y:64},
      {id:3,label:{zh:"对方表面",en:"Other (surface)"},meaning:{zh:"对方外显的立场/行为。",en:"Other's outward stance."},x:70,y:40},
      {id:4,label:{zh:"对方真实需要",en:"Other (need)"},meaning:{zh:"对方更深的需要/恐惧。",en:"Other's deeper need/fear."},x:70,y:64},
      {id:5,label:{zh:"关系动力",en:"Relational dynamic"},meaning:{zh:"你们互动的核心模式（循环）。",en:"Core interaction loop."},x:50,y:40},
      {id:6,label:{zh:"修复路径",en:"Repair path"},meaning:{zh:"可执行的修复/对齐行动。",en:"Executable repair/alignment."},x:50,y:64}
    ]
  },

  // 9) Decision 7
  {
    key:"decision7",
    name:{zh:"决策 7 张（两条路）", en:"Decision 7 (Two Paths)"},
    meta:{zh:"适合二选一：动机、代价、收益、隐形变量与建议。", en:"For A/B choices: motives, costs, benefits, hidden variable, advice."},
    positions:[
      {id:1,label:{zh:"现状核心",en:"Status quo"},meaning:{zh:"当前局面最真实的核心。",en:"Core of current situation."},x:50,y:30},
      {id:2,label:{zh:"选择A动机",en:"Path A motive"},meaning:{zh:"你为什么想选A？",en:"Why you want A."},x:28,y:44},
      {id:3,label:{zh:"选择A代价",en:"Path A cost"},meaning:{zh:"选A可能付出的代价。",en:"Cost of choosing A."},x:28,y:62},
      {id:4,label:{zh:"选择B动机",en:"Path B motive"},meaning:{zh:"你为什么想选B？",en:"Why you want B."},x:72,y:44},
      {id:5,label:{zh:"选择B代价",en:"Path B cost"},meaning:{zh:"选B可能付出的代价。",en:"Cost of choosing B."},x:72,y:62},
      {id:6,label:{zh:"隐形变量",en:"Hidden variable"},meaning:{zh:"你没计算到的关键变量。",en:"Key variable you’re missing."},x:50,y:52},
      {id:7,label:{zh:"导师建议",en:"Mentor advice"},meaning:{zh:"更成熟、可持续的选择方式。",en:"More mature, sustainable choice."},x:50,y:76}
    ]
  },

  // 10) Shadow work 6
  {
    key:"shadow6",
    name:{zh:"阴影整合 6 张", en:"Shadow Integration 6"},
    meta:{zh:"专门做阴影：投射、羞耻、回收力量与行动。", en:"Explicit shadow work: projection, shame, reclaiming power."},
    positions:[
      {id:1,label:{zh:"阴影主题",en:"Shadow theme"},meaning:{zh:"你不愿承认/不愿看见的部分。",en:"What you don’t want to see."},x:30,y:40},
      {id:2,label:{zh:"触发点",en:"Trigger"},meaning:{zh:"它通常如何被触发？",en:"How it gets triggered."},x:50,y:40},
      {id:3,label:{zh:"防御方式",en:"Defense"},meaning:{zh:"你如何保护自己（代价是什么）？",en:"Your defense and its cost."},x:70,y:40},
      {id:4,label:{zh:"阴影礼物",en:"Gift"},meaning:{zh:"阴影里藏着的生命力/资源。",en:"Vitality/resource hidden inside."},x:30,y:66},
      {id:5,label:{zh:"收回投射",en:"Withdraw projection"},meaning:{zh:"如何把力量从外界收回？",en:"How to reclaim power from outside."},x:50,y:66},
      {id:6,label:{zh:"具体行动",en:"Concrete action"},meaning:{zh:"可执行的一步（可测量）。",en:"One measurable step."},x:70,y:66}
    ]
  },

  // 11) Chakra 7
  {
    key:"chakra7",
    name:{zh:"七脉轮（7 张）", en:"Chakras (7)"},
    meta:{zh:"身心整合扫描：从安全感到意义感。", en:"Mind-body scan from safety to meaning."},
    positions:(()=>{
      const labels = [
        ["海底轮","Root"],["脐轮","Sacral"],["太阳神经丛","Solar Plexus"],["心轮","Heart"],
        ["喉轮","Throat"],["眉心轮","Third Eye"],["顶轮","Crown"]
      ];
      const meaningsZh = [
        "安全感、身体、金钱/生存焦虑。","欲望、亲密、创造力与愉悦。","自我价值、边界、掌控与羞耻。",
        "爱与哀伤、连接与分离。","表达、真实沟通、说出需要。","直觉、洞察、幻象与投射。",
        "意义、信念系统、人生方向。"
      ];
      const meaningsEn = [
        "Safety, body, survival/money anxiety.","Desire, intimacy, creativity, pleasure.","Self-worth, boundaries, control/shame.",
        "Love/grief, connection/separation.","Expression, truthful communication.","Intuition, insight, illusion/projection.",
        "Meaning, belief system, life direction."
      ];
      const ys = [78,68,58,48,38,28,18];
      return labels.map((x,i)=>({
        id:i+1,
        label:{zh:x[0],en:x[1]},
        meaning:{zh:meaningsZh[i],en:meaningsEn[i]},
        x:50,
        y:ys[i]
      }));
    })()
  },

  // 12) Career 6
  {
    key:"career6",
    name:{zh:"职业路径 6 张", en:"Career Path 6"},
    meta:{zh:"适合求职/转型：优势、阻力、环境与下一步。", en:"For career decisions: strengths, blockers, environment, next steps."},
    positions:[
      {id:1,label:{zh:"你的优势",en:"Strength"},meaning:{zh:"可依靠的核心能力/资源。",en:"Core strength/resource."},x:28,y:40},
      {id:2,label:{zh:"当前阻力",en:"Blocker"},meaning:{zh:"最主要的障碍/盲点。",en:"Main obstacle/blind spot."},x:50,y:40},
      {id:3,label:{zh:"外界机会",en:"Opportunity"},meaning:{zh:"环境给到的机会窗口。",en:"External opportunity window."},x:72,y:40},
      {id:4,label:{zh:"你需要学习",en:"Learn"},meaning:{zh:"需要补齐的关键能力/心态。",en:"What to learn/develop."},x:28,y:66},
      {id:5,label:{zh:"策略建议",en:"Strategy"},meaning:{zh:"更有效的策略/路径。",en:"Most effective strategy."},x:50,y:66},
      {id:6,label:{zh:"下一步行动",en:"Next step"},meaning:{zh:"可执行的一步（本周）。",en:"One executable step (this week)."},x:72,y:66}
    ]
  },

  // 13) Money 5
  {
    key:"money5",
    name:{zh:"金钱与价值 5 张", en:"Money & Value 5"},
    meta:{zh:"把“钱的问题”翻译成“价值与安全感的结构”。", en:"Translate money issues into value/safety structure."},
    positions:[
      {id:1,label:{zh:"金钱现实",en:"Reality"},meaning:{zh:"现状与真实压力源。",en:"Current reality & pressure."},x:30,y:48},
      {id:2,label:{zh:"内在价值观",en:"Values"},meaning:{zh:"你如何定义“足够/安全”。",en:"How you define enough/safe."},x:50,y:30},
      {id:3,label:{zh:"阻塞点",en:"Block"},meaning:{zh:"让金钱/价值流动卡住的地方。",en:"Where flow is blocked."},x:50,y:66},
      {id:4,label:{zh:"可用资源",en:"Resource"},meaning:{zh:"你可调用的资源/支持。",en:"Usable resource/support."},x:70,y:48},
      {id:5,label:{zh:"行动建议",en:"Action"},meaning:{zh:"可执行的财务/价值行动。",en:"Executable money/value step."},x:50,y:48}
    ]
  },

  // 14) Inner child 5
  {
    key:"innerchild5",
    name:{zh:"内在小孩 5 张", en:"Inner Child 5"},
    meta:{zh:"适合修复：未满足需要、保护策略与新的养育方式。", en:"For repair: unmet needs, defenses, and new nurturing."},
    positions:[
      {id:1,label:{zh:"小孩的需要",en:"Need"},meaning:{zh:"最核心未被满足的需要。",en:"Core unmet need."},x:30,y:44},
      {id:2,label:{zh:"小孩的恐惧",en:"Fear"},meaning:{zh:"最怕发生什么？",en:"What it fears most."},x:50,y:44},
      {id:3,label:{zh:"保护策略",en:"Protection"},meaning:{zh:"你如何保护自己（代价）？",en:"How you protect (and cost)."},x:70,y:44},
      {id:4,label:{zh:"新的养育",en:"New nurture"},meaning:{zh:"你现在可以如何照顾它。",en:"How you can nurture it now."},x:40,y:70},
      {id:5,label:{zh:"本周行动",en:"This week"},meaning:{zh:"本周可做的一小步。",en:"A small step this week."},x:60,y:70}
    ]
  },

  // 15) Self-care 5
  {
    key:"selfcare5",
    name:{zh:"自我照顾 5 张", en:"Self-care 5"},
    meta:{zh:"从“该更努力”转向“更可持续”。", en:"Shift from 'push harder' to sustainability."},
    positions:[
      {id:1,label:{zh:"耗竭来源",en:"Drain"},meaning:{zh:"是什么在消耗你？",en:"What drains you?"},x:30,y:44},
      {id:2,label:{zh:"被忽略的需要",en:"Neglected need"},meaning:{zh:"你忽视了什么需要？",en:"What need is neglected?"},x:50,y:30},
      {id:3,label:{zh:"修复资源",en:"Repair resource"},meaning:{zh:"什么能帮你恢复？",en:"What restores you?"},x:70,y:44},
      {id:4,label:{zh:"边界建议",en:"Boundary"},meaning:{zh:"你需要设什么边界？",en:"What boundary is needed?"},x:40,y:70},
      {id:5,label:{zh:"微行动",en:"Micro-action"},meaning:{zh:"48小时可执行的小动作。",en:"A 48h doable step."},x:60,y:70}
    ]
  },

  // 16) Dream 5
  {
    key:"dream5",
    name:{zh:"梦的象征 5 张", en:"Dream Symbolism 5"},
    meta:{zh:"把梦当成无意识信件：象征、情绪、补偿与行动。", en:"Dream as a letter from the unconscious."},
    positions:[
      {id:1,label:{zh:"梦的主象征",en:"Main symbol"},meaning:{zh:"梦里最重要的象征/角色。",en:"Key symbol/figure."},x:30,y:44},
      {id:2,label:{zh:"梦的情绪",en:"Affect"},meaning:{zh:"梦里最强的情绪是什么？",en:"Strongest affect."},x:50,y:44},
      {id:3,label:{zh:"补偿信息",en:"Compensation"},meaning:{zh:"梦在补偿你白天的立场。",en:"What it compensates in waking stance."},x:70,y:44},
      {id:4,label:{zh:"现实对照",en:"Reality link"},meaning:{zh:"它对应现实中的哪件事？",en:"Where it links to life."},x:40,y:70},
      {id:5,label:{zh:"行动线索",en:"Action clue"},meaning:{zh:"可执行的线索。",en:"Executable clue."},x:60,y:70}
    ]
  },

  // 17) Year Ahead 12 (months)
  {
    key:"year12",
    name:{zh:"年度 12 月（12 张）", en:"Year Ahead 12 (Months)"},
    meta:{zh:"按月份扫描主题与节奏（适合做计划）。", en:"Month-by-month theme scan for planning."},
    positions:(()=>{
      const coords = circlePositions(12, 38, -Math.PI/2);
      return coords.map((p,i)=>({
        id:i+1,
        label:{zh:`${i+1} 月`,en:`Month ${i+1}`},
        meaning:{zh:`第 ${i+1} 月的主题与关键任务。`,en:`Theme and key task for month ${i+1}.`},
        x:p.x, y:p.y
      }));
    })()
  },

  // 18) Problem-Solving 5
  {
    key:"solve5",
    name:{zh:"问题解决 5 张（结构化）", en:"Problem Solving 5 (Structured)"},
    meta:{zh:"把问题拆成可行动结构：核心、原因、资源、阻碍、方案。", en:"Turn a problem into an actionable structure."},
    positions:[
      {id:1,label:{zh:"核心问题",en:"Core"},meaning:{zh:"问题的核心是什么？",en:"What is the core problem?"},x:30,y:48},
      {id:2,label:{zh:"根因",en:"Root cause"},meaning:{zh:"它背后的原因/动力。",en:"Underlying cause/dynamic."},x:50,y:30},
      {id:3,label:{zh:"资源",en:"Resource"},meaning:{zh:"你可用的资源。",en:"Available resource."},x:70,y:48},
      {id:4,label:{zh:"阻碍",en:"Obstacle"},meaning:{zh:"最大的阻碍/盲点。",en:"Biggest obstacle/blind spot."},x:50,y:66},
      {id:5,label:{zh:"方案",en:"Plan"},meaning:{zh:"最可行的下一步方案。",en:"Most feasible next plan."},x:50,y:48}
    ]
  },

  // 19) 5-Card Cross
  {
    key:"cross5",
    name:{zh:"五牌十字（核心+四向）", en:"5-Card Cross"},
    meta:{zh:"看核心与四个方向的影响：上/下/左/右。", en:"Core plus four directional influences."},
    positions:[
      {id:1,label:{zh:"核心",en:"Core"},meaning:{zh:"主题核心。",en:"Core theme."},x:50,y:52},
      {id:2,label:{zh:"上（意识）",en:"Above"},meaning:{zh:"意识目标/理想。",en:"Conscious aim/ideal."},x:50,y:28},
      {id:3,label:{zh:"下（根基）",en:"Below"},meaning:{zh:"根基/潜意识。",en:"Root/unconscious."},x:50,y:76},
      {id:4,label:{zh:"左（过去）",en:"Left"},meaning:{zh:"过去影响。",en:"Past influence."},x:26,y:52},
      {id:5,label:{zh:"右（走向）",en:"Right"},meaning:{zh:"走向与下一步。",en:"Direction/next."},x:74,y:52}
    ]
  },

  // 20) 12-House Psyche Wheel (your original, upgraded meanings)
  {
    key:"circle12",
    name:{zh:"12 宫心理轮（荣格式全域扫描）", en:"12-House Psyche Wheel (Jungian Scan)"},
    meta:{zh:"从 12 个心理领域观察同一主题：自我、关系、阴影、理想与现实张力。", en:"Observe one theme through 12 psyche domains: self, relating, shadow, ideals, reality tensions."},
    positions:(()=>{
      const coords = circlePositions(12, 38, -Math.PI/2);
      const meaningsZh = [
        "自我呈现：我是谁/我如何开始。",
        "价值与稳定：我依靠什么。",
        "叙事与表达：我如何讲述与沟通。",
        "根基与安全：我真正需要的归属。",
        "欲望与创造：生命力如何流动。",
        "日常与秩序：习惯、健康与工作方式。",
        "关系与投射：我在对方身上看见谁。",
        "阴影与交换：权力、依附、控制与信任。",
        "意义与远方：理想、信念与学习。",
        "责任与成就：社会角色与边界。",
        "群体与未来：支持系统与愿景。",
        "无意识海域：梦、潜流、不可名状的动机。"
      ];
      const meaningsEn = [
        "Self-presentation: who I am / how I begin.",
        "Values & stability: what I rely on.",
        "Narrative & expression: how I communicate.",
        "Roots & safety: belonging and needs.",
        "Desire & creativity: libido flow.",
        "Daily order: habits/health/work style.",
        "Relating & projection: who I see in the other.",
        "Shadow & exchange: power/attachment/control/trust.",
        "Meaning & horizon: ideals/beliefs/learning.",
        "Responsibility & achievement: role/boundaries.",
        "Community & future: support system/vision.",
        "Unconscious sea: dreams, undercurrents, unnamed motives."
      ];
      return coords.map((p,i)=>({
        id:i+1,
        label:{zh:`第 ${i+1} 宫`, en:`House ${i+1}`},
        meaning:{zh:meaningsZh[i], en:meaningsEn[i]},
        x:p.x, y:p.y
      }));
    })()
  },

  // 21) 9-card Square (3x3)
  {
    key:"grid9",
    name:{zh:"九宫格 3×3（全息扫描）", en:"3×3 Grid (Holographic Scan)"},
    meta:{zh:"用 3×3 看“内在—外在—整合”层次。", en:"A 3×3 scan: inner, outer, integration."},
    positions:(()=>{
      const base = gridPositions(3,3, 34, 26, 16, 18);
      const labels = [
        ["内在动机","Inner motive"],["意识立场","Conscious stance"],["外显行为","Behavior"],
        ["情绪层","Affect"],["核心张力","Core tension"],["环境变量","Environment"],
        ["阴影线索","Shadow clue"],["资源/支持","Support"],["整合建议","Integration"]
      ];
      const meaningsZh = [
        "更深的动机/需要。","主观叙事与立场。","你在做/将做什么。",
        "情绪底色与感受。","最关键张力所在。","外部变量。",
        "阴影与盲点。","可用支持。","整合后的建议。"
      ];
      const meaningsEn = [
        "Deeper motive/need.","Conscious narrative/stance.","What you do/do next.",
        "Emotional tone.","Key tension.","External variable.",
        "Shadow/blind spot.","Available support.","Integration advice."
      ];
      return base.map((p,i)=>({
        id:i+1,
        label:{zh:labels[i][0],en:labels[i][1]},
        meaning:{zh:meaningsZh[i],en:meaningsEn[i]},
        x:p.x, y:p.y
      }));
    })()
  },

  // 22) 4-Week Plan (4)
  {
    key:"weeks4",
    name:{zh:"四周计划（4 张）", en:"4-Week Plan (4)"},
    meta:{zh:"把洞察落到节奏：第1-4周怎么做。", en:"Turn insight into rhythm: week 1–4."},
    positions:[
      {id:1,label:{zh:"第1周",en:"Week 1"},meaning:{zh:"启动与最小行动。",en:"Kickoff & minimal action."},x:30,y:48},
      {id:2,label:{zh:"第2周",en:"Week 2"},meaning:{zh:"稳定与微调。",en:"Stabilize & adjust."},x:46,y:48},
      {id:3,label:{zh:"第3周",en:"Week 3"},meaning:{zh:"扩展与对齐。",en:"Expand & align."},x:62,y:48},
      {id:4,label:{zh:"第4周",en:"Week 4"},meaning:{zh:"收尾与复盘。",en:"Close & review."},x:78,y:48}
    ]
  },

  // 23) 6-card Timeline
  {
    key:"timeline6",
    name:{zh:"时间线 6 张（阶段推进）", en:"Timeline 6 (Stages)"},
    meta:{zh:"适合项目/关系阶段：从起点到整合。", en:"For project/relationship stages: from start to integration."},
    positions:(()=>{
      const pts = linePositions(6, 18, 50, 14);
      const labels = [
        ["起点","Start"],["第1阶段","Stage 1"],["第2阶段","Stage 2"],["拐点","Turning point"],["整合","Integration"],["建议","Advice"]
      ];
      const meaningsZh = [
        "起点与原始动机。","第1阶段关键任务。","第2阶段关键挑战。","最大拐点与风险。","整合方式。","导师建议。"
      ];
      const meaningsEn = [
        "Start and original motive.","Key task in stage 1.","Key challenge in stage 2.","Main turning point/risk.","How to integrate.","Mentor advice."
      ];
      return pts.map((p,i)=>({
        id:i+1,
        label:{zh:labels[i][0],en:labels[i][1]},
        meaning:{zh:meaningsZh[i],en:meaningsEn[i]},
        x:p.x, y:p.y
      }));
    })()
  },

  // 24) 8-card Attachment Map
  {
    key:"attachment8",
    name:{zh:"依附地图 8 张（关系循环）", en:"Attachment Map 8 (Relational Loop)"},
    meta:{zh:"看关系里：触发—反应—需求—修复（非常心理向）。", en:"Map the loop: trigger → reaction → need → repair."},
    positions:[
      {id:1,label:{zh:"触发",en:"Trigger"},meaning:{zh:"关系里什么会触发你？",en:"What triggers you?"},x:26,y:36},
      {id:2,label:{zh:"你的反应",en:"Your reaction"},meaning:{zh:"你通常怎么反应？",en:"Your typical response."},x:44,y:36},
      {id:3,label:{zh:"你的真实需要",en:"Your need"},meaning:{zh:"你更深的需要。",en:"Your deeper need."},x:62,y:36},
      {id:4,label:{zh:"你的恐惧叙事",en:"Your fear story"},meaning:{zh:"你脑内最怕的故事。",en:"Your fear narrative."},x:80,y:36},
      {id:5,label:{zh:"对方的触发",en:"Other's trigger"},meaning:{zh:"对方可能被什么触发。",en:"What triggers the other."},x:26,y:66},
      {id:6,label:{zh:"对方的反应",en:"Other's reaction"},meaning:{zh:"对方如何反应。",en:"Other's typical response."},x:44,y:66},
      {id:7,label:{zh:"对方的需要",en:"Other's need"},meaning:{zh:"对方更深需要。",en:"Other's deeper need."},x:62,y:66},
      {id:8,label:{zh:"修复钥匙",en:"Repair key"},meaning:{zh:"修复循环的关键钥匙。",en:"Key to repair the loop."},x:80,y:66}
    ]
  }
];

function hydrateSpreadSelect(){
  const sel = document.getElementById("spreadSelect");
  const cur = sel.value || "circle12";
  sel.innerHTML = "";
  SPREADS.forEach(s=>{
    const o = document.createElement("option");
    o.value = s.key;
    o.textContent = s.name[LANG];
    sel.appendChild(o);
  });
  sel.value = cur;
  sel.onchange = () => {
    renderSpreadHeader();
    renderSlots(true);
    renderInterp();
    updatePrompt();
  };
}

function getSpread(){
  const sel = document.getElementById("spreadSelect");
  const key = sel.value || "circle12";
  return SPREADS.find(s=>s.key===key) || SPREADS[0];
}

function renderSpreadHeader(){
  const s = getSpread();
  document.getElementById("spreadTitle").innerText = s.name[LANG];
  document.getElementById("spreadMeta").innerText = I18N[LANG].spreadMetaTpl(s.positions.length) + " · " + (s.meta?.[LANG] || "");
}

/* =========================================================
   Deck (RWS 78) + Jungian Layer
   - Images via Special:FilePath => no hash path required
========================================================= */
function mkCard(opts){
  // opts: {cn,en,file, arcana, suit, rank, jung, keywords}
  return Object.freeze({
    cn: opts.cn, en: opts.en,
    file: opts.file,
    img: imgUrl(opts.file, 380),
    arcana: opts.arcana || "minor", // "major" | "minor"
    suit: opts.suit || null,
    rank: opts.rank || null,
    jung: opts.jung || null
  });
}

const SUIT_ZH = { Wands:"权杖", Cups:"圣杯", Swords:"宝剑", Pentacles:"星币" };
const SUIT_FILE = { Wands:"Wands", Cups:"Cups", Swords:"Swords", Pentacles:"Pents" };

const RANK_ZH_NUM = {
  1:"一",2:"二",3:"三",4:"四",5:"五",6:"六",7:"七",8:"八",9:"九",10:"十"
};
const COURT_ZH = { 11:"侍从", 12:"骑士", 13:"皇后", 14:"国王" };
const COURT_EN = { 11:"Page", 12:"Knight", 13:"Queen", 14:"King" };

const STAGE_ZH = {
  1:"种子/火花（潜能）",
  2:"二元/张力（选择与拉扯）",
  3:"外化/建构（开始成形）",
  4:"稳定/固化（结构建立）",
  5:"冲突/失衡（试炼）",
  6:"调整/恢复（对齐与修复）",
  7:"试炼/意志（坚持与策略）",
  8:"技能/重复（熟练与执行）",
  9:"累积/极限（临界点）",
  10:"过载/转化（收尾与新阶段）",
  11:"学习者（新经验的入口）",
  12:"推进者（行动与防御模式）",
  13:"成熟容器（内在整合与滋养）",
  14:"外在统合（责任与权威）"
};
const STAGE_EN = {
  1:"Seed/Spark (potential)",
  2:"Duality/Tension (choice)",
  3:"Formation/Building",
  4:"Stability/Structure",
  5:"Conflict/Trial",
  6:"Adjustment/Repair",
  7:"Test/Strategy",
  8:"Skill/Execution",
  9:"Accumulation/Limit",
  10:"Overload/Transition",
  11:"Learner (entry)",
  12:"Mover (action/defense)",
  13:"Mature container (integration)",
  14:"External integration (responsibility)"
};

function suitDomain(suit){
  const map = {
    Wands:{zh:"意志/行动（Libido 的推进）", en:"Will/Action (libidinal drive)"},
    Cups:{zh:"情感/关系（依附与流动）", en:"Emotion/Relating (attachment/flow)"},
    Swords:{zh:"认知/冲突（思维、防御与分裂）", en:"Mind/Conflict (defense/splitting)"},
    Pentacles:{zh:"现实/价值（身体、金钱、稳定）", en:"Reality/Value (body/money/stability)"}
  };
  return map[suit];
}

function minorJung(suit, rank){
  const sd = suitDomain(suit);
  const stageZh = STAGE_ZH[rank];
  const stageEn = STAGE_EN[rank];
  return {
    archetype:{
      zh:`${SUIT_ZH[suit]}：${sd.zh} · 阶段：${stageZh}`,
      en:`${suit}: ${sd.en} · Stage: ${stageEn}`
    },
    dynamics:{
      zh:`这张小牌呈现的是：在「${sd.zh}」这个维度上，你正处于「${stageZh}」的心理动力。重点是：能量如何流动、在哪里卡住、你用什么策略应对。`,
      en:`This minor card describes your current dynamic in the domain of "${sd.en}" at the stage "${stageEn}". Focus on flow, blockage, and coping strategy.`
    },
    compensation:{
      zh:`若该维度被压抑或过度，常见补偿是：用相反方式极端化（全有/全无），或把力量外包给他人/规则/幻想。`,
      en:`If this domain is suppressed or inflated, compensation often appears as all-or-nothing extremes or outsourcing power to others/rules/fantasy.`
    },
    shadowGift:{
      zh:`阴影：把阶段需求误当成身份（卡在“应该/必须”）；礼物：识别阶段任务并做可持续的微调整。`,
      en:`Shadow: turning a stage-demand into identity ("should/must"); Gift: naming the stage task and making sustainable micro-adjustments.`
    },
    practice:{
      zh:`行动建议：在「${sd.zh}」上做一个可测量的小动作（48小时内），让能量从想象回到现实。`,
      en:`Practice: make one measurable action in the domain "${sd.en}" within 48 hours to bring energy into reality.`
    },
    question:{
      zh:`我在「${sd.zh}」这个维度上，当前阶段最需要我面对的是什么？`,
      en:`In the domain "${sd.en}", what does this stage most require me to face?`
    }
  };
}

function minorName(suit, rank){
  const suitZh = SUIT_ZH[suit];
  const suitEn = suit;
  if(rank <= 10){
    const cn = `${suitZh}${RANK_ZH_NUM[rank]}`;
    const en = `${["Ace","Two","Three","Four","Five","Six","Seven","Eight","Nine","Ten"][rank-1]} of ${suitEn}`;
    return {cn,en};
  }
  const cn = `${suitZh}${COURT_ZH[rank]}`;
  const en = `${COURT_EN[rank]} of ${suitEn}`;
  return {cn,en};
}

function minorFile(suit, rank){
  // Wikimedia RWS minors commonly use: Wands01.jpg ... Wands14.jpg, Cups01.., Swords01.., Pents01..
  const stem = SUIT_FILE[suit];
  const n = String(rank).padStart(2,"0");
  return `${stem}${n}.jpg`;
}

function buildMinors(){
  const suits = ["Wands","Cups","Swords","Pentacles"];
  const out=[];
  for(const suit of suits){
    for(let r=1;r<=14;r++){
      const nm = minorName(suit,r);
      out.push(mkCard({
        cn:nm.cn, en:nm.en,
        file: minorFile(suit,r),
        arcana:"minor", suit, rank:r,
        jung: minorJung(suit,r)
      }));
    }
  }
  return out;
}

/* --------------------------
   Major Arcana (22)
   Images: RWS_Tarot_00_Fool.jpg ... RWS_Tarot_21_World.jpg
   Jungian notes: keep concise but mentor-grade (you can expand later)
-------------------------- */
function majorJungPack(archetypeZh, archetypeEn, dynamicsZh, dynamicsEn, compZh, compEn, shadowGiftZh, shadowGiftEn, practiceZh, practiceEn, questionZh, questionEn){
  return {
    archetype:{zh:archetypeZh,en:archetypeEn},
    dynamics:{zh:dynamicsZh,en:dynamicsEn},
    compensation:{zh:compZh,en:compEn},
    shadowGift:{zh:shadowGiftZh,en:shadowGiftEn},
    practice:{zh:practiceZh,en:practiceEn},
    question:{zh:questionZh,en:questionEn}
  };
}

const MAJORS = [
  mkCard({cn:"愚者",en:"The Fool",file:"RWS_Tarot_00_Fool.jpg",arcana:"major",
    jung:majorJungPack(
      "自性/旅途的开端","Self / Journey begins",
      "开放与冒险：自我在未知中生成。","Openness and risk: the ego forms through the unknown.",
      "过度控制会以冲动或逃离补偿。","Over-control may compensate via impulse/escape.",
      "阴影：幼稚冲动；礼物：信任与创造力。","Shadow: naivete; Gift: trust & creativity.",
      "写下一个可逆低成本的一步，并在48小时内做。","Pick one reversible low-cost step within 48h.",
      "我在哪里需要允许未知？","Where do I need to allow the unknown?"
    )
  }),
  mkCard({cn:"魔术师",en:"The Magician",file:"RWS_Tarot_01_Magician.jpg",arcana:"major",
    jung:majorJungPack(
      "意志/能动性","Will / Agency",
      "把资源组织成行动：从想法到表达。","Organize resources into action: idea → expression.",
      "无力感会以表演/操控补偿。","Powerlessness may compensate via performance/control.",
      "阴影：操纵/自恋；礼物：专注与创造。","Shadow: manipulation; Gift: focus & creation.",
      "把目标拆成3个可验证微成果，今天完成1个。","Break goal into 3 verifiable micro-results; finish 1 today.",
      "我真正能控制的变量是什么？","What variable is truly under my control?"
    )
  }),
  mkCard({cn:"女祭司",en:"The High Priestess",file:"RWS_Tarot_02_High_Priestess.jpg",arcana:"major",
    jung:majorJungPack(
      "无意识/直觉","Unconscious / Intuition",
      "信息在沉默中成形：容纳暧昧与等待。","Meaning forms in silence: tolerate ambiguity.",
      "害怕亲密会以冷感/神秘化补偿。","Fear of intimacy may compensate via coldness/mystification.",
      "阴影：隔离；礼物：深度洞察。","Shadow: isolation; Gift: insight.",
      "72小时减少外部输入，记录梦与直觉线索。","Reduce input for 72h; log dreams/intuition.",
      "我在回避哪条内在信息？","What inner message am I avoiding?"
    )
  }),
  mkCard({cn:"女皇",en:"The Empress",file:"RWS_Tarot_03_Empress.jpg",arcana:"major",
    jung:majorJungPack(
      "滋养/生命力","Nurture / Vitality",
      "成长、照料与丰盛：身体与情感的容纳。","Growth and care: holding body and feelings.",
      "匮乏感会以取悦/占有补偿。","Scarcity may compensate via pleasing/possessiveness.",
      "阴影：黏连；礼物：承载力。","Shadow: enmeshment; Gift: containment.",
      "安排一项身体层面的滋养，并量化记录。","Schedule one body-based nurture; track it.",
      "我需要怎样的滋养而没给自己？","What nourishment am I withholding from myself?"
    )
  }),
  mkCard({cn:"皇帝",en:"The Emperor",file:"RWS_Tarot_04_Emperor.jpg",arcana:"major",
    jung:majorJungPack(
      "秩序/边界","Order / Boundaries",
      "结构与责任：建立可持续规则。","Structure and responsibility: sustainable rules.",
      "不安全会以强硬/僵化补偿。","Insecurity may compensate via rigidity/domination.",
      "阴影：控制；礼物：稳定守护。","Shadow: control; Gift: stability.",
      "写1条明确边界句（含后果），本周说出口。","Write one boundary sentence (with consequence) and say it this week.",
      "如果我更有结构，会减少什么焦虑？","If I had more structure, what anxiety would reduce?"
    )
  }),
  mkCard({cn:"教皇",en:"The Hierophant",file:"RWS_Tarot_05_Hierophant.jpg",arcana:"major",
    jung:majorJungPack(
      "传统/意义系统","Tradition / Meaning system",
      "价值观与传承：你遵循的规范来自哪里？","Values & lineage: where do your rules come from?",
      "内在混乱会以教条/外部权威补偿。","Chaos may compensate via dogma/external authority.",
      "阴影：僵化顺从；礼物：仪式与共同体。","Shadow: rigidity; Gift: ritual/community.",
      "写3条原则：保留1条、挑战1条、重写1条。","Write 3 principles: keep 1, challenge 1, rewrite 1.",
      "我是在忠于价值，还是在取悦权威？","Am I honoring values or pleasing authority?"
    )
  }),
  mkCard({cn:"恋人",en:"The Lovers",file:"RWS_Tarot_06_Lovers.jpg",arcana:"major",
    jung:majorJungPack(
      "关系/选择","Relating / Choice",
      "关系中的整合：欲望、价值与承诺对齐。","Integration in relating: align desire/values/commitment.",
      "分裂会以暧昧/三角/理想化补偿。","Splitting may compensate via ambiguity/triangles/idealization.",
      "阴影：投射依附；礼物：真实选择。","Shadow: projection; Gift: true choice.",
      "列出关系里3个核心价值，并定义可观察行为。","List 3 relational values and observable behaviors.",
      "我害怕失去的是什么自我形象？","What self-image am I afraid to lose?"
    )
  }),
  mkCard({cn:"战车",en:"The Chariot",file:"RWS_Tarot_07_Chariot.jpg",arcana:"major",
    jung:majorJungPack(
      "意志整合/驾驭","Will integration / Mastery",
      "把相反力量拉到同一方向：目标与纪律。","Align opposing forces: goal + discipline.",
      "冲突会以硬扛/过度竞争补偿。","Conflict may compensate via brute forcing/over-competition.",
      "阴影：压抑感受；礼物：推进力。","Shadow: suppression; Gift: momentum.",
      "设2周冲刺：每天30分钟不可协商，记录阻抗。","Set a 2-week sprint: 30min/day; track resistance.",
      "我需要整合的两股力量是什么？","What two forces must I integrate?"
    )
  }),
  mkCard({cn:"力量",en:"Strength",file:"RWS_Tarot_08_Strength.jpg",arcana:"major",
    jung:majorJungPack(
      "温柔的力量/本能整合","Gentle power / Instinct integration",
      "不压制本能，而是与之建立关系并引导。","Relate to instinct rather than suppress it.",
      "无力感会以讨好或爆发补偿。","Powerlessness may compensate via pleasing or bursting.",
      "阴影：自我否定；礼物：慈悲与韧性。","Shadow: self-negation; Gift: compassion/resilience.",
      "写一封不发送的情绪信，提炼成一句边界表达。","Write an unsent emotion letter; distill into one boundary sentence.",
      "我在哪个情绪上最不信任自己？","Which emotion do I trust myself least with?"
    )
  }),
  mkCard({cn:"隐者",en:"The Hermit",file:"RWS_Tarot_09_Hermit.jpg",arcana:"major",
    jung:majorJungPack(
      "内省/个体化","Introspection / Individuation",
      "退一步让内在灯火显现：从角色回到自己。","Step back so the inner lantern appears.",
      "被噪音淹没会以孤立补偿。","Overwhelm may compensate via isolation.",
      "阴影：逃避；礼物：智慧与方向。","Shadow: avoidance; Gift: direction.",
      "设2小时独处窗口：不输入、不社交，只整理笔记。","2-hour solitude: no input/social; just notes.",
      "如果我不迎合任何人，我会怎么选？","If I pleased no one, what would I choose?"
    )
  }),
  mkCard({cn:"命运之轮",en:"Wheel of Fortune",file:"RWS_Tarot_10_Wheel_of_Fortune.jpg",arcana:"major",
    jung:majorJungPack(
      "变化/循环","Change / Cycles",
      "模式与时机：你在循环的转折点。","Patterns & timing: a turning point.",
      "失控会以迷信/过度归因补偿。","Loss of control may compensate via superstition.",
      "阴影：宿命被动；礼物：顺势调整。","Shadow: fatalism; Gift: adaptation.",
      "列出可控/可影响/不可控三列，只对前两列行动。","Make 3 columns: control/influence/no-control; act on first two.",
      "这个循环在重复教我什么？","What is this cycle teaching me?"
    )
  }),
  mkCard({cn:"正义",en:"Justice",file:"RWS_Tarot_11_Justice.jpg",arcana:"major",
    jung:majorJungPack(
      "衡量/伦理","Balance / Ethics",
      "一致性：行为要对得起价值。","Coherence: actions aligned with values.",
      "内疚会以苛责/投射补偿。","Guilt may compensate via harshness/projection.",
      "阴影：冷酷算账；礼物：清晰公正。","Shadow: cold accounting; Gift: clarity/fairness.",
      "做一次“事实-解释-感受-请求”四步沟通。","Practice facts-meaning-feelings-request communication.",
      "我在哪个地方对自己不公平？","Where am I being unfair to myself?"
    )
  }),
  mkCard({cn:"倒吊人",en:"The Hanged Man",file:"RWS_Tarot_12_Hanged_Man.jpg",arcana:"major",
    jung:majorJungPack(
      "悬置/视角转化","Suspension / Reframing",
      "暂停让新意义出现。","Pause allows new meaning to emerge.",
      "不敢选择会以拖延/受害叙事补偿。","Fear of choice may compensate via procrastination/victim stories.",
      "阴影：受害者姿态；礼物：重构能力。","Shadow: victim stance; Gift: deep reframing.",
      "设暂停边界：到期日 + 下一步。","Set a pause boundary: deadline + next step.",
      "如果我换角度，这件事像什么？","If I change perspective, what does this become?"
    )
  }),
  mkCard({cn:"死神",en:"Death",file:"RWS_Tarot_13_Death.jpg",arcana:"major",
    jung:majorJungPack(
      "转化/结束与更新","Transformation",
      "旧身份让位，新生命力出现。","Old identity ends; new vitality emerges.",
      "抗拒结束会以纠缠/控制补偿。","Resisting endings may compensate via clinging/control.",
      "阴影：执念恐惧；礼物：蜕变自由。","Shadow: fixation; Gift: liberation.",
      "四列表：结束/减少/保留/开始，并做一个最小结束动作。","Four lists: end/reduce/keep/start; do one minimal ending.",
      "我在抗拒什么结束？","What ending am I resisting?"
    )
  }),
  mkCard({cn:"节制",en:"Temperance",file:"RWS_Tarot_14_Temperance.jpg",arcana:"major",
    jung:majorJungPack(
      "整合/调和","Integration / Tempering",
      "把两端混合出第三种可能：节奏与配比。","Mix extremes into a third possibility: rhythm & proportion.",
      "失衡会以全有/全无补偿。","Imbalance may compensate via all-or-nothing.",
      "阴影：麻木拖延；礼物：稳态疗愈。","Shadow: numbness; Gift: homeostasis.",
      "把一个极端行为改成70%版本，坚持7天。","Turn one extreme into a 70% version for 7 days.",
      "我如何回到可持续的节奏？","How do I return to a sustainable rhythm?"
    )
  }),
  mkCard({cn:"恶魔",en:"The Devil",file:"RWS_Tarot_15_Devil.jpg",arcana:"major",
    jung:majorJungPack(
      "阴影/依附","Shadow / Attachment",
      "欲望、恐惧或投射绑住：力量外包。","Bound by desire/fear/projection: outsourcing power.",
      "羞耻会以成瘾/控制补偿。","Shame may compensate via addiction/control.",
      "阴影：麻痹依附；礼物：收回选择权。","Shadow: numb attachment; Gift: reclaim choice.",
      "对一个依附行为做24小时延迟，记录冲动曲线。","Delay one attachment behavior for 24h; log urge curve.",
      "我把力量交给了什么？","What have I given my power to?"
    )
  }),
  mkCard({cn:"高塔",en:"The Tower",file:"RWS_Tarot_16_Tower.jpg",arcana:"major",
    jung:majorJungPack(
      "解体/真相冲击","Breakdown / Truth shock",
      "旧结构坍塌以暴露真相：痛但必要。","Old structures collapse to reveal truth.",
      "长期压抑会用突发事件补偿。","Long repression may compensate via sudden rupture.",
      "阴影：恐慌破坏；礼物：解放重建。","Shadow: panic/sabotage; Gift: liberation/rebuild.",
      "两列：我以为 vs 事实，然后做一个现实对齐行动。","Two columns: assumed vs facts; take one alignment action.",
      "哪个幻觉正在崩塌？","Which illusion is collapsing?"
    )
  }),
  mkCard({cn:"星星",en:"The Star",file:"RWS_Tarot_17_Star.jpg",arcana:"major",
    jung:majorJungPack(
      "修复/希望","Restoration / Hope",
      "在脆弱中重建信任：细水长流。","Rebuild trust through vulnerability.",
      "绝望会以犬儒/过度幻想补偿。","Despair may compensate via cynicism/fantasy.",
      "阴影：逃避空想；礼物：愿景疗愈。","Shadow: escapism; Gift: healing vision.",
      "10分钟修复仪式（呼吸/写作/步行）连续14天。","10-min restoration ritual for 14 days.",
      "我如何重建对自己/关系的信任？","How can I rebuild trust in self/relating?"
    )
  }),
  mkCard({cn:"月亮",en:"The Moon",file:"RWS_Tarot_18_Moon.jpg",arcana:"major",
    jung:majorJungPack(
      "潜意识/迷雾","Unconscious / Veil",
      "不确定、梦与投射：真相被情绪折射。","Uncertainty, dreams, projections: truth refracted by emotion.",
      "焦虑会以过度解读/自我怀疑补偿。","Anxiety may compensate via over-interpretation/self-doubt.",
      "阴影：幻象恐惧；礼物：直觉想象力。","Shadow: illusion; Gift: intuition.",
      "事实核对：5条事实 vs 5条脑内故事。","Reality check: 5 facts vs 5 mind-stories.",
      "我把什么投射成了威胁？","What have I projected as a threat?"
    )
  }),
  mkCard({cn:"太阳",en:"The Sun",file:"RWS_Tarot_19_Sun.jpg",arcana:"major",
    jung:majorJungPack(
      "清晰/生命力","Clarity / Vitality",
      "让真实可见：表达与坦诚。","Let the real be seen: expression & honesty.",
      "羞耻会以躲藏/自嘲补偿。","Shame may compensate via hiding/self-deprecation.",
      "阴影：炫耀否认痛苦；礼物：喜悦坦诚。","Shadow: showiness; Gift: joy/honesty.",
      "做一个公开的小表达（作品/请求），记录反馈。","Make a small public expression; log feedback.",
      "如果我不再隐藏，我会让什么被看见？","If I stop hiding, what will be seen?"
    )
  }),
  mkCard({cn:"审判",en:"Judgement",file:"RWS_Tarot_20_Judgement.jpg",arcana:"major",
    jung:majorJungPack(
      "召唤/更新","Call / Renewal",
      "从旧叙事醒来：回应内在召唤。","Wake from an old narrative; answer the call.",
      "羞耻会以自我审判/拖延补偿。","Shame may compensate via self-judgment/delay.",
      "阴影：苛责；礼物：宽恕更新。","Shadow: harsh judgment; Gift: renewal.",
      "修复清单：1个道歉、1个补偿、1个新承诺。","Repair list: one apology, one compensation, one commitment.",
      "我在被什么召唤？","What am I being called toward?"
    )
  }),
  mkCard({cn:"世界",en:"The World",file:"RWS_Tarot_21_World.jpg",arcana:"major",
    jung:majorJungPack(
      "完成/整体","Wholeness / Completion",
      "阶段完成与更大整合。","Completion and broader integration.",
      "怕结束会以拖延/分心补偿。","Fear of endings may compensate via delay/distraction.",
      "阴影：空转不满足；礼物：成熟整体感。","Shadow: restlessness; Gift: wholeness.",
      "做一次收尾仪式：整理/归档/告别，写下一阶段主题句。","Closing ritual: organize/archive/closure; write next theme sentence.",
      "我如何完成并带走这一阶段？","How do I complete and carry this phase?"
    )
  })
];

const DECK = Object.freeze([...MAJORS, ...buildMinors()]);

/* =========================================================
   Session State
========================================================= */
let session = {
  stage: "idle", // idle | shuffled | cut | drawn
  deckShuffled: [],
  draws: null, // [{pos, card, rev}]
  createdAt: null,
  cutChosen: null
};

function setSessionPill(text){
  document.getElementById("sessionPill").innerText = text;
}

function updateSessionMeta(stateText){
  const time = session.createdAt ? session.createdAt : "—";
  document.getElementById("sessionMeta").innerText =
    (session.createdAt ? I18N[LANG].sessionMetaTpl(time, stateText) : "—");
}

/* =========================================================
   Professional Flow: Shuffle → Cut → Draw
========================================================= */
function fisherYates(arr){
  for(let i=arr.length-1;i>0;i--){
    const j = Math.floor(Math.random()*(i+1));
    [arr[i],arr[j]] = [arr[j],arr[i]];
  }
  return arr;
}

function startShuffle(){
  // 1) Shuffle
  const arr = DECK.map(x=>x);
  fisherYates(arr);

  session.stage = "shuffled";
  session.deckShuffled = arr;
  session.draws = null;
  session.createdAt = nowStamp();
  session.cutChosen = null;

  document.getElementById("cutBtn").disabled = false;
  document.getElementById("drawBtn").disabled = true;
  document.getElementById("copyBtn").disabled = true;

  document.getElementById("cutBox").style.display = "none";

  renderSpreadHeader();
  renderSlots(false);
  renderInterp();
  updatePrompt();

  setSessionPill(I18N[LANG].sessionShuffled);
  updateSessionMeta(I18N[LANG].sessionShuffled);
}

function startCut(){
  if(session.stage !== "shuffled") return;

  session.stage = "cut"; // waiting for choice
  document.getElementById("cutBox").style.display = "block";
  setSessionPill(I18N[LANG].sessionCut + " · " + (LANG==="zh" ? "请选择左/中/右" : "Choose left/middle/right"));
  updateSessionMeta(LANG==="zh" ? "等待切牌选择" : "Waiting for cut choice");
}

function chooseCut(which){
  if(session.stage !== "cut") return;

  // split into three piles, approximate equal
  const deck = session.deckShuffled.slice();
  const n = deck.length;
  const p = Math.floor(n/3);
  const a = deck.slice(0,p);
  const b = deck.slice(p,2*p);
  const c = deck.slice(2*p);

  // Choose pile as start; then stack remaining in order (symbolic)
  // which: 0=a,1=b,2=c
  let newDeck;
  if(which===0) newDeck = [...a, ...b, ...c];
  if(which===1) newDeck = [...b, ...c, ...a];
  if(which===2) newDeck = [...c, ...a, ...b];

  // Optional: another gentle shuffle to "settle" cut (mentor-like)
  // Keep very light: swap 10 random pairs
  for(let k=0;k<10;k++){
    const i = Math.floor(Math.random()*newDeck.length);
    const j = Math.floor(Math.random()*newDeck.length);
    [newDeck[i],newDeck[j]] = [newDeck[j],newDeck[i]];
  }

  session.deckShuffled = newDeck;
  session.cutChosen = which;
  session.stage = "cut_done";

  document.getElementById("cutBox").style.display = "none";
  document.getElementById("drawBtn").disabled = false;

  setSessionPill(I18N[LANG].sessionCut);
  updateSessionMeta(I18N[LANG].sessionCut);
}

function resolveOrientation(){
  const mode = document.getElementById("orientMode").value;
  if(mode === "upright") return false;
  if(mode === "none") return null; // hidden
  return (Math.random() < 0.5);
}

function drawAll(){
  if(!(session.stage==="cut_done" || session.stage==="shuffled")) return;

  const s = getSpread();
  const N = s.positions.length;
  const policy = document.getElementById("drawPolicy").value;

  let picked = [];
  if(policy === "withoutReplacement"){
    if(session.deckShuffled.length < N){
      startShuffle(); // safety
    }
    picked = session.deckShuffled.slice(0, N);
  }else{
    // with replacement: random picks
    for(let i=0;i<N;i++){
      picked.push(session.deckShuffled[Math.floor(Math.random()*session.deckShuffled.length)]);
    }
  }

  session.draws = s.positions.map((pos, idx)=>({
    pos,
    card: picked[idx],
    rev: resolveOrientation() // true/false/null
  }));

  session.stage = "drawn";

  renderSlots(true);
  renderInterp();
  updatePrompt();

  document.getElementById("copyBtn").disabled = false;
  setSessionPill(I18N[LANG].sessionDrawn);
  updateSessionMeta(I18N[LANG].sessionDrawn);
}

function resetSession(){
  session.stage = "idle";
  session.deckShuffled = [];
  session.draws = null;
  session.createdAt = null;
  session.cutChosen = null;

  document.getElementById("cutBtn").disabled = true;
  document.getElementById("drawBtn").disabled = true;
  document.getElementById("copyBtn").disabled = true;
  document.getElementById("cutBox").style.display = "none";

  renderSpreadHeader();
  renderSlots(false);
  renderInterp();
  updatePrompt();

  setSessionPill(I18N[LANG].sessionIdle);
  document.getElementById("sessionMeta").innerText = "—";
}

/* =========================================================
   Render Board
========================================================= */
function renderSlots(showCards){
  const s = getSpread();
  const board = document.getElementById("board");
  board.innerHTML = "";

  const mode = document.getElementById("orientMode").value;

  s.positions.forEach(p=>{
    const slot = document.createElement("div");
    slot.className = "slot";
    slot.style.left = `${p.x}%`;
    slot.style.top  = `${p.y}%`;

    const cardEl = document.createElement("div");
    cardEl.className = "card" + (showCards && session.draws ? "" : " empty");

    if(showCards && session.draws){
      const d = session.draws.find(x=>x.pos.id===p.id);
      if(d){
        let orientText = "";
        if(mode === "none" || d.rev === null){
          orientText = I18N[LANG].orientationNone;
        }else{
          orientText = d.rev ? I18N[LANG].orientationReversed : I18N[LANG].orientationUpright;
        }

        if(d.rev === true && mode !== "none") cardEl.classList.add("rev");
        cardEl.innerHTML = `
          <span class="badge">${orientText}</span>
          <img loading="lazy" src="${d.card.img}" alt="${LANG==="zh" ? d.card.cn : d.card.en}">
        `;

        // click to toggle upright/reversed (only if not "none")
        if(mode !== "none"){
          cardEl.addEventListener("click", ()=>{
            if(d.rev === null) d.rev = false;
            d.rev = !d.rev;
            renderSlots(true);
            renderInterp();
            updatePrompt();
          });
        }
      }
    }

    const lab = document.createElement("div");
    lab.className = "slotLabel";
    lab.textContent = p.label[LANG];

    const meaning = document.createElement("div");
    meaning.className = "slotMeaning";
    meaning.textContent = p.meaning?.[LANG] || "";

    slot.appendChild(cardEl);
    slot.appendChild(lab);
    slot.appendChild(meaning);
    board.appendChild(slot);
  });
}

/* =========================================================
   Interpretation + Mentor Synthesis
========================================================= */
function safe(x){ return x ? x : "—"; }

function cardStructuralLine(card){
  const t = I18N[LANG];
  if(card.arcana === "major"){
    return LANG==="zh" ? "大阿卡纳（原型层）" : "Major Arcana (archetypal layer)";
  }
  const suitLabel = t.suits[card.suit] || card.suit;
  const r = card.rank;
  const stage = (LANG==="zh" ? STAGE_ZH[r] : STAGE_EN[r]);
  return LANG==="zh"
    ? `小阿卡纳 · ${suitLabel} · 阶段：${stage}`
    : `Minor Arcana · ${suitLabel} · Stage: ${stage}`;
}

function orientationNote(rev){
  if(rev === null) return LANG==="zh"
    ? "本次设置为：不显示正逆位（只看象征图像）。"
    : "Orientation hidden (symbol-only reading).";
  if(rev){
    return LANG==="zh"
      ? "逆位视为：能量内收、阻抗、或补偿性表达（非吉凶）。"
      : "Reversed as: inward energy, resistance, or compensatory expression (not good/bad).";
  }
  return LANG==="zh"
    ? "正位视为：能量外显，主题更易被意识化与行动化。"
    : "Upright as: outward expression; easier to bring into awareness and action.";
}

function renderInterp(){
  const box = document.getElementById("interp");
  const t = I18N[LANG];

  if(!session.draws){
    box.innerHTML = "";
    return;
  }

  const mode = document.getElementById("orientMode").value;

  const items = session.draws.map(d=>{
    const c = d.card;
    const j = c.jung || {};
    const o = (d.rev === null || mode==="none")
      ? t.orientationNone
      : (d.rev ? t.orientationReversed : t.orientationUpright);

    return `
      <div class="interpItem">
        <div class="interpHead">
          <b>${LANG==="zh" ? c.cn : c.en} · ${o}<br><small>${safe(d.pos.label[LANG])}</small></b>
          <span class="tag">${safe(d.pos.label[LANG])}</span>
        </div>

        <div class="kv"><span class="k">${t.fields.posMeaning}</span>${safe(d.pos.meaning?.[LANG])}</div>
        <div class="kv"><span class="k">${t.fields.suitRank}</span>${cardStructuralLine(c)}</div>

        <div class="sep"></div>
        <div class="kv"><span class="k">${t.fields.archetype}</span>${safe(j.archetype?.[LANG])}</div>
        <div class="kv"><span class="k">${t.fields.dynamics}</span>${safe(j.dynamics?.[LANG])}</div>
        <div class="kv"><span class="k">${t.fields.compensation}</span>${safe(j.compensation?.[LANG])}</div>
        <div class="kv"><span class="k">${t.fields.shadowGift}</span>${safe(j.shadowGift?.[LANG])}</div>
        <div class="kv"><span class="k">${t.fields.practice}</span>${safe(j.practice?.[LANG])}</div>
        <div class="kv"><span class="k">${t.fields.question}</span>${safe(j.question?.[LANG])}</div>

        <div class="sep"></div>
        <div class="kv"><span class="k">${LANG==="zh" ? "取向说明" : "Orientation note"}</span>${orientationNote(d.rev)}</div>
      </div>
    `;
  });

  // Add synthesis at bottom (mentor-style)
  items.push(renderSynthesisCard());

  box.innerHTML = items.join("");
}

function renderSynthesisCard(){
  const t = I18N[LANG];
  const draws = session.draws || [];
  const majors = draws.filter(d=>d.card.arcana==="major").length;
  const minors = draws.length - majors;

  const suitCount = {Wands:0,Cups:0,Swords:0,Pentacles:0};
  draws.forEach(d=>{
    if(d.card.arcana==="minor" && d.card.suit) suitCount[d.card.suit]++;
  });

  const sortedSuits = Object.entries(suitCount).sort((a,b)=>b[1]-a[1]);
  const topSuit = sortedSuits[0][0];
  const topSuitN = sortedSuits[0][1];

  const revKnown = draws.filter(d=>d.rev !== null);
  const revN = revKnown.filter(d=>d.rev===true).length;
  const uprN = revKnown.filter(d=>d.rev===false).length;

  const focus =
    LANG==="zh"
      ? `本次共 ${draws.length} 张：大阿卡纳 ${majors}（原型层更强），小阿卡纳 ${minors}（现实细节更多）。花色主导：${t.suits[topSuit]}（${topSuitN} 张）——说明你的议题主要在这个心理维度上发生。`
      : `Total ${draws.length} cards: ${majors} majors (strong archetypal layer) and ${minors} minors (more concrete details). Dominant suit: ${t.suits[topSuit]} (${topSuitN}) — your issue concentrates in that domain.`;

  const pattern =
    LANG==="zh"
      ? `正逆位（仅统计可见者）：正位 ${uprN} / 逆位 ${revN}。逆位偏多时，通常代表“能量内收、阻抗或补偿策略”正在主导——需要先把情绪/防御翻译成可沟通、可行动的语言。`
      : `Orientation (visible-only): upright ${uprN} / reversed ${revN}. More reversals often imply inward energy, resistance, or compensatory coping—translate defenses into communicable, actionable language first.`;

  const shadow =
    LANG==="zh"
      ? `把“你在别人/事件里看到的东西”当作投射线索：问自己——我在这里想要什么？我害怕承认什么？我把力量交给了谁/什么规则？然后把力量收回到一个具体动作上。`
      : `Treat what you see in others/events as projection clues: what do I want here, what do I fear admitting, where did I outsource power? Then reclaim it through one concrete action.`;

  const plan =
    LANG==="zh"
      ? `24h：写下“事实-解释-感受-请求”四行并发出一个小沟通/行动。\n7d：围绕主导花色维度做一个可量化习惯（每天10–30分钟）。\n30d：复盘一次：哪些补偿策略减少了？哪个边界更清晰了？下一个阶段目标是什么？`
      : `24h: write 4 lines (facts-meaning-feelings-request) and send one small message/action.\n7d: build one measurable micro-habit in the dominant suit domain (10–30min/day).\n30d: review: which compensations reduced, which boundary got clearer, what’s the next stage goal?`;

  return `
    <div class="interpItem">
      <div class="interpHead">
        <b>${t.synthesisTitle}</b>
        <span class="tag">${t.synthesisTitle}</span>
      </div>

      <div class="kv"><span class="k">${t.synthesisFocus}</span>${focus}</div>
      <div class="kv"><span class="k">${t.synthesisPattern}</span>${pattern}</div>
      <div class="kv"><span class="k">${t.synthesisShadow}</span>${shadow}</div>
      <div class="kv"><span class="k">${t.synthesisPlan}</span><pre style="white-space:pre-wrap;margin:6px 0 0 0;color:rgba(230,237,246,.9)">${plan}</pre></div>
    </div>
  `;
}

/* =========================================================
   Prompt Builder (Professional, Mentor-grade)
========================================================= */
function updatePrompt(){
  const out = document.getElementById("aiPrompt");
  if(!session.draws){
    out.value = "";
    return;
  }

  const s = getSpread();
  const intent = (document.getElementById("intent").value || (LANG==="zh" ? "自我探索" : "Self-exploration")).trim();
  const t = I18N[LANG];

  const mode = document.getElementById("orientMode").value;

  const cardsBlock = session.draws.map(d=>{
    const orient =
      (mode==="none" || d.rev===null)
        ? "Hidden"
        : (d.rev ? "Reversed" : "Upright");
    return `- ${d.pos.label.en} / ${d.pos.label.zh} (${d.pos.meaning.en}): ${d.card.en} (${orient}) | ${d.card.cn}`;
  }).join("\n");

  out.value =
`${t.promptRole}:
You are a senior Jungian-oriented symbolic analysis mentor. You use Tarot (RWS) as a projective psychological tool — not fortune-telling.

${t.promptContext}:
- Intent: ${intent}
- Spread: ${s.name.en} / ${s.name.zh}
- Stance: meaning-making, compensation patterns, shadow integration, actionable reflection

${t.promptCards}:
${cardsBlock}

${t.promptConstraints}:
- No fatalistic predictions, no guaranteed outcomes, no “you will meet X” claims
- Do not diagnose medical conditions
- Treat reversed cards as inward/blocked/compensatory expressions, not “bad luck”
- Be psychologically grounded and client-safe (no spiritual absolutism)
- Use the position meaning to structure the narrative

${t.promptOutput}:
1) One-paragraph case formulation (Jungian lens): core tension + likely compensation
2) Spread-by-spread synthesis: identify 2–4 domains (e.g., self/relating/shadow/meaning)
3) Shadow work: 1–2 projections + how to withdraw them
4) Action plan: 24h / 7d / 30d (each measurable)
5) 5 reflection questions for journaling

Write in ${LANG==="zh" ? "Simplified Chinese" : "English"}.
`;
}

async function copyPrompt(){
  const text = document.getElementById("aiPrompt").value || "";
  if(!text) return;
  try{
    await navigator.clipboard.writeText(text);
    toast(LANG==="zh" ? "已复制" : "Copied");
  }catch(e){
    const ta = document.getElementById("aiPrompt");
    ta.focus(); ta.select();
    document.execCommand("copy");
    toast(LANG==="zh" ? "已复制" : "Copied");
  }
}

/* =========================================================
   Init
========================================================= */
(function init(){
  hydrateSpreadSelect();
  renderSpreadHeader();
  renderSlots(false);
  setSessionPill(I18N[LANG].sessionIdle);
  setLang("zh");
})();
</script>
</body>
</html>



