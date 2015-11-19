# hit-the-luka


#java skript#

var levelFactor = 2;
var startSpeed = 1000;

var board = $('#board');

var i = 0;
while (i < 16) {
    board.append('<span></span>');
    i = i + 1;
}

var fields = board.find('span');
console.log(fields);

var interval;
var intervalTime;

function setLevel(level) {
    intervalTime = startSpeed * Math.pow(levelFactor, -level);
    if (interval) {
        clearInterval(interval);
    }
    interval = setInterval(newHitMe, intervalTime);
    console.log(intervalTime);
    $('#level span').text(level);
}
setLevel(0);

function newHitMe() {
    var index = Math.floor(Math.random() * fields.length);
    fields.eq(index).addClass('hitme');
    
    setTimeout(function () {
        fields.eq(index).removeClass('hitme');
    }, intervalTime * 2/3);
}


var score = 0;
function updateScore(add) {
    score = score + add;
    $('#score span').text(score);
    if (score % 5 == 0) {
        setLevel(score / 5);
    }
}
updateScore(0);

function fieldClick() {
    var el = $(this);
    if (el.hasClass('hitme')) {
        el.addClass('catched');
        el.removeClass('hitme');
        updateScore(1);
        
        setTimeout(function () {
            el.removeClass('hitme catched');
        }, intervalTime * 1/3);
    }
}

fields.on('click', fieldClick);



#css#

#board {
    border: 1p solid black;
    width: 400px;
    height: 400px;
}

#board span {
    width: 100px;
    height: 100px;
    float: left;
    background: black;
    transition: background 0.5s;
}

#board span.hitme {
    background: red;
    background-size: contain;
    transition: background 0.5s;
}

#board span.catched {
    background: blue;
    transition: background 0.2s;
}

#board span {
}

h1 {
   font-family: monospace;
   color: grey;
   text-align: center;
}



#html#

<h1>Catch me!</h1>
<div id="board">

</div>
<div id="score">Your score is <span></span></div>
<div id="level">At level <span></span></div>
