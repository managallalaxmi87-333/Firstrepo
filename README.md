from pathlib import Path

html = r"""<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Peach Tic Tac Toe Pro</title>
<style>
body{font-family:Segoe UI,sans-serif;background:linear-gradient(135deg,#ffd6c2,#fff0e6);display:flex;justify-content:center;align-items:center;min-height:100vh;margin:0}
.dark{background:#222;color:#fff}
.card{background:#fff;padding:20px;border-radius:20px;box-shadow:0 10px 30px rgba(0,0,0,.15);width:360px;text-align:center}
.board{display:grid;grid-template-columns:repeat(3,1fr);gap:8px;margin:15px 0}
.cell{height:95px;background:#fff3ed;border-radius:12px;font-size:42px;display:flex;align-items:center;justify-content:center;cursor:pointer}
button{padding:10px 14px;border:none;border-radius:10px;margin:4px;cursor:pointer}
</style>
</head>
<body>
<div class="card">
<h2>🎮 Tic Tac Toe Pro</h2>
<div id="status">Player X Turn</div>
<div class="board" id="board"></div>
<div>
<button onclick="restart()">Restart</button>
<button onclick="toggleTheme()">Dark Mode</button>
</div>
<p>X Wins: <span id="xw">0</span> | O Wins: <span id="ow">0</span></p>
</div>
<script>
const boardEl=document.getElementById('board');
let board=["","","","","","","","",""];
let player="X",active=true;
let x=+localStorage.getItem("xw")||0;
let o=+localStorage.getItem("ow")||0;
xw.textContent=x;ow.textContent=o;

for(let i=0;i<9;i++){
 let c=document.createElement('div');
 c.className='cell';
 c.onclick=()=>move(i,c);
 boardEl.appendChild(c);
}
const wins=[[0,1,2],[3,4,5],[6,7,8],[0,3,6],[1,4,7],[2,5,8],[0,4,8],[2,4,6]];
function move(i,cell){
 if(board[i]||!active)return;
 board[i]=player; cell.textContent=player;
 if(check()){active=false;return;}
 player=player==="X"?"O":"X";
 status.textContent="Player "+player+" Turn";
}
function check(){
 for(let w of wins){
  let[a,b,c]=w;
  if(board[a]&&board[a]===board[b]&&board[a]===board[c]){
   status.textContent="🏆 "+board[a]+" Wins";
   if(board[a]=="X"){x++;localStorage.setItem("xw",x);xw.textContent=x;}
   else{o++;localStorage.setItem("ow",o);ow.textContent=o;}
   return true;
  }
 }
 if(!board.includes("")){status.textContent="Draw";return true;}
 return false;
}
function restart(){
 board=["","","","","","","","",""];
 [...document.getElementsByClassName('cell')].forEach(c=>c.textContent='');
 player="X";active=true;status.textContent="Player X Turn";
}
function toggleTheme(){document.body.classList.toggle('dark');}
</script>
</body>
</html>"""
path = "/mnt/data/Peach_TicTacToe_Pro.html"
Path(path).write_text(html, encoding="utf-8")
print(path)

