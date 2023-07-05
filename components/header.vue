
<script setup>
const colorMode = useColorMode();
</script>
<template>
    <Head>
        <link rel="preconnect" href="https://fonts.googleapis.com">
        <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
        <link href="https://fonts.googleapis.com/css2?family=Poppins:wght@400;600&display=swap" rel="stylesheet">

        <link rel="icon" href="/favicon.png" type="image/png" />
        <link rel="apple-touch-icon" href="/favicon.png" />
        <link rel="shortcut icon" href="/favicon.png" type="image/x-icon">
    </Head>
    <header>
        <div class="logo">
            <nuxt-link to="/"><img src="/favicon.png" /></nuxt-link>
        </div>
        <button onclick="show_menu();" class='bx bx-menu-alt-right menu-icon magic-hover magic-hover__square'
            id="menu_btn_id"></button>
        <div class="menu1" id="menu_list_id">
            <button onclick="show_menu();" class='bx bx-x menu-icon' id="menu_btn_id"></button>

            <ul>
                <li>
                    <nuxt-link to="/" class="magic-hover magic-hover__square">Home</nuxt-link>
                </li>
                <li>
                    <nuxt-link to="/portfolio" class="magic-hover magic-hover__square">Portfolio</nuxt-link>
                </li>
                <li>
                    <nuxt-link to="/employment" class="magic-hover magic-hover__square">Employment</nuxt-link>
                </li>
                <li>
                    <nuxt-link to="/education" class="magic-hover magic-hover__square">Education</nuxt-link>
                </li>
                <li>
                    <nuxt-link to="/skills" class="magic-hover magic-hover__square">Skills</nuxt-link>
                </li>
                <li>
                    <nuxt-link to="/contact" class="magic-hover magic-hover__square">Contact</nuxt-link>
                </li>
                <li>
                    <label id="switch" class="switch">
                        <input type="checkbox" v-on:click="toggleTheme()" v-model="lighttheme" id="slider">
                        <span class="slider round"></span>
                    </label>
                </li>
            </ul>
        </div>
    </header>
</template>

<script>
import '~/assets/style.css'

export default {
    data() {
        return {
            lighttheme: this.$colorMode.value != "dark",
        }
    },
    methods: {
        setTheme(mode) {
            if (mode !== "light" && mode !== "dark" && mode !== "auto") {
                console.error(`Got invalid theme mode: ${mode}. Resetting to auto.`);
                mode = "auto";
            }
            document.documentElement.className = mode;
            document.documentElement.dataset.theme = mode;
            localStorage.setItem("theme", mode);
        },
        toggleTheme() {
            if (this.$colorMode.value === 'dark') {
                this.setTheme("light")
                this.$colorMode.preference = "light";
            } else {
                this.setTheme("dark")
                this.$colorMode.preference = "dark";
            }
        }
    },
}
</script>

<style scoped>
header {
    padding: 20px 12px 3px;
    padding-left: 6px;
    float: right;
    z-index: 9;
    width: 100%;
    display: flex;
    justify-content: space-between;
    transition: all 0.1s ease;
    position: relative;
}

header .menu-icon {
    display: none;
}

header .logo {
    font-size: 23px;
    color: var(--header-color);
    text-shadow: 0px 0px 1px rgb(255 255 255) !important;
    border-bottom: 1px dotted transparent;
    float: right;
    display: flex;
    align-items: center;
    font-weight: 600;
    border-radius: 1px;
    letter-spacing: -0.3px;
}

header .logo a {
    padding: 5px 12px;
    margin: 0;
    color: var(--text-color-2);
}

header .logo img {
    height: 72px;
    width: 72px;
    margin-left: 9px;
}


header.stick {
    animation-name: headerstick;
    animation-duration: 0s;
    position: sticky;
    top: 0;
    padding: 9px 12px;
    background-color: var(--header-back-color);
    backdrop-filter: blur(45px);
    box-shadow: 1px 0 13px var(--header-border-color);
}

@keyframes headerstick {
    from {
        top: -90px;
    }

    to {
        top: 0;
    }
}

header.stick .logo a {
    background-color: transparent;
    padding: 0;
    height: 30px;
    width: 30px;
}

header.stick .logo img {
    height: 30px;
    width: 30px;
    margin: 0;
}

header.stick .logo {
    font-size: 18px;
}

header .switch {
    position: relative;
    display: inline-block;
    width: 63px;
    margin: 9px 12px 6px;
    height: 16px;
}

header .switch input {
    opacity: 0;
    width: 0;
    height: 0;
}


header .switch .slider {
    position: absolute;

    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    background-color: #03f2ef;
    -webkit-transition: 0.4s;
    transition: 0.4s;
}


header .switch .slider:before {
    position: absolute;
    content: "";
    height: 18px;
    width: 18px;
    left: 0px;
    bottom: 4px;
    padding: 7px;
    top: 0;
    bottom: 0;
    margin: auto 0;
    -webkit-transition: 0.4s;
    transition: 0.4s;
    box-shadow: 0 0px 15px #2020203d;
    border: 2px dotted #03f2ef;
    background-color: var(--change-theme-back-color);
    background-image: url('/theme/night.png');
    background-repeat: no-repeat;
    background-position: center;
}


header .switch input:checked+.slider {
    background-color: #0044ff21;
}


header .switch input:focus+.slider {
    box-shadow: 0 0 1px #e6e6e6;
}


header .switch input:checked+.slider:before {
    -webkit-transform: translateX(33px);
    -ms-transform: translateX(33px);
    transform: translateX(33px);
    background: white url('/theme/light.png');
    background-repeat: no-repeat;
    background-position: center;
}

/* Rounded sliders */

header .switch .slider.round {
    border-radius: 34px;
}


header .switch .slider.round:before {
    border-radius: 50%;
}

header ul {
    list-style: none;
    margin: 0;
    padding: 0 5px;
    display: flex;
    align-items: flex-start;
}

header ul li a {
    font-size: 16px;
    color: var(--header-color);
    text-shadow: 0px 0px 1px rgb(255 255 255) !important;

    padding: 3px 9px;
    border-bottom: 2px dotted transparent;
    margin: 3px 0;
    float: right;
    font-weight: 600;
    display: flex;
    align-items: center;
    border-radius: 5px;
}

header ul li a.active {
    border-bottom: 2px solid var(--header-border-active-color);
    background-color: var(--header-back-active-color);
    backdrop-filter: blur(18px);
    pointer-events: none;
    cursor: default;
}

header ul li a span {
    font-size: 0px;
    display: inline;
}

header ul li a:hover {
    color: var(--header-hover-color);
    justify-content: center;
    align-items: center;
    transform: matrix(190);
}

header ul li a:hover span {
    display: inline;
    padding-left: 7px;
    margin-right: 7px;

}
</style>