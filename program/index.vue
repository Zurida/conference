<template>
    <section class="program">
        <div class="container program__container">
            <ui-heading><h1>{{$t('title')}}</h1></ui-heading>
            <div class="table">
                <div class="table-body">
                    <div class="program__date">{{$t('date12')}}</div>
                    <div class="table-row row-intro">
                        <div class="table-cell table-cell_reverse">
                            <div class="table-cell table-cell_logo">
                                <div class="program__photo">
                                    <img src="./img/uruk.png" alt=""/>
                                </div>
                            </div>
                            <div class="table-cell table-cell_time">
                                <div class="program__start">19:00</div>
                            </div>
                        </div>
                        <div class="table-cell table-cell_name">
                            <div class="program__name">
                                <span class="program__stage">Pre-party 2.0</span>
                                <p class="place">{{$t('prepartyClub')}}</p>
                                <p><a href="https://goo.gl/maps/tBQsRD562WKyLguy9" target="_blank">{{$t('prepartyAddr')}}</a>
                                </p>
                            </div>

                            <div class="program__topic" v-if="prePartyPrice">
                                <Ticket :text="prePartyPrice + ' ₽'" :btnText="$t('btnText')" :pageURL="linkToTickets"/>
                            </div>
                        </div>
                    </div>

                    <div class="program__date">{{$t('mainDate')}}</div>
                    <div class="table-row row-dark noTimeEnd">
                        <div class="table-cell table-cell_reverse">
                            <div class="table-cell table-cell_logo">
                                <div class="program__photo">
                                    <img src="./img/logo.jpg" alt=""/>
                                </div>
                            </div>
                            <div class="table-cell table-cell_time">
                                <div class="program__start">8:45</div>
                            </div>
                        </div>
                        <div class="table-cell table-cell_name">
                            <div class="program__name">
                                <span class="regist">{{$t('register')}}</span>
                                <p class="place">Music Media Dome</p>
                                <p>{{$t('mainAddr')}}</p>
                            </div>

                            <div class="program__topic topic">

                            </div>
                        </div>
                    </div>
                    <div class="table-row row-light">
                        <div class="table-cell">
                            <span>{{$t('smHall')}}</span>
                        </div>
                        <div class="table-cell">
                            <h2>{{$t('workshops.title')}}</h2>
                        </div>
                    </div>

                    <div v-for="master in masters" class="table-row row-master animated fadeIn">
                        <div class="table-cell table-cell_reverse">
                            <div class="table-cell table-cell_logo">
                                <div class="program__photo" v-if="master.photo">
                                    <img
                                            :src="master.photo"
                                            :alt="master.speaker.name"
                                    />
                                </div>
                            </div>
                            <div class="table-cell table-cell_time">
                                <div class="program__start">{{master.time.start}}</div>
                            </div>
                        </div>
                        <div class="table-cell table-cell_name">
                            <div class="program__name" v-if="master.speaker">
                                <div class="program__speak">{{$t(master.speaker.name)}}</div>
                                <ui-btn @click.native="onModalShow(master.type)" disabled>{{$t('signup')}}</ui-btn>
                            </div>

                            <div class="program__topic topic" v-if="master.topic">
                                <span class="topic__title">{{$t('topicTitle')}}</span>
                                <p class="topic__text">{{$t(master.topic.text)}} <span class="topic__text_dark">{{$t('analysis')}}</span>
                                </p>
                            </div>
                        </div>
                    </div>

                    <div class="table-row row-light">
                        <div class="table-cell">
                            <span>{{$t('largeHall')}}</span>
                        </div>
                        <div class="table-cell">
                            <h2>{{$t("speech")}}</h2>
                        </div>
                    </div>

                    <div v-for="program in programs" class="table-row animated fadeIn"
                         :class="{'row-dark': program.rowDark, 'row-hello': program.rowHello, 'noTimeEnd': program.noTimeEnd}">
                        <div class="table-cell table-cell_reverse">
                            <div class="table-cell table-cell_logo">
                                <div class="program__photo" v-if="program.photo">
                                    <img
                                            :src="program.photo"
                                            :alt="$t('program.speaker.name')"
                                    />
                                </div>
                            </div>
                            <div class="table-cell table-cell_time">
                                <div class="program__start" v-if="program.time">{{program.time.start}}</div>
                                <div class="program__end" v-if="program.time">{{program.time.end}}</div>
                            </div>
                        </div>
                        <div class="table-cell table-cell_name">
                            <div class="program__name" v-if="program.speaker">
                                <h3 class="program__speak">{{$t(program.speaker.name)}}</h3>
                                <span v-if="program.speaker.position">{{$t(program.speaker.position)}}</span>
                            </div>

                            <div class="program__topic topic" v-if="program.topic">
                                <span class="topic__title">{{$t('topicTitle')}}</span>
                                <p class="topic__text" v-if="program.topic.text">{{$t(program.topic.text)}}</p>
                            </div>
                        </div>
                    </div>
                    <div class="table-row row-intro row-intro_afterparty">
                        <div class="table-cell table-cell_reverse">
                            <div class="table-cell table-cell_logo">
                                <div class="program__photo">
                                    <img src="./img/soho.jpg" alt=""/>
                                </div>
                            </div>
                            <div class="table-cell table-cell_time">
                                <div class="program__start">20:00</div>
                                <div class="program__end">6:00</div>
                            </div>
                        </div>
                        <div class="table-cell table-cell_name">
                            <div class="program__name">
                                <span class="program__stage">AFTERPARTY 2.0</span>
                                <p class="place">{{$t('afterpartyPlace')}}</p>
                                <p><a href="https://goo.gl/maps/NvVw4JuoxxMJy56s8" target="_blank">{{$t('afterpartyAddr')}}</a>
                                </p>
                            </div>

                            <div class="program__topic">
                                <nuxt-link :to="linkToAfterParty">
                                    <p class="goBtn goBtn_desk">{{$t('goto')}}
                                        <Arrow/>
                                    </p>
                                    <p class="goBtn goBtn_mob">afterparty
                                        <Arrow/>
                                    </p>
                                </nuxt-link>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>

    </section>
</template>

<i18n>
    {
        "en": {
            "title": "Agenda",
            "date12": "November, 12",
            "prepartyClub": "Restaurant Grand Uryuk",
            "prepartyAddr": "Presnenskaya Naberezhnaya, 8, b.1, \"Gorod Stolits\", Moscow",
            "btnText": "Buy a ticket",
            "mainDate": "November, 13",
            "register": "REGISTRATION",
            "mainAddr": "Moscow, Enthusiasts Highway, 5 b. 2",
            "signup": "Sign up",
            "smHall": "Small Hall",
            "topicTitle": "Topic:",
            "workshops": {
                "title": "WORKSHOPS",
                "vkname": "VK",
                "text1": "VK ad campaigns features",
                "text2": "Asian drift - how to work on the most promising market in the world",
                "text3": "Quick start on Facebook: farming, setting up, launching and profit"
            },
            "analysis": "+ analysis of the master-class participants' ad campaigns",
            "largeHall": "Big Hall",
            "speech": "Speeches",
            "welcome": "Welcome speech by the organiser ",
            "speakers": {
                "gusev": {
                    "name": "Roman Gusev",
                    "topic": "7 rules of effective networking: from pre-party to afterparty"
                },
                "lazareva": {
                    "name": "YULIA LAZAREVA",
                    "position": "Head of VK PR-agency communication team",
                    "topic": "VK capabilities for marketing. Main instruments and updates for 2019, development plans for 2020"
                },
                "vinec": {
                    "name": "IGOR VINETSKIY",
                    "position": "Senior manager of the myTarget-agency communication team",
                    "topic": "myTarget. New tools and opportunities in targeted advertising"
                },
                "bark": {
                    "name": "EDUARD BARK",
                    "position": "Co-owner of Aiviz and EXMO",
                    "topic": "How webmasters make millions on crypto offers?"
                },
                "duzhn": {
                    "name": "ALEXANDER DUZHNIKOV",
                    "position": "Co-founder of Marketcall",
                    "topic": "PPC case-studies in the USA market"
                },
                "fridman": {
                    "name": "ALEXANDER FRIDMAN",
                    "position": "CEO NaBurzh",
                    "topic": "Entering the European market. How to launch COD offers in Europe in 1 month"
                },
                "gabit": {
                    "name": "RAFAEL GABITOV A.K.A SENSEY",
                    "position": "CEO Indigobrowser.com, fbtool.pro и diasp.pro",
                    "topic": "Secret speech about Facebook"
                },
                "voistr": {
                    "name": "ANTON VOYSTRIKOV",
                    "position": "Founder of Сlicklead.ru",
                    "topic": "Affiliate marketing through CPA-applications: iGaming, Daiting, Finance"
                },
                "adclever": {
                    "name": "ALEXANDER ADCLEVER",
                    "position": "Owner of the group of companies AdClever and AdProfit",
                    "topic": "Organization and management of affiliate teams as a business process"
                },
                "andy": {
                    "name": "ANDY WULLMER (TRAFFIC CAPTAIN)",
                    "position": "Captain of TrafficPartner.com",
                    "topic": "Monetization in the Adult Industry"
                },
                "oscar": {
                    "name": "OSCAR RUIZ",
                    "position": "Business Development Manager LovePlanet",
                    "topic": "How to earn money with dating apps"
                },
                "artemprok": {
                    "name": "Artem Prokofiev",
                    "position": "Owner of gambling.pro",
                    "topic": "What brings 100%+ ROI in gambling?"
                },
                "lagut": {
                    "name": "DENIS LAGUTENKO",
                    "position": "Co-founder of 8bitgroup, LeadBit.com, shakes.pro, Adsprofit.com, ProTraffic.com",
                    "topic": "Lecture on financial and legal safety for an affiliate. Making your profit legal"
                },
                "arbocpa": {
                    "name": "OLEG ARBOCPA",
                    "position": "Co-owner of the ArboCPA affiliate team",
                    "topic": "How can affiliates deal with shaving?"
                }
            },
            "coffee": "Coffee break / Lunch",
            "afterpartyPlace": "SOHO Rooms",
            "afterpartyAddr": "Bol'shoy Savvinskiy Pereulok, 12 b. 8, Moscow",
            "goto": "Afterparty page"
        },
        "ru": {
            "title": "Программа конференции CPA LIFE",
            "date12": "12 ноября",
            "prepartyClub": "Ресторан Grand Урюк",
            "prepartyAddr": "Пресненская набережная 8/1 \"Город столиц\"",
            "btnText": "Купить билет",
            "mainDate": "13 ноября",
            "register": "РЕГИСТРАЦИЯ",
            "mainAddr": "Москва, ш. Энтузиастов,5, стр. 2",
            "signup": "Записаться",
            "smHall": "Малый зал",
            "topicTitle": "Тема:",
            "workshops": {
                "title": "Мастер-классы CPA Life",
                "vkname": "ВКонтакте",
                "text1": "Особенности рекламной кампании в ВКонтакте",
                "text2": "Азиатский дрифт — как работать на самом перспективном рынке мира",
                "text3": "Быстрый старт в Facebook: фарм, настройка, запуск и профит"
            },
            "analysis": "+ разбор рекламных кампаний участников мастер-класса",
            "largeHall": "Большой зал",
            "speech": "ДОКЛАДЫ CPA Life",
            "welcome": "ПРИВЕТСТВЕННОЕ СЛОВО ОТ ОРГАНИЗАТОРА",
            "speakers": {
                "gusev": {
                    "name": "РОМАН ГУСЕВ",
                    "topic": "7 законов эффективного нетворкинга: от препати до афтепати"
                },
                "lazareva": {
                    "name": "ЮЛИЯ ЛАЗАРЕВА",
                    "position": "Руководитель группы по работе с рекламными агентствами ВКонтакте",
                    "topic": "Возможности ВКонтакте для рекламы. Основные инструменты и обновления 2019, планы разработки в 2020 году"
                },
                "vinec": {
                    "name": "ИГОРЬ ВИНЕЦКИЙ",
                    "position": "Старший менеджер по работе с агентствами myTarget",
                    "topic": "myTarget. Новые инструменты и возможности в таргетированной рекламе"
                },
                "bark": {
                    "name": "ЭДУАРД БАРК",
                    "position": "Совладелец компании Aivix и EXMO",
                    "topic": "Как арбитражники зарабатывают миллионы на криптоофферах!"
                },
                "duzhn": {
                    "name": "АЛЕКСАНДР ДУЖНИКОВ",
                    "position": "Соучредитель Marketcall",
                    "topic": "Кейсы в формате pay per call на американском рынке"
                },
                "fridman": {
                    "name": "АЛЕКСАНДР ФРИДМАН",
                    "position": "CEO NaBurzh",
                    "topic": "Идём NaБурж. Как запустить свою товарку в Европе за 1 месяц"
                },
                "gabit": {
                    "name": "РАФАЭЛЬ ГАБИТОВ A.K.A SENSEY",
                    "position": "CEO Indigobrowser.com, fbtool.pro и diasp.pro",
                    "topic": "Секретный доклад по Facebook"
                },
                "voistr": {
                    "name": "АНТОН ВОЙСТРИКОВ",
                    "position": "Владелец партнерской сети Сlicklead.ru",
                    "topic": "Арбитраж трафика через CPA-приложения: iGaming, Daiting, Finance"
                },
                "adclever": {
                    "name": "АЛЕКСАНДР ADCLEVER",
                    "position": "Овнер группы компаний AdClever и AdProfit",
                    "topic": "Организация и управление арбитражными командами как бизнес-процесс"
                },
                "andy": {
                    "name": "ЭНДИ ВУЛМЕР (TRAFFIC CAPTAIN)",
                    "position": "Капитан TrafficPartner.com",
                    "topic": "Монетизация в Адалт индустрии"
                },
                "oscar": {
                    "name": "ОСКАР РУИЗ",
                    "position": "Business Development Manager LovePlanet",
                    "topic": "Как зарабатывать на приложениях для знакомств"
                },
                "artemprok": {
                    "name": "Артём прокофьев",
                    "position": "Owner gambling.pro",
                    "topic": "Что приносит больше 100% ROI в гемблинге"
                },
                "lagut": {
                    "name": "ДЕНИС ЛАГУТЕНКО",
                    "position": "Сооснователь 8bitgroup , LeadBit.com, shakes.pro, Adsprofit.com, ProTraffic.com",
                    "topic": "Ликбез по финансовой и юридической безопасности для арбитражника. Обеляем свои доходы"
                },
                "arbocpa": {
                    "name": "ОЛЕГ ARBOCPA",
                    "position": "Совладелец арбитражной команды ArboCPA",
                    "topic": "Как арбитражнику бороться с шейвом в партнерках"
                }
            },
            "coffee": "КОФЕ-БРЕЙК / ОБЕД",
            "afterpartyPlace": "Клуб SOHO rooms",
            "afterpartyAddr": "Москва, Большой Саввинский пер, 12с8",
            "goto": "Перейти на страницу afterparty"
        }
    }
</i18n>

<script>
    import {mapState} from 'vuex'
    import Ticket from '@/components/blocks/party/ticket'
    import Arrow from '@/assets/icons/ui/arrow'

    export default {
        name: 'Program',
        components: {
            Ticket,
            Arrow
        },
        data() {
            return {
                accountProgram: true,
                masters: [
                    {
                        categoryId: 0,
                        photo: require('./img/vk.jpg'),
                        time: {start: '09:00'},
                        speaker: {name: 'workshops.vkname'},
                        type: "Заявка на мастер-класс - VK",
                        topic: {
                            title: 'topic.title',
                            text: 'workshops.text1'
                        }
                    },
                    {
                        categoryId: 1,
                        photo: require('./img/master-ads.jpg'),
                        time: {start: '10:00'},
                        speaker: {name: 'AdsKeeper'},
                        type: "Заявка на мастер-класс - AdsKeeper",
                        topic: {
                            title: 'topic.title',
                            text: 'workshops.text2'
                        }
                    },
                    {
                        categoryId: 2,
                        photo: require('./img/m1master.jpg'),
                        time: {start: '11:00'},
                        speaker: {name: 'M1-Shop'},
                        type: "Заявка на мастер-класс - M1-shop",
                        topic: {
                            title: 'topic.title',
                            text: 'workshops.text3'
                        }
                    }
                ],
                programs: [
                    {
                        categoryId: 0,
                        rowDark: true,
                        rowHello: true,
                        noTimeEnd: true,
                        photo: require('./img/cher.jpg'),
                        time: {start: '12:00'},
                        speaker: {
                            name: 'welcome',
                        }
                    },
                    {
                        categoryId: 1,
                        photo: require('./img/gusev.jpg'),
                        time: {start: '12:25'},
                        speaker: {
                            name: 'speakers.gusev.name',
                            position: 'CMO Lucky.Online'
                        },
                        topic: {
                            text: 'speakers.gusev.topic'
                        }
                    },
                    {
                        categoryId: 2,
                        photo: require('./img/lazar.jpg'),
                        time: {start: '12:50'},
                        speaker: {
                            name: 'speakers.lazareva.name',
                            position: 'speakers.lazareva.position'
                        },
                        topic: {
                            text: 'speakers.lazareva.topic'
                        }
                    },
                    {
                        categoryId: 3,
                        photo: require('./img/vin.jpg'),
                        time: {start: '13:15'},
                        speaker: {
                            name: 'speakers.vinec.name',
                            position: 'speakers.vinec.position'
                        },
                        topic: {
                            text: 'speakers.vinec.topic'
                        }
                    },
                    {
                        categoryId: 4,
                        photo: require('./img/bark.jpg'),
                        time: {start: '13:40'},
                        speaker: {
                            name: 'speakers.bark.name',
                            position: 'speakers.bark.position'
                        },
                        topic: {
                            text: 'speakers.bark.topic'
                        }
                    },
                    {
                        categoryId: 5,
                        rowDark: true,
                        rowHello: true,
                        photo: require('./img/logo_dark.jpg'),
                        time: {start: '14:05', end: '15:00'},
                        speaker: {
                            name: 'coffee',
                        }
                    },
                    {
                        categoryId: 6,
                        photo: require('./img/duzh.jpg'),
                        time: {start: '15:00'},
                        speaker: {
                            name: 'speakers.duzhn.name',
                            position: 'speakers.duzhn.position'
                        },
                        topic: {
                            text: 'speakers.duzhn.topic'
                        }
                    },

                    {
                        categoryId: 7,
                        photo: require('./img/frid.jpg'),
                        time: {start: '15:25'},
                        speaker: {
                            name: 'speakers.fridman.name',
                            position: 'speakers.fridman.position'
                        },
                        topic: {
                            text: 'speakers.fridman.topic'
                        }
                    },
                    {
                        categoryId: 8,
                        photo: require('./img/gabit.jpg'),
                        time: {start: '15:50'},
                        speaker: {
                            name: 'speakers.gabit.name',
                            position: 'speakers.gabit.position'
                        },
                        topic: {
                            text: 'speakers.gabit.topic'
                        }
                    },
                    {
                        categoryId: 9,
                        photo: require('./img/voistr.jpg'),
                        time: {start: '16:15'},
                        speaker: {
                            name: 'speakers.voistr.name',
                            position: 'speakers.voistr.position'
                        },
                        topic: {
                            text: 'speakers.voistr.topic'
                        }
                    },
                    {
                        categoryId: 10,
                        photo: require('./img/arbo.jpg'),
                        time: {start: '16:40'},
                        speaker: {
                            name: 'speakers.arbocpa.name',
                            position: 'speakers.arbocpa.position'
                        },
                        topic: {
                            text: 'speakers.arbocpa.topic'
                        }
                    },
                    {
                        categoryId: 11,
                        photo: require('./img/vulmer.jpg'),
                        time: {start: '17:05'},
                        speaker: {
                            name: 'speakers.andy.name',
                            position: 'speakers.andy.position'
                        },
                        topic: {
                            text: 'speakers.andy.topic'
                        }
                    },
                    {
                        categoryId: 12,
                        photo: require('./img/ruiz.jpg'),
                        time: {start: '17:30'},
                        speaker: {
                            name: 'speakers.oscar.name',
                            position: 'speakers.oscar.position'
                        },
                        topic: {
                            text: 'speakers.oscar.topic'
                        }
                    },
                    {
                        categoryId: 13,
                        photo: require('./img/artem-prok.jpg'),
                        time: {start: '17:55'},
                        speaker: {
                            name: 'speakers.artemprok.name',
                            position: 'speakers.artemprok.position'
                        },
                        topic: {
                            text: 'speakers.artemprok.topic'
                        }
                    },
                    {
                        categoryId: 14,
                        photo: require('./img/lagut.jpg'),
                        time: {start: '18:20'},
                        speaker: {
                            name: 'speakers.lagut.name',
                            position: 'speakers.lagut.position'
                        },
                        topic: {
                            text: 'speakers.lagut.topic'
                        }
                    }
                    // {
                    //     categoryId: 16,
                    //     rowDark: true,
                    //     rowHello: true,
                    //     photo: require('./img/logo_dark.jpg'),
                    //     time: {start: '19:10', end: '19:30'},
                    //     speaker: {
                    //         name: 'Розыгрыш призов от партнеров',
                    //     }
                    // },
                ]
            }
        },
        computed: {
            ...mapState({
                priceCategory: state => state.tickets.priceCategory
            }),
            linkToTickets() {
                return this.$i18n.locale === 'en' ? '/en/tickets' : '/tickets'
            },
            linkToAfterParty() {
                return this.$i18n.locale === 'en' ? '/en/afterparty' : '/afterparty'
            },
            prePartyPrice() {
                const {priceCategory} = this;
                if (priceCategory) {
                    let result = Math.round(priceCategory.find(item => item.id === 4).price);
                    return result.toLocaleString();
                }
                return 0
            }
        },
        methods: {
            onModalShow(name) {
                this.$store.dispatch('popup/onShow', {name});
            }
        }
    }
</script>

<style lang="stylus" scoped>
    .program {
        background-image: url(img/bg.png)
        background-repeat no-repeat
        background-position top 150px center
        padding-top 250px

        .page--language-en & {
            background-image url(img/bg_en.png)
            background-repeat no-repeat
            background-position top 150px center
        }

        .heading h1 {
            color: $color-default
            font-family: $font-black;
            font-size: 64px;
            line-height: 55px;
            position: relative;
            z-index: 5;
            +mob(){
                font-size: 28px;
                line-height: 28px;
            }
        }


        .table {
            margin-top 100px

            &-body {
                display: table;
            }

            &-row {
                padding-top: 25px;
                padding-bottom: 25px;
                /* width: 1214px;*/
                max-width: 100%;
                margin-left 58px
                display flex

                &:nth-of-type(even) {
                    background-image: linear-gradient(90deg, #1B3A57 0%, rgba(1, 30, 57, 0) 100%);
                }
            }

            .row-intro {
                padding-top 30px
                background-image none

                .table-cell_time {
                    justify-content center
                    padding-top 0
                }

                .table-cell_name {
                    align-items center
                    padding-top 0
                }

                p {
                    font-family $font-bold
                }

                .place {
                    text-transform uppercase
                }

                &_afterparty {
                    background-image linear-gradient(90deg, #290926 33.85%, rgba(1, 30, 57, 0) 99.99%, rgba(1, 30, 57, 0) 100%);

                    .program__stage {
                        color $color-default
                    }

                    .program__start {
                        color $color-default
                    }

                    .goBtn {
                        font-family $font-black
                        padding 27px 10px
                        color #AD0C4F
                        border 2px solid #AD0C4F
                        text-transform uppercase
                        text-align center
                        transition 0.2s
                        margin-left 20px

                        & >>> .icon-ui-arrow {
                            width 21px
                            transition 0.3s
                            margin-left 10px

                            & polygon {
                                fill #AD0C4F
                            }
                        }

                        &:hover {
                            background-color #AD0C4F
                            color $color-default

                            & >>> .icon-ui-arrow {
                                margin-left 15px

                                & polygon {
                                    fill $color-default
                                }
                            }
                        }
                    }

                    .goBtn_mob {
                        display none
                    }
                }
            }

            .row-dark {
                background-image linear-gradient(90deg, #010F1E 60.42%, rgba(1, 30, 57, 0) 100%)
                margin-bottom 78px

                .table-cell_time {
                    justify-content center
                    padding-top 0
                }

                .table-cell_name {
                    align-items center
                    padding-top 0
                }

                .program__stage, .program__start {
                    color $color-default
                }

                .program__name {
                    width auto
                }

                .program__speak {
                    color $color-default
                    font-family $font-black
                    font-size 25px
                    line-height 30px
                }

                p {
                    font-family $font-bold
                }

                .regist {
                    font-size: 25px;
                    line-height: 30px;
                    font-family $font-black
                    color $color-primary
                }

                .place {
                    text-transform uppercase
                }
            }

            .row-hello {
                margin-bottom 0
            }

            .row-light {
                padding 20px 23px
                background-image: linear-gradient(90deg, #FFFFFF 39.38%, rgba(255, 255, 255, 0) 94.95%);
                font-family $font-black
                margin-left 0
                margin-bottom 21px
                margin-top 21px

                span {
                    color $color-primary
                    font-size 20px
                    line-height 24px
                }

                p {
                    color $color-primary
                    text-transform: uppercase
                    font-size 25px
                    line-height 30px
                    margin-left 155px
                }

                h2 {
                    color $color-primary
                    text-transform: uppercase
                    font-size 25px
                    line-height 30px
                    margin-left 155px
                }
            }


            &-cell {
                display: flex;
                color: #fff;
            }

            &-cell_logo {
                width: 155px;
                max-width 100%

            }

            &-cell_name {
                padding-top 20px
            }

            &-cell_time {
                width: 102px;
                max-width 100%
                flex-direction column
                padding-top 20px
            }


            .row-master {

                .ui-btn {
                    background-color $color-primary
                    color $color-default
                    margin-top 12px
                    font-size 12px
                    line-height 14px
                    padding 15px 20px

                    & >>> .icon-ui-caret {
                        width 20px

                        & path {
                            fill $color-default
                        }
                    }

                    &.disabled {
                        background-color gray
                    }

                    +mob() {
                        padding 10px 15px
                    }
                }

                .program__speak {
                    color $color-primary
                }

                .table-cell_time {
                    width: 102px;
                    max-width 100%
                }

            }
        }

        &__date {
            font-size 64px
            line-height 76px
            font-family $font-bold
            color $color-primary
            position: relative;
            width: 100%
            margin-top 55px
            margin-bottom 29px

            &:after {
                content: '';
                position: absolute;
                right: 0;
                bottom: 0;
                left: 0;
                width 100%
                background: linear-gradient(90deg, #FFFFFF 39.87%, rgba(255, 255, 255, 0) 96.91%);
                height 5px

            }
        }

        &__stage {
            font-family $font-black
            color $color-primary
            font-size 25px
            line-height 30px
            text-transform uppercase
        }

        &__start {
            font-size: 20px;
            font-family: $font-heavy;
            color: #00a8ff;
            margin-left -58px
        }

        &__end {
            font-size: 16px;
            font-family: $font-regular;
            color: #fff;
            line-height: 35px;
            margin-left -58px
        }

        &__photo {
            position relative
            left -58px
        }

        &__name {
            font-size: 16px;
            line-height 24px
            font-family: $font-regular;
            color: #fff;
            width: 320px;
            max-width 100%
            display: inline-block;
            margin-right 60px
            margin-left -20px

        }

        &__topic {
            width: 475px;
            display: inline-block;

            & >>> .ticket {
                &__price {
                    width 100%
                }

                .btn {
                    right -160px
                }
            }
        }

        &__speak {
            font-family: $font-bold;
            color $color-primary
            text-transform uppercase
        }


        .topic {
            &__title {
                font-size: 18px;
                line-height: 22px;
                font-family: $font-bold;
                color $color-primary
            }

            &__text {
                font-size: 18px;
                line-height: 22px;
                font-family: $font-regular;

                &_dark {
                    color #5F7285
                }
            }
        }
    }

    +mob() {
        .program {
            background-image url(./img/bg_mob.png)
            background-repeat no-repeat
            background-position top 80px center
            padding-top 120px

            .page--language-en & {
                background-image url(./img/bg_en_mob.png)
                background-repeat no-repeat
                background-position top 80px center
            }

            &__photo {
                width: 109px;
            }

            &__start {
                font-size: 14px;
            }

            &__end {
                font-size: 12px;

            }

            &__topic {
                margin-top: 15px;
                padding-right 5px
            }

            &__name {
                font-size: 12px;
                line-height 17px
                margin-left 0
                max-width 150px
                padding-right 5px
                margin-right 0
            }

            &__topic {
                margin-left: 0;
                max-width 153px
            }

            .topic__title {
                font-size: 14px;
                line-height: 18px;
            }

            .topic__text {
                font-size: 14px;
            }

            .ticket {
                display none
            }

            &__stage {
                font-size 16px
                line-height 17px
                display block
                margin-bottom 10px
            }

            &__photo {
                left 0
            }

            &__start {
                margin-left 105px
            }

            &__date {
                font-size 20px
                line-height 24px
                margin-top 19px
                margin-bottom 37px

                &:after {
                    bottom -10px

                }
            }

            .table {
                margin-top 20px
                max-width 320px

                &-row {
                    width: auto;
                    margin-left 0px
                    padding 23px 12px
                    max-width 320px
                }

                &-cell {
                    flex-direction column

                    &_reverse {
                        flex-direction column-reverse
                        align-items flex-start
                        justify-content flex-end
                    }
                }

                &-cell_logo {
                    width: 63px;
                    text-align: center;
                }

                &-cell_time {
                    width: 70px;
                    padding-left 0
                    align-items center
                    margin-bottom 10px
                    padding-top 0

                    .program__end {
                        font-family $font-black
                    }
                }

                .table-cell_name {
                    margin-left 70px
                    padding-top 0
                }

                .row-intro {
                    padding-top 0
                    padding-bottom 20px

                    &_afterparty {
                        padding-top 20px
                        padding-bottom 90px
                        position relative

                        .table-cell_time {
                            padding-left 0
                            position: relative;

                            .program__start {
                                position: relative;
                                margin-left 16px

                                &:after {
                                    content "-"
                                    display inline-block
                                    position: relative;
                                    left 4px
                                }
                            }

                            .program__end {
                                position: absolute;
                                right: -39px;
                                top -7px
                                font-size 14px
                            }
                        }

                        .goBtn {
                            position absolute
                            width 210px
                            bottom 20px
                            left 50%
                            transform translateX(-50%)
                            padding 11px 20px
                            margin-left 0
                        }

                        .goBtn_desk {
                            display none
                        }

                        .goBtn_mob {
                            display block
                        }
                    }
                }

                .row-light {
                    padding 10px
                    background-image none
                    background-color #fff
                    align-items center

                    span {
                        font-size 12px
                        line-height 14px
                    }

                    p {
                        font-size 14px
                        line-height 17px
                        margin-left 59px
                    }
                    h2 {
                        font-size 14px
                        line-height 17px
                        margin-left 25px
                    }
                }

                .row-dark {
                    margin-bottom 0

                    .program__speak {
                        font-size 14px
                        line-height 17px
                    }

                    .regist {
                        font-size: 14px;
                        line-height: 17px;
                        margin-bottom 10px
                        display block
                    }

                    .table-cell_time {
                        padding-left 0
                        position: relative;

                        .program__start {
                            position: relative;
                            margin-left 16px

                            &:after {
                                content " -"
                            }
                        }

                        .program__end {
                            position: absolute;
                            right: -39px;
                            top -7px
                            font-size 14px
                        }
                    }
                }

                .noTimeEnd {
                    .table-cell_time {
                        .program__start {
                            margin-left 110px

                            &:after {
                                display none
                            }
                        }
                    }

                }

                .row-master {
                    .table-cell_time {
                        width 70px
                        padding-top 0
                    }

                    .table-cell_name {
                        padding-top 0
                    }
                }
            }
        }
    }

</style>