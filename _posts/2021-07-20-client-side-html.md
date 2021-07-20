# Client Side HTML

The client side of the game is designed to be a single webpage which is loaded once and includes a login window, game board, individual player menus and dynamic interfaces which change dependent on the choices facing a player.

The HTML below is enclosed in the ```<body></body>``` tags of the page and serves as a framework which is dynamically populated with elements generated for each player by the server.

## Login Screen

The login screen utilises a modal div to select their house and log in to their game using their password and game-id. Inclusion of a game-id enables multiple games to be played concurrently.

```html
<!-- Login Screen-->
  <div id="login">
    <div id="loginModal">
      <div id="loginContent">
        <div id="title"></div>
        <div id="logo">
          <div id="starkSigil" class="houseSigil"></div>
          <div id="greyjoySigil" class="houseSigil"></div>
          <div id="martellSigil" class="houseSigil"></div>
          <div id="tyrellSigil" class="houseSigil"></div>
          <div id="baratheonSigil" class="houseSigil"></div>
          <div id="lannisterSigil" class="houseSigil"></div>
        </div>
        <!-- <div > -->
        <form id="loginInput">
          <input
            type="text"
            id="gameIdInput"
            name="gameId"
            value="1234"
            autocomplete="off"
            class="faded"
          />
          <input
            type="password"
            id="passwordInput"
            name="password"
            placeholder="password"
            autocomplete="off"
            class="faded"
          />
        </form>
        <!-- </div> -->
      </div>
    </div>
  </div>
```
## Menu

Throughout the game players have different pieces of information available to them allowing them to make informed choices about their next phase of play. Much of this infomation is public and so kept in a drop down menu toggled using one of the six buttons at the top of thier screen.

The menu is divided into three vertical sections. Firstly the menuButtonPanel containing the six menu buttons. Secondly the dialogPanel which is populated with additional infomation, player choices, order tokens, battle stats etc. at the approptiate point during the game. Thirdly the menuPanel contains the six sub-panels with general player information. 

### Menu Panel

The menu panel holds the following sub-panels.
1. Player resources - the units and power tokens available (not on the board) to each player at that point in time. Power tokens are hidden during bidding phases of the game.
2. House cards - a players own house cards compared to one of the other five houses. Available cards are shown in full colour. Discarded house cards are shown greyed out and translucent. 
3. Westeros decks - the most recently played westeros cards.
4. Wildling deck - the most recently played wildling card (or the top card during the messenger raven portion of the game).
5. Game messenger - an in built chat window allowing the player to message the whole game, and five individual chats for players to message one another privately. In the whole game chat the game automatically posts the outcome of battles, choices made, cards revealed to inform players of the games progress when they have not been online.
6. Settings - check boxes to hide/show units, order tokens, power tokens. Ability to diable game notifications in the messenger.

```html
  <!-- Menu  -->
  <div id="menu">
    <div id="menuButtonPanel">
      <div id="resource" class="panelButton">Resources</div>
      <div id="houseCard" class="panelButton">House Cards</div>
      <div id="westerosCard" class="panelButton">Westeros Decks</div>
      <div id="wildlingCard" class="panelButton">Wildling Deck</div>
      <div id="messenger" class="panelButton">Messenger</div>
      <div id="settings" class="panelButton">&#8984</div>
    </div>
    <div id="dialogPanel" class="panel"></div>
    <div id="menuPanel" class="panel">
      <div id="resourcePanel" class="subPanel">
        <div id="resourceGridContainer">
          <div id="baratheonResources" class="resourceGrid"></div>
          <div id="greyjoyResources" class="resourceGrid"></div>
          <div id="lannisterResources" class="resourceGrid"></div>
          <div id="martellResources" class="resourceGrid"></div>
          <div id="starkResources" class="resourceGrid"></div>
          <div id="tyrellResources" class="resourceGrid"></div>
        </div>
      </div>
      <div id="houseCardPanel" class="subPanel">
        <div id="galleryButtons">
          <div id="baratheonCard" class="galleryButton">Baratheon</div>
          <div id="greyjoyCard" class="galleryButton">Greyjoy</div>
          <div id="lannisterCard" class="galleryButton">Lannister</div>
          <div id="martellCard" class="galleryButton">Martell</div>
          <div id="starkCard" class="galleryButton">Stark</div>
          <div id="tyrellCard" class="galleryButton">Tyrell</div>
        </div>
        <div id="cardGallery">
          <div id="ownHouseCardFocus"></div>
          <div id="ownHouseCardGallery"></div>
          <div id="enemyHouseCardGallery">
            <div id="baratheonCardGallery" class="enemyHouseCardGallery"></div>
            <div id="greyjoyCardGallery" class="enemyHouseCardGallery"></div>
            <div id="lannisterCardGallery" class="enemyHouseCardGallery"></div>
            <div id="martellCardGallery" class="enemyHouseCardGallery"></div>
            <div id="starkCardGallery" class="enemyHouseCardGallery"></div>
            <div id="tyrellCardGallery" class="enemyHouseCardGallery"></div>
          </div>
          <div id="enemyHouseCardFocus">
            <div id="baratheonCardFocus" class="enemyHouseCardFocus"></div>
            <div id="greyjoyCardFocus" class="enemyHouseCardFocus"></div>
            <div id="lannisterCardFocus" class="enemyHouseCardFocus"></div>
            <div id="martellCardFocus" class="enemyHouseCardFocus"></div>
            <div id="starkCardFocus" class="enemyHouseCardFocus"></div>
            <div id="tyrellCardFocus" class="enemyHouseCardFocus"></div>
          </div>
        </div>
      </div>
      <div id="westerosCardPanel" class="subPanel">
        <div id="westerosDecks">
          <div id="westerosDeck1"></div>
          <div id="westerosDeck2"></div>
          <div id="westerosDeck3"></div>
        </div>
      </div>
      <div id="wildlingCardPanel" class="subPanel">
        <div id="wildlingDeck"></div>
      </div>
      <div id="messengerPanel" class="subPanel">
        <div id="messengerContainer">
          <div id="contactWindow" class="contactPanel">

          </div>
          <div id="messengerWindow">
            <div id="gameChat" class="messengerChat">
              <div id="gameMessageContainer" class="messageContainer"></div>
              <div class="sendContainer">
                <input
                  type="text"
                  id="gameMessageInput"
                  name="game"
                  class="messageInput"
                />
                <button type="submit" name="game" class="sendButton">
                  Send
                </button>
              </div>
            </div>
            <div id="baratheonChat" class="messengerChat">
              <div
                id="baratheonMessageContainer"
                class="messageContainer"
              ></div>
              <div class="sendContainer">
                <input
                  type="text"
                  id="baratheonMessageInput"
                  name="baratheon"
                  class="messageInput"
                />
                <button type="submit" name="baratheon" class="sendButton">
                  Send
                </button>
              </div>
            </div>
            <div id="greyjoyChat" class="messengerChat">
              <div id="greyjoyMessageContainer" class="messageContainer"></div>
              <div class="sendContainer">
                <input
                  type="text"
                  id="greyjoyMessageInput"
                  name="greyjoy"
                  class="messageInput"
                />
                <button type="submit" name="greyjoy" class="sendButton">
                  Send
                </button>
              </div>
            </div>
            <div id="lannisterChat" class="messengerChat">
              <div
                id="lannisterMessageContainer"
                class="messageContainer"
              ></div>
              <div class="sendContainer">
                <input
                  type="text"
                  id="lannisterMessageInput"
                  name="lannister"
                  class="messageInput"
                />
                <button type="submit" name="lannister" class="sendButton">
                  Send
                </button>
              </div>
            </div>
            <div id="martellChat" class="messengerChat">
              <div id="martellMessageContainer" class="messageContainer"></div>
              <div class="sendContainer">
                <input
                  type="text"
                  id="martellMessageInput"
                  name="martell"
                  class="messageInput"
                />
                <button type="submit" name="martell" class="sendButton">
                  Send
                </button>
              </div>
            </div>
            <div id="starkChat" class="messengerChat">
              <div id="starkMessageContainer" class="messageContainer"></div>
              <div class="sendContainer">
                <input
                  type="text"
                  id="starkMessageInput"
                  name="stark"
                  class="messageInput"
                />
                <button type="submit" name="stark" class="sendButton">
                  Send
                </button>
              </div>
            </div>
            <div id="tyrellChat" class="messengerChat">
              <div id="tyrellMessageContainer" class="messageContainer"></div>
              <div class="sendContainer">
                <input
                  type="text"
                  id="tyrellMessageInput"
                  name="tyrell"
                  class="messageInput"
                />
                <button type="submit" name="tyrell" class="sendButton">
                  Send
                </button>
              </div>
            </div>
          </div>
        </div>
      </div>
      <div id="settingsPanel" class="subPanel">
        <div id="settingsContainer">
          <div class="settingsOption">
            <input id="disableNotifications" type="checkbox" onchange="togglePreference('disableNotifications')">
            Disable Game Notifications
          </div>
          <div class="settingsOption">
            <input id="hideUnit" type="checkbox" onchange="togglePreference('hideUnit')">
            Hide Units
          </div>
          <div class="settingsOption">
            <input id="hideOrder" type="checkbox" onchange="togglePreference('hideOrder')">
            Hide Order Tokens
          </div>
          <div class="settingsOption">
            <input id="hidePower" type="checkbox" onchange="togglePreference('hidePower')">
            Hide Power Tokens
          </div>
        </div>
      </div>
    </div>
  </div>
```

### Game Board & Context Menu

Options and choices given to players on selecting a unit or token are dynamically placed in the context menu which appears at the cursor location. 

All visible game pieces, units, tokens, markers are dynammically added to and removed from ```<div id="board"></div>```. This forms the virtual game board players interact with in the same manner they would a real game board - placing tokens, units etc.

``` html
  <!-- Dynamic menu -->
  <div id="contextMenu"></div>
  <!-- Took Tip text-->
  <div id="activePlayerText">Active Player</div>
  <!-- Board image -->
  <div id="boardModal"></div>
  <div id="board"></div>
</body>
```



