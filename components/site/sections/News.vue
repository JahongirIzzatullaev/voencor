<template>
    <div class="news" id="news" ref="news">
        <div class="container">
            <div class="row">
                <div class="col-12">
                    <div class="my-head-text">последние военные новости
                        <div class="slider-buttons">
                            <div @click.prevent="slidePrev" class="back-left">
                                <img src="../../../assets/images/icons/back-left.png" height="31" width="31"/>
                            </div>
                            <div @click.prevent="slideNext" class="back-right">
                                <img src="../../../assets/images/icons/back-right.png" height="31" width="31"/>
                            </div>
                        </div>
                    </div>
                </div>
                <hooper ref="carousel" :settings="hooperSettings" :infiniteScroll="true"
                        style="outline: none !important;">
                    <slide class="slide-box" v-for="item in news" :key="item.id">
                        <div class="card-news">
                            <div class="card-news-header">
                                <img :src='item.imgUrl===null?notFoundImg:item.imgUrl' alt="img" draggable="false">
                            </div>
                            <div class="card-news-body">
                                <p class="news-title"> {{item.title}}</p>
                                <p class="news-text"> {{setLength(item.text)}}</p>
                                <a @click='showModalFunc(item.id)' class="text-blue"
                                   style="cursor: pointer;">Подробнее</a>
                            </div>
                        </div>
                    </slide>
                </hooper>
            </div>
        </div>
        <modal v-if="showModal" @close="closeModal" class="modal-news">
            <span slot="header">{{one_new.title}}</span>
            <div slot="body">
                <p>{{one_new.title}}</p>
                <p class="create-date">{{one_new.create_date}}</p>
                <img :src='one_new.imgUrl===null?notFoundImg:one_new.imgUrl' alt="img"
                     draggable="false" width="100%" style="max-width: 100%;margin-bottom: 10px">
                <p class="news-text"> {{one_new.text}}</p>
            </div>
        </modal>
    </div>
</template>

<script>
    import img from '../../../assets/images/img-news.png'
    import notFoundImg from '../../../assets/images/not-found-img.png'
    import {Hooper, Slide} from 'hooper';
    import 'hooper/dist/hooper.css';
    import Button from "../button/Button";
    import Modal from "./Modal";
    import Timer from "./Timer";

    export default {
        name: "News",
        data() {
            return {
                hooperSettings: {
                    itemsToShow: 4,
                    centerMode: false,
                    mouseDrag: true,
                    autoPlay: true,
                    touchDrag: true,
                    wheelControl: false,
                    itemsToSlide: 1,
                    carouselData: 0,
                    hoverPause: false,
                    breakpoints: {
                        0: {
                            centerMode: false,
                            itemsToShow: 1
                        }, 576: {
                            centerMode: false,
                            itemsToShow: 2
                        },
                        1000: {
                            itemsToShow: 4,
                            pagination: 'fraction'
                        }
                    }
                },
                one_new:{},
                notFoundImg: notFoundImg,
                news: [
                    {
                        id: 1110,
                        create_date: "19.01.2021",
                        imgUrl: null,
                        title: "Минобороны и РВИО будут вместе популяризировать военные музеи ",
                        text: "Заместитель Министра обороны Российской Федерации – начальник будут вместе популяризировать военные музеи будут вместе популяризировать Заместитель Министра обороны Российской Федерации – начальник будут вместе популяризировать военные музеи будут вместе популяризировать Заместитель Министра обороны Российской Федерации – начальник будут " +
                            "вместе популяризировать военные музеи будут вместе популяризировать"
                    },
                    {
                        id: 1109,
                        create_date: "10.02.2021",
                        imgUrl: img,
                        title: "Минобороны и РВИО будут вместе популяризировать военные музеи ",
                        text: "Заместитель Министра обороны Российской Федерации – начальник будут вместе популяризировать военные музеи будут вместе популяризировать Заместитель Министра обороны Российской Федерации – начальник будут вместе популяризировать военные музеи будут вместе популяризировать Заместитель Министра обороны Российской Федерации – начальник будут " +
                            "вместе популяризировать военные музеи будут вместе популяризировать"
                    },
                    {
                        id: 1108,
                        create_date: "13.01.2021",
                        imgUrl: img,
                        title: "Минобороны и РВИО будут вместе популяризировать военные музеи  ",
                        text: "В Абу-Даби открылась 15-ая Международная оборонная выставка «IDEX 2021». Международная выставка вооружений IDEX 2021 считается наиболее крупной и престижной не только в регионе Ближнего Востока и Северной Африки, но и во всём мире. Начиная с 1993 года, она проходит регулярно каждые два года в столице ОАЭ Абу-Даби. И каждый год её участником традиционно становится Россия – концерн «Рособоронэкспорт» как организатор российской экспозиции на выставке. Тематическая направленность выставки – техника и вооружения для сухопутных войск, военно-морских и военно-воздушных сил, а также для войск противовоздушной обороны.\n" +
                            "\n" +
                            "В этом году на российском стенде представлено более 400 видов военной продукции (на предыдущей выставке Россия показала более 200 перспективных разработок). В частности, будут продемонстрированы новинки экспортного каталога: бронетранспортёр и боевая машина пехоты «Бумеранг», ЗРС «Антей-4000», ЗРК «Викинг», ЗРК «Тор-Э2». Впервые пройдёт презентация танка «Армата», а также автомата «КОРД», пистолета Лебедева и новейшей модификации автомата Калашникова. Ещё одна новинка от Рособоронэкспорта – система противодействия беспилотным аппаратам «Купол-ПРО».\n" +
                            "\n" +
                            "Также посетители выставки увидят многоцелевой сверхманевренный истребитель Су-35 и вертолёт Ми-38Т. Представлены и популярные на Ближнем Востоке комплексы ПВО – «Триумф» и «Тор». Среди военно-морских новинок будут показаны модели патрульного корабля и малого ракетного корабля «Каракурт-Э».\n" +
                            "\n" +
                            "Как заявляют в Рособоронэкспорте, российская экспозиция продемонстрирует средства и решения по обеспечению безопасности в условиях развития средств нападения, в том числе ракетные и ударные беспилотники. Представленное российское вооружение предназначено для противостояния в первую очередь террористическим группировкам и обеспечивает безопасность государственных объектов, инфраструктуры, транспорта и энергетики.\n" +
                            "\n" +
                            "Как отмечают в Рособоронэкспорте, опыт локальных войн и военных конфликтов последних двух лет выявил новые вызовы и угрозы. Террористическим группам стали широко доступны беспилотные аппараты, с помощью которых наносятся удары по промышленным и военным объектам. В этой связи возрастает роль противовоздушной обороны именно против беспилотников. Новый российский комплекс противодействия беспилотным летательным аппаратам сочетает средства радиоэлектронной борьбы и комплексы ПВО различных классов. Подобные системы подавления БЛА наиболее эффективно противостоят дронам лёгкого и частично среднего класса. Они способны обеспечить надёжную защиту объекта во время массированного воздушного налёта путём подавления их командно-телеметрических каналов и каналов навигации.\n" +
                            "\n" +
                            "Российское оружие хорошо известно в регионе Ближнего Востока и Северной Африки и пользуется здесь высоким спросом. Поэтому для российского оружейного экспорта этот регион представляет особую важность: по итогам 2020 года именно на страны данного региона пришлось более 50% всех поставок оружия из России. Общий объём российских поставок оружия в зарубежные страны в 2020 году составил 13 млрд долларов."
                    },
                    {
                        id: 1107,
                        create_date: "12.02.2021",
                        imgUrl: img,
                        title: "Минобороны и РВИО будут вместе популяризировать военные музеи ",
                        text: "Заместитель Министра обороны Российской Федерации – начальник будут вместе популяризировать военные музеи будут вместе популяризировать Заместитель Министра обороны Российской Федерации – начальник будут вместе популяризировать военные музеи будут вместе популяризировать Заместитель Министра обороны Российской Федерации – начальник будут " +
                            "вместе популяризировать военные музеи будут вместе популяризировать"
                    },
                ],
                showModal: false,
            }
        },
        components: {
            Hooper,
            Slide,
            Timer, Button, Modal
        },
        methods: {
            setLength(text) {
                if (!!text) {
                    if ((!!text) && text.length > 61) {
                        return text.substring(0, 61) + '...'
                    } else {
                        return text
                    }
                }
            },
            slidePrev() {
                this.$refs.carousel.slidePrev();
            },
            slideNext() {
                this.$refs.carousel.slideNext();
            },
            showModalFunc(id) {
                this.showModal = true;
                this.showFunc(id);
                if (window.innerWidth < 576) {
                    document.body.className = 'hidden';
                }
            },
            showFunc(id) {
                if (id) {
                    this.one_new = this.news.find(x => x.id ==id)
                }
            },
            closeModal() {
                this.showModal = false;
                document.body.className = '';
            }
        }
    }
</script>

<style lang="scss">

</style>