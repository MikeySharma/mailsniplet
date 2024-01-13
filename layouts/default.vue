
<script>
export default {
    data() {
        return {
            isMenuHidden: false,
            isQuickPickBar: false,
            menuArrow: 'https://internetl.ink/static_html/icons/icon_v_left_pink.svg',
            quickPickBarArrow: 'https://internetl.ink/static_html/icons/icon_v_down_pink.svg',
            menuPosition: 'left',
        }
    },
    mounted() {
        // Initialize tooltips
        this.$nextTick(() => {
            let tooltipTriggerList = [].slice.call(document.querySelectorAll('[data-bs-toggle="tooltip"]'));
            tooltipTriggerList.map((tooltipTriggerEl) => {
                return new bootstrap.Tooltip(tooltipTriggerEl);
            });
        });
        const dropdowns = document.querySelectorAll(".btn-group");
        dropdowns.forEach((dropdown) => {
            dropdown.addEventListener("mouseover", () => {
                const dropdownToggle = dropdown.querySelector('[data-bs-toggle="dropdown"]');
                const bsDropdown = bootstrap.Dropdown.getOrCreateInstance(dropdownToggle);
                bsDropdown.show();
            });

            dropdown.addEventListener("mouseout", () => {
                const dropdownToggle = dropdown.querySelector('[data-bs-toggle="dropdown"]');
                const bsDropdown = bootstrap.Dropdown.getInstance(dropdownToggle);
                if (bsDropdown) {
                    bsDropdown.hide();
                }
            });
        });

    },
    methods: {
        toggleMenu() {
            this.isMenuHidden = !this.isMenuHidden;
            if (this.isMenuHidden) {
                this.menuArrow = 'https://internetl.ink/static_html/icons/icon_v_right_pink.svg'
            } else {
                this.menuArrow = 'https://internetl.ink/static_html/icons/icon_v_left_pink.svg'
            }
        },
        toggleQuickPickBar(){
            this.isQuickPickBar = !this.isQuickPickBar;
            if(this.isQuickPickBar){
                this.quickPickBarArrow = 'https://internetl.ink/static_html/icons/icon_v_up_pink.svg'
            }else{
                this.quickPickBarArrow = 'https://internetl.ink/static_html/icons/icon_v_down_pink.svg'
            }
        },
        toggleMenuPosition(position){
            if(position === 'right'){
                this.menuPosition = 'right'
            }else if(position === 'left'){
                this.menuPosition = 'left'
            }else if(position === 'top'){
                this.menuPosition = 'top'
            }
        }
    }
}
const signOut = (name) => {
    console.log(name);
}
</script>
<template>
    <main class="flex gap-5 min-h-screen overflow-x-hidden" :class="menuPosition === 'left' ? 'flex-row' : (menuPosition === 'right') ? 'flex-row-reverse' : '!gap-0'" >
        <aside class="w-fit bg-gray-800 text-white  flex flex-col relative" :class="menuPosition === 'top' ? 'hidden' : ''">
            <img @click="toggleMenu()" class="w-[1.3rem] max-w-[2rem] absolute top-5 cursor-pointer" :class="menuPosition === 'right' ? 'right-[102%] rotate-180' : 'left-[102%]'"
                :src="menuArrow" alt="iconVMenu">
            <div class="h-full p-2 w-[12rem] overflow-hidden bg-transparent flex flex-col transition-all duration-300"
                :class="{ 'hide-menu': isMenuHidden }">
                <div class="logo-holder py-2 bg-transparent w-full mt-4">
                    <Logo />
                </div>
                <div class="bg-gray-700 rounded-lg p-2  flex items-center gap-2 w-full">
                    <UAvatar src="https://avatars.githubusercontent.com/u/739984?v=4" alt="Avatar" />
                    <p class="font-bold w-fit">
                        Mikey Sharma
                    </p>
                </div>
                <div class="flex flex-col gap-y-3 mt-3">
                    <UButton block to="/dashboard"> Dashboard </UButton>
                    <UButton block to="/create-email-compose">
                        Create Email
                    </UButton>
                </div>
                <UButton block @click="signOut({ callbackUrl: '/auth/login' })" class="mt-auto" color="gray"
                    variant="solid">
                    Logout
                </UButton>
                <p class="text-center mt-3 text-sm">Mailsniplet V{{ '0.0.2' }}</p>
            </div>
        </aside>
        <section class="flex-grow flex flex-col gap-[0.75vw] items-center">
            <aside class="w-full bg-gray-800 text-white flex-row relative " :class="menuPosition === 'top' ? 'flex' : 'hidden'">
            <img @click="toggleMenu()" class="w-[1.3rem] max-w-[2rem] absolute left-5 cursor-pointer top-[102%] rotate-90"
                :src="menuArrow" alt="iconVMenu">
            <div class="h-full p-2 w-full overflow-hidden bg-transparent flex flex-row gap-[0.75vw] items-center justify-between transition-all duration-300"
                :class="{ 'hide-menu-top': isMenuHidden }">
                <div class="logo-holder py-2 bg-transparent w-[20vw]">
                    <Logo />
                </div>
                <div class="bg-gray-700 rounded-lg p-2  flex items-center gap-2 w-fit h-fit">
                    <UAvatar src="https://avatars.githubusercontent.com/u/739984?v=4" alt="Avatar" />
                    <p class="font-bold w-fit">
                        Mikey Sharma
                    </p>
                </div>
                <div class="flex flex-row gap-[0.75vw] mt-1 h-fit w-fit">
                    <UButton class="w-fit" block to="/dashboard"> Dashboard </UButton>
                    <UButton class="w-fit" block to="/create-email-compose">
                        Create Email
                    </UButton>
                </div>
                <UButton block @click="signOut({ callbackUrl: '/auth/login' })" class=" w-fit h-fit" color="gray"
                    variant="solid">
                    Logout
                </UButton>
                <p class="text-center  text-sm">Mailsniplet V{{ '0.0.2' }}</p>
            </div>
        </aside>
            <slot />
        </section>
        <aside class="min-w-[4vw] lg:w-[7vw] w-[4vw] bg-gray-700 p-[1vw]">
            <div class="flex items-center flex-col gap-[0.75vw]">
                <a href="https://internetl.ink/static_html/web_user_settings.html"
                    class="text-decoration-none text-reset w-[4vw]" data-bs-trigger="hover" data-bs-placement="left"
                    data-bs-toggle="tooltip" data-bs-title="Click to navigate to Setting page">
                    <img alt="settings" src="https://internetl.ink/static_html/icons/icon_settings_pink.svg"  class="w-[4vw]" />
                </a>
                <a  @click="toggleQuickPickBar()" class="text-decoration-none text-reset w-[4vw] cursor-pointer" data-bs-trigger="hover"
                    data-bs-toggle="tooltip" data-bs-placement="left" data-bs-title="Click to toggle quick-pick bar">
                    <img alt="down-arrow" :src="quickPickBarArrow" class="w-[4vw]" />
                </a>
                <div class="flex items-center flex-col gap-[0.75vw] transition-all duration-300" :class="{'hide-quickpickbar' : isQuickPickBar}">
                    <!-- different mode -->
                    <div class="btn-group dropstart">
                        <button type="button" class="btn btn-icon p-0 text-decoration-none text-reset" id="modeToggleMenu"
                            data-bs-toggle="dropdown" aria-expanded="false">
                            <img src="https://internetl.ink/static_html/icons/icon_colour_flower.svg"
                                class="main-img-mode w-[4vw]" alt="Theme Mode" />
                        </button>
                        <ul class="dropdown-menu dropdown-mode dropdown-menu-dark text-center"
                            aria-labelledby="modeToggleMenu">
                            <li>
                                <span class="dropdown-item dropdown-item-mode active" data-bs-toggle="tooltip"
                                    data-bs-trigger="hover" data-bs-placement="left" data-mode="1"
                                    data-bs-title="Click to activate Dark Mode 1">
                                    <img class="w-full px-1" data-mode="1"
                                        src="https://internetl.ink/static_html/icons/icon_webpage_dark_1.svg" alt="">
                                </span>
                            </li>
                            <li>
                                <span class="dropdown-item dropdown-item-mode" data-bs-toggle="tooltip"
                                    data-bs-trigger="hover" data-bs-placement="left" data-mode="2"
                                    data-bs-title="Click to activate Dark Mode 2">
                                    <img class="w-full px-1" data-mode="2"
                                        src="https://internetl.ink/static_html/icons/icon_webpage_dark_2.svg" alt="">
                                </span>
                            </li>
                            <li>
                                <span class="dropdown-item dropdown-item-mode" data-bs-toggle="tooltip"
                                    data-bs-trigger="hover" data-bs-placement="left" data-mode="3"
                                    data-bs-title="Click to activate Dark Mode 3" id="3">
                                    <img class="w-full px-1" data-mode="3"
                                        src="https://internetl.ink/static_html/icons/icon_webpage_dark_3.svg" alt="">
                                </span>
                            </li>
                            <li>
                                <span class="dropdown-item dropdown-item-mode" data-bs-toggle="tooltip"
                                    data-bs-trigger="hover" data-bs-placement="left" data-mode="4"
                                    data-bs-title="Click to activate Dark Mode 4">
                                    <img class="w-full px-1" data-mode="4"
                                        src="https://internetl.ink/static_html/icons/icon_webpage_dark_4.svg" alt="">
                                </span>
                            </li>
                            <li>
                                <span class="dropdown-item dropdown-item-mode" href="#" data-bs-toggle="tooltip"
                                    data-bs-trigger="hover" data-bs-placement="left" data-mode="5"
                                    data-bs-title="Click to activate Light Mode 1">
                                    <img class="w-full px-1" data-mode="5"
                                        src="https://internetl.ink/static_html/icons/icon_webpage_light_1.svg" alt="">
                                </span>
                            </li>
                            <li>
                                <span class="dropdown-item dropdown-item-mode" href="#" data-bs-toggle="tooltip"
                                    data-bs-trigger="hover" data-bs-placement="left" data-mode="6"
                                    data-bs-title="Click to activate Light Mode 2">
                                    <img class="w-full px-1" data-mode="6"
                                        src="https://internetl.ink/static_html/icons/icon_webpage_light_2.svg" alt="">
                                </span>
                            </li>
                            <li>
                                <span class="dropdown-item dropdown-item-mode" href="#" data-bs-toggle="tooltip"
                                    data-bs-trigger="hover" data-bs-placement="left" data-mode="7"
                                    data-bs-title="Click to activate Light Mode 3">
                                    <img class="w-full px-1" data-mode="7"
                                        src="https://internetl.ink/static_html/icons/icon_webpage_light_3.svg" alt="">
                                </span>
                            </li>
                            <li>
                                <span class="dropdown-item dropdown-item-mode" href="#" data-bs-toggle="tooltip"
                                    data-bs-trigger="hover" data-bs-placement="left" data-mode="8"
                                    data-bs-title="Click to activate Light Mode 4">
                                    <img class="w-full px-1" data-mode="8"
                                        src="https://internetl.ink/static_html/icons/icon_webpage_light_4.svg" alt="">
                                </span>
                            </li>
                        </ul>
                    </div>
                    <!-- different favicon -->
                    <div class="btn-group dropstart">
                        <a href="#" class="btn btn-icon p-0 text-decoration-none text-reset" data-bs-toggle="dropdown"
                            aria-expanded="false">
                            <img src="https://internetl.ink/static_html/icons/ew_favicon_dark_1.svg"
                                class="main-img-favicon w-[4vw]" alt="Favicon Type" />
                        </a>
                        <ul class="dropdown-menu dropdown-mode dropdown-menu-dark text-center">
                            <li>
                                <a class="dropdown-item dropdown-item-favicon active" data-bs-toggle="tooltip"
                                    data-bs-trigger="hover" data-bs-placement="left" data-mode="1"
                                    data-bs-title="Click to activate Dark Favicon 1">
                                    <img class="w-full p-1" data-mode="1"
                                        src="https://internetl.ink/static_html/icons/ew_favicon_dark_1.svg" alt="">
                                </a>
                            </li>
                            <li>
                                <a class="dropdown-item dropdown-item-favicon" data-bs-toggle="tooltip"
                                    data-bs-trigger="hover" data-bs-placement="left" data-mode="2"
                                    data-bs-title="Click to activate Dark Favicon 2">
                                    <img class="w-full p-1" data-mode="2"
                                        src="https://internetl.ink/static_html/icons/ew_favicon_dark_2.svg" alt="">
                                </a>
                            </li>
                            <li>
                                <a class="dropdown-item dropdown-item-favicon" data-bs-toggle="tooltip"
                                    data-bs-trigger="hover" data-bs-placement="left" data-mode="3"
                                    data-bs-title="Click to activate Dark Favicon 3" id="3">
                                    <img class="w-full p-1" data-mode="3"
                                        src="https://internetl.ink/static_html/icons/ew_favicon_dark_3.svg" alt="">
                                </a>
                            </li>
                            <li>
                                <a class="dropdown-item dropdown-item-favicon" data-bs-toggle="tooltip"
                                    data-bs-trigger="hover" data-bs-placement="left" data-mode="4"
                                    data-bs-title="Click to activate Dark Favicon 4">
                                    <img class="w-full p-1" data-mode="4"
                                        src="https://internetl.ink/static_html/icons/ew_favicon_dark_4.svg" alt="">
                                </a>
                            </li>
                            <li>
                                <a class="dropdown-item dropdown-item-favicon" href="#" data-bs-toggle="tooltip"
                                    data-bs-trigger="hover" data-bs-placement="left" data-mode="5"
                                    data-bs-title="Click to activate Light Favicon 1">
                                    <img class="w-full p-1" data-mode="5"
                                        src="https://internetl.ink/static_html/icons/ew_favicon_light_1.svg" alt="">
                                </a>
                            </li>
                            <li>
                                <a class="dropdown-item dropdown-item-favicon" href="#" data-bs-toggle="tooltip"
                                    data-bs-trigger="hover" data-bs-placement="left" data-mode="6"
                                    data-bs-title="Click to activate Light Favicon 2">
                                    <img class="w-full p-1" data-mode="6"
                                        src="https://internetl.ink/static_html/icons/ew_favicon_light_2.svg" alt="">
                                </a>
                            </li>
                            <li>
                                <a class="dropdown-item dropdown-item-favicon" href="#" data-bs-toggle="tooltip"
                                    data-bs-trigger="hover" data-bs-placement="left" data-mode="7"
                                    data-bs-title="Click to activate Light Favicon 3">
                                    <img class="w-full p-1" data-mode="7"
                                        src="https://internetl.ink/static_html/icons/ew_favicon_light_3.svg" alt="">
                                </a>
                            </li>
                            <li>
                                <a class="dropdown-item dropdown-item-favicon" href="#" data-bs-toggle="tooltip"
                                    data-bs-trigger="hover" data-bs-placement="left" data-mode="8"
                                    data-bs-title="Click to activate Light Favicon 4">
                                    <img class="w-full p-1" data-mode="8"
                                        src="https://internetl.ink/static_html/icons/ew_favicon_light_4.svg" alt="">
                                </a>
                            </li>
                        </ul>
                    </div>
                    <div class="btn-group dropstart">
                        <a href="#" class="btn btn-icon p-0" data-bs-toggle="dropdown" aria-expanded="false">
                            <img alt="Screen Type"
                                src="https://internetl.ink/static_html/icons/icon_screen_auto_detect_pink.svg"
                                class="main-img w-[4vw]" />
                        </a>
                        <ul class="dropdown-menu dropdown-menu-dark text-center">
                            <li>
                                <a class="dropdown-item dropdown-item-1 active" href="#" data-bs-toggle="tooltip"
                                    data-bs-placement="left" data-bs-custom-class="custom-tooltip"
                                    data-bs-title="Automatic detection of the screen type">
                                    <img class="w-full p-1"
                                        src="https://internetl.ink/static_html/icons/icon_screen_auto_detect_pink.svg"
                                        alt="Auto Detect" data-screen-type="auto_detect" />
                                </a>
                            </li>
                            <li>
                                <a class="dropdown-item dropdown-item-1" href="#" data-bs-toggle="tooltip"
                                    data-bs-placement="left" data-bs-custom-class="custom-tooltip"
                                    data-bs-title="Select for mobile version">
                                    <img class="w-full p-1"
                                        src="https://internetl.ink/static_html/icons/icon_mobile_pink.svg" alt="Mobile"
                                        data-screen-type="mobile" />
                                </a>
                            </li>
                            <li>
                                <a class="dropdown-item dropdown-item-1" href="#" data-bs-toggle="tooltip"
                                    data-bs-placement="left" data-bs-custom-class="custom-tooltip"
                                    data-bs-title="Select for tablet version">
                                    <img class="w-full p-1" alt="Tablet"
                                        src="https://internetl.ink/static_html/icons/icon_tablet_pink.svg"
                                        data-screen-type="tablet" />
                                </a>
                            </li>
                            <li>
                                <a class="dropdown-item dropdown-item-1" href="#" data-bs-toggle="tooltip"
                                    data-bs-placement="left" data-bs-custom-class="custom-tooltip"
                                    data-bs-title="Select for laptop and desktop">
                                    <img class="w-full p-1" alt="Laptop"
                                        src="https://internetl.ink/static_html/icons/icon_laptop_pink.svg"
                                        data-screen-type="laptop" /></a>
                            </li>
                            <li>
                                <a class="dropdown-item dropdown-item-1" href="#" data-bs-toggle="tooltip"
                                    data-bs-placement="left" data-bs-custom-class="custom-tooltip"
                                    data-bs-title="Select for wide and high-resolution screens">
                                    <img class="w-full p-1" alt="Monitor"
                                        src="https://internetl.ink/static_html/icons/icon_monitor_pink.svg"
                                        data-screen-type="monitor" /></a>
                            </li>
                        </ul>
                    </div>
                    <!-- different menu position -->
                    <div class="btn-group dropstart">
                        <a href="#" class="btn btn-icon p-0 text-decoration-none text-reset" data-bs-toggle="dropdown"
                            aria-expanded="false">
                            <img alt="Menu Position" src="https://internetl.ink/static_html/icons/icon_menu_left_pink.svg"
                                class="main-img-2 w-[4vw]" />
                        </a>
                        <ul class="dropdown-menu dropdown-menu-dark text-center">
                            <li>
                                <a @click="toggleMenuPosition('right')" class="dropdown-item dropdown-item-2" :class="{'active' : menuPosition === 'right'}" data-bs-toggle="tooltip"
                                    data-bs-placement="left" data-bs-custom-class="custom-tooltip"
                                    data-bs-title="Menu Position Right">
                                    <img class="w-full p-1" src="https://internetl.ink/static_html/icons/icon_menu_right_pink.svg"
                                        alt="Menu Right" data-menu-type="right" />
                                </a>
                            </li>
                            <li>
                                <a @click="toggleMenuPosition('top')" class="dropdown-item dropdown-item-2" :class="{'active' : menuPosition === 'top'}" data-bs-toggle="tooltip"
                                    data-bs-placement="left" data-bs-custom-class="custom-tooltip"
                                    data-bs-title="Menu Position Top">
                                    <img class="w-full p-1"
                                        src="https://internetl.ink/static_html/icons/icon_menu_top_pink.svg" alt="Menu Top"
                                        data-menu-type="top" />
                                </a>
                            </li>
                            <li>
                                <a @click="toggleMenuPosition('left')" class="dropdown-item dropdown-item-2" :class="{'active' : menuPosition === 'left'}" data-bs-toggle="tooltip"
                                    data-bs-placement="left" data-bs-custom-class="custom-tooltip"
                                    data-bs-title="Menu Position Left">
                                    <img class="w-full p-1"
                                        src="https://internetl.ink/static_html/icons/icon_menu_left_pink.svg"
                                        alt="Menu Left" data-menu-type="left" />
                                </a>
                            </li>
                        </ul>
                    </div>
                    <!-- for font family -->
                    <div class="btn-group dropstart">
                        <a href="#" class="btn btn-icon p-0 text-decoration-none text-reset" data-bs-toggle="dropdown"
                            aria-expanded="false">
                            <img src="https://internetl.ink/static_html/icons/icon_aa_pink.svg"
                                class="main-img-family w-[4vw]" alt="Font Family" />
                        </a>
                        <ul class="dropdown-menu dropdown-menu-dark text-center">
                            <li>
                                <a class="dropdown-item dropdown-item-family active" data-bs-toggle="tooltip"
                                    data-bs-trigger="hover" data-bs-placement="left" data-mode="lato_regular"
                                    data-bs-title="Click to activate Lato Regular">
                                    <span class="w-full text-center" data-mode="lato_regular">Lato Regular</span>
                                </a>
                            </li>
                            <li>
                                <a class="dropdown-item dropdown-item-family" data-bs-toggle="tooltip"
                                    data-bs-trigger="hover" data-bs-placement="left" data-mode="roboto"
                                    data-bs-title="Click to activate Roboto">
                                    <span class="w-full text-center" data-mode="roboto">Roboto</span>
                                </a>
                            </li>
                            <li>
                                <a class="dropdown-item dropdown-item-family" data-bs-toggle="tooltip"
                                    data-bs-trigger="hover" data-bs-placement="left" data-mode="open_sans"
                                    data-bs-title="Click to activate Open Sans" id="3">
                                    <span class="w-full text-center" data-mode="open_sans">Open Sans</span>
                                </a>
                            </li>
                            <li>
                                <a class="dropdown-item dropdown-item-family" data-bs-toggle="tooltip"
                                    data-bs-trigger="hover" data-bs-placement="left" data-mode="montserrat"
                                    data-bs-title="Click to activate Montserrat">
                                    <span class="w-full text-center" data-mode="montserrat">Montserrat</span>
                                </a>
                            </li>
                        </ul>
                    </div>
                    <!-- forfont -->
                    <div class="btn-group dropstart">
                        <a href="#" class="btn btn-icon p-0 text-decoration-none text-reset" data-bs-toggle="dropdown"
                            aria-expanded="false">
                            <span class="main-img-2 main-font-size" style=" line-height: 1; padding: 4px;">18</span>
                        </a>
                        <ul class="dropdown-menu dropdown-font dropdown-menu-dark text-center">
                            <li>
                                <a class="dropdown-item dropdown-item-fonts" id="minus_1" href="#" data-font-correction="-1"
                                    data-bs-toggle="tooltip" data-bs-trigger="hover" data-bs-placement="top"
                                    data-bs-title="Decrease the text size by 1">
                                    <img class="w-full p-1"
                                        src="https://internetl.ink/static_html/icons/icon_minus_one_pink.svg" alt="" />
                                </a>
                            </li>
                            <li>
                                <a class="dropdown-item dropdown-item-fonts-current dropdown-item-fonts active"
                                    id="current_size" href="#" data-bs-toggle="tooltip" data-bs-trigger="hover"
                                    data-bs-placement="top" data-bs-title="Current Size">
                                    <span class="main-font-size li"
                                        style="font-size: 4em !important; padding: 0px 15px;">18</span>
                                </a>
                            </li>
                            <li>
                                <a class="dropdown-item dropdown-item-fonts" id="plus_1" href="#" data-font-correction="+1"
                                    data-bs-toggle="tooltip" data-bs-trigger="hover" data-bs-placement="top"
                                    data-bs-title="Increase the text size by 1">
                                    <img class="w-full p-1"
                                        src="https://internetl.ink/static_html/icons/icon_plus_one_pink.svg" alt="" />
                                </a>
                            </li>

                        </ul>
                    </div>
                    <!-- split_screen-->
                    <a href="#" data-bs-toggle="tooltip" data-bs-placement="left"
                        data-bs-title="Click to toggle split srceen" data-bs-trigger="hover"
                        class="text-decoration-none text-reset" @click="splitScreen()">
                        <img class="w-[4vw] p-0" src="https://internetl.ink/static_html/icons/icon_single_pane_pink.svg"
                            alt="split_screen" />
                    </a>
                </div>
            </div>
        </aside>
    </main>
</template>
<style>
.dropdown-menu {
    min-width: 50% !important;
    padding: 5px;
}

.dropdown-item {
    border: 4px solid transparent;
    padding: 2px;
    width: fit-content;
}

.dropdown-item img {
    cursor: pointer;
    max-width: 10em;
    width: 6em !important;
}
.dropdown-item-family{
    width: 100% !important;
    cursor: pointer;
}
.dropdown-item.active {
    border: 4px solid var(--border-dropdown-active-item, #888);
    border-radius: 20px;
    background-color: transparent;
}

.dropdown-item:hover {
    border: 4px solid var(--border-dropdown-hover-item, #888);
    border-radius: 20px;
    background-color: transparent;
}

.dropdown-mode.show {
    display: grid;
    grid-template-columns: repeat(2, 1fr);
    gap: 10px;
}

.main-font-size {
    font-weight: 600;
    color: transparent;
    -webkit-text-stroke: 2px #dd1d4c;
    font-size: 3em !important;
}

.btn-icon {
    padding: 4px !important;
    border: 3px solid transparent;
    border-radius: 20px;
}

.btn-icon.show {
    border-color: #888;
}

.dropdown-font.show {
    display: flex !important;
    gap: 10px;
}
.hide-quickpickbar{
    height: 0px;
    min-height: 0px;
    overflow: hidden;
    padding: 0px !important;
    transition: all 0.3s ease-in-out;
}

.hide-menu-top {
    height: 0px;
    opacity: 0;
    padding: 0px !important;
    transition: all 0.3s ease-in-out;
}
.hide-menu {
    width: 0px;
    opacity: 0;
    padding: 0px !important;
    transition: all 0.3s ease-in-out;
}</style>