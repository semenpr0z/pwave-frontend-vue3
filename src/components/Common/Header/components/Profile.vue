<script>
import { useUserStore } from '@/stores/userStore.js';

export default {
    data() {
        return {
            opened: false
        }
    },
    methods: {
        openModal() {
            this.opened = !this.opened
        }
    },
    setup() {
        const userStore = useUserStore()

        return {
            userStore
        }
    },
}
</script>

<template>
    <div class="profile" @click="openModal">
        <svg class="profile__img" width="40" height="40" viewBox="0 0 40 40" fill="none" xmlns="http://www.w3.org/2000/svg">
            <g clip-path="url(#clip0_2_4)">
                <path
                    d="M20 39.2C30.6039 39.2 39.2 30.6039 39.2 20C39.2 9.39612 30.6039 0.799988 20 0.799988C9.39612 0.799988 0.799988 9.39612 0.799988 20C0.799988 30.6039 9.39612 39.2 20 39.2Z"
                    stroke="white" stroke-width="2" stroke-miterlimit="10" stroke-linecap="round" />
                <path
                    d="M23.9464 28.4224C23.8296 27.1328 23.8744 26.2328 23.8744 25.0544C24.4584 24.748 25.5048 22.7944 25.6816 21.144C26.1408 21.1064 26.8648 20.6584 27.0768 18.8896C27.1912 17.94 26.7368 17.4056 26.46 17.2376C27.2072 14.9904 28.7592 8.03841 23.5896 7.32001C23.0576 6.38561 21.6952 5.91281 19.9248 5.91281C12.8416 6.04321 11.9872 11.2616 13.54 17.2376C13.264 17.4056 12.8096 17.94 12.9232 18.8896C13.136 20.6584 13.8592 21.1064 14.3184 21.144C14.4944 22.7936 15.5824 24.748 16.168 25.0544C16.168 26.2328 16.212 27.1328 16.0952 28.4224C15.0864 31.1344 9.90561 31.3464 6.91681 33.9616C10.0416 37.108 15.1056 39.3584 20.4496 39.3584C25.7936 39.3584 32.0752 35.1392 33.1208 33.988C30.1504 31.3488 24.9576 31.144 23.9464 28.4224Z"
                    fill="black" />
            </g>
            <defs>
                <clipPath id="clip0_2_4">
                    <rect width="40" height="40" fill="white" />
                </clipPath>
            </defs>
        </svg>
        <svg :class="['profile__arrow', { 'profile__arrow_opened': opened }]" width="12" height="8" viewBox="0 0 12 8"
            fill="none" xmlns="http://www.w3.org/2000/svg">
            <path d="M1.415 0.209991L6 4.79499L10.585 0.209991L12 1.62499L6 7.62499L0 1.62499L1.415 0.209991Z"
                fill="white" />
        </svg>
        <div :class="['profile__modal', { 'profile__modal_opened': opened }]">
            <router-link to="/profile" class="span-2 text">Profile</router-link>
            <router-link to="/settings" class="span-2 text">Settings</router-link>
            <span class="span-2" @click="userStore.clearUser()">Log out</span>
        </div>
    </div>
</template>

<style lang='scss' scoped>
.profile {
    cursor: pointer;
    display: flex;
    align-items: center;
    gap: 6px;
    position: relative;

    &__img {
        width: 32px;
        fill: var(--White);
    }

    &:hover .profile__arrow {
        transform: rotate(0deg) scaleX(-1);
    }

    &__arrow {
        transition: transform 0.3s ease;


        &_opened {
            transform: rotate(180deg) scaleX(-1);
        }
    }

    &:hover .profile__arrow_opened {
        transform: rotate(180deg) scaleX(-1);
    }


    &__modal {
        overflow: hidden;
        width: 0;
        height: 0;
        position: absolute;
        bottom: 0;
        right: 50%;
        background-color: var(--White);
        transition: all 0.3s ease;
        border-radius: 5px;
        display: flex;
        flex-direction: column;
        justify-content: space-between;
        box-sizing: border-box;
        z-index: 10;

        &_opened {
            padding: 8px 7px;
            bottom: -95px;
            right: 0;
            width: 134px;
            height: 90px;
        }
        .text{
            text-decoration: none;
            color: var(--bs-dark);
        }
    }
}
</style>