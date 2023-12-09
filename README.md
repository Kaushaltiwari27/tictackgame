# tictackgame
html code
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Tic-Tac-Toe Game</title>
    <link rel="stylesheet" href="tictac.css" />
  </head>
  <body>
    <div class="msg-container hide">
        <p id="msg">Winner</p>
        <button id="new">New Game</button>
    </div>
    <main>
        <h1>Tic Tac Toe</h1>
      <div class="container">
        <div class="game">
          <button class="box"></button>
          <button class="box"></button>
          <button class="box"></button>
          <button class="box"></button>
          <button class="box"></button>
          <button class="box"></button>
          <button class="box"></button>
          <button class="box"></button>
          <button class="box"></button>
        </div>
      </div>
      <button id="reset">Reset Game</button>
      
    </main>
    <script src="tictac.js"></script>
  </body>
</html>



css code
*{
    margin: 0;
    padding: 0;
}

body{
    background-color: #548687;
    text-align: center;
}

.container{
    height: 70vh;
    display: flex;
    justify-content: center;
    align-items: center;
}

.game{
    height: 60vmin;
    width: 60vmin;
    display: flex;
    flex-wrap: wrap;
    justify-content: center;
    align-items: center;
    gap: 1.2vmin;
}

.box{
    height: 18vmin;
    width: 18vmin;
    border-radius: 1rem;
    border: none;
    box-shadow: 0 0 1rem rgba(0,0,0,0.3);
    font-size: 8vmin;
    color: #b0416b;
    background-color: #ffffcf;
}

#reset{
    padding: 1rem;
    font-size: 1.25rem;
    background-color: #191913;
    color:#fff;
    border-radius: 1rem;
    border: none;
}
#new{
    padding: 1rem;
    font-size: 1.25rem;
    background-color: #191913;
    color:#fff;
    border-radius: 1rem;
    border: none;
}
#msg{
    color: #ffffc7;
    font-size: 8vmin;
}

.msg-container{
    height: 100vmin;
    display: flex;
    justify-content: center;
    align-items: center;
    flex-direction: column;
    gap: 2rem;
}

.hide{
    display: none;
}



javascript code
let boxes = document.querySelectorAll(".box");
let reserBtn = document.querySelector("#reset");
let newgamBtn=document.querySelector("#new");
let msgcontainer=document.querySelector(".msg-container");
let msg=document.querySelector("#msg");

let turnO = true;

const winPatterns = [
  [0, 1, 2],
  [0, 3, 6],
  [0, 4, 8],
  [1, 4, 7],
  [2, 5, 8],
  [2, 4, 6],
  [2, 4, 5],
  [6, 7, 8],
];

boxes.forEach((box) => {
  box.addEventListener("click", () => {
    if (turnO) {
      box.innerHTML = "O";
      turnO = false;
    } else {
      box.innerHTML = "X";
      turnO = true;
    }
    box.disable = true;

    chekWinner();
  });
});
const showWinner=(winner)=>{
    msg.innerText=`Conratulation, Winner is ${winner}`;
    msgcontainer.classList.remove("hide");
};

const disableBoxes=()=>{
    for(let box of boxes){
        box.disable=true;
    }
};
const enableBoxes=()=>{
    for(let box of boxes){
        box.disable=false;
        box.innerText="";
    }
};
const resertGame=()=>{
     trueO=true;
     enableBoxes();
     msgcontainer.classList.add("hide");
};

const chekWinner = () => {
  for (let pattern of winPatterns) {
    let pos1 = boxes[pattern[0]].innerText;
    let pos2 = boxes[pattern[1]].innerText;
    let pos3 = boxes[pattern[2]].innerText;
    if (pos1 != "" && pos2 != "" && pos3 != "") {
      if (pos1 == pos2 && pos2 == pos3) {
        disableBoxes();
        showWinner(pos1);
      }
    }
  }
};




newgamBtn.addEventListener("click",resertGame);
reserBtn.addEventListener("click",resertGame);
