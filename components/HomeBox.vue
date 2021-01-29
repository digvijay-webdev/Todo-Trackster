<template>
  <div class="box container">
    <!-- TITLEBAR OF BOX -->
    <div class="titleBar">
      <div class="controlSwitches">
        <div @click="changeTheme('red')" class="red"></div>
        <div @click="changeTheme('yellow')" class="yellow"></div>
        <div @click="changeTheme('green')" class="green"></div>
        <div @click="changeTheme('dark')" class="dark"></div>
      </div>
      <div class="contactBtn">
        <a href="mailto:djpadhiyar881@gmail.com">Contact</a>
      </div>
    </div>

    <!-- ACTUAL BOX -->
    <div class="mainBox">
      <div class="contentWrapper">
        <h1>Todo Trackster</h1>
        <h3>Just another todo application</h3>
        <p>You can install this web app locally on your device, Chrome is preferred browser.</p>
        <p>You can change theme color by clicking the color buttons on top left corner. Your color preference will be stored for later use.</p>
        <p>Created by <strong>'Digvijaysinh Padhiyar'</strong>, code can be found on <a href="https://github.com/digvijay-webdev" target="_blank">Github</a></p>
      </div>

      <div class="todoRedirects">
        <div class="board">
          <h2 class="textCenter">Go to</h2>
          <div class="boardButtons textCenter">
            <NuxtLink to="/todolist">Todo List</NuxtLink>
            <a href="https://github.com/digvijay-webdev" target="_blank">Github</a>
            <a href="https://pulsatingbirds.com" target="_blank">About Developer</a>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'HomeBox',
  methods: {
    changeTheme(color) {
      // Selecting Elems
      let body = document.querySelector("body");

      // Changing Theme
      body.style.backgroundColor = `var(--${color})`;

      // Storing in LS
      localStorage.setItem("themeColor", color);
    }
  },
  mounted() {
    // changing themeColor according to the LS memory
    let themeColor = localStorage.getItem("themeColor");
    let body = document.querySelector("body");
    
    if (themeColor === null || themeColor === undefined) {
      body.style.backgroundColor = `var(--yellow)`;
      localStorage.setItem("themeColor", JSON.stringify('yellow'));
    } else {
      body.style.backgroundColor = `var(--${themeColor})`;
    }
  }
}
</script>

<style scoped>
/****************** TITLE BAR ******************/
.box {
  border: 2px solid var(--white);
}

.box .titleBar {
  border-bottom: 2px solid var(--white);
  display: flex;
  flex-direction: row;
  justify-content: space-between;
  align-items: center;
  padding: 6px 4px;
}

.box .titleBar .controlSwitches {
  display: flex;
  flex-direction: row;
}

.box .titleBar .controlSwitches div {
  margin: 0 4px;
  width: 22px;
  height: 22px;
  border-radius: 100%;
  border: 4px solid #f7f7f7;
  background-color: var(--yellow);
  cursor: pointer;
}

.box .titleBar .controlSwitches div:hover {
  border: 2px solid #f7f7f7;
  width: 24px;
  height: 24px;
}

.box .titleBar .controlSwitches .red {
  background-color: var(--red);
}

.box .titleBar .controlSwitches .yellow {
  background-color: var(--yellow);
}

.box .titleBar .controlSwitches .green {
  background-color: var(--green);
}

.box .titleBar .controlSwitches .dark {
  background-color: var(--dark);
}

.box .titleBar .contactBtn {
  font-size: 18px;
  font-weight: bold;
  margin: 0 4px;
}

.box .titleBar .contactBtn a {
  text-decoration: none;
  color: var(--white);
}

/****************** MAIN BOX ******************/
.box .mainBox {
  display: flex;
  flex-direction: row;
  justify-content: space-between;
  align-items: center;
}

.box .mainBox .contentWrapper {
  flex: 2;
  padding: 12px;
}

.box .mainBox .contentWrapper h1 {
  font-family: var(--sketch);
  font-size: 42px;
}

.box .mainBox .contentWrapper h3 {
  font-family: var(--magic);
}

.box .mainBox .contentWrapper p {
  font-family: var(--nunito);
  font-size: 18px;
}

.box .mainBox .contentWrapper a {
  color: #2e86de;
}

.box .mainBox .todoRedirects {
  flex: 1;
  padding: 8px;
  margin: 0 12px 0 12px;
  border: 1px solid var(--white);
  border-radius: 4px;
  box-shadow: 4px 4px 3px  #5555559c;
}

.box .mainBox .todoRedirects .board h2 {
  color: var(--white);
  margin-bottom: 8px;
}

.box .mainBox .todoRedirects .board .boardButtons {
  margin: 0 16px;
}

.box .mainBox .todoRedirects .board .boardButtons a {
  display: block;
  background-color: var(--white);
  margin-bottom: 6px;
  padding: 4px;
  text-decoration: none;
  font-family: var(--magic);
  color: var(--dark);
  border-radius: 4px;
}

.box .mainBox .todoRedirects .board .boardButtons a:hover {
  opacity: 0.9;
}

/* MEDIA QUERIES */
@media screen and (max-width: 820px) {
  .box .mainBox {
    flex-direction: column;
  }
  .box .mainBox .todoRedirects {
    width: 95%;
    padding: 8px;
    margin: 12px;
  }
}

@media screen and (max-width: 420px) {
  .box .mainBox .contentWrapper h3 {
    font-size: 18px;
  }
  .box .mainBox .contentWrapper p {
    font-size: 16px;
  }
}

@media screen and (max-width: 340px) {
  .box .mainBox .contentWrapper h1 {
    font-size: 32px;
  }
}
</style>
