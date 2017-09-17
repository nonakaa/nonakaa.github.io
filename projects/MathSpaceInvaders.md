---
layout: project
type: project
image: images/pewpew.png
title: Math Space Invaders
permalink: projects/mathSpaceInvaders
date: 2014
labels:
  -Javascript
  -Python
summary:My partner and I made a space invaders math game for the STEM Conference
---


// http://docs.phaser.io/
// http://examples.phaser.io/_site/view_full.html?d=collision&f=bounding+box.js&t=bounding%20box
var game = new Phaser.Game(1024, 1182, Phaser.CANVAS,
  'phaser-game', {
    preload: preload,
    create: create,
    update: update
  });

function preload() {

   game.load.image('mole', 'assets/pewpew.png');
   
   game.load.image('arrow_controls_up', 'assets/arrow_controls_up.png');
   game.load.image('arrow_controls_down', 'assets/arrow_controls_down.png');
   game.load.image('arrow_controls_left', 'assets/arrow_controls_left.png');
   game.load.image('arrow_controls_right', 'assets/arrow_controls_right.png');
    game.load.image('button', 'assets/button.png');
   game.load.image('bullet', 'assets/bullet.png');
   game.load.image('n1', 'assets/01.png');
   game.load.image('n2', 'assets/02.png');
  game.load.image('n3', 'assets/03.png');
game.load.image('n4', 'assets/04.png');
  game.load.image('n5', 'assets/05.png');
game.load.image('n6', 'assets/06.png');
game.load.image('n7', 'assets/07.png');
game.load.image('n8', 'assets/08.png');
game.load.image('n9', 'assets/09.png');
game.load.image('n0', 'assets/00.png');
game.load.image('health', 'assets/health.png');

   // bg
   game.load.image('arrow_controls', 'assets/arrow_controls.png');

}
var movespeed = 5;
var cursors;
var sprite1;
var controlsbg;
var control_d_up;
var control_d_down;
var control_d_left;
var control_d_right;

var button_pressed = false;
var bullets; //keep track of bullets in a group
var enemies; //keep track of enemies in a group
var health1;
var health2;
var health3;
var correct_answer;

function create() {

  bullets = game.add.group(); //create the bullets group
  enemies = game.add.group(); // creates enemies

    health1 = game.add.sprite(25, 25, 'health');
health1.scale.setTo( 1, 1);
    health1.x = 50;
    health1.y = 25;

    health2 = game.add.sprite(25, 25, 'health');
health2.scale.setTo( 1, 1);
    health2.x = 90;
    health2.y = 25;

    health3 = game.add.sprite(25, 25, 'health');
health3.scale.setTo( 1, 1);
    health3.x = 130;
    health3.y = 25;

    cursors = game.input.keyboard.createCursorKeys();

    sprite1 = game.add.sprite(50, 50, 'mole');
sprite1.scale.setTo(.75,.75);
    sprite1.x = 200;
    sprite1.y = 100;

    var dpad_origin = { x:20, y: 750 };

    // bg
    controlsbg = game.add.sprite(dpad_origin.x, dpad_origin.y, 'arrow_controls');

    control_d_up = game.add.sprite(dpad_origin.x+63, dpad_origin.y, 'arrow_controls_up');
    control_d_up.inputEnabled=true;
    control_d_up.events.onInputDown.add(controls_listener_touch_up,this);
    control_d_up.events.onInputUp.add(controls_listener_untouch_up,this);

    control_d_down = game.add.sprite(dpad_origin.x+63, dpad_origin.y+134, 'arrow_controls_down');
    control_d_down.inputEnabled=true;
    control_d_down.events.onInputDown.add(controls_listener_touch_down,this);
    control_d_down.events.onInputUp.add(controls_listener_untouch_down,this);

    control_d_left = game.add.sprite(dpad_origin.x, dpad_origin.y+64, 'arrow_controls_left');
    control_d_left.inputEnabled=true;
    control_d_left.events.onInputDown.add(controls_listener_touch_left,this);
    control_d_left.events.onInputUp.add(controls_listener_untouch_left,this);

    control_d_right = game.add.sprite(dpad_origin.x+134, dpad_origin.y+64, 'arrow_controls_right');
    control_d_right.inputEnabled=true;
    control_d_right.events.onInputDown.add(controls_listener_touch_right,this);
    control_d_right.events.onInputUp.add(controls_listener_untouch_right,this);

    control_button = game.add.sprite(580, 800, 'button');
    control_button.inputEnabled=true;
    control_button.events.onInputDown.add(controls_listener_touch_button,this);
    control_button.events.onInputUp.add(controls_listener_untouch_button,this);

    createProblem();
}



var control_touched = {
  up : false,
  down : false,
  left : false,
  right : false
}

function controls_listener_touch_up (event) {
  control_touched.up = true;
}
function controls_listener_untouch_up (event) {
  control_touched.up = false;
}

function controls_listener_touch_down (event) {
  control_touched.down = true;
}
function controls_listener_untouch_down (event) {
  control_touched.down = false;
}

function controls_listener_touch_left (event) {
  control_touched.left = true;
}
function controls_listener_untouch_left (event) {
  control_touched.left = false;
}

function controls_listener_touch_right (event) {
  control_touched.right = true;
}
function controls_listener_untouch_right (event) {
  control_touched.right = false;
}

function controls_listener_touch_button (event) {
  if (!button_pressed){
    fire();
    button_pressed = true;
  }
}
function controls_listener_untouch_button (event) {
  button_pressed = false;
}

function fire(){
//spawn a bullet
var newbulllet = bullets.create(sprite1.x+(sprite1.width/2.725), sprite1.y-10, 'bullet');

}

function spawnenemies(num,x,y){
var newenemies = enemies.create(x,y,'n'+num);

}

function createProblem () {
  //random
  var first_operator = Math.floor(Math.random()*10); //0-9
  var second_operator = Math.floor(Math.random()*10); //0-9
  //check that answer is lss than 10
  while(first_operator + second_operator > 9){ //roll again
    first_operator = Math.floor(Math.random()*10); //0-9
    second_operator = Math.floor(Math.random()*10); //0-9
  }

  //store correct answer
  correct_answer = first_operator + second_operator;

  //render
  problem_str = first_operator + " + " + second_operator;
  document.getElementById('math_problem_container').innerHTML = problem_str;
}

function bulletHit(bullet, enemy){
  // console.log('hit');

  // kill the bullet
  bullet.kill();
  // bullets.remove(bullet); // THIS BREAKS

  // kill the enemy
  enemy.kill();
  enemies.remove(enemy);

  // score
  // handle scoring, check if it's the right answer




}

function update() {

  playerEnemyHit(enemy, player)

  //randomly spawn enemy between 0-10
    var frequency = 20; //higher is more frequent, 1000 is max
    if (Math.random()*1000 < frequency){
      spawnenemies (Math.floor(Math.random()*10), Math.random()*1024, -20);
    }

  // keyboard controls || touch controls
    if (cursors.up.isDown || control_touched.up)
    {
        //check if player is at top of page
        if(sprite1.body.y - movespeed > 0){
        sprite1.body.y -= movespeed;
    }
  }
    else if (cursors.down.isDown || control_touched.down)
    {
        //check if player is at bottom of screen
        if(sprite1.body.y + movespeed < 1100){
        sprite1.body.y += movespeed;
    }
  }

    if (cursors.left.isDown || control_touched.left)
    {
        //check if player is at left of screen
        if(sprite1.body.x - movespeed >0){
        sprite1.body.x -= movespeed;
    }
  }
    else if (cursors.right.isDown || control_touched.right)
    {
        //check if player is at left of screen
        if(sprite1.body.x + movespeed <860){
        sprite1.body.x += movespeed;
      }
    }


    bullets.forEachAlive(function(bullet){
      if(bullet !== undefined && bullet !== null && bullet.willDestroy !== undefined){
        bullet.kill(); // destroy later
      }else if(bullet !== null){
        //move bullets up
        bullet.body.y-=4;//bullet speed
      }

    });

      enemies.forEachAlive(function(enemy){
        enemy.body.y+=1;//bullet speed
    });


    game.physics.collide(bullets, enemies, bulletHit, null, this);
    game.physics.collide(enemies, sprite1, playerEnemyHit, null, this);
    
    // clean up
    // I HAVE NO IDEA HOW TO CLEAN UP THE DEAD!
    // bullets.forEachDead(function(bullet){
    //   bullet.destroy();
    // });

function resetBullet (bullet) {
bullet.kill();
}

}

