function assignValues(mode){ //randomly assigns numbers to buttons so that no numbers repeat
    if(mode == 2 && gameStart == true){
        alert("Cannot Randomize in middle of a Game!!!");
        return;
    }
    let count = 0;
    let arr = [];

    for(let i=0;i<25;i++){
        arr[i] = i+1;
        count++;
    }

    do{
        let num = randomInteger(1 ,25);
        let exist = arr.find(element => element == num); 
        if(exist == null){
            continue;
        }
        else{
            document.getElementById(--count).innerHTML = num;      
            arr[arr.indexOf(exist)] = null;        
        }
    }while(count != 0);
}

var rows = [0,0,0,0,0];
var cols = [0,0,0,0,0];
var turns = 0;
var diag1 = 0;
var diag2 = 0;
var gameStart = false;

function pressedLocation(r_id,c_id,id){ //highlights the pressed button 
    gameStart = true;
    turns++; 

    document.getElementById(id).style.backgroundColor = "#7FFF00";
    document.getElementById("turns").innerHTML = turns;

    let win_condition = 0;
    
    rows[r_id]++;
    cols[c_id]++;

    if(turns > 4){
        for(let i=0;i<5;i++){
            if(rows[i] == 5 && cols[0]>0 && cols[1]>0 && cols[2]>0 && cols[3]>0 && cols[4]>0){
                highlight(win_condition++);
            }
            if(cols[i] == 5 && rows[0]>0 && rows[1]>0 && rows[2]>0 && rows[3]>0 && rows[4]>0){
                highlight(win_condition++);
            }
        }
        if(diag1 == 5){
            highlight(win_condition++);
        }
        if(diag2 == 5){
            highlight(win_condition++);
        }
    }
}
    
function randomInteger(min, max) {
    return Math.floor(Math.random() * (max - min + 1)) + min;
}

function highlight(location){
    let bingo = ['B','I','N','G','O'];

    document.getElementById(bingo[location]).style.backgroundColor = "#c0c0c0";
    document.getElementById(bingo[location]).style.color = "black";
}