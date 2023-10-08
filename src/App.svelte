<script lang="ts">
  import TailwindCss from "./TailwindCSS.svelte";
  let cookies: number = 0;
  let timesClicked: number = 0;
  let Cookiesps: number = 0;
  let lifeTimeCookies: number = 0;
  let cursors: number[] = [];
  let cursor: number = 0;
  let cursorPrice: number = 10;
  let grandmas: number = 0;
  let grandmaPrice: number = 10;
  let farm: number = 0;
  let farms: number[] = [];
  let farmPrice: number = 1100;
  let temples: number[] = [];
  let temple: number = 0;
  let templePrice: number = 30000;

  type Achivments = {
    [key: string]: number;
  };

  let achivments: Achivments[] = [
    { "clicked 100 times": 100 },
    { "clicked 1000 times": 1000 },
    { "clicked 10000 times": 10000 },
  ];

  /*const loadSave = localStorage.getItem("cookies");

  if (loadSave) {
    const parseJSON = JSON.parse(loadSave);
    cookies = parseJSON.cookies;
    Cookiesps = parseJSON.Cookiesps;
    cursor = parseJSON.cursor;
    cursors = parseJSON.cursors;
    cursorPrice = parseJSON.cursorPrice;
    grandmas = parseJSON.grandmas;
    farm = parseJSON.farm;
    farmPrice = parseJSON.farmPrice;
    grandmaPrice = parseJSON.grandmaPrice;
  }*/

  setInterval(() => {
    cps();
  }, 1000);

  function clickCookie() {
    cookies++;
    lifeTimeCookies++;
    timesClicked++;
    CheckAchivments(timesClicked);
    //saveData();
  }

  function buyCursors() {
    if (cookies >= cursorPrice) {
      cursors.push(1);
      cursor++;
      cookies -= cursorPrice;
      cursorPrice += 2;
      //saveData();
    } else {
      alert("You Dont Have Enough Cookies");
    }
  }

  function buyGrandma() {
    if (cookies >= grandmaPrice) {
      grandmas++;
      cookies -= grandmaPrice;
      grandmaPrice += 2;
      //saveData();
    } else {
      alert("You Dont Have Enough Cookies");
    }
  }

  function buyFarm() {
    if (cookies >= farmPrice) {
      farms.push(1);
      farm++;
      cookies -= farmPrice;
      farmPrice += 100;
      //saveData();
    } else {
      alert("You Dont Have Enough Cookies");
    }
  }

  function buyTemple() {
    if (cookies >= templePrice) {
      temples.push(1);
      temple++;
      cookies -= templePrice;
      templePrice += 10000;
    } else {
      alert("You Dont Have Enough Cookies");
    }
  }

  function CheckAchivments(clickCount: number): void {
    achivments.forEach((achivment) => {
      for (let achiv in achivment) {
        let clicksRequired = Number(achiv.split(" ")[1]);
        if (clickCount == clicksRequired) {
          AlertAchivment(clickCount);
        }
      }
    });
  }

  function AlertAchivment(clickCount: number): void {
    alert(`You Have Clicked ${clickCount} Times!`);
  }

  function cps() {
    Cookiesps = 0;
    cookies += grandmas;
    Cookiesps += grandmas;
    lifeTimeCookies += grandmas;
    cursors.forEach(() => {
      cookies += 0.1;
      Cookiesps += 0.1;
      lifeTimeCookies += 0.1;
    });
    farms.forEach(() => {
      cookies += 10;
      Cookiesps += 10;
      lifeTimeCookies += 10;
    });
    temples.forEach(() => {
      cookies += 100;
      Cookiesps += 100;
      lifeTimeCookies += 100;
    });
  }

  /*function saveData() {
    localStorage.setItem(
      "cookies",
      JSON.stringify({
        cookies,
        Cookiesps,
        cursors,
        cursor,
        cursorPrice,
        grandmas,
        grandmaPrice,
        farm,
        farms,
        farmPrice,
      })
    );
  }*/
</script>

<TailwindCss />

<main>
  <div>Cookies: {cookies.toFixed(1)}</div>
  <button class="bg-gray-500 rounded" on:click={clickCookie}
    >Click To Add A Cookie</button
  >

  <div>Cookies Per Second: {Cookiesps.toFixed(1)}</div>
  <div>LifeTime Cookies: {lifeTimeCookies.toFixed(1)}</div>

  <div>Cursors: {cursor}</div>
  <div>Cursor Price: {cursorPrice}</div>
  <button class="bg-gray-500 rounded" on:click={buyCursors}>Buy Cursor</button>

  <div>Grandmas: {grandmas}</div>
  <div class="">Grandma Price: {grandmaPrice}</div>
  <button class="bg-gray-500 rounded" on:click={buyGrandma}>Buy Grandma</button>

  <div>Farms: {farm}</div>
  <div>Farm Price: {farmPrice}</div>
  <button class="bg-gray-500 rounded" on:click={buyFarm}>Buy Farm</button>

  <div>Temples: {temple}</div>
  <div>Temple Price: {templePrice}</div>
  <button class="bg-gray-500 rounded" on:click={buyTemple}>Buy Temple</button>
</main>
