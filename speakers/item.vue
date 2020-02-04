<template>
    <div class="speaker-item">

        <div class="speaker-item__img" :style="{backgroundImage:`url(${item.img})`}"></div>

        <div class="speaker-item__wrap">

            <div class="speaker-item__top">
                <a
                        class="speaker-item__company"
                        :style="{backgroundImage:`url(${item.company.img})`}"
                        :href="item.company.url"
                        target="_blank"
                        rel="nofollow"
                />
                <div class="speaker-item__socials" v-if="item.socials && item.socials.length > 0">
                    <a v-for="social in item.socials" :href="social.url" class="speaker-item__social" target="_blank" rel="nofollow">
                        <component v-bind:is="social.type"/>
                    </a>
                </div>
            </div>

            <div class="speaker-item__body">
                <div class="speaker-item__name" v-html="item.name"/>
                <div class="speaker-item__position" v-html="item.position"/>
                <div class="speaker-item__theme">
                    <strong>{{$t('topic')}}:</strong>
                    {{item.theme}}
                </div>
            </div>

            <div class="speaker-item__bottom">
                <div class="speaker-item__socials">
                    <a v-for="social in item.socials" :href="social.url" class="speaker-item__social" target="_blank" rel="nofollow">
                        <component v-bind:is="social.type"/>
                    </a>
                </div>
            </div>

        </div>

    </div>
</template>

<i18n>
    {
        "en": {
            "topic": "Topic"
        },
        "ru": {
            "topic": "Тема"
        }
    }
</i18n>

<script>
    import vk from '@/assets/icons/ui/vk'
    import fb from '@/assets/icons/ui/fb'
    import insta from '@/assets/icons/ui/insta'
    import tg from '@/assets/icons/ui/teleg'

    export default {
        props: {
            item: Object
        },
        components: {
            vk, fb, insta, tg
        }
    }
</script>

<style lang="stylus" scoped>
    .speaker-item {
        display flex
        justify-items flex-start
        margin-bottom 90px
        $parent = selector()

        +mob() {
            padding-bottom 45px
            margin-bottom @padding-bottom
            flex-direction column
            border-bottom 1px solid #25517E
            &:last-child {
                border-bottom none
            }
        }

        &__img {
            margin-right 35px
            width 230px
            min-width @width
            height 270px
            background-repeat no-repeat
            background-size cover
            background-position left top
            +mob() {
                width 100%
                min-width 100%
                margin-right 0
                margin-bottom 30px
            }
        }

        &__social {
            flex-basis 18px
            display block

            & .icon {
                height 18px

                & >>> svg {
                    & path {
                        fill #fff
                        transition fill .4s ease-in-out
                    }
                }
            }


            & + & {
                margin-left 22px
                +mob() {
                    margin-left 50px
                }
            }

            &:hover, &:focus {
                & .icon {
                    & >>> svg {
                        & path {
                            fill $color-primary
                        }
                    }
                }
            }
        }

        &__body {
            width 250px
            +mob() {
                width 100%
            }
        }

        &__bottom {
            display none
            margin-top 25px
            +mob() {
                display block
            }
        }

        &__top {
            margin-bottom 20px
            display flex
            align-items center
            +mob() {
                & {$parent}__socials {
                    display none
                }
            }
        }

        &__socials {
            margin-left 25px
            display flex
            +mob() {
                margin-left 0
            }
        }

        &__position {
            font-size 15px
            line-height 120%
            opacity 0.5
            margin-bottom 30px
        }

        &__name {
            font-family $font-black
            font-size 26px
            letter-spacing -0.02em
            line-height 110%
            text-transform uppercase
            margin-bottom 5px
        }

        &__company {
            width 92px
            min-width @width
            height 38px
        }

        &__theme {
            font-size 14px
            line-height 150%

            & strong {
                color $color-primary
                text-transform uppercase
                display block
                margin-bottom 5px
            }
        }
    }
</style>