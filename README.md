# synonyms-and-antonymsfrom pathlib import Path

html = r'''<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Grade 9 Synonyms & Antonyms Challenge</title>
<style>
*{box-sizing:border-box}
body{margin:0;font-family:Arial,Helvetica,sans-serif;background:linear-gradient(135deg,#e8f0ff,#f8fbff);color:#18243a;min-height:100vh}
.container{max-width:850px;margin:auto;padding:20px}
header{background:#fff;border-radius:22px;padding:24px;text-align:center;box-shadow:0 8px 25px rgba(30,50,90,.12)}
h1{margin:0 0 8px;font-size:clamp(28px,6vw,44px)}
.subtitle{margin:0;color:#5d6b82}
.panel{background:#fff;border-radius:22px;padding:24px;margin-top:18px;box-shadow:0 8px 25px rgba(30,50,90,.10)}
.hidden{display:none!important}
.stats{display:flex;gap:10px;justify-content:space-between;flex-wrap:wrap;margin-bottom:18px}
.badge{background:#eef3ff;border-radius:999px;padding:10px 14px;font-weight:700}
.progress{height:10px;background:#e8edf5;border-radius:99px;overflow:hidden;margin:12px 0 22px}
.progress span{display:block;height:100%;width:0;background:#4169e1;transition:.3s}
.type{display:inline-block;background:#e9f7ef;color:#17643a;border-radius:999px;padding:7px 12px;font-weight:800}
.question{font-size:clamp(21px,4vw,30px);font-weight:800;line-height:1.3;margin:18px 0}
.options{display:grid;grid-template-columns:1fr 1fr;gap:12px}
button{font:inherit}
.option,.main-btn{border:0;border-radius:14px;padding:14px 16px;min-height:52px;font-weight:750;cursor:pointer}
.option{text-align:left;background:#f3f6fb;border:2px solid #dce3ef}
.option:hover:not(:disabled){border-color:#4169e1;background:#edf2ff}
.option:disabled{cursor:default}
.correct{background:#dff6e8!important;border-color:#249653!important}
.wrong{background:#ffe3e0!important;border-color:#c33b2e!important}
.feedback{min-height:30px;font-weight:800;margin:16px 0}
.actions{display:flex;justify-content:space-between;gap:12px;align-items:center;flex-wrap:wrap}
.main-btn{background:#4169e1;color:#fff}
.main-btn.secondary{background:#eef2f8;color:#18243a}
.center{text-align:center}
.big-score{font-size:58px;font-weight:900;margin:10px 0}
.small{color:#5d6b82}
.name-input{width:100%;max-width:420px;padding:14px;border:2px solid #dce3ef;border-radius:12px;font-size:16px;margin:12px 0}
.review{margin-top:20px;text-align:left;background:#f7f9fc;padding:16px;border-radius:14px}
.review div{padding:8px 0;border-bottom:1px solid #e3e8f0}
@media(max-width:600px){.options{grid-template-columns:1fr}.container{padding:12px}.panel{padding:18px}}
</style>
</head>
<body>
<div class="container">
<header>
<h1>📚 Grade 9 Vocabulary Challenge</h1>
<p class="subtitle">Synonyms & Antonyms • English Language Game</p>
</header>

<section id="start" class="panel center">
<h2>Ready to test your vocabulary?</h2>
<p class="small">Answer 20 questions. Each correct answer earns 5 points.</p>
<input id="learnerName" class="name-input" type="text" maxlength="40" placeholder="Enter your name (optional)">
<br>
<button class="main-btn" id="startBtn">Start Game ▶</button>
</section>

<section id="game" class="panel hidden">
<div class="stats">
<span class="badge" id="qCount">Question 1 of 20</span>
<span class="badge" id="score">Score: 0</span>
<span class="badge" id="timer">Time: 30s</span>
</div>
<div class="progress"><span id="bar"></span></div>
<div id="type" class="type">Synonym</div>
<div id="question" class="question"></div>
<div id="options" class="options"></div>
<div id="feedback" class="feedback" aria-live="polite"></div>
<div class="actions">
<span class="small" id="hint"></span>
<button class="main-btn hidden" id="nextBtn">Next Question →</button>
</div>
</section>

<section id="result" class="panel center hidden">
<h2>🎉 Game Complete!</h2>
<p id="resultName" class="small"></p>
<div class="big-score" id="finalScore">0 / 100</div>
<h3 id="resultMessage"></h3>
<p id="percentage"></p>
<button class="main-btn" id="againBtn">Play Again</button>
<div class="review">
<h3>Learning Review</h3>
<p class="small">Remember: a <b>synonym</b> has a similar meaning, while an <b>antonym</b> has an opposite meaning.</p>
<div id="reviewList"></div>
</div>
</section>
</div>

<script>
const questions = [
{type:"Synonym",q:"Which word is closest in meaning to 'abundant'?",o:["Scarce","Plentiful","Empty","Weak"],a:1},
{type:"Antonym",q:"Which word is opposite in meaning to 'ancient'?",o:["Historic","Modern","Old","Traditional"],a:1},
{type:"Synonym",q:"Which word is closest in meaning to 'reluctant'?",o:["Unwilling","Excited","Certain","Eager"],a:0},
{type:"Antonym",q:"Which word is opposite in meaning to 'expand'?",o:["Increase","Stretch","Contract","Develop"],a:2},
{type:"Synonym",q:"Which word is closest in meaning to 'fortunate'?",o:["Lucky","Unhappy","Poor","Careless"],a:0},
{type:"Antonym",q:"Which word is opposite in meaning to 'generous'?",o:["Kind","Selfish","Helpful","Giving"],a:1},
{type:"Synonym",q:"Which word is closest in meaning to 'essential'?",o:["Optional","Necessary","Unusual","Difficult"],a:1},
{type:"Antonym",q:"Which word is opposite in meaning to 'temporary'?",o:["Brief","Short","Permanent","Limited"],a:2},
{type:"Synonym",q:"Which word is closest in meaning to 'accurate'?",o:["Correct","Confusing","Rough","False"],a:0},
{type:"Antonym",q:"Which word is opposite in meaning to 'hostile'?",o:["Angry","Friendly","Violent","Unkind"],a:1},
{type:"Synonym",q:"Which word is closest in meaning to 'vital'?",o:["Unimportant","Necessary","Tiny","Distant"],a:1},
{type:"Antonym",q:"Which word is opposite in meaning to 'optimistic'?",o:["Hopeful","Positive","Pessimistic","Confident"],a:2},
{type:"Synonym",q:"Which word is closest in meaning to 'preserve'?",o:["Destroy","Protect","Forget","Remove"],a:1},
{type:"Antonym",q:"Which word is opposite in meaning to 'complex'?",o:["Complicated","Simple","Difficult","Advanced"],a:1},
{type:"Synonym",q:"Which word is closest in meaning to 'observe'?",o:["Ignore","Watch","Break","Hide"],a:1},
{type:"Antonym",q:"Which word is opposite in meaning to 'diligent'?",o:["Hardworking","Careful","Lazy","Responsible"],a:2},
{type:"Synonym",q:"Which word is closest in meaning to 'significant'?",o:["Important","Tiny","Ordinary","Unclear"],a:0},
{type:"Antonym",q:"Which word is opposite in meaning to 'scarce'?",o:["Rare","Limited","Abundant","Small"],a:2},
{type:"Synonym",q:"Which word is closest in meaning to 'construct'?",o:["Build","Destroy","Separate","Forget"],a:0},
{type:"Antonym",q:"Which word is opposite in meaning to 'permit'?",o:["Allow","Approve","Forbid","Accept"],a:2}
];

let current=0,score=0,time=30,timerId=null,answered=false,name="";
let missed=[];

const $=id=>document.getElementById(id);

function startGame(){
 name=$("learnerName").value.trim();
 current=0;score=0;missed=[];
 $("start").classList.add("hidden");
 $("result").classList.add("hidden");
 $("game").classList.remove("hidden");
 renderQuestion();
}

function renderQuestion(){
 clearInterval(timerId);
 answered=false;
 time=30;
 const q=questions[current];
 $("qCount").textContent=`Question ${current+1} of ${questions.length}`;
 $("score").textContent=`Score: ${score}`;
 $("timer").textContent=`Time: ${time}s`;
 $("bar").style.width=`${(current/questions.length)*100}%`;
 $("type").textContent=q.type;
 $("question").textContent=q.q;
 $("feedback").textContent="";
 $("hint").textContent="Choose the best answer.";
 $("nextBtn").classList.add("hidden");
 const box=$("options");
 box.innerHTML="";
 q.o.forEach((answer,index)=>{
   const btn=document.createElement("button");
   btn.className="option";
   btn.textContent=answer;
   btn.addEventListener("click",()=>selectAnswer(index,btn));
   box.appendChild(btn);
 });
 timerId=setInterval(()=>{
   time--;
   $("timer").textContent=`Time: ${time}s`;
   if(time<=0){
     clearInterval(timerId);
     if(!answered) timeUp();
   }
 },1000);
}

function selectAnswer(index,button){
 if(answered)return;
 answered=true;
 clearInterval(timerId);
 const q=questions[current];
 const buttons=[...$("options").children];
 buttons.forEach(b=>b.disabled=true);
 if(index===q.a){
   score+=5;
   button.classList.add("correct");
   $("feedback").textContent="✅ Correct! You earned 5 points.";
 }else{
   button.classList.add("wrong");
   buttons[q.a].classList.add("correct");
   $("feedback").textContent=`❌ Incorrect. The correct answer is "${q.o[q.a]}".`;
   missed.push({q:q.q,correct:q.o[q.a]});
 }
 $("score").textContent=`Score: ${score}`;
 $("hint").textContent="";
 $("nextBtn").classList.remove("hidden");
}

function timeUp(){
 answered=true;
 const q=questions[current];
 [...$("options").children].forEach(b=>b.disabled=true);
 $("options").children[q.a].classList.add("correct");
 $("feedback").textContent=`⏰ Time's up! The correct answer is "${q.o[q.a]}".`;
 missed.push({q:q.q,correct:q.o[q.a]});
 $("nextBtn").classList.remove("hidden");
}

function next(){
 if(current<questions.length-1){
   current++;
   renderQuestion();
 }else finish();
}

function finish(){
 clearInterval(timerId);
 $("game").classList.add("hidden");
 $("result").classList.remove("hidden");
 $("bar").style.width="100%";
 $("finalScore").textContent=`${score} / 100`;
 $("resultName").textContent=name?`Well done, ${name}!`:"Well done, learner!";
 const pct=score;
 $("percentage").textContent=`Percentage: ${pct}%`;
 let msg=pct>=90?"Outstanding vocabulary knowledge! 🌟":pct>=75?"Excellent work! Keep building your vocabulary. 👏":pct>=50?"Good effort! Review the words you missed and try again. 💪":"Keep practising! You can improve your vocabulary with regular practice. 📖";
 $("resultMessage").textContent=msg;
 const review=$("reviewList");
 review.innerHTML="";
 if(missed.length===0){
   review.innerHTML="<div>Perfect score — no questions to review! 🎯</div>";
 }else{
   missed.forEach(item=>{
     const d=document.createElement("div");
     d.innerHTML=`<b>${escapeHtml(item.q)}</b><br><span class="small">Correct answer: ${escapeHtml(item.correct)}</span>`;
     review.appendChild(d);
   });
 }
}

function escapeHtml(s){
 return s.replace(/[&<>"']/g,c=>({"&":"&amp;","<":"&lt;",">":"&gt;",'"':"&quot;","'":"&#039;"}[c]));
}

$("startBtn").addEventListener("click",startGame);
$("nextBtn").addEventListener("click",next);
$("againBtn").addEventListener("click",()=>{
 $("result").classList.add("hidden");
 $("start").classList.remove("hidden");
});
</script>
</body>
</html>
'''

path = Path("/mnt/data/Grade_9_Synonyms_Antonyms_Game.html")
path.write_text(html, encoding="utf-8")
print(f"Created: {path}")
