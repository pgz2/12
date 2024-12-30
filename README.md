/* ROOM */
const roomName = "Enter the name of your room";
const botName = "Judge";
const maxPlayers = 24; // maximum number of players in the room
const roomPublic = true; // true = public room | false = players only enter via the room link (it does not appear in the room list)
const geo = [{"lat": -22.9201, "lon": -43.3307, "code": "br"}, {"code": "FR", "lat": 46.2, "lon": 2.2}, {"code": "PL", "lat": 51.9, "lon": 19.1}, {"code": "GB", "lat": 55.3, "lon": -3.4}, {"code": "PT", "lat": 39.3, "lon": -8.2}]; 
// place your geoloc, so as not to have a leaky room

const room = HBInit({
    roomName: roomName,
    maxPlayers: maxPlayers,
    public: roomPublic,
    playerName: botName,
});
    geo: geo[0]

const scoreLimitPractice = 3;
const timeLimitPractice = 3;

let Cor = {
    Vermelho: 0xFA5646,
    Laranja: 0xFFC12F,
    Verde: 0x7DFA89,
    Azul: 0x05C5FF,
    Amarelo: 0xFFFF17,
    Cinza: 0xCCCCCC,
    Branco: 0xFFFFFF,
    Azulclaro: 0x6ECAFF,
    Powderblue: 0xB0E0E6,
    Roxo: 0x800080,
    Platinum: 0xE5E4E2,
    Gold: 0xffd700,
    Silver: 0xd5d5d5,
    Bronze: 0x896728,
    Thistle: 0xD8BFD8,
    Khaki: 0xF0E68C,
    AliceBlue: 0xF0F8FF,
    GhostWhite: 0xF8F8FF,
    Snow: 0xFFFAFA,
    Seashell:0xFFF5EE,
    FloralWhite: 0xFFFAF0,
    WhiteSmoke: 0xF5F5F5,
    Beige: 0xF5F5DC,
    OldLace: 0xFDF5E6,
    Ivory: 0xFFFFF0,
    Linen: 0xFAF0E6,
    Cornsilk: 0xFFF8DC,
    AntiqueWhite: 0xFAEBD7,
    BlanchedAlmond: 0xFFEBCD,
    Bisque: 0xFFE4C4,
    LightYellow: 0xFFFFE0,
    LemonChiffon: 0xFFFACD,
    LightGoldenrodYellow: 0xFAFAD2,
    PapayaWhip: 0xFFEFD5,
    PeachPuff: 0xFFDAB9,
    Moccasin: 0xFFE4B5,
    PaleGoldenrod: 0xEEE8AA,
    Azulescuro: 0x426AD6,
    Warn: 0xff9966
        }
    // here you can place/edit goal messages, always respecting the " , ". Example: "Belo gooool," the player's name will always be after the comma.     
    const frasesGols = [" WHAT A GOAL IS THAT, LADIES AND GENTLEMEN! You are a legend, ",
        " GOOOOOOOOOOL! THE WORLD NEEDS MORE LIKE YOU, ",
        " Look at this goal from ",
        " IT'S GOOOOOL from ",
        " What a great goal from ",
        " GOOOOOOOOOOL! SHOWING UP WHEN WE NEED IT MOST, THANKS TO ",
        " MY GOODNESS!!!! THE IMPOSSIBLE HAPPENED MY GOD IN HEAVEN, IT’S A GOAL FOR YOU ",
        " WHAT A GOAL FROM ",
        " Impressive completion of the ",
        " Sorry for the insults, BUT HOLY SHIT, WHAT A GOAL IS THAT, ",
        " IT'S CASH, IT'S CASH, IT'S CASH, IT'S GOOOOOOOOOL FROM "
    ];
    // here you can place/edit assistance messages, always respecting the " , ". Example: "Nice pass," the player's name will always be after the comma.
    const frasesasis = [" with the beautiful of ",
        " accompanied by the beautiful pass of ",
        " with the ball in the mouth of the goal by ",
        " with the phenomenal assistance of ",
        " and we cannot forget the magnificent pass of"
    ];
    // here you can post/edit messages for mockery, for own goals, always respecting the " , ". Example: "Try to kick to the other side," the player's name will always be after the comma.
    const frasesautogol = [" I'm sure it was by accident, right, ",
        " YOU'RE PLAYING FOR THE WRONG TEAM, ",
        " CONGRATULATIONS!! THE OPPONENT TEAM THANKS YOU, ",
        " IT'S GOOOOOOOOOL... against ",
        " Return to the sea offering, "
    ];

const secondsToResetAvatar = 3;
var registro = new Map();
const css = "border:2px solid;padding:8px;background:";
room.setTeamsLock(true);
var message;
var Botdivulga;
var msg1;
var msg1Time = 1500000;
var Deus = [];
var BotdivulgaTime = 900000;
var adminPassword = 4002;

var vip1 = [];
var vip2 = [];
var vip3 = [];

/* ESTÁDIO */

const playerRadius = 15;
var ballRadius = 6.25;
const triggerDistance = playerRadius + ballRadius + 0.01;

var practiceMap = `{
	"name": "Arena x3",
	"width": 648,
	"height": 270,
	"spawnDistance": 350,
	"bg": {
		"type": "",
		"width": 550,
		"height": 240,
		"kickOffRadius": 80,
		"cornerRadius": 0,
		"color": "1b2029"
	},
	"vertexes": [
		{
			"x": 550,
			"y": 240,
			"trait": "ballArea"
		},
		{
			"x": 550,
			"y": -240,
			"trait": "ballArea"
		},
		{
			"x": 0,
			"y": 270,
			"trait": "kickOffBarrier"
		},
		{
			"x": 0,
			"y": 80,
			"trait": "kickOffBarrier",
			"color": "F8F8F8",
			"vis": true,
			"curve": 180
		},
		{
			"x": 0,
			"y": -80,
			"trait": "kickOffBarrier",
			"color": "F8F8F8",
			"vis": true,
			"curve": 180
		},
		{
			"x": 0,
			"y": -270,
			"trait": "kickOffBarrier"
		},
		{
			"x": -550,
			"y": -80,
			"cMask": [
				"red",
				"blue",
				"ball"
			],
			"trait": "goalNet",
			"curve": 0,
			"color": "FF6666",
			"pos": [
				-700,
				-80
			]
		},
		{
			"x": -590,
			"y": -80,
			"cMask": [
				"ball"
			],
			"trait": "goalNet",
			"curve": -28.940588200131774,
			"color": "FF6666",
			"pos": [
				-700,
				-80
			]
		},
		{
			"x": -590,
			"y": 80,
			"cMask": [
				"ball"
			],
			"trait": "goalNet",
			"curve": -28.940588200131774,
			"color": "FF6666",
			"pos": [
				-700,
				80
			]
		},
		{
			"x": -550,
			"y": 80,
			"cMask": [
				"red",
				"blue",
				"ball"
			],
			"trait": "goalNet",
			"curve": 0,
			"color": "FF6666",
			"pos": [
				-700,
				80
			]
		},
		{
			"x": 550,
			"y": -80,
			"cMask": [
				"red",
				"blue",
				"ball"
			],
			"trait": "goalNet",
			"curve": 0,
			"color": "479BD8",
			"pos": [
				700,
				-80
			]
		},
		{
			"x": 590,
			"y": -80,
			"cMask": [
				"ball"
			],
			"trait": "goalNet",
			"curve": 0,
			"color": "479BD8",
			"pos": [
				700,
				-80
			]
		},
		{
			"x": 590,
			"y": 80,
			"cMask": [
				"ball"
			],
			"trait": "goalNet",
			"curve": 0,
			"color": "479BD8",
			"pos": [
				700,
				80
			]
		},
		{
			"x": 550,
			"y": 80,
			"cMask": [
				"red",
				"blue",
				"ball"
			],
			"trait": "goalNet",
			"curve": 0,
			"color": "479BD8",
			"pos": [
				700,
				80
			]
		},
		{
			"x": -550,
			"y": 80,
			"bCoef": 1.25,
			"cMask": [
				"ball"
			],
			"trait": "ballArea",
			"color": "F8F8F8",
			"pos": [
				-700,
				80
			]
		},
		{
			"x": -550,
			"y": 240,
			"bCoef": 1.25,
			"cMask": [
				"ball"
			],
			"trait": "ballArea",
			"color": "F8F8F8"
		},
		{
			"x": -550,
			"y": -80,
			"bCoef": 1.25,
			"cMask": [
				"ball"
			],
			"trait": "ballArea",
			"color": "F8F8F8",
			"pos": [
				-700,
				-80
			]
		},
		{
			"x": -550,
			"y": -240,
			"bCoef": 1.25,
			"cMask": [
				"ball"
			],
			"trait": "ballArea",
			"color": "F8F8F8"
		},
		{
			"x": -550,
			"y": 240,
			"bCoef": 1,
			"cMask": [
				"ball"
			],
			"trait": "ballArea"
		},
		{
			"x": 550,
			"y": 240,
			"bCoef": 1,
			"cMask": [
				"ball"
			],
			"trait": "ballArea"
		},
		{
			"x": 550,
			"y": 80,
			"bCoef": 1.25,
			"cMask": [
				"ball"
			],
			"trait": "ballArea",
			"pos": [
				700,
				80
			]
		},
		{
			"x": 550,
			"y": 240,
			"bCoef": 1.25,
			"cMask": [
				"ball"
			],
			"trait": "ballArea"
		},
		{
			"x": 550,
			"y": -240,
			"bCoef": 1.25,
			"cMask": [
				"ball"
			],
			"trait": "ballArea",
			"color": "F8F8F8"
		},
		{
			"x": 550,
			"y": -80,
			"bCoef": 1.25,
			"cMask": [
				"ball"
			],
			"trait": "ballArea",
			"color": "F8F8F8",
			"pos": [
				700,
				-80
			]
		},
		{
			"x": 550,
			"y": -240,
			"bCoef": 0,
			"cMask": [
				"ball"
			],
			"trait": "ballArea"
		},
		{
			"x": 550,
			"y": -240,
			"bCoef": 0,
			"cMask": [
				"ball"
			],
			"trait": "ballArea"
		},
		{
			"x": -550,
			"y": -240,
			"bCoef": 1,
			"cMask": [
				"ball"
			],
			"trait": "ballArea",
			"curve": 0
		},
		{
			"x": 550,
			"y": -240,
			"bCoef": 1,
			"cMask": [
				"ball"
			],
			"trait": "ballArea",
			"curve": 0
		},
		{
			"x": 0,
			"y": -240,
			"bCoef": 0.1,
			"cMask": [
				"red",
				"blue"
			],
			"cGroup": [
				"redKO",
				"blueKO"
			],
			"trait": "kickOffBarrier"
		},
		{
			"x": 0,
			"y": -80,
			"bCoef": 0.1,
			"cMask": [
				"red",
				"blue"
			],
			"cGroup": [
				"redKO",
				"blueKO"
			],
			"trait": "kickOffBarrier"
		},
		{
			"x": 0,
			"y": 80,
			"bCoef": 0.1,
			"cMask": [
				"red",
				"blue"
			],
			"cGroup": [
				"redKO",
				"blueKO"
			],
			"trait": "kickOffBarrier"
		},
		{
			"x": 0,
			"y": 240,
			"bCoef": 0.1,
			"cMask": [
				"red",
				"blue"
			],
			"cGroup": [
				"redKO",
				"blueKO"
			],
			"trait": "kickOffBarrier"
		},
		{
			"x": 0,
			"y": -80,
			"bCoef": 0.1,
			"cMask": [
				"red",
				"blue"
			],
			"trait": "kickOffBarrier",
			"vis": true,
			"color": "F8F8F8"
		},
		{
			"x": 0,
			"y": 80,
			"bCoef": 0.1,
			"cMask": [
				"red",
				"blue"
			],
			"trait": "kickOffBarrier",
			"vis": true,
			"color": "F8F8F8"
		},
		{
			"x": 0,
			"y": 80,
			"trait": "kickOffBarrier",
			"color": "F8F8F8",
			"vis": true,
			"curve": -180
		},
		{
			"x": 0,
			"y": -80,
			"trait": "kickOffBarrier",
			"color": "F8F8F8",
			"vis": true,
			"curve": -180
		},
		{
			"x": 0,
			"y": 80,
			"trait": "kickOffBarrier",
			"color": "F8F8F8",
			"vis": true,
			"curve": 0
		},
		{
			"x": 0,
			"y": -80,
			"trait": "kickOffBarrier",
			"color": "F8F8F8",
			"vis": true,
			"curve": 0
		},
		{
			"x": -557.5,
			"y": 80,
			"bCoef": 0.1,
			"cMask": [
				"ball"
			],
			"trait": "ballArea",
			"curve": 0,
			"vis": false,
			"pos": [
				-700,
				80
			]
		},
		{
			"x": -557.5,
			"y": 240,
			"bCoef": 2,
			"cMask": [
				"ball"
			],
			"trait": "ballArea",
			"curve": 0,
			"vis": false
		},
		{
			"x": -557.5,
			"y": -240,
			"bCoef": 2,
			"cMask": [
				"ball"
			],
			"trait": "ballArea",
			"vis": false,
			"curve": 0
		},
		{
			"x": -557.5,
			"y": -80,
			"bCoef": 0.1,
			"cMask": [
				"ball"
			],
			"trait": "ballArea",
			"vis": false,
			"curve": 0,
			"pos": [
				-700,
				-80
			]
		},
		{
			"x": 557.5,
			"y": -240,
			"bCoef": 2,
			"cMask": [
				"ball"
			],
			"trait": "ballArea",
			"vis": false,
			"curve": 0
		},
		{
			"x": 557.5,
			"y": -80,
			"bCoef": 0.1,
			"cMask": [
				"ball"
			],
			"trait": "ballArea",
			"vis": false,
			"curve": 0,
			"pos": [
				700,
				-80
			]
		},
		{
			"x": 557.5,
			"y": 80,
			"bCoef": 0.1,
			"cMask": [
				"ball"
			],
			"trait": "ballArea",
			"curve": 0,
			"vis": false,
			"pos": [
				700,
				80
			]
		},
		{
			"x": 557.5,
			"y": 240,
			"bCoef": 2,
			"cMask": [
				"ball"
			],
			"trait": "ballArea",
			"curve": 0,
			"vis": false
		},
		{
			"x": 0,
			"y": -80,
			"bCoef": 0.1,
			"trait": "line"
		},
		{
			"x": 0,
			"y": 80,
			"bCoef": 0.1,
			"trait": "line"
		},
		{
			"x": -550,
			"y": -80,
			"bCoef": 0.1,
			"trait": "line"
		},
		{
			"x": -550,
			"y": 80,
			"bCoef": 0.1,
			"trait": "line"
		},
		{
			"x": 550,
			"y": -80,
			"bCoef": 0.1,
			"trait": "line"
		},
		{
			"x": 550,
			"y": 80,
			"bCoef": 0.1,
			"trait": "line"
		},
		{
			"x": -381,
			"y": 240,
			"bCoef": 0.1,
			"trait": "line"
		},
		{
			"x": -381,
			"y": 256,
			"bCoef": 0.1,
			"trait": "line"
		},
		{
			"x": -550,
			"y": 200,
			"bCoef": 0.1,
			"trait": "line",
			"color": "F8F8F8",
			"curve": -90
		},
		{
			"x": -390,
			"y": 70,
			"bCoef": 0.1,
			"trait": "line",
			"color": "F8F8F8",
			"curve": 0
		},
		{
			"x": -550,
			"y": 226,
			"bCoef": 0.1,
			"trait": "line",
			"curve": -90
		},
		{
			"x": -536,
			"y": 240,
			"bCoef": 0.1,
			"trait": "line",
			"curve": -90
		},
		{
			"x": -550,
			"y": -200,
			"bCoef": 0.1,
			"trait": "line",
			"color": "F8F8F8",
			"curve": 90
		},
		{
			"x": -390,
			"y": -70,
			"bCoef": 0.1,
			"trait": "line",
			"color": "F8F8F8",
			"curve": 0
		},
		{
			"x": -550,
			"y": -226,
			"bCoef": 0.1,
			"trait": "line",
			"curve": 90
		},
		{
			"x": -536,
			"y": -240,
			"bCoef": 0.1,
			"trait": "line",
			"curve": 90
		},
		{
			"x": -556,
			"y": 123,
			"bCoef": 0.1,
			"trait": "line"
		},
		{
			"x": -575,
			"y": 123,
			"bCoef": 0.1,
			"trait": "line"
		},
		{
			"x": 556,
			"y": 123,
			"bCoef": 0.1,
			"trait": "line"
		},
		{
			"x": 575,
			"y": 123,
			"bCoef": 0.1,
			"trait": "line"
		},
		{
			"x": -556,
			"y": -123,
			"bCoef": 0.1,
			"trait": "line"
		},
		{
			"x": -575,
			"y": -123,
			"bCoef": 0.1,
			"trait": "line"
		},
		{
			"x": 556,
			"y": -123,
			"bCoef": 0.1,
			"trait": "line"
		},
		{
			"x": 575,
			"y": -123,
			"bCoef": 0.1,
			"trait": "line"
		},
		{
			"x": -381,
			"y": -240,
			"bCoef": 0.1,
			"trait": "line"
		},
		{
			"x": -381,
			"y": -256,
			"bCoef": 0.1,
			"trait": "line"
		},
		{
			"x": 381,
			"y": 240,
			"bCoef": 0.1,
			"trait": "line"
		},
		{
			"x": 381,
			"y": -240,
			"bCoef": 0.1,
			"trait": "line"
		},
		{
			"x": 381,
			"y": -256,
			"bCoef": 0.1,
			"trait": "line"
		},
		{
			"x": 550,
			"y": -226,
			"bCoef": 0.1,
			"trait": "line",
			"curve": -90
		},
		{
			"x": 536,
			"y": -240,
			"bCoef": 0.1,
			"trait": "line",
			"curve": -90
		},
		{
			"x": 550,
			"y": 226,
			"bCoef": 0.1,
			"trait": "line",
			"curve": 90
		},
		{
			"x": 536,
			"y": 240,
			"bCoef": 0.1,
			"trait": "line",
			"curve": 90
		},
		{
			"x": 550,
			"y": 200,
			"bCoef": 0.1,
			"trait": "line",
			"color": "F8F8F8",
			"curve": 90
		},
		{
			"x": 390,
			"y": 70,
			"bCoef": 0.1,
			"trait": "line",
			"color": "F8F8F8",
			"curve": 90
		},
		{
			"x": 550,
			"y": -200,
			"bCoef": 0.1,
			"trait": "line",
			"color": "F8F8F8",
			"curve": -90
		},
		{
			"x": 390,
			"y": -70,
			"bCoef": 0.1,
			"trait": "line",
			"color": "F8F8F8",
			"curve": -90
		},
		{
			"x": 390,
			"y": 70,
			"bCoef": 0.1,
			"trait": "line",
			"color": "F8F8F8",
			"curve": 0
		},
		{
			"x": 390,
			"y": -70,
			"bCoef": 0.1,
			"trait": "line",
			"color": "F8F8F8",
			"curve": 0
		},
		{
			"x": -375,
			"y": 1,
			"bCoef": 0.1,
			"trait": "line",
			"curve": 180
		},
		{
			"x": -375,
			"y": -1,
			"bCoef": 0.1,
			"trait": "line",
			"curve": 180
		},
		{
			"x": -375,
			"y": 3,
			"bCoef": 0.1,
			"trait": "line",
			"curve": 180
		},
		{
			"x": -375,
			"y": -3,
			"bCoef": 0.1,
			"trait": "line",
			"curve": 180
		},
		{
			"x": -375,
			"y": -2,
			"bCoef": 0.1,
			"trait": "line",
			"curve": 180
		},
		{
			"x": -375,
			"y": 2,
			"bCoef": 0.1,
			"trait": "line",
			"curve": 180
		},
		{
			"x": -375,
			"y": -3.5,
			"bCoef": 0.1,
			"trait": "line",
			"curve": 180
		},
		{
			"x": -375,
			"y": 3.5,
			"bCoef": 0.1,
			"trait": "line",
			"curve": 180
		},
		{
			"x": 375,
			"y": 1,
			"bCoef": 0.1,
			"trait": "line",
			"curve": 180
		},
		{
			"x": 375,
			"y": -1,
			"bCoef": 0.1,
			"trait": "line",
			"curve": 180
		},
		{
			"x": 375,
			"y": 3,
			"bCoef": 0.1,
			"trait": "line",
			"curve": 180
		},
		{
			"x": 375,
			"y": -3,
			"bCoef": 0.1,
			"trait": "line",
			"curve": 180
		},
		{
			"x": 375,
			"y": -2,
			"bCoef": 0.1,
			"trait": "line",
			"curve": 180
		},
		{
			"x": 375,
			"y": 2,
			"bCoef": 0.1,
			"trait": "line",
			"curve": 180
		},
		{
			"x": 375,
			"y": -3.5,
			"bCoef": 0.1,
			"trait": "line",
			"curve": 180
		},
		{
			"x": 375,
			"y": 3.5,
			"bCoef": 0.1,
			"trait": "line",
			"curve": 180
		},
		{
			"x": -277.5,
			"y": 1,
			"bCoef": 0.1,
			"trait": "line",
			"curve": 180
		},
		{
			"x": -277.5,
			"y": -1,
			"bCoef": 0.1,
			"trait": "line",
			"curve": 180
		},
		{
			"x": -277.5,
			"y": 3,
			"bCoef": 0.1,
			"trait": "line",
			"curve": 180
		},
		{
			"x": -277.5,
			"y": -3,
			"bCoef": 0.1,
			"trait": "line",
			"curve": 180
		},
		{
			"x": -277.5,
			"y": -2,
			"bCoef": 0.1,
			"trait": "line",
			"curve": 180
		},
		{
			"x": -277.5,
			"y": 2,
			"bCoef": 0.1,
			"trait": "line",
			"curve": 180
		},
		{
			"x": -277.5,
			"y": -3.5,
			"bCoef": 0.1,
			"trait": "line",
			"curve": 180
		},
		{
			"x": -277.5,
			"y": 3.5,
			"bCoef": 0.1,
			"trait": "line",
			"curve": 180
		},
		{
			"x": 277.5,
			"y": 1,
			"bCoef": 0.1,
			"trait": "line",
			"curve": 180
		},
		{
			"x": 277.5,
			"y": -1,
			"bCoef": 0.1,
			"trait": "line",
			"curve": 180
		},
		{
			"x": 277.5,
			"y": 3,
			"bCoef": 0.1,
			"trait": "line",
			"curve": 180
		},
		{
			"x": 277.5,
			"y": -3,
			"bCoef": 0.1,
			"trait": "line",
			"curve": 180
		},
		{
			"x": 277.5,
			"y": -2,
			"bCoef": 0.1,
			"trait": "line",
			"curve": 180
		},
		{
			"x": 277.5,
			"y": 2,
			"bCoef": 0.1,
			"trait": "line",
			"curve": 180
		},
		{
			"x": 277.5,
			"y": -3.5,
			"bCoef": 0.1,
			"trait": "line",
			"curve": 180
		},
		{
			"x": 277.5,
			"y": 3.5,
			"bCoef": 0.1,
			"trait": "line",
			"curve": 180
		}
	],
	"segments": [
		{
			"v0": 6,
			"v1": 7,
			"curve": 0,
			"color": "FF6666",
			"cMask": [
				"red",
				"blue",
				"ball"
			],
			"trait": "goalNet",
			"pos": [
				-700,
				-80
			],
			"y": -80
		},
		{
			"v0": 7,
			"v1": 8,
			"curve": -28.940588200131774,
			"color": "FF6666",
			"cMask": [
				"ball"
			],
			"trait": "goalNet",
			"x": -590
		},
		{
			"v0": 8,
			"v1": 9,
			"curve": 0,
			"color": "FF6666",
			"cMask": [
				"red",
				"blue",
				"ball"
			],
			"trait": "goalNet",
			"pos": [
				-700,
				80
			],
			"y": 80
		},
		{
			"v0": 10,
			"v1": 11,
			"curve": 0,
			"color": "479BD8",
			"cMask": [
				"red",
				"blue",
				"ball"
			],
			"trait": "goalNet",
			"pos": [
				700,
				-80
			],
			"y": -80
		},
		{
			"v0": 11,
			"v1": 12,
			"curve": 28.940588200131774,
			"color": "479BD8",
			"cMask": [
				"ball"
			],
			"trait": "goalNet",
			"x": 590
		},
		{
			"v0": 12,
			"v1": 13,
			"curve": 0,
			"color": "479BD8",
			"cMask": [
				"red",
				"blue",
				"ball"
			],
			"trait": "goalNet",
			"pos": [
				700,
				80
			],
			"y": 80
		},
		{
			"v0": 2,
			"v1": 3,
			"trait": "kickOffBarrier"
		},
		{
			"v0": 3,
			"v1": 4,
			"curve": 180,
			"vis": true,
			"color": "F8F8F8",
			"cGroup": [
				"blueKO"
			],
			"trait": "kickOffBarrier"
		},
		{
			"v0": 3,
			"v1": 4,
			"curve": -180,
			"vis": true,
			"color": "F8F8F8",
			"cGroup": [
				"redKO"
			],
			"trait": "kickOffBarrier"
		},
		{
			"v0": 4,
			"v1": 5,
			"trait": "kickOffBarrier"
		},
		{
			"v0": 14,
			"v1": 15,
			"vis": true,
			"color": "F8F8F8",
			"bCoef": 1.25,
			"cMask": [
				"ball"
			],
			"trait": "ballArea",
			"x": -550
		},
		{
			"v0": 16,
			"v1": 17,
			"vis": true,
			"color": "F8F8F8",
			"bCoef": 1.25,
			"cMask": [
				"ball"
			],
			"trait": "ballArea",
			"x": -550
		},
		{
			"v0": 18,
			"v1": 19,
			"vis": true,
			"color": "F8F8F8",
			"bCoef": 1,
			"cMask": [
				"ball"
			],
			"trait": "ballArea",
			"y": 240
		},
		{
			"v0": 20,
			"v1": 21,
			"vis": true,
			"color": "F8F8F8",
			"bCoef": 1.25,
			"cMask": [
				"ball"
			],
			"trait": "ballArea",
			"x": 550
		},
		{
			"v0": 22,
			"v1": 23,
			"vis": true,
			"color": "F8F8F8",
			"bCoef": 1.25,
			"cMask": [
				"ball"
			],
			"trait": "ballArea",
			"x": 550
		},
		{
			"v0": 24,
			"v1": 25,
			"vis": true,
			"color": "F8F8F8",
			"bCoef": 0,
			"cMask": [
				"ball"
			],
			"trait": "ballArea",
			"x": 550,
			"y": -240
		},
		{
			"v0": 26,
			"v1": 27,
			"curve": 0,
			"vis": true,
			"color": "F8F8F8",
			"bCoef": 1,
			"cMask": [
				"ball"
			],
			"trait": "ballArea",
			"y": -240
		},
		{
			"v0": 28,
			"v1": 29,
			"vis": true,
			"color": "F8F8F8",
			"bCoef": 0.1,
			"cMask": [
				"red",
				"blue"
			],
			"cGroup": [
				"redKO",
				"blueKO"
			],
			"trait": "kickOffBarrier"
		},
		{
			"v0": 30,
			"v1": 31,
			"vis": true,
			"color": "F8F8F8",
			"bCoef": 0.1,
			"cMask": [
				"red",
				"blue"
			],
			"cGroup": [
				"redKO",
				"blueKO"
			],
			"trait": "kickOffBarrier"
		},
		{
			"v0": 38,
			"v1": 39,
			"curve": 0,
			"vis": false,
			"color": "F8F8F8",
			"bCoef": 2,
			"cMask": [
				"ball"
			],
			"trait": "ballArea",
			"x": -557.5
		},
		{
			"v0": 40,
			"v1": 41,
			"curve": 0,
			"vis": false,
			"color": "F8F8F8",
			"bCoef": 2,
			"cMask": [
				"ball"
			],
			"trait": "ballArea",
			"x": -557.5
		},
		{
			"v0": 42,
			"v1": 43,
			"curve": 0,
			"vis": false,
			"color": "F8F8F8",
			"bCoef": 2,
			"cMask": [
				"ball"
			],
			"trait": "ballArea",
			"x": 557.5
		},
		{
			"v0": 44,
			"v1": 45,
			"curve": 0,
			"vis": false,
			"color": "F8F8F8",
			"bCoef": 2,
			"cMask": [
				"ball"
			],
			"trait": "ballArea",
			"x": 557.5
		},
		{
			"v0": 46,
			"v1": 47,
			"curve": 0,
			"vis": true,
			"color": "F8F8F8",
			"bCoef": 0.1,
			"trait": "line",
			"x": 0
		},
		{
			"v0": 48,
			"v1": 49,
			"curve": 0,
			"vis": true,
			"color": "F8F8F8",
			"bCoef": 0.1,
			"trait": "line",
			"x": -550
		},
		{
			"v0": 50,
			"v1": 51,
			"curve": 0,
			"vis": true,
			"color": "F8F8F8",
			"bCoef": 0.1,
			"trait": "line",
			"x": 550
		},
		{
			"v0": 52,
			"v1": 53,
			"curve": 0,
			"vis": true,
			"color": "F8F8F8",
			"bCoef": 0.1,
			"trait": "line",
			"x": -381
		},
		{
			"v0": 54,
			"v1": 55,
			"curve": -90,
			"vis": true,
			"color": "F8F8F8",
			"bCoef": 0.1,
			"trait": "line"
		},
		{
			"v0": 57,
			"v1": 56,
			"curve": -90,
			"vis": true,
			"color": "F8F8F8",
			"bCoef": 0.1,
			"trait": "line"
		},
		{
			"v0": 58,
			"v1": 59,
			"curve": 90,
			"vis": true,
			"color": "F8F8F8",
			"bCoef": 0.1,
			"trait": "line"
		},
		{
			"v0": 55,
			"v1": 59,
			"curve": 0,
			"vis": true,
			"color": "F8F8F8",
			"bCoef": 0.1,
			"trait": "line"
		},
		{
			"v0": 61,
			"v1": 60,
			"curve": 90,
			"vis": true,
			"color": "F8F8F8",
			"bCoef": 0.1,
			"trait": "line"
		},
		{
			"v0": 62,
			"v1": 63,
			"curve": 0,
			"vis": true,
			"color": "F8F8F8",
			"bCoef": 0.1,
			"trait": "line",
			"x": -240,
			"y": 123
		},
		{
			"v0": 64,
			"v1": 65,
			"curve": 0,
			"vis": true,
			"color": "F8F8F8",
			"bCoef": 0.1,
			"trait": "line",
			"x": -240,
			"y": 123
		},
		{
			"v0": 66,
			"v1": 67,
			"curve": 0,
			"vis": true,
			"color": "F8F8F8",
			"bCoef": 0.1,
			"trait": "line",
			"x": -240,
			"y": -123
		},
		{
			"v0": 68,
			"v1": 69,
			"curve": 0,
			"vis": true,
			"color": "F8F8F8",
			"bCoef": 0.1,
			"trait": "line",
			"x": -240,
			"y": -123
		},
		{
			"v0": 70,
			"v1": 71,
			"curve": 0,
			"vis": true,
			"color": "F8F8F8",
			"bCoef": 0.1,
			"trait": "line",
			"x": -381
		},
		{
			"v0": 73,
			"v1": 74,
			"curve": 0,
			"vis": true,
			"color": "F8F8F8",
			"bCoef": 0.1,
			"trait": "line",
			"x": 381
		},
		{
			"v0": 76,
			"v1": 75,
			"curve": -90,
			"vis": true,
			"color": "F8F8F8",
			"bCoef": 0.1,
			"trait": "line"
		},
		{
			"v0": 78,
			"v1": 77,
			"curve": 90,
			"vis": true,
			"color": "F8F8F8",
			"bCoef": 0.1,
			"trait": "line"
		},
		{
			"v0": 79,
			"v1": 80,
			"curve": 90,
			"vis": true,
			"color": "F8F8F8",
			"bCoef": 0.1,
			"trait": "line"
		},
		{
			"v0": 81,
			"v1": 82,
			"curve": -90,
			"vis": true,
			"color": "F8F8F8",
			"bCoef": 0.1,
			"trait": "line"
		},
		{
			"v0": 83,
			"v1": 84,
			"curve": 0,
			"vis": true,
			"color": "F8F8F8",
			"bCoef": 0.1,
			"trait": "line",
			"x": 390
		},
		{
			"v0": 86,
			"v1": 85,
			"curve": 180,
			"vis": true,
			"color": "F8F8F8",
			"bCoef": 0.1,
			"trait": "line",
			"x": -375
		},
		{
			"v0": 85,
			"v1": 86,
			"curve": 180,
			"vis": true,
			"color": "F8F8F8",
			"bCoef": 0.1,
			"trait": "line",
			"x": -375
		},
		{
			"v0": 88,
			"v1": 87,
			"curve": 180,
			"vis": true,
			"color": "F8F8F8",
			"bCoef": 0.1,
			"trait": "line",
			"x": -375
		},
		{
			"v0": 87,
			"v1": 88,
			"curve": 180,
			"vis": true,
			"color": "F8F8F8",
			"bCoef": 0.1,
			"trait": "line",
			"x": -375
		},
		{
			"v0": 90,
			"v1": 89,
			"curve": 180,
			"vis": true,
			"color": "F8F8F8",
			"bCoef": 0.1,
			"trait": "line",
			"x": -375
		},
		{
			"v0": 89,
			"v1": 90,
			"curve": 180,
			"vis": true,
			"color": "F8F8F8",
			"bCoef": 0.1,
			"trait": "line",
			"x": -375
		},
		{
			"v0": 92,
			"v1": 91,
			"curve": 180,
			"vis": true,
			"color": "F8F8F8",
			"bCoef": 0.1,
			"trait": "line",
			"x": -375
		},
		{
			"v0": 91,
			"v1": 92,
			"curve": 180,
			"vis": true,
			"color": "F8F8F8",
			"bCoef": 0.1,
			"trait": "line",
			"x": -375
		},
		{
			"v0": 94,
			"v1": 93,
			"curve": 180,
			"vis": true,
			"color": "F8F8F8",
			"bCoef": 0.1,
			"trait": "line",
			"x": 375
		},
		{
			"v0": 93,
			"v1": 94,
			"curve": 180,
			"vis": true,
			"color": "F8F8F8",
			"bCoef": 0.1,
			"trait": "line",
			"x": 375
		},
		{
			"v0": 96,
			"v1": 95,
			"curve": 180,
			"vis": true,
			"color": "F8F8F8",
			"bCoef": 0.1,
			"trait": "line",
			"x": 375
		},
		{
			"v0": 95,
			"v1": 96,
			"curve": 180,
			"vis": true,
			"color": "F8F8F8",
			"bCoef": 0.1,
			"trait": "line",
			"x": 375
		},
		{
			"v0": 98,
			"v1": 97,
			"curve": 180,
			"vis": true,
			"color": "F8F8F8",
			"bCoef": 0.1,
			"trait": "line",
			"x": 375
		},
		{
			"v0": 97,
			"v1": 98,
			"curve": 180,
			"vis": true,
			"color": "F8F8F8",
			"bCoef": 0.1,
			"trait": "line",
			"x": 375
		},
		{
			"v0": 100,
			"v1": 99,
			"curve": 180,
			"vis": true,
			"color": "F8F8F8",
			"bCoef": 0.1,
			"trait": "line",
			"x": 375
		},
		{
			"v0": 99,
			"v1": 100,
			"curve": 180,
			"vis": true,
			"color": "F8F8F8",
			"bCoef": 0.1,
			"trait": "line",
			"x": 375
		},
		{
			"v0": 102,
			"v1": 101,
			"curve": 180,
			"vis": true,
			"color": "F8F8F8",
			"bCoef": 0.1,
			"trait": "line",
			"x": -277.5
		},
		{
			"v0": 101,
			"v1": 102,
			"curve": 180,
			"vis": true,
			"color": "F8F8F8",
			"bCoef": 0.1,
			"trait": "line",
			"x": -277.5
		},
		{
			"v0": 104,
			"v1": 103,
			"curve": 180,
			"vis": true,
			"color": "F8F8F8",
			"bCoef": 0.1,
			"trait": "line",
			"x": -277.5
		},
		{
			"v0": 103,
			"v1": 104,
			"curve": 180,
			"vis": true,
			"color": "F8F8F8",
			"bCoef": 0.1,
			"trait": "line",
			"x": -277.5
		},
		{
			"v0": 106,
			"v1": 105,
			"curve": 180,
			"vis": true,
			"color": "F8F8F8",
			"bCoef": 0.1,
			"trait": "line",
			"x": -277.5
		},
		{
			"v0": 105,
			"v1": 106,
			"curve": 180,
			"vis": true,
			"color": "F8F8F8",
			"bCoef": 0.1,
			"trait": "line",
			"x": -277.5
		},
		{
			"v0": 108,
			"v1": 107,
			"curve": 180,
			"vis": true,
			"color": "F8F8F8",
			"bCoef": 0.1,
			"trait": "line",
			"x": -277.5
		},
		{
			"v0": 107,
			"v1": 108,
			"curve": 180,
			"vis": true,
			"color": "F8F8F8",
			"bCoef": 0.1,
			"trait": "line",
			"x": -277.5
		},
		{
			"v0": 110,
			"v1": 109,
			"curve": 180,
			"vis": true,
			"color": "F8F8F8",
			"bCoef": 0.1,
			"trait": "line",
			"x": 277.5
		},
		{
			"v0": 109,
			"v1": 110,
			"curve": 180,
			"vis": true,
			"color": "F8F8F8",
			"bCoef": 0.1,
			"trait": "line",
			"x": 277.5
		},
		{
			"v0": 112,
			"v1": 111,
			"curve": 180,
			"vis": true,
			"color": "F8F8F8",
			"bCoef": 0.1,
			"trait": "line",
			"x": 277.5
		},
		{
			"v0": 111,
			"v1": 112,
			"curve": 180,
			"vis": true,
			"color": "F8F8F8",
			"bCoef": 0.1,
			"trait": "line",
			"x": 277.5
		},
		{
			"v0": 114,
			"v1": 113,
			"curve": 180,
			"vis": true,
			"color": "F8F8F8",
			"bCoef": 0.1,
			"trait": "line",
			"x": 277.5
		},
		{
			"v0": 113,
			"v1": 114,
			"curve": 180,
			"vis": true,
			"color": "F8F8F8",
			"bCoef": 0.1,
			"trait": "line",
			"x": 277.5
		},
		{
			"v0": 116,
			"v1": 115,
			"curve": 180,
			"vis": true,
			"color": "F8F8F8",
			"bCoef": 0.1,
			"trait": "line",
			"x": 277.5
		},
		{
			"v0": 115,
			"v1": 116,
			"curve": 180,
			"vis": true,
			"color": "F8F8F8",
			"bCoef": 0.1,
			"trait": "line",
			"x": 277.5
		}
	],
	"goals": [
		{
			"p0": [
				-556.3,
				-80
			],
			"p1": [
				-556.3,
				80
			],
			"team": "red"
		},
		{
			"p0": [
				556.3,
				80
			],
			"p1": [
				556.3,
				-80
			],
			"team": "blue"
		}
	],
	"discs": [
		{
			"radius": 5,
			"pos": [
				-550,
				80
			],
			"color": "FF6666",
			"trait": "goalPost",
			"y": 80
		},
		{
			"radius": 5,
			"pos": [
				-550,
				-80
			],
			"color": "FF6666",
			"trait": "goalPost",
			"y": -80,
			"x": -560
		},
		{
			"radius": 5,
			"pos": [
				550,
				80
			],
			"color": "479BD8",
			"trait": "goalPost",
			"y": 80
		},
		{
			"radius": 5,
			"pos": [
				550,
				-80
			],
			"color": "479BD8",
			"trait": "goalPost",
			"y": -80
		},
		{
			"radius": 3,
			"invMass": 0,
			"pos": [
				-550,
				240
			],
			"color": "FFCC00",
			"bCoef": 0.1,
			"trait": "line"
		},
		{
			"radius": 3,
			"invMass": 0,
			"pos": [
				-550,
				-240
			],
			"color": "FFCC00",
			"bCoef": 0.1,
			"trait": "line"
		},
		{
			"radius": 3,
			"invMass": 0,
			"pos": [
				550,
				-240
			],
			"color": "FFCC00",
			"bCoef": 0.1,
			"trait": "line"
		},
		{
			"radius": 3,
			"invMass": 0,
			"pos": [
				550,
				240
			],
			"color": "FFCC00",
			"bCoef": 0.1,
			"trait": "line"
		}
	],
	"planes": [
		{
			"normal": [
				0,
				1
			],
			"dist": -240,
			"bCoef": 1,
			"trait": "ballArea",
			"vis": false,
			"curve": 0,
			"_data": {
				"extremes": {
					"normal": [
						0,
						1
					],
					"dist": -240,
					"canvas_rect": [
						-350.0942371572802,
						-145.87259881553342,
						350.0942371572802,
						145.87259881553342
					],
					"a": [
						-350.0942371572802,
						-240
					],
					"b": [
						350.0942371572802,
						-240
					]
				}
			}
		},
		{
			"normal": [
				0,
				-1
			],
			"dist": -240,
			"bCoef": 1,
			"trait": "ballArea",
			"_data": {
				"extremes": {
					"normal": [
						0,
						-1
					],
					"dist": -240,
					"canvas_rect": [
						-350.0942371572802,
						-145.87259881553342,
						350.0942371572802,
						145.87259881553342
					],
					"a": [
						-350.0942371572802,
						240
					],
					"b": [
						350.0942371572802,
						240
					]
				}
			}
		},
		{
			"normal": [
				0,
				1
			],
			"dist": -270,
			"bCoef": 0.1,
			"_data": {
				"extremes": {
					"normal": [
						0,
						1
					],
					"dist": -270,
					"canvas_rect": [
						-350.0942371572802,
						-145.87259881553342,
						350.0942371572802,
						145.87259881553342
					],
					"a": [
						-350.0942371572802,
						-270
					],
					"b": [
						350.0942371572802,
						-270
					]
				}
			}
		},
		{
			"normal": [
				0,
				-1
			],
			"dist": -270,
			"bCoef": 0.1,
			"_data": {
				"extremes": {
					"normal": [
						0,
						-1
					],
					"dist": -270,
					"canvas_rect": [
						-350.0942371572802,
						-145.87259881553342,
						350.0942371572802,
						145.87259881553342
					],
					"a": [
						-350.0942371572802,
						270
					],
					"b": [
						350.0942371572802,
						270
					]
				}
			}
		},
		{
			"normal": [
				1,
				0
			],
			"dist": -642,
			"bCoef": 0.1,
			"_data": {
				"extremes": {
					"normal": [
						1,
						0
					],
					"dist": -642,
					"canvas_rect": [
						-350.0942371572802,
						-145.87259881553342,
						350.0942371572802,
						145.87259881553342
					],
					"a": [
						-642,
						-145.87259881553342
					],
					"b": [
						-642,
						145.87259881553342
					]
				}
			}
		},
		{
			"normal": [
				-1,
				0
			],
			"dist": -644,
			"bCoef": 0.1,
			"_data": {
				"extremes": {
					"normal": [
						-1,
						0
					],
					"dist": -644,
					"canvas_rect": [
						-350.0942371572802,
						-145.87259881553342,
						350.0942371572802,
						145.87259881553342
					],
					"a": [
						644,
						-145.87259881553342
					],
					"b": [
						644,
						145.87259881553342
					]
				}
			}
		},
		{
			"normal": [
				1,
				0
			],
			"dist": -642,
			"bCoef": 0.1,
			"trait": "ballArea",
			"vis": false,
			"curve": 0,
			"_data": {
				"extremes": {
					"normal": [
						1,
						0
					],
					"dist": -642,
					"canvas_rect": [
						-350.0942371572802,
						-145.87259881553342,
						350.0942371572802,
						145.87259881553342
					],
					"a": [
						-642,
						-145.87259881553342
					],
					"b": [
						-642,
						145.87259881553342
					]
				}
			}
		},
		{
			"normal": [
				-1,
				0
			],
			"dist": -643,
			"bCoef": 0.1,
			"trait": "ballArea",
			"vis": false,
			"curve": 0,
			"_data": {
				"extremes": {
					"normal": [
						-1,
						0
					],
					"dist": -643,
					"canvas_rect": [
						-350.0942371572802,
						-145.87259881553342,
						350.0942371572802,
						145.87259881553342
					],
					"a": [
						643,
						-145.87259881553342
					],
					"b": [
						643,
						145.87259881553342
					]
				}
			}
		}
	],
	"traits": {
		"ballArea": {
			"vis": false,
			"bCoef": 1,
			"cMask": [
				"ball"
			]
		},
		"goalPost": {
			"radius": 8,
			"invMass": 0,
			"bCoef": 0.5
		},
		"goalNet": {
			"vis": true,
			"bCoef": 0.1,
			"cMask": [
				"ball"
			]
		},
		"line": {
			"vis": true,
			"bCoef": 0.1,
			"cMask": [
				""
			]
		},
		"kickOffBarrier": {
			"vis": false,
			"bCoef": 0.1,
			"cGroup": [
				"redKO",
				"blueKO"
			],
			"cMask": [
				"red",
				"blue"
			]
		}
	},
	"playerPhysics": {
		"bCoef": 0,
		"acceleration": 0.11,
		"kickingAcceleration": 0.083,
		"kickStrength": 4.5,
		"radius": 15,
		"invMass": 0.5,
		"damping": 0.96,
		"cGroup": [
			"red",
			"blue"
		],
		"gravity": [
			0,
			0
		],
		"kickingDamping": 0.96,
		"kickback": 0
	},
	"ballPhysics": {
		"radius": 6.2,
		"bCoef": 0.4,
		"invMass": 1.6,
		"damping": 0.99,
		"color": "FF9214",
		"cMask": [
			"all"
		],
		"gravity": [
			0,
			0
		],
		"cGroup": [
			"ball"
		]
	},
	"cameraWidth": 0,
	"cameraHeight": 0,
	"maxViewWidth": 0,
	"cameraFollow": "ball",
	"redSpawnPoints": [],
	"blueSpawnPoints": [],
	"canBeStored": false,
	"kickOffReset": "partial",
	"joints": []
}`
/* OPÇÕES */

var afkLimit = 12; // limite de afk (12 segundos)
var drawTimeLimit = 1; // minutos
var maxTeamSize = 3; // máximo de jogadores num time, isso funciona para 1 (você pode querer adaptar as coisas para remover algumas estatísticas inúteis em 1v1, como assist ou cs), 2, 3 ou 4
var slowMode = 0;

/* JOGADORES */

const Team = {
    SPECTATORS: 0,
    RED: 1,
    BLUE: 2
};
var extendedP = [];
const eP = {
    ID: 0,
    AUTH: 1,
    CONN: 2,
    AFK: 3,
    ACT: 4,
    GK: 5,
    MUTE: 6
};
const Ss = {
    GA: 0,
    WI: 1,
    DR: 2,
    LS: 3,
    WR: 4,
    GL: 5,
    AS: 6,
    GK: 7,
    CS: 8,
    CP: 9,
    RL: 10,
    NK: 11
}
var players;
var TeamR;
var TeamB;
var teamS;
var messageHistory = [0, 0, 0, 0, 0, 0];
var messageCounter = 0;

/* GAME */

let forbid = ['macaco', 'adolf hitler', 'nazismo', 'cuzao', 'cuzão', 'autista', 'cu', 'hitler', 'Macaco', 'Hitler', "Pênis"];

let link = ['https://www.haxball.com/play?c=_', 'https://www.haxball.com', 'haxball.com', '.com', 'https://', 'https:', 'https://www.'];
let regex = ["fdp", "cu", "carai", "cuzao", "porra", "arrombado", "cu preto", "lixo", "autista", "lixeira", "verme", "Horrível", "seu merda", "filho da puta", "vsfd",
"caralho", "seu gordo", "cuzão", "vadia", "sua mãe", "seu fdp", "cala a boca", "puta", "fudido", "krl", "f d p", "vtnc", "vai tomar no cu", "crl", "cadeirante", "caderante",
"nigga", "prr", "CARALHO", "PORRA", "CARAI", "CUZAO", "CUZÃO", "FDP", "FILHO DA PUTA", "Cu", "CU", "CÚ", "PORR", "porr", "PRRA", "fodido", "FODIDO", "CRALHO", "CARLHO", "poha",
"prr" , "PRR", "POHA", "bct", "BCT"];
let xingo = ["seu preto", "seu macaco", "macaco", "seu negro", "pretinho", "resto de aborto", "seu mcc", "Negrinho", "carvão", "nazista", "Nazista"];

function nameForbid(player) {
    if (forbid.includes(player.name)) { room.kickPlayer(player.id, 'nick proibido nessa sala', false) }
};

var lastTeamTouched; // records who was the last to touch the ball
var lastPlayersTouched; // allows you to receive good goal notifications (must be lastPlayersKicked, waiting for a next update to get better control of shots on target)
var countAFK = false; // created to get better control of the activity, kicks if it's AFK
var activePlay = false; // created to gain better control of ball possession
var goldenGoal = false;
var SMSet = new Set(); // set created to get slow mode which is useful in ChooseMode
var banList = []; // keep track of bans, so we can unban people if we want

/* STATS */

var game;
var GKList = ["", ""];
var Rposs = 0;
var Bposs = 0;
var point = [{
    "x": 0,
    "y": 0
}, {
    "x": 0,
    "y": 0
}]; // created to obtain ball speed
var ballSpeed;
var lastWinner = Team.SPECTATORS;
var streak = 0;
var allBlues = []; // this is to count the players who should be counted for statistics. This includes players who left after the game started.
var allReds = [];

/* BALANCE AND RECRUITMENT */

var inChooseMode = false; // this variable allows you to distinguish the 2 phases of the game and choose which ones should be treated very differently
var redCaptainChoice = "";
var blueCaptainChoice = "";
var chooseTime = 20;
var timeOutCap;

/* ASSISTANT */

var checkTimeVariable = false; // this is created so that chat doesn't get spammed when a game ends via timeLimit
var announced = false;
var statNumber = 0; // this allows the room to receive statistical information every X minutes
var endGameVariable = false; // this variable with the one below helps distinguish cases where games are stopped because they are over from those where games are stopped due to player movements or team resets
var resettingTeams = false;
var capLeft = false;
var statInterval = 6;

loadMap(practiceMap, scoreLimitPractice, timeLimitPractice);

/* OBJECTS */

function Goal(time, team, striker, assist) {
    this.time = time;
    this.team = team;
    this.striker = striker;
    this.assist = assist;
}

function Game(date, scores, goals) {
    this.date = date;
    this.scores = scores;
    this.goals = goals;
}

// function setRegister(player, senha) {
//    if (registro.get(player.name)) room.sendAnnouncement('Você já está registrado.', player.id);
//    else {
//        registro.set(player.name, senha);
//        localStorage.setItem("registros", JSON.stringify([...registro]));
//        room.sendAnnouncement('Registrado!', player.id, 0x2FE436);
//        room.sendAnnouncement(`Senha: ${senha}`, player.id, 0x2FE436);
//    }
//}

//function getLogin(player, senha) {
//    if (registro.get(player.name)) {
//        if (registro.get(player.name) == senha) {
//            room.sendAnnouncement(`${player.name} logou!`, null, 0x2FE436);
//        } else room.sendAnnouncement('Senha incorreta.', player.id, 0xFF0000);
//    } else room.sendAnnouncement('Você não está registrado.', player.id, 0xFF0000);
//}

/* FUNCTIONS */

function centerText(string) {
    var space = parseInt((80 - string.length) * 0.8, 10);
    if (space <= 0) {
        return '';
    }
    return ' '.repeat(space) + string + ' '.repeat(space);
};

/* CHASING */
function golcontra(goaler) {
    var messages = [
        "I'm sure it was unintentional, right, " + goaler.name + "?",
        "YOU'RE PLAYING FOR THE WRONG TEAM, " + goaler.name,
        "CONGRATULATIONS, " + goaler.name + " THE OPPONENT TEAM THANKS YOU!",
        "Pro tip " + goaler.name + ": Next time... DON'T AIM AT YOUR GOAL!!",
        goaler.name + " I tried, who am I to judge?"
    ];
    var randomIndex = Math.floor(Math.random() * messages.length);
    var announcement = messages[randomIndex];
    setTimeout(function () {
        room.sendAnnouncement(centerText(announcement), null, Cor.White, "bold");
    }, 3000);
};

/* AUXILIARY FUNCTIONS */

function getRandomInt(max) { // returns a random number from 0 to max-1
    return Math.floor(Math.random() * Math.floor(max));
}

function getTime(scores) { // returns the current game time
    return "[" + Math.floor(Math.floor(scores.time / 60) / 10).toString() + Math.floor(Math.floor(scores.time / 60) % 10).toString() + ":" + Math.floor(Math.floor(scores.time - (Math.floor(scores.time / 60) * 60)) / 10).toString() + Math.floor(Math.floor(scores.time - (Math.floor(scores.time / 60) * 60)) % 10).toString() + "]"
}

function pointDistance(p1, p2) {
    var d1 = p1.x - p2.x;
    var d2 = p1.y - p2.y;
    return Math.sqrt(d1 * d1 + d2 * d2);
}

/* BUTTONS */

function download(conteudo, nomeDoArquivo, tipoDeArquivo) {
    let blob = new Blob([conteudo], {
        type: tipoDeArquivo
    });
    const link = window.document.createElement('a');
    link.href = window.URL.createObjectURL(blob);
    link.download = nomeDoArquivo;
    link.click();
    window.URL.revokeObjectURL(link.href);
}

function topBtn() {
    if (teamS.length == 0) {
        return;
    } else {
        if (TeamR.length == TeamB.length) {
            if (teamS.length > 1) {
                room.setPlayerTeam(teamS[0].id, Team.RED);
                room.setPlayerTeam(teamS[1].id, Team.BLUE);
            }
            return;
        } else if (TeamR.length < TeamB.length) {
            room.setPlayerTeam(teamS[0].id, Team.RED);
        } else {
            room.setPlayerTeam(teamS[0].id, Team.BLUE);
        }
    }
}

function randomBtn() {
    if (teamS.length == 0) {
        return;
    } else {
        if (TeamR.length == TeamB.length) {
            if (teamS.length > 1) {
                var r = getRandomInt(teamS.length);
                room.setPlayerTeam(teamS[r].id, Team.RED);
                teamS = teamS.filter((spec) => spec.id != teamS[r].id);
                room.setPlayerTeam(teamS[getRandomInt(teamS.length)].id, Team.BLUE);
            }
            return;
        } else if (TeamR.length < TeamB.length) {
            room.setPlayerTeam(teamS[getRandomInt(teamS.length)].id, Team.RED);
        } else {
            room.setPlayerTeam(teamS[getRandomInt(teamS.length)].id, Team.BLUE);
        }
    }
}

function blueToSpecBtn() {
    resettingTeams = true;
    setTimeout(() => {
        resettingTeams = false;
    }, 100);
    for (var i = 0; i < TeamB.length; i++) {
        room.setPlayerTeam(TeamB[TeamB.length - 1 - i].id, Team.SPECTATORS);
    }
}

function redToSpecBtn() {
    resettingTeams = true;
    setTimeout(() => {
        resettingTeams = false;
    }, 100);
    for (var i = 0; i < TeamR.length; i++) {
        room.setPlayerTeam(TeamR[TeamR.length - 1 - i].id, Team.SPECTATORS);
    }
}

function resetBtn() {
    resettingTeams = true;
    setTimeout(() => {
        resettingTeams = false;
    }, 100);
    if (TeamR.length <= TeamB.length) {
        for (var i = 0; i < TeamR.length; i++) {
            room.setPlayerTeam(TeamB[TeamB.length - 1 - i].id, Team.SPECTATORS);
            room.setPlayerTeam(TeamR[TeamR.length - 1 - i].id, Team.SPECTATORS);
        }
        for (var i = TeamR.length; i < TeamB.length; i++) {
            room.setPlayerTeam(TeamB[TeamB.length - 1 - i].id, Team.SPECTATORS);
        }
    } else {
        for (var i = 0; i < TeamB.length; i++) {
            room.setPlayerTeam(TeamB[TeamB.length - 1 - i].id, Team.SPECTATORS);
            room.setPlayerTeam(TeamR[TeamR.length - 1 - i].id, Team.SPECTATORS);
        }
        for (var i = TeamB.length; i < TeamR.length; i++) {
            room.setPlayerTeam(TeamR[TeamR.length - 1 - i].id, Team.SPECTATORS);
        }
    }
}

function blueToRedBtn() {
    resettingTeams = true;
    setTimeout(() => {
        resettingTeams = false;
    }, 100);
    for (var i = 0; i < TeamB.length; i++) {
        room.setPlayerTeam(TeamB[i].id, Team.RED);
    }
}

/* GAME FUNCTIONS */

function checkTime() {
    const scores = room.getScores();
    game.scores = scores;
    if (Math.abs(scores.time - scores.timeLimit) <= 0.01 && scores.timeLimit != 0) {
        if (scores.red != scores.blue) {
            if (checkTimeVariable == false) {
                checkTimeVariable = true;
                setTimeout(() => {
                    checkTimeVariable = false;
                }, 3000);
                scores.red > scores.blue ? endGame(Team.RED) : endGame(Team.BLUE);
                setTimeout(() => {
                    room.stopGame();
                }, 2000);
            }
            return;
        }
        goldenGoal = true;
       // room.sendAnnouncement("⚽ Gol de Gold!", null, 0xF1AF09);
        room.sendAnnouncement(centerText("PROLONGATION"), null, Cor.Amarelo, "bold");
        room.sendAnnouncement(centerText("I'll give " + drawTimeLimit * 60 + " seconds!"), null, Cor.White, "normal");
        room.sendAnnouncement(centerText("⚽ First goal wins! ⚽"), null, Cor.White, "normal");
    }
    if (scores.time > scores.timeLimit + drawTimeLimit * 60 - 15 && scores.time <= scores.timeLimit + drawTimeLimit * 60) {
        if (checkTimeVariable == false && announced == false) {
            checkTimeVariable = true;
            announced = true;
            setTimeout(() => {
                checkTimeVariable = false;
            }, 10);
            room.sendAnnouncement(centerText("⌛ 15 seconds to a tie!"), null, Cor.Amarelo, "bold");
        }
    }
    if (scores.time > (scores.timeLimit + drawTimeLimit * 60)) {
        if (checkTimeVariable == false) {
            checkTimeVariable = true;
            setTimeout(() => { checkTimeVariable = false; }, 10);
            endGame(Team.SPECTATORS);
            room.stopGame();
            goldenGoal = false;
        }
    }
};

function endGame(winner) { // lida com o final de um jogo: nenhuma função stopGame dentro
    players.length >= 2 * maxTeamSize - 1 ? activateChooseMode() : null;
    const scores = room.getScores();
    game.scores = scores;
    Rposs = Rposs/(Rposs+Bposs);
    Bposs = 1 - Rposs;
    lastWinner = winner;
    endGameVariable = true;
    if (winner == Team.RED) {
        streak++;
        room.sendAnnouncement(centerText("🏆 Red team won! | Win Streak(s):") + streak + " 🏆", null, 0xFDC43A);
    }
    else if (winner == Team.BLUE) {
        streak = 1;
        room.sendAnnouncement(centerText("🏆 Blue team won! | Win streak(s):") + streak + " 🏆", null, 0xFDC43A);
    }
    else {
        streak = 0;
        room.sendAnnouncement("💤 Limit reached");
    }
    //room.sendAnnouncement("📊 Posse de Bola: 🔴 " + (Rposs*100).toPrecision(3).toString() + "% | " + (Bposs*100).toPrecision(3).toString() + "% 🔵", null, 0xFDC43A);
    room.sendAnnouncement(centerText("🏆 END OF MATCH 🏆"), null, Cor.White, "bold");
    room.sendAnnouncement(centerText(" " + scores.red + " - " + scores.blue), null, Cor.White, "normal");
    room.sendAnnouncement(centerText((Rposs * 100).toPrecision(3).toString() + "% | Ball possession | " + (Bposs * 100).toPrecision(3).toString() + "% "), null, Cor.White, "normal");
    scores.red == 0 ? (scores.blue == 0 ? room.sendAnnouncement("🥅 " + GKList[0].name + " it's a man? no, it's a barrier! " + GKList[1].name + " saved all goals ", null, 0xFDC43A) : room.sendAnnouncement("🥅 it's a man? no, it's a barrier! " + GKList[1].name + " saved all goals ", null, 0xFDC43A)) : scores.blue == 0 ? room.sendAnnouncement("🥅 it's a man? no, it's a barrier! " + GKList[0].name + " saved all goals ", null, 0xFDC43A) : null;
    updateStats();
    //sendDiscordWebhook(scores);
    //room.sendAnnouncement("A partida foi gravada e enviada em nosso discord. ID: " + `${getDate()}`, null, Cor.Amrelo, Negrito);
    
}

function quickRestart() {
    room.stopGame();
    setTimeout(() => {
        room.startGame();
    }, 2000);
}

function resumeGame() {
    setTimeout(() => {
        room.startGame();
    }, 2000);
    setTimeout(() => {
        room.pauseGame(false);
    }, 1000);
}

function activateChooseMode() {
    inChooseMode = true;
    slowMode = 2;
    room.sendAnnouncement("Recruitment mode activated!", null, 0x55bae2, "normal");
}

function deactivateChooseMode() {
    inChooseMode = false;
    clearTimeout(timeOutCap);
    if (slowMode != 0) {
        slowMode = 0;
        room.sendAnnouncement("Recruitment mode closed.", null, 0xf2a000, "normal");
    }
    redCaptainChoice = "";
    blueCaptainChoice = "";
}

function loadMap(map, scoreLim, timeLim) {
    if (map != '') {
        room.setCustomStadium(map);
    } else {
        console.log("There was an error loading the stadium")
        room.setDefaultStadium("Classic");
    }
    room.setScoreLimit(scoreLim);
    room.setTimeLimit(timeLim);
}

/* PLAYER FUNCTIONS */

function updateTeams() { // updates the list of players and the list of all teams
    players = room.getPlayerList().filter((player) => player.id != 0 && !getAFK(player));
    TeamR = players.filter(p => p.team === Team.RED);
    TeamB = players.filter(p => p.team === Team.BLUE);
    teamS = players.filter(p => p.team === Team.SPECTATORS);
}

function handleInactivity() { // handles inactivity: players will be kicked after afkLimit
    if (countAFK && (TeamR.length + TeamB.length) > 1) {
        for (var i = 0; i < TeamR.length; i++) {
            setActivity(TeamR[i], getActivity(TeamR[i]) + 1);
        }
        for (var i = 0; i < TeamB.length; i++) {
            setActivity(TeamB[i], getActivity(TeamB[i]) + 1);
        }
    }
    for (var i = 0; i < extendedP.length; i++) {
        if (extendedP[i][eP.ACT] == 60 * (2 / 3 * afkLimit)) {
            room.sendAnnouncement("@" + room.getPlayer(extendedP[i][eP.ID]).name + ", if you don't move in the next " + Math.floor(afkLimit / 3) + " seconds, you will be kicked!", extendedP[i][eP.ID], 0xf4a404, "bold", 2);
        }
        if (extendedP[i][eP.ACT] >= 60 * afkLimit) {
            extendedP[i][eP.ACT] = 0;
            if (room.getScores().time <= afkLimit - 0.5) {
                setTimeout(() => {
                    !inChooseMode ? quickRestart() : room.stopGame();
                }, 10);
            }
            room.kickPlayer(extendedP[i][eP.ID], "AFK", false);
        }
    }
}

function getAuth(player) {
    return extendedP.filter((a) => a[0] == player.id) != null ? extendedP.filter((a) => a[0] == player.id)[0][eP.AUTH] : null;
}

function getAFK(player) {
    return extendedP.filter((a) => a[0] == player.id) != null ? extendedP.filter((a) => a[0] == player.id)[0][eP.AFK] : null;
}

function setAFK(player, value) {
    extendedP.filter((a) => a[0] == player.id).forEach((player) => player[eP.AFK] = value);
}

fun... (Tiempo restante: 95 KB)
