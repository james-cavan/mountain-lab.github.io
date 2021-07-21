# Data Structure

Maintaining a sensible data structure which also has strong parallels to the physical game representation has been important choice as specific game pieces are removed, added and manipulated. To retain game state during server down-time and player disconnects the game data is converted to strings and written to a file. JS objects are the chosen method to store the data in for the ease of succinctly addressing and returning data and values.

## Game Data

Non-house specific data is stored in the object outlined below. This includes the order of the three westeros decks and the wildling deck, control markers for the westeros phase of the game, and general data for ongoing battles which is not tied to a specific house. 

The mode object key controls what information, choices, and functions are run before sending data to each client. The turnPos object key controls which player is currently taking their turn. Between these two keys the game is able to loop through players and rounds until game completion.

```javascript
  round: 1,
  mode: 'planning-place-tokens',
  turnPos: 1,
  westerosPhase: {
    complete: false,
    revealCards: false,
    decks: {
      deck1: {
        resolved: false,
        stack: [
          'Card0',
          'Card1',
          'Card2',
          'Card3',
          'Card4',
          'Card5',
          'Card6',
          'Card7',
          'Card8',
          'Card9',
        ],
      },
    },
    bidTrack: ['throne', 'fiefdom', 'court'],
    bidTie: false,
  },
  wildlings: {
    deck: [
      'Card0',
      'Card1',
      'Card2',
      'Card3',
      'Card4',
      'Card5',
      'Card6',
      'Card7',
      'Card8',
    ],
    strength: 2,
    defence: 0,
    lowestBidder: '',
    highestBidder: '',
    nonParticipant: '',
    attack: false,
    resolveCardSetup: false,
    resolveCard: false,
  },
  garrisons: {
    dragon: 2,
    pykeis: 2,
    lannis: 2,
    sunspe: 2,
    winter: 2,
    higgar: 2,
  },
  neutralForce: {
    kinlan: 5,
    theeyr: 6,
  },
  battle: {
    battleArea: '',
    supportSetup: false,
    bladeUsed: false,
    bladePlus: false,
  },
```

## House Data

Each player has order tokens, units, power tokens and house cards. Each house has the structure below to keep track of the state and location of all their board pieces. Additionally player information for readiness, battle and bidding is also stored. Board pieces share the same structure: a unique id within the player's pieces, an availability indicator (false = on the board, true = ready to be used), an area marker (which of the areas on the board they have been placed), and status (a string to control their display to players e.g. routed, attacking or defending). House cards utilise a similar idea.
Note: the code below is incomplete in order to reduce the length for illustrative purposes.

```javascript
  player: 'baratheon', 
  passwordHash: '',
  socketId: '',
  connected: false,
  logoutTime: 0,
  preferences: {
    disableNotifications: false,
    hideUnit: false,
    hideOrder: false,
    hidePower: false,
  },
  acknowledge: false,
  playerConf: false,
  bidAmount: 0,
  damage: 0,
  musterPoints: 0,
  tracks: {
    throne: 1,
    fiefdom: 5,
    court: 4,
    supply: 2,
    victory: 1,
  },
  battle: {
    side: null,
    support: null,
    supportAccepted: null,
    cardResolved: false,
    tobCard: false,
    casualties: 0,
    strengthMod: 0,
    victor: null,
    finalStrength: 0,
    retreatArea: '',
  },
  tokens: {
    raid0: {
      id: 'raid0',
      available: true,
      area: '',
      status: '',
    },
    raid1: {
      id: 'raid1',
      available: true,
      area: '',
      status: '',
    },
    raid2: {
      id: 'raid2',
      available: true,
      area: '',
      status: '',
    },
  },
  units: {
    FM0: {
      id: 'FM0',
      available: false,
      area: 'kingsw',
      status: '',
    },
    FM1: {
      id: 'FM1',
      available: false,
      area: 'dragon',
      status: '',
    },
    FM2: {
      id: 'FM2',
      available: true,
      area: '',
      status: '',
    },
    KN0: {
      id: 'KN0',
      available: false,
      area: 'dragon',
      status: '',
    },
    KN1: {
      id: 'KN1',
      available: true,
      area: '',
      status: '',
    },
    SE0: {
      id: 'SE0',
      available: true,
      area: '',
      status: '',
    },
    SH0: {
      id: 'SH0',
      available: false,
      area: 'shibay',
      status: '',
    },
    SH1: {
      id: 'SH1',
      available: false,
      area: 'shibay',
      status: '',
    },
    SH2: {
      id: 'SH2',
      available: true,
      area: '',
      status: '',
    },
  },
  powerTokens: {
    PTHB: {
      id: 'PTHB',
      available: false,
      area: 'dragon',
    },
    PT01: {
      id: 'PT01',
      available: true,
      area: '',
    },
  },
  houseCards: {
    Card0: {
      available: true,
      selected: false,
    },
    Card1: {
      available: true,
      selected: false,
    },
  }
```
