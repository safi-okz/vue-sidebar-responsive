<template>
    <aside :class="`${is_expended && 'is_expended'}`">
        <div class="logo">
            <img src="../assets/vue.svg" alt="Logo SVG" class="logo">
        </div>
        <div class="menu-toggle-wrap">
            <button class="menu-toggle" @click="toggleMenu">
                <span class="material-symbols-outlined">keyboard_double_arrow_right</span>
            </button>
        </div>

        <h3>Menu</h3>
        <div class="menu">
            <router-link to="/" class="button">
                <span class="material-symbols-outlined">home</span>
                <span class="text">Home</span>
            </router-link>
            <router-link to="/about" class="button">
                <span class="material-symbols-outlined">visibility</span>
                <span class="text">About</span>
            </router-link>
            <router-link to="/about" class="button">
                <span class="material-symbols-outlined">group</span>
                <span class="text">Team</span>
            </router-link>
            <router-link to="/about" class="button">
                <span class="material-symbols-outlined">email</span>
                <span class="text">Contact</span>
            </router-link>
        </div>

        <div class="flex"></div>
        <div class="menu">
            <router-link to="/" class="button">
                <span class="material-symbols-outlined">settings</span>
                <span class="text">Setting</span>
            </router-link>
        </div>
    </aside>
</template>

<script setup>
import { ref } from 'vue';

const is_expended = ref(localStorage.getItem('is_expended') === 'true');

const toggleMenu = () => {
    is_expended.value = !is_expended.value;
    localStorage.setItem('is_expended', is_expended.value);
} 
</script>

<style lang="scss" scoped>
aside {
    display: flex;
    flex-direction: column;
    width: calc(2rem + 32px);
    overflow: hidden;
    background-color: var(--dark);
    color: var(--light);
    min-height: 100vh;
    padding: 1rem;
    transition: all .2s ease-out;

    .flex {
        flex: 1 1 0;
    }
    .logo {
        margin-bottom: 1rem;

        img {
            width: 2rem;
        }
    }

    .menu-toggle-wrap {
        display: flex;
        justify-content: flex-end;
        margin-bottom: 1rem;
        position: relative;
        top: 0;
        transition: all .2s ease-out;

        .menu-toggle {
            transition: all .2s ease-out;

            .material-symbols-outlined {
                font-size: 2rem;
                color: var(--light);
                transition: all .2s ease-out;
            }

            &:hover {
                .material-symbols-outlined:hover {
                    font-size: 2rem;
                    color: var(--primary);
                    transform: translateX(.5rem);
                }
            }
        }
    }

    h3, .button .text {
        opacity: 0;
        transition: all 0.3s ;
    } 

    h3 {
        color: var(--grey);
        font-size: .875rem;
        margin-bottom: .5rem;
        text-transform: uppercase;
    }

    .menu {
        margin: 0 -1rem;

        .button {
            display: flex;
            align-items: center;
            text-decoration: none;
            padding: 0.5rem 1rem;
            transition: .2s ease-out;

            .material-symbols-outlined{
                    font-size: 2rem;
                    color: var(--light);
                    margin-right: 1rem;
                    transition: all .2s ease-out;
            }

            .text {
                color: var(--light);
                transition: all .2s ease-out;
            }

            &:hover, &.router-link-exact-active {
                background-color: var(--dark-alt);

                .material-symbols-outlined, .text {
                    color: var(--primary);
                }
            }

            &.router-link-exact-active {
                border-right: 5px solid var(--primary);
            }
        }
    }

    &.is_expended {
        width: var(--sidebar-width);
        
        .menu-toggle-wrap {
            top: -3rem;

            .menu-toggle {
                transform: rotate(-180deg);
            }
        }

        h3, .button, .text {
        opacity: 1;
        transition: all 0.3s ;
    } 

    .button {
        .material-symbols-outlined {
                margin-right: 1rem;
        }
    }

    }


    @media (max-width: 768px) {
        position: fixed;
        z-index: 99;
    }
}
</style>