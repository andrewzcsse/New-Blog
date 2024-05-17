---
title: Andrew Zaletski College Articulation Blog
description: Blog post to describe the processes within platformer3x
layout: post
type: ccc
courses: { csse: {week: 21} }
comments: true
toc: true
---

## Game Control Code: Total __/5, Grade __/1 
- The `gameSetup` file begins by importing all relevant gameObjects from the other files within the repository 

```js
import Background from './Background.js'
import BackgroundHills from './BackgroundHills.js';
import BackgroundCoral from './BackgroundCoral.js';
import BackgroundMountains from './BackgroundMountains.js';
import BackgroundTransitions from './BackgroundTransitions.js';
import BackgroundClouds from './BackgroundClouds.js';
import BackgroundWinter from './BackgroundWinter.js';
import BackgroundSnow from './BackgroundSnow.js';
import BackgroundFish from './BackgroundFish.js';
import Platform from './Platform.js';
import JumpPlatform from './JumpPlatform.js';
import Player from './Player.js';
import PlayerHills from './PlayerHills.js';
import PlayerSkibidi from './PlayerSkibidi.js';
import PlayerWinter from './PlayerWinter.js';
import PlayerMini from './PlayerMini.js';
import PlayerQuidditch from './PlayerQuidditch.js';
import PlayerBase from './PlayerBase.js';
import Tube from './Tube.js';
import Tube1 from './Tube1.js';
import Tree from './Tree.js';
import Cabin from './Cabin.js';
import Goomba from './Goomba.js';
import FlyingGoomba from './FlyingGoomba.js';
import GlowBlock from './GlowBlock.js';
import Mushroom from './Mushroom.js';
import Coin from './Coin.js';
import Snowflake from './Snowflake.js';
import FlyingUFO from './FlyingUFO.js';
import Alien from './Alien.js';
import GameControl from './GameControl.js';
import Enemy from './Enemy.js';
import Owl from './Owl.js';
import Snowman from './Snowman.js';
import Cerberus from './Cerberus.js';
import PlayerGreece from './PlayerGreece.js';
import Flag from './Flag.js';
import Dragon from './Dragon.js';
import Star from './Star.js';
import Dementor from './Dementor.js';
import Draco from './Draco.js';
import skibidiTitan from './SkibidiTitan.js';
import Laser from './Laser.js';
import SkibidiToilet from './SkibidiToilet.js';
```

- For our level specifically, the referenced objects are `playerSkibidi`, `skibidiTitan`, `Laser` and `skibidiToilet`
- Then the objects are all initilized at the start of the game when `startGameCallBack` is called via an event listener

```js
startGameCallback: async function() {
        const id = document.getElementById("gameBegin");
        // Unhide the gameBegin button
        id.hidden = false;
        
        // Wait for the startGame button to be clicked
        await this.waitForButtonStart('startGame');
        // Hide the gameBegin button after it is clicked
        id.hidden = true;
        
        return true;
    }, 
```

- Following this, all appropriate assets are defined and given parameters 
- For our level, these assets include `vucbks` under obstacles, `skibidiSand` under platforms, `escaper` under players, and `skibidiToilet` and `skibidiTitan` under enemies
- After this, the level is defined under `skibidiGameObjects` and set to be a new gameLevel

```js
const skibidiGameObjects = [
          // GameObject(s), the order is important to z-index...
          { name: 'desert', id: 'background', class: Background, data: this.assets.backgrounds.desert },
          //{ name: 'clouds', id: 'background', class: BackgroundClouds, data: this.assets.backgrounds.clouds },
          { name: 'skibidiTitan', id: 'skibidiTitan', class: skibidiTitan, data: this.assets.enemies.skibidiTitan, xPercentage:  0.35, minPosition: 0.5 }, 
          { name: 'sand', id: 'platform', class: Platform, data: this.assets.platforms.sand },
          { name: 'blocks', id: 'jumpPlatform', class: BlockPlatform, data: this.assets.platforms.skibidiSand, xPercentage: 0.2, yPercentage: 1 },
          { name: 'blocks', id: 'jumpPlatform', class: BlockPlatform, data: this.assets.platforms.skibidiSand, xPercentage: 0.4, yPercentage: 0.6 },
          { name: 'blocks', id: 'jumpPlatform', class: BlockPlatform, data: this.assets.platforms.skibidiSand, xPercentage: 0.325, yPercentage: 0.8 },
          { name: 'blocks', id: 'jumpPlatform', class: BlockPlatform, data: this.assets.platforms.skibidiSand, xPercentage: 0.2, yPercentage: 0.5 },
          { name: 'blocks', id: 'jumpPlatform', class: BlockPlatform, data: this.assets.platforms.skibidiSand, xPercentage: 0.225, yPercentage: 0.5 },
          { name: 'blocks', id: 'jumpPlatform', class: BlockPlatform, data: this.assets.platforms.skibidiSand, xPercentage: 0.0, yPercentage: 0.5 } ,
          { name: 'blocks', id: 'jumpPlatform', class: BlockPlatform, data: this.assets.platforms.skibidiSand, xPercentage: 0.025, yPercentage: 0.5 },
          { name: 'blocks', id: 'jumpPlatform', class: BlockPlatform, data: this.assets.platforms.skibidiSand, xPercentage: 0.025, yPercentage: 0.5 },
          { name: 'coin', id: 'coin', class: Coin, data: this.assets.obstacles.vbucks, xPercentage: 0.325, yPercentage: 0.7 },
          { name: 'coin', id: 'coin', class: Coin, data: this.assets.obstacles.vbucks, xPercentage: -0.0125, yPercentage: 0.4 },
          { name: 'coin', id: 'coin', class: Coin, data: this.assets.obstacles.vbucks, xPercentage: 0.0125, yPercentage: 0.4 },
          { name: 'coin', id: 'coin', class: Coin, data: this.assets.obstacles.vbucks, xPercentage: 0.0325, yPercentage: 0.4 },
          { name: 'SkibidiToilet', id: 'SkibidiToilet', class: SkibidiToilet, data: this.assets.enemies.skibidiToilet, xPercentage:  0.3, minPosition: 0.07 },
          { name: 'SkibidiToilet', id: 'SkibidiToilet', class: SkibidiToilet, data: this.assets.enemies.skibidiToilet, xPercentage:  0.5, minPosition: 0.3 },
          { name: 'SkibidiToilet', id: 'SkibidiToilet', class: SkibidiToilet, data: this.assets.enemies.skibidiToilet, xPercentage:  0.75, minPosition: 0.5 }, //this special name is used for random event 2 to make sure that only one of the Goombas ends the random event
          { name: 'escaper', id: 'player', class: PlayerSkibidi, data: this.assets.players.escaper  },
          { name: 'laser', id: 'Laser', class: Laser, data: this.assets.obstacles.laser, xPercentage:  0.75, yPercentage: 0.5 },
          { name: 'toiletTube', id: 'toiletEnd', class: Tree, data: this.assets.obstacles.toilet },
          { name: 'complete3', id: 'background', class: BackgroundTransitions,  data: this.assets.backgrounds.complete3 },
        ];

        new GameLevel( {tag: "skibidi", callback: this.playerOffScreenCallBack, objects: skibidiGameObjects} );
```

- Finally the file is exported so that all properites can be called when necessary

```js
export default GameSetup;
```

## Class Design Using DrawIO Tool: Total __/3 Grade __/1