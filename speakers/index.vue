<template>
    <section class="speaker">
        <div class="container">

            <ui-heading>{{$t('title')}}</ui-heading>

            <div class="speaker__items">
                <Speaker v-for="(speaker, index) in speakers" :item="speaker" :key="index"/>
            </div>

        </div>
    </section>
</template>

<i18n>
    {
        "en": {
            "title": "Speakers"
        },
        "ru": {
            "title": "Спикеры"
        }
    }
</i18n>

<script>
    import speakers from './data'
    import Speaker from './item'

    export default {
        components: {
            Speaker
        },
        /*data() {
            return {
                speakers
            }
        },*/
        computed: {
            speakers() {
                return this.$i18n.locale === 'en' ? speakers.en : speakers.ru
            }
        }
    }
</script>

<style lang="stylus" scoped>
    .speaker {
        background-image url(./img/bg_ru.png)
        background-position top 150px center
        background-repeat no-repeat
        padding-top 250px

        .page--language-en & {
            background-image url(./img/bg_en.png)
            +mob() {
                background none
            }
        }
        +mob() {
            background-image none
            padding-top 125px
        }

        & .heading {
            margin-bottom 200px
            +mob() {
                margin-bottom 45px
            }
        }

        &__items {
            display flex
            flex-wrap wrap
            justify-content space-between
            margin-bottom -20px

            & .speaker-item {
                flex-basis 50%
                +mob() {
                    flex-basis 100%
                }
            }
        }
    }
</style>