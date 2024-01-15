
<script>
export default {
    data() { 
        return {
            isMenuHidden: false,
            isQuickPickBar: false,
            menuArrow: 'https://internetl.ink/static_html/icons/icon_v_left_pink.svg',
            quickPickBarArrow: 'https://internetl.ink/static_html/icons/icon_v_down_pink.svg',
            menuPosition: 'left',
            mainMenuPosition: 'https://internetl.ink/static_html/icons/icon_menu_left_pink.svg',
            rightisMenuHidden: false,
            rightisQuickPickBar: false,
            rightmenuArrow: 'https://internetl.ink/static_html/icons/icon_v_left_pink.svg',
            rightquickPickBarArrow: 'https://internetl.ink/static_html/icons/icon_v_down_pink.svg',
            rightmenuPosition: 'left',
            rightmainMenuPosition: 'https://internetl.ink/static_html/icons/icon_menu_left_pink.svg',
            faviconNo: '1',
            mainFavicon: 'https://internetl.ink/static_html/icons/ew_favicon_dark_1.svg',
            fontFamily: 'lato_regular',
            rightfontFamily: 'lato_regular',
            fontSize: 18,
            screenType: 'auto_detect',
            mainScreenType: 'https://internetl.ink/static_html/icons/icon_screen_auto_detect_pink.svg',
            rightfontSize: 18,
            rightscreenType: 'auto_detect',
            rightmainScreenType: 'https://internetl.ink/static_html/icons/icon_screen_auto_detect_pink.svg',
            isRightPanel: false,
            mainSplitScreen: 'https://internetl.ink/static_html/icons/icon_dual_pane_pink.svg',
            mode: '1',
            rightmode: '1',
            isLoading: true,
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
        if (this.getCookie('menu_position')) {
            this.toggleMenuPosition(this.getCookie('menu_position'))
        }
        if (this.getCookie('menu_position_right')) {
            this.righttoggleMenuPosition(this.getCookie('menu_position_right'))
        }
        if (this.getCookie('favicon')) {
            this.toggleFavicon(this.getCookie('favicon'))
        }
        if (this.getCookie('font_family')) {
            this.toggleFont(this.getCookie('font_family'))
        }
        if (this.getCookie('font_family_right')) {
            this.righttoggleFont(this.getCookie('font_family_right'))
        }
        if (this.getCookie('font_size')) {
            this.toggleFontSize(this.getCookie('font_size'))
        }
        if (this.getCookie('font_size_right')) {
            this.righttoggleFontSize(this.getCookie('font_size_right'))
        }
        if (this.getCookie('screen_type')) {
            this.toggleScreenType(this.getCookie('screen_type'))
        }
        if (this.getCookie('screen_type_right')) {
            this.righttoggleScreenType(this.getCookie('screen_type_right'))
        }
        if (this.getCookie('split_screen')) {
            this.toggleScreen(true)
        }

        if (this.getCookie('mode')) {
            this.toggleMode(this.getCookie('mode'))
        }
        if (this.getCookie('right_mode')) {
            this.togglerightMode(this.getCookie('right_mode'))
        }
        this.isLoading = false;
    },
    methods: {
        setCookie(cookieName, cookieValue) {
            document.cookie = `${cookieName}=${cookieValue}; path=${location.pathname}`
        },
        getCookie(cookieName) {
            const cookies = document.cookie.split(';');
            for (const item of cookies) {
                const [name, value] = item.split('=');
                if (name.trim() === cookieName) {
                    const cookieValue = decodeURIComponent(value)
                    return cookieValue;
                }
            }
            return null;
        },
        toggleMenu() {
            this.isMenuHidden = !this.isMenuHidden;
            if (this.isMenuHidden) {
                this.menuArrow = 'https://internetl.ink/static_html/icons/icon_v_right_pink.svg'
            } else {
                this.menuArrow = 'https://internetl.ink/static_html/icons/icon_v_left_pink.svg'
            }
        },
        righttoggleMenu() {
            this.rightisMenuHidden = !this.rightisMenuHidden;
            if (this.rightisMenuHidden) {
                this.rightmenuArrow = 'https://internetl.ink/static_html/icons/icon_v_right_pink.svg'
            } else {
                this.rightmenuArrow = 'https://internetl.ink/static_html/icons/icon_v_left_pink.svg'
            }
        },
        toggleQuickPickBar() {
            this.isQuickPickBar = !this.isQuickPickBar;
            if (this.isQuickPickBar) {
                this.quickPickBarArrow = 'https://internetl.ink/static_html/icons/icon_v_up_pink.svg'
            } else {
                this.quickPickBarArrow = 'https://internetl.ink/static_html/icons/icon_v_down_pink.svg'
            }
        },
        righttoggleQuickPickBar() {
            this.rightisQuickPickBar = !this.rightisQuickPickBar;
            if (this.rightisQuickPickBar) {
                this.rightquickPickBarArrow = 'https://internetl.ink/static_html/icons/icon_v_up_pink.svg'
            } else {
                this.rightquickPickBarArrow = 'https://internetl.ink/static_html/icons/icon_v_down_pink.svg'
            }
        },
        toggleMenuPosition(position) {
            if (position === 'right') {
                this.menuPosition = 'right';
                this.mainMenuPosition = 'https://internetl.ink/static_html/icons/icon_menu_right_pink.svg'
               
            } else if (position === 'left') {
                this.menuPosition = 'left';
                this.mainMenuPosition = 'https://internetl.ink/static_html/icons/icon_menu_left_pink.svg'
                
            } else if (position === 'top') {
                this.menuPosition = 'top';
                this.mainMenuPosition = 'https://internetl.ink/static_html/icons/icon_menu_top_pink.svg'
                
            }
            this.setCookie('menu_position', position)
        },
        righttoggleMenuPosition(position) {
            if (position === 'right') {
                this.rightmenuPosition = 'right';
                this.rightmainMenuPosition = 'https://internetl.ink/static_html/icons/icon_menu_right_pink.svg'
               
            } else if (position === 'left') {
                this.rightmenuPosition = 'left';
                this.rightmainMenuPosition = 'https://internetl.ink/static_html/icons/icon_menu_left_pink.svg';
               
            } else if (position === 'top') {
                this.rightmenuPosition = 'top';
                this.rightmainMenuPosition = 'https://internetl.ink/static_html/icons/icon_menu_top_pink.svg';
               
            }
            this.setCookie('menu_position_right', position)
        },
        toggleFavicon(favicon) {
            const faviconElem = document.querySelector('#dynamic-favicon')
            if (favicon === '1') {
                faviconElem.href = 'https://internetl.ink/static_html/icons/ew_favicon_dark_1.svg'
                this.faviconNo = '1';
                this.mainFavicon = 'https://internetl.ink/static_html/icons/ew_favicon_dark_1.svg'
            } else if (favicon === '2') {
                faviconElem.href = 'https://internetl.ink/static_html/icons/ew_favicon_dark_2.svg'
                this.faviconNo = '2';
                this.mainFavicon = 'https://internetl.ink/static_html/icons/ew_favicon_dark_2.svg'
            } else if (favicon === '3') {
                faviconElem.href = 'https://internetl.ink/static_html/icons/ew_favicon_dark_3.svg'
                this.faviconNo = '3';
                this.mainFavicon = 'https://internetl.ink/static_html/icons/ew_favicon_dark_3.svg'
            } else if (favicon === '4') {
                faviconElem.href = 'https://internetl.ink/static_html/icons/ew_favicon_dark_4.svg'
                this.faviconNo = '4';
                this.mainFavicon = 'https://internetl.ink/static_html/icons/ew_favicon_dark_4.svg'
            } else if (favicon === '5') {
                faviconElem.href = 'https://internetl.ink/static_html/icons/ew_favicon_light_1.svg'
                this.faviconNo = '5';
                this.mainFavicon = 'https://internetl.ink/static_html/icons/ew_favicon_light_1.svg'
            } else if (favicon === '6') {
                faviconElem.href = 'https://internetl.ink/static_html/icons/ew_favicon_light_2.svg'
                this.faviconNo = '6';
                this.mainFavicon = 'https://internetl.ink/static_html/icons/ew_favicon_light_2.svg'
            } else if (favicon === '7') {
                faviconElem.href = 'https://internetl.ink/static_html/icons/ew_favicon_light_3.svg'
                this.faviconNo = '7';
                this.mainFavicon = 'https://internetl.ink/static_html/icons/ew_favicon_light_3.svg'
            } else if (favicon === '8') {
                faviconElem.href = 'https://internetl.ink/static_html/icons/ew_favicon_light_4.svg'
                this.faviconNo = '8';
                this.mainFavicon = 'https://internetl.ink/static_html/icons/ew_favicon_light_4.svg'
            }
            this.setCokie('favicon', favicon);
        },
        toggleFont(font) {
            const bodyElem = document.querySelector('#left-panel')
            if (font === 'lato_regular') {
                this.fontFamily = 'lato_regular'
                bodyElem.style.fontFamily = 'var(--lato)'
            } else if (font === 'roboto') {
                this.fontFamily = 'roboto'
                bodyElem.style.fontFamily = 'var(--roboto)'
            } else if (font === 'open_sans') {
                this.fontFamily = 'open_sans'
                bodyElem.style.fontFamily = 'var(--open_sans)'
            } else if (font === 'montserrat') {
                this.fontFamily = 'montserrat'
                bodyElem.style.fontFamily = 'var(--montserrat)'
            }
            this.setCookie('font_family', font);
        },
        righttoggleFont(font) {
            const bodyElem = document.querySelector('#right-panel')
            if (font === 'lato_regular') {
                this.rightfontFamily = 'lato_regular'
                bodyElem.style.fontFamily = 'var(--lato)'
            } else if (font === 'roboto') {
                this.rightfontFamily = 'roboto'
                bodyElem.style.fontFamily = 'var(--roboto)'
            } else if (font === 'open_sans') {
                this.rightfontFamily = 'open_sans'
                bodyElem.style.fontFamily = 'var(--open_sans)'
            } else if (font === 'montserrat') {
                this.rightfontFamily = 'montserrat'
                bodyElem.style.fontFamily = 'var(--montserrat)'
            }
            this.setCookie('font_family_right', font);
        },
        toggleFontSize(value) {
            if (value === '+1') {
                this.fontSize += 1;
            } else if (value === '-1') {
                this.fontSize -= 1;
            } else {
                this.fontSize = parseInt(value);
            }
            const leftPanel = document.getElementById('left-panel');
            leftPanel.querySelectorAll('*').forEach((item) => {
                item.style.fontSize = `${this.fontSize}px`;
            })
            this.setCookie('font_size', this.fontSize);
        },
        righttoggleFontSize(value) {
            if (value === '+1') {
                this.rightfontSize += 1;
            } else if (value === '-1') {
                this.rightfontSize -= 1;
            } else {
                this.rightfontSize = parseInt(value);
            }
            const rightPanel = document.getElementById('right-panel');
            rightPanel.querySelectorAll('*').forEach((item) => {
                item.style.fontSize = `${this.rightfontSize}px`;
            })
            this.setCookie('font_size_right', this.rightfontSize);
        },
        toggleScreenType(value) {
            if (value === 'mobile') {
                this.screenType = 'mobile';
                if (!this.getCookie('font_size')) {
                    this.toggleFontSize(14);
                }
                this.mainScreenType = 'https://internetl.ink/static_html/icons/icon_mobile_pink.svg'
            } else if (value === 'tablet') {
                this.screenType = 'tablet';
                if (!this.getCookie('font_size')) {
                    this.toggleFontSize(16);
                }
                this.mainScreenType = 'https://internetl.ink/static_html/icons/icon_tablet_pink.svg'
            } else if (value === 'laptop') {
                this.screenType = 'laptop';
                if (!this.getCookie('font_size')) {
                    this.toggleFontSize(18);
                }
                this.mainScreenType = 'https://internetl.ink/static_html/icons/icon_laptop_pink.svg'
            } else if (value === 'monitor') {
                this.screenType = 'monitor';
                if (!this.getCookie('font_size')) {
                    this.toggleFontSize(20);
                }
                this.mainScreenType = 'https://internetl.ink/static_html/icons/icon_monitor_pink.svg'
            } else if (value === 'auto_detect') {
                this.screenType = 'auto_detect';
                if (!this.getCookie('font_size')) {
                    this.toggleFontSize(18);
                }
                this.mainScreenType = 'https://internetl.ink/static_html/icons/icon_screen_auto_detect_pink.svg'
            }
            this.setCookie('screen_type', value);
        },
        righttoggleScreenType(value) {
            if (value === 'mobile') {
                this.rightscreenType = 'mobile';
                if (!this.getCookie('font_size_right')) {
                    this.righttoggleFontSize(14);
                }
                this.rightmainScreenType = 'https://internetl.ink/static_html/icons/icon_mobile_pink.svg'
            } else if (value === 'tablet') {
                this.rightscreenType = 'tablet';
                if (!this.getCookie('font_size_right')) {
                    this.righttoggleFontSize(16);
                }
                this.rightmainScreenType = 'https://internetl.ink/static_html/icons/icon_tablet_pink.svg'
            } else if (value === 'laptop') {
                this.rightscreenType = 'laptop';
                if (!this.getCookie('font_size_right')) {
                    this.righttoggleFontSize(18);
                }
                this.rightmainScreenType = 'https://internetl.ink/static_html/icons/icon_laptop_pink.svg'
            } else if (value === 'monitor') {
                this.rightscreenType = 'monitor';
                if (!this.getCookie('font_size_right')) {
                    this.righttoggleFontSize(20);
                }
                this.rightmainScreenType = 'https://internetl.ink/static_html/icons/icon_monitor_pink.svg'
            } else if (value === 'auto_detect') {
                this.rightscreenType = 'auto_detect';
                if (!this.getCookie('font_size_right')) {
                    this.righttoggleFontSize(18);
                }
                this.rightmainScreenType = 'https://internetl.ink/static_html/icons/icon_screen_auto_detect_pink.svg'
            }
            this.setCookie('screen_type_right', value);
        },
        toggleScreen(isCookie) {
            if (isCookie) {
                if (this.getCookie('split_screen') === 'yes') {
                    this.isRightPanel = true;
                } else if (this.getCookie('split_screen') === 'no') {
                    this.isRightPanel = false;
                }
            } else {
                this.isRightPanel = !this.isRightPanel;
            }
            if (this.isRightPanel) {
                this.mainSplitScreen = 'https://internetl.ink/static_html/icons/icon_single_pane_pink.svg';
                this.setCookie('split_screen', 'yes')
            } else {
                this.mainSplitScreen = 'https://internetl.ink/static_html/icons/icon_dual_pane_pink.svg';
                this.setCookie('split_screen', 'no')
            }

        },
        toggleMode(value) {
            const documentBody = document.querySelector('#left-panel');
            if (value === '1') {
                this.mode = '1';
                documentBody.style.setProperty('--body-bg-color', '#2D3E50');
                documentBody.style.setProperty('--body-text-color', '#C8D6E5');
                documentBody.style.setProperty('--bg-quick-pick-bar', '#1F2A36');
                documentBody.style.setProperty('--bg-dropdown-menu', '#35445A');
                documentBody.style.setProperty('--border-dropdown-active-item', '#8096A8');
                documentBody.style.setProperty('--border-dropdown-hover-item', '#6F839D');
                documentBody.style.setProperty('--bg-menu', '#2F445A');
            } else if (value === '2') {
                this.mode = '2';
                documentBody.style.setProperty('--body-bg-color', '#8E44AD');
                documentBody.style.setProperty('--body-text-color', '#F4ECF7');
                documentBody.style.setProperty('--bg-quick-pick-bar', '#4E1D5D');
                documentBody.style.setProperty('--bg-dropdown-menu', '#512D69');
                documentBody.style.setProperty('--border-dropdown-active-item', '#B26CC3');
                documentBody.style.setProperty('--border-dropdown-hover-item', '#F4ECF7');
                documentBody.style.setProperty('--bg-menu', '#6B2D8A');
            } else if (value === '3') {
                this.mode = '3';
                documentBody.style.setProperty('--body-bg-color', '#D35400');
                documentBody.style.setProperty('--body-text-color', '#FDEBD0');
                documentBody.style.setProperty('--bg-quick-pick-bar', '#6F3900');
                documentBody.style.setProperty('--bg-dropdown-menu', '#B74D00');
                documentBody.style.setProperty('--border-dropdown-active-item', '#F3CA80');
                documentBody.style.setProperty('--border-dropdown-hover-item', '#E48C0D');
                documentBody.style.setProperty('--bg-menu', '#D77C08');
            } else if (value === '4') {
                this.mode = '4';
                documentBody.style.setProperty('--body-bg-color', '#16A085');
                documentBody.style.setProperty('--body-text-color', '#D1F2EB');
                documentBody.style.setProperty('--bg-quick-pick-bar', '#0D5E4C');
                documentBody.style.setProperty('--bg-dropdown-menu', '#1F917A');
                documentBody.style.setProperty('--border-dropdown-active-item', '#117058');
                documentBody.style.setProperty('--border-dropdown-hover-item', '#1FAE53');
                documentBody.style.setProperty('--bg-menu', '#1B886A');
            } else if (value === '5') {
                this.mode = '5';
                documentBody.style.setProperty('--body-bg-color', '#AED6F1');
                documentBody.style.setProperty('--body-text-color', '#1B4F72');
                documentBody.style.setProperty('--bg-quick-pick-bar', '#336E89');
                documentBody.style.setProperty('--bg-dropdown-menu', '#7FB3D1');
                documentBody.style.setProperty('--dropdown-active-border-item', '#2384B3');
                documentBody.style.setProperty('--border-dropdown-hover-item', '#60A1C3');
                documentBody.style.setProperty('--bg-menu', '#6D9FBB');
            } else if (value === '6') {
                this.mode = '6';
                documentBody.style.setProperty('--body-bg-color', '#FADBD8');
                documentBody.style.setProperty('--body-text-color', '#78281F');
                documentBody.style.setProperty('--bg-quick-pick-bar', '#FAC0BE');
                documentBody.style.setProperty('--bg-dropdown-menu', '#F8E8E6');
                documentBody.style.setProperty('--dropdown-active-border-item', '#9A322C');
                documentBody.style.setProperty('--border-dropdown-hover-item', '#C1574F');
                documentBody.style.setProperty('--bg-menu', '#F6E2E0');
            } else if (value === '7') {
                this.mode = '7';
                documentBody.style.setProperty('--body-bg-color', '#FAD7A0');
                documentBody.style.setProperty('--body-text-color', '#784212');
                documentBody.style.setProperty('--bg-quick-pick-bar', '#D17952');
                documentBody.style.setProperty('--bg-dropdown-menu', '#DC8C63');
                documentBody.style.setProperty('--dropdown-active-border-item', '#E6B37D');
                documentBody.style.setProperty('--border-dropdown-hover-item', '#E4B690');
                documentBody.style.setProperty('--bg-menu', '#F3BD7C');
            } else if (value === '8') {
                this.mode = '8';
                documentBody.style.setProperty('--body-bg-color', '#A3E4D7');
                documentBody.style.setProperty('--body-text-color', '#0E6251');
                documentBody.style.setProperty('--bg-quick-pick-bar', '#008B5E');
                documentBody.style.setProperty('--bg-dropdown-menu', '#48CDBD');
                documentBody.style.setProperty('--dropdown-active-border-item', '#00A881');
                documentBody.style.setProperty('--border-dropdown-hover-item', '#D6FFF8');
                documentBody.style.setProperty('--bg-menu', '#2DBFAE');
            }
            this.setCookie('mode', value)
        },
        togglerightMode(value) {
            const documentBody = document.querySelector('#right-panel');
            if (value === '1') {
                this.rightmode = '1';
                documentBody.style.setProperty('--body-bg-color', '#2D3E50');
                documentBody.style.setProperty('--body-text-color', '#C8D6E5');
                documentBody.style.setProperty('--bg-quick-pick-bar', '#1F2A36');
                documentBody.style.setProperty('--bg-dropdown-menu', '#35445A');
                documentBody.style.setProperty('--border-dropdown-active-item', '#8096A8');
                documentBody.style.setProperty('--border-dropdown-hover-item', '#6F839D');
                documentBody.style.setProperty('--bg-menu', '#2F445A');
            } else if (value === '2') {
                this.rightmode = '2';
                documentBody.style.setProperty('--body-bg-color', '#8E44AD');
                documentBody.style.setProperty('--body-text-color', '#F4ECF7');
                documentBody.style.setProperty('--bg-quick-pick-bar', '#4E1D5D');
                documentBody.style.setProperty('--bg-dropdown-menu', '#512D69');
                documentBody.style.setProperty('--border-dropdown-active-item', '#B26CC3');
                documentBody.style.setProperty('--border-dropdown-hover-item', '#F4ECF7');
                documentBody.style.setProperty('--bg-menu', '#6B2D8A');
            } else if (value === '3') {
                this.rightmode = '3';
                documentBody.style.setProperty('--body-bg-color', '#D35400');
                documentBody.style.setProperty('--body-text-color', '#FDEBD0');
                documentBody.style.setProperty('--bg-quick-pick-bar', '#6F3900');
                documentBody.style.setProperty('--bg-dropdown-menu', '#B74D00');
                documentBody.style.setProperty('--border-dropdown-active-item', '#F3CA80');
                documentBody.style.setProperty('--border-dropdown-hover-item', '#E48C0D');
                documentBody.style.setProperty('--bg-menu', '#D77C08');
            } else if (value === '4') {
                this.rightmode = '4';
                documentBody.style.setProperty('--body-bg-color', '#16A085');
                documentBody.style.setProperty('--body-text-color', '#D1F2EB');
                documentBody.style.setProperty('--bg-quick-pick-bar', '#0D5E4C');
                documentBody.style.setProperty('--bg-dropdown-menu', '#1F917A');
                documentBody.style.setProperty('--border-dropdown-active-item', '#117058');
                documentBody.style.setProperty('--border-dropdown-hover-item', '#1FAE53');
                documentBody.style.setProperty('--bg-menu', '#1B886A');
            } else if (value === '5') {
                this.rightmode = '5';
                documentBody.style.setProperty('--body-bg-color', '#AED6F1');
                documentBody.style.setProperty('--body-text-color', '#1B4F72');
                documentBody.style.setProperty('--bg-quick-pick-bar', '#336E89');
                documentBody.style.setProperty('--bg-dropdown-menu', '#7FB3D1');
                documentBody.style.setProperty('--dropdown-active-border-item', '#2384B3');
                documentBody.style.setProperty('--border-dropdown-hover-item', '#60A1C3');
                documentBody.style.setProperty('--bg-menu', '#6D9FBB');
            } else if (value === '6') {
                this.rightmode = '6';
                documentBody.style.setProperty('--body-bg-color', '#FADBD8');
                documentBody.style.setProperty('--body-text-color', '#78281F');
                documentBody.style.setProperty('--bg-quick-pick-bar', '#FAC0BE');
                documentBody.style.setProperty('--bg-dropdown-menu', '#F8E8E6');
                documentBody.style.setProperty('--dropdown-active-border-item', '#9A322C');
                documentBody.style.setProperty('--border-dropdown-hover-item', '#C1574F');
                documentBody.style.setProperty('--bg-menu', '#F6E2E0');
            } else if (value === '7') {
                this.rightmode = '7';
                documentBody.style.setProperty('--body-bg-color', '#FAD7A0');
                documentBody.style.setProperty('--body-text-color', '#784212');
                documentBody.style.setProperty('--bg-quick-pick-bar', '#D17952');
                documentBody.style.setProperty('--bg-dropdown-menu', '#DC8C63');
                documentBody.style.setProperty('--dropdown-active-border-item', '#E6B37D');
                documentBody.style.setProperty('--border-dropdown-hover-item', '#E4B690');
                documentBody.style.setProperty('--bg-menu', '#F3BD7C');
            } else if (value === '8') {
                this.rightmode = '8';
                documentBody.style.setProperty('--body-bg-color', '#A3E4D7');
                documentBody.style.setProperty('--body-text-color', '#0E6251');
                documentBody.style.setProperty('--bg-quick-pick-bar', '#008B5E');
                documentBody.style.setProperty('--bg-dropdown-menu', '#48CDBD');
                documentBody.style.setProperty('--dropdown-active-border-item', '#00A881');
                documentBody.style.setProperty('--border-dropdown-hover-item', '#D6FFF8');
                documentBody.style.setProperty('--bg-menu', '#2DBFAE');
            }
            this.setCookie('right_mode', value)
        }
    }
}
const signOut = (name) => {
    console.log(name);
}
</script>
<template>
    <section class="panel-container" :class="{ 'filter blur-md': isLoading }">
        <div id="left-panel" class="flex-grow">
            <main class="flex gap-[2.5vw] min-h-screen overflow-x-hidden"
                :class="menuPosition === 'left' ? 'flex-row' : (menuPosition === 'right') ? 'flex-row-reverse' : '!gap-0'">
                <aside class="w-fit menu    flex flex-col relative" :class="menuPosition === 'top' ? 'hidden' : ''">
                    <img @click="toggleMenu()" class="w-[1.3vw] max-w-[2vw] absolute top-5 cursor-pointer"
                        :class="menuPosition === 'right' ? 'right-[102%] rotate-180' : 'left-[102%]'" :src="menuArrow"
                        alt="iconVMenu">
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
                        <p class="text-center mt-3">Mailsniplet V{{ '0.0.5' }}</p>
                    </div>
                </aside>
                <section class="flex-grow flex flex-col gap-[0.75vw] items-center">
                    <aside class="w-full menu   flex-row relative " :class="menuPosition === 'top' ? 'flex' : 'hidden'">
                        <img @click="toggleMenu()"
                            class="w-[1.3vw] max-w-[2vw] absolute left-5 cursor-pointer top-[102%] rotate-90"
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
                            <UButton block @click="signOut({ callbackUrl: '/auth/login' })" class=" w-fit h-fit"
                                color="gray" variant="solid">
                                Logout
                            </UButton>
                            <p class="text-center">Mailsniplet V{{ '0.0.5' }}</p>
                        </div>
                    </aside>
                    <slot />
                </section>
                <aside class="min-w-[4vw] lg:w-[4vw] w-[6vw]  quick-pick-bar p-[0.25vw]">
                    <div class="flex items-center flex-col gap-[0.75vw]">
                        <a href="https://internetl.ink/static_html/web_user_settings.html"
                            class="text-decoration-none text-reset w-[4vw]" data-bs-trigger="hover" data-bs-placement="left"
                            data-bs-toggle="tooltip" data-bs-title="Click to navigate to Setting page">
                            <img alt="settings" src="https://internetl.ink/static_html/icons/icon_settings_pink.svg"
                                class="w-[4vw] p-[0.75vw]" />
                        </a>
                        <a @click="toggleQuickPickBar()" class="text-decoration-none text-reset w-[4vw] cursor-pointer"
                            data-bs-trigger="hover" data-bs-toggle="tooltip" data-bs-placement="left"
                            data-bs-title="Click to toggle quick-pick bar">
                            <img alt="down-arrow" :src="quickPickBarArrow" class="w-[4vw] p-[0.75vw]" />
                        </a>
                        <div class="flex items-center w-full flex-col gap-[0.75vw] transition-all duration-300"
                            :class="{ 'hide-quickpickbar': isQuickPickBar }">
                            <!-- different mode -->
                            <div class="btn-group dropstart">
                                <button type="button" class="btn btn-icon p-0 text-decoration-none text-reset"
                                    id="modeToggleMenu" data-bs-toggle="dropdown" aria-expanded="false">
                                    <img src="https://internetl.ink/static_html/icons/icon_colour_flower.svg"
                                        class="main-img-mode w-[4vw]" alt="Theme Mode" />
                                </button>
                                <ul class="dropdown-menu dropdown-mode dropdown-menu-dark text-center"
                                    aria-labelledby="modeToggleMenu">
                                    <li>
                                        <span class="dropdown-item dropdown-item-mode" :class="{ 'active': mode === '1' }"
                                            @click="toggleMode('1')" data-bs-toggle="tooltip" data-bs-trigger="hover"
                                            data-bs-placement="top" data-bs-title="Click to activate Dark Mode 1">
                                            <img class="w-full px-1"
                                                src="https://internetl.ink/static_html/icons/icon_webpage_dark_1.svg"
                                                alt="">
                                        </span>
                                    </li>
                                    <li>
                                        <span class="dropdown-item dropdown-item-mode" :class="{ 'active': mode === '2' }"
                                            @click="toggleMode('2')" data-bs-toggle="tooltip" data-bs-trigger="hover"
                                            data-bs-placement="top" data-bs-title="Click to activate Dark Mode 2">
                                            <img class="w-full px-1"
                                                src="https://internetl.ink/static_html/icons/icon_webpage_dark_2.svg"
                                                alt="">
                                        </span>
                                    </li>
                                    <li>
                                        <span class="dropdown-item dropdown-item-mode" :class="{ 'active': mode === '3' }"
                                            @click="toggleMode('3')" data-bs-toggle="tooltip" data-bs-trigger="hover"
                                            data-bs-placement="top" data-bs-title="Click to activate Dark Mode 3" id="3">
                                            <img class="w-full px-1"
                                                src="https://internetl.ink/static_html/icons/icon_webpage_dark_3.svg"
                                                alt="">
                                        </span>
                                    </li>
                                    <li>
                                        <span class="dropdown-item dropdown-item-mode" :class="{ 'active': mode === '4' }"
                                            @click="toggleMode('4')" data-bs-toggle="tooltip" data-bs-trigger="hover"
                                            data-bs-placement="top" data-bs-title="Click to activate Dark Mode 4">
                                            <img class="w-full px-1"
                                                src="https://internetl.ink/static_html/icons/icon_webpage_dark_4.svg"
                                                alt="">
                                        </span>
                                    </li>
                                    <li>
                                        <span class="dropdown-item dropdown-item-mode" :class="{ 'active': mode === '5' }"
                                            @click="toggleMode('5')" data-bs-toggle="tooltip" data-bs-trigger="hover"
                                            data-bs-placement="top" data-bs-title="Click to activate Light Mode 1">
                                            <img class="w-full px-1"
                                                src="https://internetl.ink/static_html/icons/icon_webpage_light_1.svg"
                                                alt="">
                                        </span>
                                    </li>
                                    <li>
                                        <span class="dropdown-item dropdown-item-mode" :class="{ 'active': mode === '6' }"
                                            @click="toggleMode('6')" data-bs-toggle="tooltip" data-bs-trigger="hover"
                                            data-bs-placement="top" data-bs-title="Click to activate Light Mode 2">
                                            <img class="w-full px-1"
                                                src="https://internetl.ink/static_html/icons/icon_webpage_light_2.svg"
                                                alt="">
                                        </span>
                                    </li>
                                    <li>
                                        <span class="dropdown-item dropdown-item-mode" :class="{ 'active': mode === '7' }"
                                            @click="toggleMode('7')" data-bs-toggle="tooltip" data-bs-trigger="hover"
                                            data-bs-placement="top" data-bs-title="Click to activate Light Mode 3">
                                            <img class="w-full px-1"
                                                src="https://internetl.ink/static_html/icons/icon_webpage_light_3.svg"
                                                alt="">
                                        </span>
                                    </li>
                                    <li>
                                        <span class="dropdown-item dropdown-item-mode" :class="{ 'active': mode === '8' }"
                                            @click="toggleMode('8')" data-bs-toggle="tooltip" data-bs-trigger="hover"
                                            data-bs-placement="top" data-bs-title="Click to activate Light Mode 4">
                                            <img class="w-full px-1"
                                                src="https://internetl.ink/static_html/icons/icon_webpage_light_4.svg"
                                                alt="">
                                        </span>
                                    </li>
                                </ul>
                            </div>
                            <!-- different favicon -->
                            <div class="btn-group dropstart">
                                <a class="btn btn-icon p-0 text-decoration-none text-reset" data-bs-toggle="dropdown"
                                    aria-expanded="false">
                                    <img :src="mainFavicon" class="main-img-favicon w-[4vw]" alt="Favicon Type" />
                                </a>
                                <ul class="dropdown-menu dropdown-mode dropdown-menu-dark text-center">
                                    <li>
                                        <a @click="toggleFavicon('1')" class="dropdown-item dropdown-item-favicon"
                                            :class="{ 'active': faviconNo === '1' }" data-bs-toggle="tooltip"
                                            data-bs-trigger="hover" data-bs-placement="top" data-mode="1"
                                            data-bs-title="Click to activate Dark Favicon 1">
                                            <img class="w-full p-1" data-mode="1"
                                                src="https://internetl.ink/static_html/icons/ew_favicon_dark_1.svg" alt="">
                                        </a>
                                    </li>
                                    <li>
                                        <a @click="toggleFavicon('2')" class="dropdown-item dropdown-item-favicon"
                                            :class="{ 'active': faviconNo === '2' }" data-bs-toggle="tooltip"
                                            data-bs-trigger="hover" data-bs-placement="top" data-mode="2"
                                            data-bs-title="Click to activate Dark Favicon 2">
                                            <img class="w-full p-1" data-mode="2"
                                                src="https://internetl.ink/static_html/icons/ew_favicon_dark_2.svg" alt="">
                                        </a>
                                    </li>
                                    <li>
                                        <a @click="toggleFavicon('3')" :class="{ 'active': faviconNo === '3' }"
                                            class="dropdown-item dropdown-item-favicon" data-bs-toggle="tooltip"
                                            data-bs-trigger="hover" data-bs-placement="top" data-mode="3"
                                            data-bs-title="Click to activate Dark Favicon 3" id="3">
                                            <img class="w-full p-1" data-mode="3"
                                                src="https://internetl.ink/static_html/icons/ew_favicon_dark_3.svg" alt="">
                                        </a>
                                    </li>
                                    <li>
                                        <a @click="toggleFavicon('4')" class="dropdown-item dropdown-item-favicon"
                                            :class="{ 'active': faviconNo === '4' }" data-bs-toggle="tooltip"
                                            data-bs-trigger="hover" data-bs-placement="top" data-mode="4"
                                            data-bs-title="Click to activate Dark Favicon 4">
                                            <img class="w-full p-1" data-mode="4"
                                                src="https://internetl.ink/static_html/icons/ew_favicon_dark_4.svg" alt="">
                                        </a>
                                    </li>
                                    <li>
                                        <a @click="toggleFavicon('5')" class="dropdown-item dropdown-item-favicon"
                                            :class="{ 'active': faviconNo === '5' }" data-bs-toggle="tooltip"
                                            data-bs-trigger="hover" data-bs-placement="top" data-mode="5"
                                            data-bs-title="Click to activate Light Favicon 1">
                                            <img class="w-full p-1" data-mode="5"
                                                src="https://internetl.ink/static_html/icons/ew_favicon_light_1.svg" alt="">
                                        </a>
                                    </li>
                                    <li>
                                        <a class="dropdown-item dropdown-item-favicon" data-bs-toggle="tooltip"
                                            :class="{ 'active': faviconNo === '6' }" @click="toggleFavicon('6')"
                                            data-bs-trigger="hover" data-bs-placement="top" data-mode="6"
                                            data-bs-title="Click to activate Light Favicon 2">
                                            <img class="w-full p-1" data-mode="6"
                                                src="https://internetl.ink/static_html/icons/ew_favicon_light_2.svg" alt="">
                                        </a>
                                    </li>
                                    <li>
                                        <a class="dropdown-item dropdown-item-favicon" data-bs-toggle="tooltip"
                                            @click="toggleFavicon('7')" data-bs-trigger="hover" data-bs-placement="top"
                                            data-mode="7" :class="{ 'active': faviconNo === '7' }"
                                            data-bs-title="Click to activate Light Favicon 3">
                                            <img class="w-full p-1" data-mode="7"
                                                src="https://internetl.ink/static_html/icons/ew_favicon_light_3.svg" alt="">
                                        </a>
                                    </li>
                                    <li>
                                        <a class="dropdown-item dropdown-item-favicon" data-bs-toggle="tooltip"
                                            @click="toggleFavicon('8')" data-bs-trigger="hover" data-bs-placement="top"
                                            data-mode="8" :class="{ 'active': faviconNo === '8' }"
                                            data-bs-title="Click to activate Light Favicon 4">
                                            <img class="w-full p-1" data-mode="8"
                                                src="https://internetl.ink/static_html/icons/ew_favicon_light_4.svg" alt="">
                                        </a>
                                    </li>
                                </ul>
                            </div>
                            <div class="btn-group dropstart">
                                <a class="btn btn-icon p-0" data-bs-toggle="dropdown" aria-expanded="false">
                                    <img alt="Screen Type" :src="mainScreenType" class="main-img w-[4vw]" />
                                </a>
                                <ul class="dropdown-menu dropdown-menu-dark text-center">
                                    <li>
                                        <a @click="toggleScreenType('auto_detect')" class="dropdown-item dropdown-item-1"
                                            :class="{ 'active': screenType === 'auto_detect' }" data-bs-toggle="tooltip"
                                            data-bs-placement="left" data-bs-custom-class="custom-tooltip"
                                            data-bs-title="Automatic detection of the screen type">
                                            <img class="w-full p-1"
                                                src="https://internetl.ink/static_html/icons/icon_screen_auto_detect_pink.svg"
                                                alt="Auto Detect" data-screen-type="auto_detect" />
                                        </a>
                                    </li>
                                    <li>
                                        <a @click="toggleScreenType('mobile')" class="dropdown-item dropdown-item-1"
                                            :class="{ 'active': screenType === 'mobile' }" data-bs-toggle="tooltip"
                                            data-bs-placement="left" data-bs-custom-class="custom-tooltip"
                                            data-bs-title="Select for mobile version">
                                            <img class="w-full p-1"
                                                src="https://internetl.ink/static_html/icons/icon_mobile_pink.svg"
                                                alt="Mobile" data-screen-type="mobile" />
                                        </a>
                                    </li>
                                    <li>
                                        <a @click="toggleScreenType('tablet')" class="dropdown-item dropdown-item-1"
                                            :class="{ 'active': screenType === 'tablet' }" data-bs-toggle="tooltip"
                                            data-bs-placement="left" data-bs-custom-class="custom-tooltip"
                                            data-bs-title="Select for tablet version">
                                            <img class="w-full p-1" alt="Tablet"
                                                src="https://internetl.ink/static_html/icons/icon_tablet_pink.svg"
                                                data-screen-type="tablet" />
                                        </a>
                                    </li>
                                    <li>
                                        <a @click="toggleScreenType('laptop')" class="dropdown-item dropdown-item-1"
                                            :class="{ 'active': screenType === 'laptop' }" data-bs-toggle="tooltip"
                                            data-bs-placement="left" data-bs-custom-class="custom-tooltip"
                                            data-bs-title="Select for laptop and desktop">
                                            <img class="w-full p-1" alt="Laptop"
                                                src="https://internetl.ink/static_html/icons/icon_laptop_pink.svg"
                                                data-screen-type="laptop" /></a>
                                    </li>
                                    <li>
                                        <a @click="toggleScreenType('monitor')" class="dropdown-item dropdown-item-1"
                                            :class="{ 'active': screenType === 'monitor' }" data-bs-toggle="tooltip"
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
                                <a class="btn btn-icon p-0 text-decoration-none text-reset" data-bs-toggle="dropdown"
                                    aria-expanded="false">
                                    <img alt="Menu Position" :src="mainMenuPosition" class="main-img-2 w-[4vw]" />
                                </a>
                                <ul class="dropdown-menu dropdown-menu-dark text-center">
                                    <li>
                                        <a @click="toggleMenuPosition('right')" class="dropdown-item dropdown-item-2"
                                            :class="{ 'active': menuPosition === 'right' }" data-bs-toggle="tooltip"
                                            data-bs-placement="left" data-bs-custom-class="custom-tooltip"
                                            data-bs-title="Menu Position Right">
                                            <img class="w-full p-1"
                                                src="https://internetl.ink/static_html/icons/icon_menu_right_pink.svg"
                                                alt="Menu Right" data-menu-type="right" />
                                        </a>
                                    </li>
                                    <li>
                                        <a @click="toggleMenuPosition('top')" class="dropdown-item dropdown-item-2"
                                            :class="{ 'active': menuPosition === 'top' }" data-bs-toggle="tooltip"
                                            data-bs-placement="left" data-bs-custom-class="custom-tooltip"
                                            data-bs-title="Menu Position Top">
                                            <img class="w-full p-1"
                                                src="https://internetl.ink/static_html/icons/icon_menu_top_pink.svg"
                                                alt="Menu Top" data-menu-type="top" />
                                        </a>
                                    </li>
                                    <li>
                                        <a @click="toggleMenuPosition('left')" class="dropdown-item dropdown-item-2"
                                            :class="{ 'active': menuPosition === 'left' }" data-bs-toggle="tooltip"
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
                                <a class="btn btn-icon p-0 text-decoration-none text-reset" data-bs-toggle="dropdown"
                                    aria-expanded="false">
                                    <img src="https://internetl.ink/static_html/icons/icon_aa_pink.svg"
                                        class="main-img-family w-[4vw]" alt="Font Family" />
                                </a>
                                <ul class="dropdown-menu dropdown-menu-dark text-center">
                                    <li>
                                        <a class="dropdown-item dropdown-item-family"
                                            :class="{ 'active': fontFamily === 'lato_regular' }"
                                            @click="toggleFont('lato_regular')" data-bs-toggle="tooltip"
                                            data-bs-trigger="hover" data-bs-placement="left" data-mode="lato_regular"
                                            data-bs-title="Click to activate Lato Regular">
                                            <span class="w-full text-center" data-mode="lato_regular">Lato Regular</span>
                                        </a>
                                    </li>
                                    <li>
                                        <a class="dropdown-item dropdown-item-family"
                                            :class="{ 'active': fontFamily === 'roboto' }" @click="toggleFont('roboto')"
                                            data-bs-toggle="tooltip" data-bs-trigger="hover" data-bs-placement="left"
                                            data-mode="roboto" data-bs-title="Click to activate Roboto">
                                            <span class="w-full text-center" data-mode="roboto">Roboto</span>
                                        </a>
                                    </li>
                                    <li>
                                        <a class="dropdown-item dropdown-item-family" data-bs-toggle="tooltip"
                                            :class="{ 'active': fontFamily === 'open_sans' }"
                                            @click="toggleFont('open_sans')" data-bs-trigger="hover"
                                            data-bs-placement="left" data-mode="open_sans"
                                            data-bs-title="Click to activate Open Sans" id="3">
                                            <span class="w-full text-center" data-mode="open_sans">Open Sans</span>
                                        </a>
                                    </li>
                                    <li>
                                        <a class="dropdown-item dropdown-item-family"
                                            :class="{ 'active': fontFamily === 'montserrat' }"
                                            @click="toggleFont('montserrat')" data-bs-toggle="tooltip"
                                            data-bs-trigger="hover" data-bs-placement="left" data-mode="montserrat"
                                            data-bs-title="Click to activate Montserrat">
                                            <span class="w-full text-center" data-mode="montserrat">Montserrat</span>
                                        </a>
                                    </li>
                                </ul>
                            </div>
                            <!-- forfont -->
                            <div class="btn-group dropstart">
                                <a class="btn btn-icon p-0 text-decoration-none text-reset" data-bs-toggle="dropdown"
                                    aria-expanded="false">
                                    <span class="main-img-2 main-font-size" style=" line-height: 1;">{{ fontSize }}</span>
                                </a>
                                <ul class="dropdown-menu dropdown-font dropdown-menu-dark text-center">
                                    <li>
                                        <a class="dropdown-item dropdown-item-fonts" id="minus_1"
                                            @click="toggleFontSize('-1')" data-font-correction="-1" data-bs-toggle="tooltip"
                                            data-bs-trigger="hover" data-bs-placement="top"
                                            data-bs-title="Decrease the text size by 1">
                                            <img class="w-full p-1"
                                                src="https://internetl.ink/static_html/icons/icon_minus_one_pink.svg"
                                                alt="" />
                                        </a>
                                    </li>
                                    <li>
                                        <a class="dropdown-item dropdown-item-fonts-current dropdown-item-fonts active"
                                            id="current_size" data-bs-toggle="tooltip" data-bs-trigger="hover"
                                            data-bs-placement="top" data-bs-title="Current Size">
                                            <span class="main-font-size li" style=" padding: 0px 15px;">{{ fontSize
                                            }}</span>
                                        </a>
                                    </li>
                                    <li>
                                        <a class="dropdown-item dropdown-item-fonts" id="plus_1"
                                            @click="toggleFontSize('+1')" data-font-correction="+1" data-bs-toggle="tooltip"
                                            data-bs-trigger="hover" data-bs-placement="top"
                                            data-bs-title="Increase the text size by 1">
                                            <img class="w-full p-1"
                                                src="https://internetl.ink/static_html/icons/icon_plus_one_pink.svg"
                                                alt="" />
                                        </a>
                                    </li>

                                </ul>
                            </div>
                            <!-- split_screen-->
                            <a @click="toggleScreen()" data-bs-toggle="tooltip" data-bs-placement="left"
                                data-bs-title="Click to toggle split srceen" data-bs-trigger="hover"
                                class="text-decoration-none text-reset cursor-pointer">
                                <img class="w-[4vw] p-0" :src="mainSplitScreen" alt="split_screen" />
                            </a>
                        </div>
                    </div>
                </aside>
            </main>
        </div>
        <div id="right-panel" class="hidden flex-grow" :class="{ '!block': isRightPanel }">
            <main class="flex gap-[2.5vw] min-h-screen overflow-x-hidden"
                :class="rightmenuPosition === 'left' ? 'flex-row' : (rightmenuPosition === 'right') ? 'flex-row-reverse' : '!gap-0'">
                <aside class="w-fit menu    flex flex-col relative" :class="rightmenuPosition === 'top' ? 'hidden' : ''">
                    <img @click="righttoggleMenu()" class="w-[1.3vw] max-w-[2vw] absolute top-5 cursor-pointer"
                        :class="rightmenuPosition === 'right' ? 'right-[102%] rotate-180' : 'left-[102%]'"
                        :src="rightmenuArrow" alt="iconVMenu">
                    <div class="h-full p-2 w-[12rem] overflow-hidden bg-transparent flex flex-col transition-all duration-300"
                        :class="{ 'hide-menu': rightisMenuHidden }">
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
                        <p class="text-center mt-3">Mailsniplet V{{ '0.0.5' }}</p>
                    </div>
                </aside>
                <section class="flex-grow flex flex-col gap-[0.75vw] items-center">
                    <aside class="w-full menu   flex-row relative "
                        :class="rightmenuPosition === 'top' ? 'flex' : 'hidden'">
                        <img @click="toggleMenu()"
                            class="w-[1.3vw] max-w-[2vw] absolute left-5 cursor-pointer top-[102%] rotate-90"
                            :src="rightmenuArrow" alt="iconVMenu">
                        <div class="h-full p-2 w-full overflow-hidden bg-transparent flex flex-row gap-[0.75vw] items-center justify-between transition-all duration-300"
                            :class="{ 'hide-menu-top': rightisMenuHidden }">
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
                            <UButton block @click="signOut({ callbackUrl: '/auth/login' })" class=" w-fit h-fit"
                                color="gray" variant="solid">
                                Logout
                            </UButton>
                            <p class="text-center">Mailsniplet V{{ '0.0.5' }}</p>
                        </div>
                    </aside>
                    <slot />
                </section>
                <aside class="min-w-[4vw] lg:w-[4vw] w-[6vw]  quick-pick-bar p-[0.25vw]">
                    <div class="flex items-center flex-col gap-[0.75vw]">
                        <a href="https://internetl.ink/static_html/web_user_settings.html"
                            class="text-decoration-none text-reset w-[4vw]" data-bs-trigger="hover" data-bs-placement="left"
                            data-bs-toggle="tooltip" data-bs-title="Click to navigate to Setting page">
                            <img alt="settings" src="https://internetl.ink/static_html/icons/icon_settings_pink.svg"
                                class="w-[4vw] p-[0.75vw]" />
                        </a>
                        <a @click="righttoggleQuickPickBar()" class="text-decoration-none text-reset w-[4vw] cursor-pointer"
                            data-bs-trigger="hover" data-bs-toggle="tooltip" data-bs-placement="left"
                            data-bs-title="Click to toggle quick-pick bar">
                            <img alt="down-arrow" :src="rightquickPickBarArrow" class="w-[4vw] p-[0.75vw]" />
                        </a>
                        <div class="flex items-center w-full flex-col gap-[0.75vw] transition-all duration-300"
                            :class="{ 'hide-quickpickbar': rightisQuickPickBar }">
                            <!-- different mode -->
                            <div class="btn-group dropstart">
                                <button type="button" class="btn btn-icon p-0 text-decoration-none text-reset"
                                    id="modeToggleMenu" data-bs-toggle="dropdown" aria-expanded="false">
                                    <img src="https://internetl.ink/static_html/icons/icon_colour_flower.svg"
                                        class="main-img-mode w-[4vw]" alt="Theme Mode" />
                                </button>
                                <ul class="dropdown-menu dropdown-mode dropdown-menu-dark text-center"
                                    aria-labelledby="modeToggleMenu">
                                    <li>
                                        <span class="dropdown-item dropdown-item-mode"
                                            :class="{ 'active': rightmode === '1' }" @click="togglerightMode('1')"
                                            data-bs-toggle="tooltip" data-bs-trigger="hover" data-bs-placement="top"
                                            data-bs-title="Click to activate Dark Mode 1">
                                            <img class="w-full px-1"
                                                src="https://internetl.ink/static_html/icons/icon_webpage_dark_1.svg"
                                                alt="">
                                        </span>
                                    </li>
                                    <li>
                                        <span class="dropdown-item dropdown-item-mode"
                                            :class="{ 'active': rightmode === '2' }" @click="togglerightMode('2')"
                                            data-bs-toggle="tooltip" data-bs-trigger="hover" data-bs-placement="top"
                                            data-bs-title="Click to activate Dark Mode 2">
                                            <img class="w-full px-1"
                                                src="https://internetl.ink/static_html/icons/icon_webpage_dark_2.svg"
                                                alt="">
                                        </span>
                                    </li>
                                    <li>
                                        <span class="dropdown-item dropdown-item-mode"
                                            :class="{ 'active': rightmode === '3' }" @click="togglerightMode('3')"
                                            data-bs-toggle="tooltip" data-bs-trigger="hover" data-bs-placement="top"
                                            data-bs-title="Click to activate Dark Mode 3" id="3">
                                            <img class="w-full px-1"
                                                src="https://internetl.ink/static_html/icons/icon_webpage_dark_3.svg"
                                                alt="">
                                        </span>
                                    </li>
                                    <li>
                                        <span class="dropdown-item dropdown-item-mode"
                                            :class="{ 'active': rightmode === '4' }" @click="togglerightMode('4')"
                                            data-bs-toggle="tooltip" data-bs-trigger="hover" data-bs-placement="top"
                                            data-bs-title="Click to activate Dark Mode 4">
                                            <img class="w-full px-1"
                                                src="https://internetl.ink/static_html/icons/icon_webpage_dark_4.svg"
                                                alt="">
                                        </span>
                                    </li>
                                    <li>
                                        <span class="dropdown-item dropdown-item-mode"
                                            :class="{ 'active': rightmode === '5' }" @click="togglerightMode('5')"
                                            data-bs-toggle="tooltip" data-bs-trigger="hover" data-bs-placement="top"
                                            data-bs-title="Click to activate Light Mode 1">
                                            <img class="w-full px-1"
                                                src="https://internetl.ink/static_html/icons/icon_webpage_light_1.svg"
                                                alt="">
                                        </span>
                                    </li>
                                    <li>
                                        <span class="dropdown-item dropdown-item-mode"
                                            :class="{ 'active': rightmode === '6' }" @click="togglerightMode('6')"
                                            data-bs-toggle="tooltip" data-bs-trigger="hover" data-bs-placement="top"
                                            data-bs-title="Click to activate Light Mode 2">
                                            <img class="w-full px-1"
                                                src="https://internetl.ink/static_html/icons/icon_webpage_light_2.svg"
                                                alt="">
                                        </span>
                                    </li>
                                    <li>
                                        <span class="dropdown-item dropdown-item-mode"
                                            :class="{ 'active': rightmode === '7' }" @click="togglerightMode('7')"
                                            data-bs-toggle="tooltip" data-bs-trigger="hover" data-bs-placement="top"
                                            data-bs-title="Click to activate Light Mode 3">
                                            <img class="w-full px-1"
                                                src="https://internetl.ink/static_html/icons/icon_webpage_light_3.svg"
                                                alt="">
                                        </span>
                                    </li>
                                    <li>
                                        <span class="dropdown-item dropdown-item-mode"
                                            :class="{ 'active': rightmode === '8' }" @click="togglerightMode('8')"
                                            data-bs-toggle="tooltip" data-bs-trigger="hover" data-bs-placement="top"
                                            data-bs-title="Click to activate Light Mode 4">
                                            <img class="w-full px-1"
                                                src="https://internetl.ink/static_html/icons/icon_webpage_light_4.svg"
                                                alt="">
                                        </span>
                                    </li>
                                </ul>
                            </div>
                            <!-- Screen Type -->
                            <div class="btn-group dropstart">
                                <a class="btn btn-icon p-0" data-bs-toggle="dropdown" aria-expanded="false">
                                    <img alt="Screen Type" :src="rightmainScreenType" class="main-img w-[4vw]" />
                                </a>
                                <ul class="dropdown-menu dropdown-menu-dark text-center">
                                    <li>
                                        <a @click="righttoggleScreenType('auto_detect')"
                                            class="dropdown-item dropdown-item-1"
                                            :class="{ 'active': rightscreenType === 'auto_detect' }"
                                            data-bs-toggle="tooltip" data-bs-placement="left"
                                            data-bs-custom-class="custom-tooltip"
                                            data-bs-title="Automatic detection of the screen type">
                                            <img class="w-full p-1"
                                                src="https://internetl.ink/static_html/icons/icon_screen_auto_detect_pink.svg"
                                                alt="Auto Detect" data-screen-type="auto_detect" />
                                        </a>
                                    </li>
                                    <li>
                                        <a @click="righttoggleScreenType('mobile')" class="dropdown-item dropdown-item-1"
                                            :class="{ 'active': rightscreenType === 'mobile' }" data-bs-toggle="tooltip"
                                            data-bs-placement="left" data-bs-custom-class="custom-tooltip"
                                            data-bs-title="Select for mobile version">
                                            <img class="w-full p-1"
                                                src="https://internetl.ink/static_html/icons/icon_mobile_pink.svg"
                                                alt="Mobile" data-screen-type="mobile" />
                                        </a>
                                    </li>
                                    <li>
                                        <a @click="righttoggleScreenType('tablet')" class="dropdown-item dropdown-item-1"
                                            :class="{ 'active': rightscreenType === 'tablet' }" data-bs-toggle="tooltip"
                                            data-bs-placement="left" data-bs-custom-class="custom-tooltip"
                                            data-bs-title="Select for tablet version">
                                            <img class="w-full p-1" alt="Tablet"
                                                src="https://internetl.ink/static_html/icons/icon_tablet_pink.svg"
                                                data-screen-type="tablet" />
                                        </a>
                                    </li>
                                    <li>
                                        <a @click="righttoggleScreenType('laptop')" class="dropdown-item dropdown-item-1"
                                            :class="{ 'active': rightscreenType === 'laptop' }" data-bs-toggle="tooltip"
                                            data-bs-placement="left" data-bs-custom-class="custom-tooltip"
                                            data-bs-title="Select for laptop and desktop">
                                            <img class="w-full p-1" alt="Laptop"
                                                src="https://internetl.ink/static_html/icons/icon_laptop_pink.svg"
                                                data-screen-type="laptop" /></a>
                                    </li>
                                    <li>
                                        <a @click="righttoggleScreenType('monitor')" class="dropdown-item dropdown-item-1"
                                            :class="{ 'active': rightscreenType === 'monitor' }" data-bs-toggle="tooltip"
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
                                <a class="btn btn-icon p-0 text-decoration-none text-reset" data-bs-toggle="dropdown"
                                    aria-expanded="false">
                                    <img alt="Menu Position" :src="rightmainMenuPosition" class="main-img-2 w-[4vw]" />
                                </a>
                                <ul class="dropdown-menu dropdown-menu-dark text-center">
                                    <li>
                                        <a @click="righttoggleMenuPosition('right')" class="dropdown-item dropdown-item-2"
                                            :class="{ 'active': rightmenuPosition === 'right' }" data-bs-toggle="tooltip"
                                            data-bs-placement="left" data-bs-custom-class="custom-tooltip"
                                            data-bs-title="Menu Position Right">
                                            <img class="w-full p-1"
                                                src="https://internetl.ink/static_html/icons/icon_menu_right_pink.svg"
                                                alt="Menu Right" data-menu-type="right" />
                                        </a>
                                    </li>
                                    <li>
                                        <a @click="righttoggleMenuPosition('top')" class="dropdown-item dropdown-item-2"
                                            :class="{ 'active': rightmenuPosition === 'top' }" data-bs-toggle="tooltip"
                                            data-bs-placement="left" data-bs-custom-class="custom-tooltip"
                                            data-bs-title="Menu Position Top">
                                            <img class="w-full p-1"
                                                src="https://internetl.ink/static_html/icons/icon_menu_top_pink.svg"
                                                alt="Menu Top" data-menu-type="top" />
                                        </a>
                                    </li>
                                    <li>
                                        <a @click="righttoggleMenuPosition('left')" class="dropdown-item dropdown-item-2"
                                            :class="{ 'active': rightmenuPosition === 'left' }" data-bs-toggle="tooltip"
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
                                <a class="btn btn-icon p-0 text-decoration-none text-reset" data-bs-toggle="dropdown"
                                    aria-expanded="false">
                                    <img src="https://internetl.ink/static_html/icons/icon_aa_pink.svg"
                                        class="main-img-family w-[4vw]" alt="Font Family" />
                                </a>
                                <ul class="dropdown-menu dropdown-menu-dark text-center">
                                    <li>
                                        <a class="dropdown-item dropdown-item-family"
                                            :class="{ 'active': rightfontFamily === 'lato_regular' }"
                                            @click="righttoggleFont('lato_regular')" data-bs-toggle="tooltip"
                                            data-bs-trigger="hover" data-bs-placement="left" data-mode="lato_regular"
                                            data-bs-title="Click to activate Lato Regular">
                                            <span class="w-full text-center" data-mode="lato_regular">Lato Regular</span>
                                        </a>
                                    </li>
                                    <li>
                                        <a class="dropdown-item dropdown-item-family"
                                            :class="{ 'active': rightfontFamily === 'roboto' }"
                                            @click="righttoggleFont('roboto')" data-bs-toggle="tooltip"
                                            data-bs-trigger="hover" data-bs-placement="left" data-mode="roboto"
                                            data-bs-title="Click to activate Roboto">
                                            <span class="w-full text-center" data-mode="roboto">Roboto</span>
                                        </a>
                                    </li>
                                    <li>
                                        <a class="dropdown-item dropdown-item-family" data-bs-toggle="tooltip"
                                            :class="{ 'active': rightfontFamily === 'open_sans' }"
                                            @click="righttoggleFont('open_sans')" data-bs-trigger="hover"
                                            data-bs-placement="left" data-mode="open_sans"
                                            data-bs-title="Click to activate Open Sans" id="3">
                                            <span class="w-full text-center" data-mode="open_sans">Open Sans</span>
                                        </a>
                                    </li>
                                    <li>
                                        <a class="dropdown-item dropdown-item-family"
                                            :class="{ 'active': rightfontFamily === 'montserrat' }"
                                            @click="righttoggleFont('montserrat')" data-bs-toggle="tooltip"
                                            data-bs-trigger="hover" data-bs-placement="left" data-mode="montserrat"
                                            data-bs-title="Click to activate Montserrat">
                                            <span class="w-full text-center" data-mode="montserrat">Montserrat</span>
                                        </a>
                                    </li>
                                </ul>
                            </div>
                            <!-- forfont -->
                            <div class="btn-group dropstart">
                                <a class="btn btn-icon p-0 text-decoration-none text-reset" data-bs-toggle="dropdown"
                                    aria-expanded="false">
                                    <span class="main-img-2 main-font-size" style=" line-height: 1;">{{ rightfontSize
                                    }}</span>
                                </a>
                                <ul class="dropdown-menu dropdown-font dropdown-menu-dark text-center">
                                    <li>
                                        <a class="dropdown-item dropdown-item-fonts" id="minus_1"
                                            @click="righttoggleFontSize('-1')" data-font-correction="-1"
                                            data-bs-toggle="tooltip" data-bs-trigger="hover" data-bs-placement="top"
                                            data-bs-title="Decrease the text size by 1">
                                            <img class="w-full p-1"
                                                src="https://internetl.ink/static_html/icons/icon_minus_one_pink.svg"
                                                alt="" />
                                        </a>
                                    </li>
                                    <li>
                                        <a class="dropdown-item dropdown-item-fonts-current dropdown-item-fonts active"
                                            id="current_size" data-bs-toggle="tooltip" data-bs-trigger="hover"
                                            data-bs-placement="top" data-bs-title="Current Size">
                                            <span class="main-font-size li" style=" padding: 0px 15px;">{{ rightfontSize
                                            }}</span>
                                        </a>
                                    </li>
                                    <li>
                                        <a class="dropdown-item dropdown-item-fonts" id="plus_1"
                                            @click="righttoggleFontSize('+1')" data-font-correction="+1"
                                            data-bs-toggle="tooltip" data-bs-trigger="hover" data-bs-placement="top"
                                            data-bs-title="Increase the text size by 1">
                                            <img class="w-full p-1"
                                                src="https://internetl.ink/static_html/icons/icon_plus_one_pink.svg"
                                                alt="" />
                                        </a>
                                    </li>

                                </ul>
                            </div>
                            <!-- split_screen-->
                            <a @click="toggleScreen()" data-bs-toggle="tooltip" data-bs-placement="left"
                                data-bs-title="Click to toggle split srceen" data-bs-trigger="hover"
                                class="text-decoration-none text-reset cursor-pointer">
                                <img class="w-[4vw] p-0" :src="mainSplitScreen" alt="split_screen" />
                            </a>
                        </div>
                    </div>
                </aside>
            </main>
        </div>
    </section>
    <div class="fixed top-1/2 left-1/2 transform -translate-x-1/2 -translate-y-1/2" :class="{ 'hidden': !isLoading }"
        id="loadingContainer">
        <div class="border-t-4 border-blue-500 border-solid h-12 w-12 rounded-full animate-spin"></div>
    </div>
</template>
<style>
@import url('https://fonts.googleapis.com/css2?family=Lato:ital,wght@0,100;0,300;0,400;0,700;0,900;1,100;1,300;1,400;1,700;1,900&family=Montserrat:ital,wght@0,100;0,200;0,300;0,400;0,500;0,600;0,700;0,800;0,900;1,100;1,200;1,300;1,400;1,500;1,600;1,700;1,800;1,900&family=Open+Sans:ital,wght@0,300;0,400;0,500;0,600;0,700;0,800;1,300;1,400;1,500;1,600;1,700;1,800&family=Roboto:ital,wght@0,100;0,300;0,400;0,500;0,700;0,900;1,100;1,300;1,400;1,500;1,700;1,900&display=swap');

:root {
    --lato: 'Lato', sans-serif;
    --montserrat: 'Montserrat', sans-serif;
    --open_sans: 'Open Sans', sans-serif;
    --roboto: 'Roboto', sans-serif;
}

/* Color modes Here*/
body {
    font-family: var(--lato);

}

#left-panel {
    background-color: var(--body-bg-color, #2D3E50);
    color: var(--body-text-color, #C8D6E5);
}

#right-panel {
    background-color: var(--body-bg-color, #2D3E50);
    color: var(--body-text-color, #C8D6E5);
}

#left-panel .quick-pick-bar {
    background-color: var(--bg-quick-pick-bar, #1F2A36);
}

#right-panel .quick-pick-bar {
    background-color: var(--bg-quick-pick-bar, #1F2A36);
}

#left-panel .dropdown-menu-dark {
    background-color: var(--bg-dropdown-menu, #35445A);
}

#right-panel .dropdown-menu-dark {
    background-color: var(--bg-dropdown-menu, #35445A);
}

#left-panel .menu {
    background-color: var(--bg-menu, #2F445A);
}

#right-panel .menu {
    background-color: var(--bg-menu, #2F445A);
}

/*Color modes ends here*/

.panel-container {
    display: flex;
    width: 100%;
    height: 100%;
    align-items: center;
    justify-content: flex-start;
}

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
    max-width: 10vw;
    width: 6vw !important;
}

.dropdown-item-family {
    width: 100% !important;
    cursor: pointer;
}

.dropdown-item-family span {
    font-size: 1.5vw !important;
}

.dropdown-item.active {
    border-radius: 20px;
    background-color: transparent;
}

#left-panel .dropdown-item.active {
    border: 4px solid var(--border-dropdown-active-item, #8096A8);
}

#right-panel .dropdown-item.active {
    border: 4px solid var(--border-dropdown-active-item, #8096A8);
}

.dropdown-item:hover {
    border-radius: 20px;
    background-color: transparent;
}

#left-panel .dropdown-item:hover {
    border: 4px solid var(--border-dropdown-hover-item, #6F839D);
}

#right-panel .dropdown-item:hover {
    border: 4px solid var(--border-dropdown-hover-item, #6F839D);
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
    font-size: 2.5vw !important;
}

.main-font-size.li {
    font-size: 4vw !important;
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

.hide-quickpickbar {
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