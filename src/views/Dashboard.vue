<template>
    <div class="overflow-hidden">
        <!-- <h2 class="mb-4">Welcome back, Jolly!</h2>
        <div class="row">
            <div class="col-sm-6 mb-5">
                <ChartBigSessions/>
            </div>
            <div class="col-sm-6 mb-5">
                <ChartBigPageViews/>
            </div>
        </div>
        <div class="row">
            <div class="col-12">
                <Card body-classes="p-0" class="mb-5">
                    <template v-slot:header>
                        <div class="d-flex align-items-center justify-content-between">
                            <span>Customers Database</span>
                            <Input v-model="dataTableSearch" size="sm" placeholder="Filter table data" class="mb-0 w-25"/>
                        </div>
                    </template>
                    <div>
                        <DataTable  show-filter-buttons :data="dataTable" :headers="dataTableHeaders"
                                    :search-keyword="dataTableSearch" :per-page="dataTablePerPage" :current-page="dataTablePage">
                            <template v-slot:default="{row, rowKey}">
                                <Cell
                                        v-for="(cellData, key) in row"
                                        :key="key"
                                        :cell-classes="[
                                    // Center
                                    ['selected', 'status'].indexOf(key.toString().toLowerCase()) !== -1?'d-flex justify-content-center':'',
                                ]"
                                        :class="[
                                    {'bg-info-light':dataTable[rowKey].Selected===true},
                                ]">
                                    <Badge v-if="key.toString().toLowerCase() === 'status' || key === 4" pill :type="getPillByStatus(cellData)">
                                        {{cellData}}
                                    </Badge>
                                    <Checkbox v-else-if="key.toString().toLowerCase() === 'selected'"
                                              v-model="dataTable[rowKey].Selected"></Checkbox>
                                    <span v-else>{{cellData}}</span>
                                </Cell>
                            </template>
                        </DataTable>
                    </div>
                    <div class="d-flex flex-wrap pt-3 pb-4 align-items-end mx-4 justify-content-end">

                        <div class="me-sm-4 mb-sm-0 mb-3">
                            <p class="mb-2 small">Rows per page</p>
                            <Select  :data="[5, 10, 15, 25, 100]" :selected="dataTablePerPage"
                                     @change="dataTablePerPage = $event,dataTablePage = 1"></Select>
                        </div>
                        <div>
                            <Pagination v-model="dataTablePage" :pages="Math.ceil(dataTable.length/dataTablePerPage)">
                                <template v-slot:next>
                                    Next
                                </template>
                                <template v-slot:previous>
                                    Prev
                                </template>
                            </Pagination>
                        </div>
                    </div>
                </Card>
            </div>
        </div>
        <div class="row">
            <div class="col-sm-7 mb-5">
                <TaskList/>
            </div>
            <div class="col-sm-5">
                <Messages/>
            </div>
        </div> -->
        <section class="mb-5">
            <!-- <b-carousel
                id="carousel-1"
                :interval="4000"
                controls
                indicators
                background="#ababab"
                style="text-shadow: 1px 1px 2px #333;"
            >
                <b-carousel-slide
                    img-src="https://imgur.com/O8ELpMe.jpg"
                    img-height="1024"
                ></b-carousel-slide>
                <b-carousel-slide
                    img-src="https://imgur.com/hlQOWiT.jpg"
                    img-height="1024"
                ></b-carousel-slide>
            </b-carousel> -->
            <VueSlickCarousel v-bind="bannerOpt">
                <b-img
                    src="https://imgur.com/O8ELpMe.jpg"
                    height="450"
                    class="fit-cover"
                ></b-img>
                <b-img
                    src="https://imgur.com/hlQOWiT.jpg"
                    height="450"
                    class="fit-cover"
                ></b-img>
            </VueSlickCarousel>
        </section>
        <section class="container">
            <h3 class="font-weight-bold">Kategori</h3>
            <!-- <ul class="d-flex mb-3">
                <b-link :to="{ name: '' }" v-for="(item, idx) in kategori" :key="item.name" class="col-3">
                    <li>
                        <div v-if="idx < 4" class="mx-3">
                            <div class="shadow-sm rounded-lg p-3 d-flex justify-content-center align-items-center border-0">
                                <b-img-lazy :src="item.img" :alt="item.name" width="80" height="80" class="fit" />
                                <p class="mb-0 p-3 font-weight-bold"> {{ item.name }}</p>
                            </div>
                        </div>
                    </li>
                </b-link>
            </ul>
            <ul class="d-flex mb-3 flex-wrap">
                <b-link :to="{ name: '' }" v-for="(item, idx) in kategori" :key="item.name" class="col-3">
                    <li>
                        <div v-if="idx >= 4" class="mx-3">
                            <div class="shadow-sm rounded-lg p-3 d-flex justify-content-center align-items-center border-0">
                                <b-img-lazy :src="item.img" :alt="item.name" width="80" height="80" class="fit" />
                                <p class="mb-0 p-3 font-weight-bold"> {{ item.name }}</p>
                            </div>
                        </div>
                    </li>
                </b-link>
            </ul> -->
            <VueSlickCarousel v-bind="kategoriOpt" class="barang">
                <!-- <ul class="mb-3"> -->
                    <li draggable="false" v-for="item in kategori" :key="item.name" class="p-2">
                        <b-link :to="{ name: '' }" draggable="false">
                            <div class="mx-3">
                                <div class="shadow-sm rounded-lg p-3 d-flex justify-content-center align-items-center border-0">
                                    <b-img-lazy :src="item.img" :alt="item.name" width="100" height="80" class="fit" draggable="false" />
                                    <p class="mb-0 p-3"> {{ item.name }}</p>
                                </div>
                            </div>
                        </b-link>
                    </li>
                    <template #prevArrow="arrowOption">
                        <div class="custom-arrow d-md-block d-none">
                            <p class="mb-0 font-weight-bold" :class="arrowOption.currentSlide === 0 ?'d-none': 'text-dark'"><</p>
                        </div>
                    </template>
                    <template #nextArrow="arrowOption">
                        <div class="custom-arrow d-md-block d-none">
                            <p class="mb-0 font-weight-bold" :class="arrowOption.currentSlide === 4 ?'d-none': 'text-dark'">></p>
                        </div>
                    </template>
                <!-- </ul> -->
            </VueSlickCarousel>
        </section>
        <section class="my-5 container">
            <h3 class="font-weight-bold">Untuk Kamu</h3>
            <VueSlickCarousel v-bind="forYouOpt" class="barang">
                <b-link
                    v-for="item in forYou"
                    :key="item.title"
                    class="p-2"
                    draggable="false"
                >
                    <b-card>
                        <!-- <b-img-lazy :src="item.img" :alt="item.title" height="100px" class="fit w-100 mb-3" /> -->
                        <b-card-img
                            :src="item.img"
                            :alt="item.title"
                            :height="180"
                            draggable="false"
                            class="fit w-100 mb-3"
                        ></b-card-img>
                        <div>
                            <b-icon-star-fill variant="danger"></b-icon-star-fill>
                            <span class="font-sm mx-2">{{ item.rating.toFixed(2) }}</span>
                            <span class="font-sm text-secondary">({{ item.totalUlasan }})</span>
                        </div>
                        <b-card-title>{{ item.title }}</b-card-title>
                        <b-card-text class="font-weight-bold harga">
                            {{formatCurrency(item.harga)}} 
                        </b-card-text>
                    </b-card>
                </b-link>
                <template #prevArrow="arrowOption">
                    <div class="custom-arrow d-md-block d-none">
                        <p class="mb-0 font-weight-bold" :class="arrowOption.currentSlide === 0 ?'d-none': 'text-dark'"><</p>
                    </div>
                </template>
                <template #nextArrow="arrowOption">
                    <div class="custom-arrow d-md-block d-none">
                        <p class="mb-0 font-weight-bold" :class="arrowOption.currentSlide === 4 ?'d-none': 'text-dark'">></p>
                    </div>
                </template>
            </VueSlickCarousel>
        </section>
        <section class="container d-lg-block d-none">
            <b-card
                overlay
                img-src="https://a0.muscache.com/im/pictures/eff28e1d-51c4-49ff-8266-68d6929ea1ec.jpg?im_w=1680"
                class="rounded-lg"
            >
                <b-jumbotron class="display-5 text-white font-weight-bold m-4" style="max-width:20rem;">
                    Selalu ada yang murah untuk kamu
                </b-jumbotron>
                <b-button class="m-4 p-3" variant="light" style="font-weight:500;">
                    Lihat Selengkapnya
                </b-button>
            </b-card>
        </section>
        <section class="my-5 container">
            <h3 class="font-weight-bold">Elektronik</h3>
            <VueSlickCarousel v-bind="forYouOpt" class="barang">
                <b-link
                    v-for="item in forYou"
                    :key="item.title"
                    class="p-2"
                    draggable="false"
                >
                    <b-card>
                        <!-- <b-img-lazy :src="item.img" :alt="item.title" height="100px" class="fit w-100 mb-3" /> -->
                        <b-card-img
                            :src="item.img"
                            :alt="item.title"
                            :height="180"
                            draggable="false"
                            class="fit w-100 mb-3"
                        ></b-card-img>
                        <div>
                            <b-icon-star-fill variant="danger"></b-icon-star-fill>
                            <span class="font-sm mx-2">{{ item.rating.toFixed(2) }}</span>
                            <span class="font-sm text-secondary">({{ item.totalUlasan }} ulasan)</span>
                        </div>
                        <b-card-title>{{ item.title }}</b-card-title>
                        <b-card-text class="font-weight-bold harga">
                            {{formatCurrency(item.harga)}} 
                        </b-card-text>
                    </b-card>
                </b-link>
                <template #prevArrow="arrowOption">
                    <div class="custom-arrow d-md-block d-none">
                        <p class="mb-0 font-weight-bold" :class="arrowOption.currentSlide === 0 ?'d-none': 'text-dark'"><</p>
                    </div>
                </template>
                <template #nextArrow="arrowOption">
                    <div class="custom-arrow d-md-block d-none">
                        <p class="mb-0 font-weight-bold" :class="arrowOption.currentSlide === 4 ?'d-none': 'text-dark'">></p>
                    </div>
                </template>
            </VueSlickCarousel>
        </section>
        <footer class="mt-5 border-top py-4 pb-5 bg-grey">
            <ul class="d-flex w-100 justify-content-between flex-wrap container font-sm mt-3">
                <li class="m-3">
                    <h4>Tentang</h4>
                    <ul class="footer-link">
                        <li>
                            <b-link>Investor</b-link>
                        </li>
                        <li>
                            <b-link>Mitra</b-link>
                        </li>
                        <li>
                            <b-link>Sejarah</b-link>
                        </li>
                        <li>
                            <b-link>Karir</b-link>
                        </li>
                    </ul>
                </li>
                <li class="m-3">
                    <h4>Dukungan</h4>
                    <ul class="footer-link">
                        <li>
                            <b-link>Pusat Bantuan</b-link>
                        </li>
                        <li>
                            <b-link>Opsi Pembatalan Pesanan</b-link>
                        </li>
                        <li>
                            <b-link>Dukungan Ekspedisi</b-link>
                        </li>
                        <li>
                            <b-link>Kebijakan dan Privasi</b-link>
                        </li>
                    </ul>
                </li>
                <li class="m-3">
                    <h4>Beli</h4>
                    <ul class="footer-link">
                        <li>
                            <b-link>Cara Kerja</b-link>
                        </li>
                        <li>
                            <b-link>Top up</b-link>
                        </li>
                        <li>
                            <b-link>COD</b-link>
                        </li>
                    </ul>
                </li>
                <li class="m-3">
                    <h4>Jual</h4>
                    <ul class="footer-link">
                        <li>
                            <b-link>Cara Kerja</b-link>
                        </li>
                        <li>
                            <b-link>Pusat Ekspedisi Seller</b-link>
                        </li>
                        <li>
                            <b-link>Penarikan Dana</b-link>
                        </li>
                        <li>
                            <b-link>Daftar Store</b-link>
                        </li>
                    </ul>
                </li>
            </ul>
            <div class="text-center">
                Copyright © 2021, PT. Beli Barang Bekas
            </div>
        </footer>
    </div>
</template>

<script>
    import TaskList from "../widgets/TaskList";
    // import tableData from '@/data/tables.js'
    import ChartBigSessions from "../widgets/ChartBigSessions";
    import ChartBigPageViews from "../widgets/ChartBigPageViews";
    import Messages from "../widgets/Messages";
    import VueSlickCarousel from 'vue-slick-carousel'
    export default {
        name: "Dashboard",

        components: {Messages, ChartBigPageViews, ChartBigSessions, TaskList, VueSlickCarousel},

        data(){
            return {
                // dataTableHeaders: [
                //     null,
                //     'Name',
                //     'Surname',
                //     'Phone',
                //     'Website',
                //     'Status',
                //     'Revenue',
                // ],
                // dataTable: tableData,
                // dataTableSearch: '',carouselOpt
                // dataTablePage: 1,
                // dataTablePerPage: 10,
                bannerOpt: {
                    "dots": true,
                    "dotsClass": "slick-dots custom-dot-class",
                    "edgeFriction": 0.35,
                    "infinite": true,
                    "speed": 500,
                    "slidesToShow": 1,
                    "slidesToScroll": 1,
                    "autoplay": true,
                },
                forYouOpt: {
                    "infinite": false,
                    "slidesToShow": 4,
                    "slidesToScroll": 4,
                    "speed": 500,
                    "rows": 1,
                    "slidesPerRow": 1,
                    "edgeFriction": 0.1,
                    "responsive": [
                        {
                        "breakpoint": 1024,
                        "settings": {
                                "slidesToShow": 3,
                                "slidesToScroll": 3,
                                "infinite": false,
                                "dots": false
                            }
                        },
                        {
                        "breakpoint": 600,
                        "settings": {
                                "slidesToShow": 2,
                                "slidesToScroll": 2,
                                "initialSlide": 2,
                                "rows": 2
                            }
                        },
                        {
                        "breakpoint": 480,
                        "settings": {
                                "slidesToShow": 1,
                                "slidesToScroll": 1,
                                "rows": 2
                            }
                        }
                    ]
                },
                kategoriOpt: {
                    "infinite": false,
                    "slidesToShow": 4,
                    "speed": 500,
                    "rows": 2,
                    "slidesPerRow": 1,
                    "edgeFriction": 0.1,
                    "swipe": false,
                    "responsive": [
                        {
                        "breakpoint": 1024,
                        "settings": {
                                "slidesToShow": 3,
                                "slidesToScroll": 3,
                                "infinite": false,
                                "dots": true,
                                "swipe": true
                            }
                        },
                        {
                        "breakpoint": 600,
                        "settings": {
                                "slidesToShow": 2,
                                "slidesToScroll": 2,
                                "initialSlide": 2,
                                "swipe": true
                            }
                        },
                        {
                            "breakpoint": 480,
                            "settings": {
                                "slidesToShow": 2,
                                "slidesToScroll": 1,
                                "swipe": true
                            }
                        }
                    ]
                },
                kategori: [
                    {
                        name: "Elektronik",
                        img: "https://imgur.com/TP1pmvY.png"
                    },
                    {
                        name: "Handphone",
                        img: "https://imgur.com/SXdGOkh.png"
                    },
                    {
                        name: "Sepatu Pria",
                        img: "https://imgur.com/JyTrZBM.png"
                    },
                    {
                        name: "Sepatu Wanita",
                        img: "https://imgur.com/LLD3ntW.png"
                    },
                    {
                        name: "Tas Pria",
                        img: "https://png2.cleanpng.com/sh/291cc3778b74bffb73724e7cc6ead174/L0KzQYm3WcI4N5N5e5H0aYP2gLBuTf1me6Rqhtlucj3lcbj6TfhidpVnedk2bHB4ecS0lwVqfKV0hp9rYXfqcbjsTf1mdqQyetNwcz3ndcTwhB5mel5xhAdycz35hbr7lP9vNZlmhtZrYXf2PcPslvlmf146etNtYUW8Q4TqVfE1Pl89TKY8NkS3QYK8U8gyOGc8T6M7NEe1PsH1h5==/kisspng-messenger-bags-handbag-louis-vuitton-baggage-mens-bags-designer-louis-vuitton-handbags-review-5bada5933c5a46.8443644115381067712472.png"
                    },
                    {
                        name: "Tas Wanita",
                        img: "https://i.imgur.com/C6iqXce.png"
                    },
                    {
                        name: "Figure",
                        img: "https://imgur.com/7RJYBx0.png"
                    },
                    {
                        name: "Musik",
                        img: "https://imgur.com/IpwsEfY.png"
                    },
                ],
                forYou: [
                    {
                        title: "TV Samsung LED 38\" SM-TV2354 paling murah",
                        harga: 3200000,
                        img: "https://imgur.com/TP1pmvY.png",
                        rating: 4.79,
                        totalUlasan: 45
                    },
                    {
                        title: "Iphone XR 256GB",
                        harga: 9500000,
                        img: "https://imgur.com/SXdGOkh.png",
                        rating: 4.85,
                        totalUlasan: 102
                    },
                    {
                        title: "Adidas Woman Sport AD3253 Ukuran 36-41",
                        harga: 1400000,
                        img: "https://imgur.com/JyTrZBM.png",
                        rating: 4.39,
                        totalUlasan: 24
                    },
                    {
                        title: "Nike Cool X Sport NK-3254 Pria Ukuran 39 - 43",
                        harga: 1650000,
                        img: "https://imgur.com/LLD3ntW.png",
                        rating: 4.9,
                        totalUlasan: 21
                    },
                    {
                        title: "Tas Pria keren serbaguna",
                        harga: 180000,
                        img: "https://png2.cleanpng.com/sh/291cc3778b74bffb73724e7cc6ead174/L0KzQYm3WcI4N5N5e5H0aYP2gLBuTf1me6Rqhtlucj3lcbj6TfhidpVnedk2bHB4ecS0lwVqfKV0hp9rYXfqcbjsTf1mdqQyetNwcz3ndcTwhB5mel5xhAdycz35hbr7lP9vNZlmhtZrYXf2PcPslvlmf146etNtYUW8Q4TqVfE1Pl89TKY8NkS3QYK8U8gyOGc8T6M7NEe1PsH1h5==/kisspng-messenger-bags-handbag-louis-vuitton-baggage-mens-bags-designer-louis-vuitton-handbags-review-5bada5933c5a46.8443644115381067712472.png",
                        rating: 4.4,
                        totalUlasan: 143
                    },
                    {
                        title: "Tas Tenteng Wanita kualitas super",
                        harga: 350000,
                        img: "https://i.imgur.com/C6iqXce.png",
                        rating: 4.75,
                        totalUlasan: 94
                    },
                    {
                        title: "Action Figure Wolverine 1:10 Bahan Terbaik",
                        harga: 490000,
                        img: "https://imgur.com/7RJYBx0.png",
                        rating: 4.85,
                        totalUlasan: 32
                    },
                    {
                        title: "Gitar Kapok paling murah",
                        harga: 300000,
                        img: "https://imgur.com/IpwsEfY.png",
                        rating: 4.6,
                        totalUlasan: 31
                    },
                ]
            }
        },

        methods:{
            // Presentational helper
            // getPillByStatus(cellData) {
            //     switch (cellData) {
            //         case 'Lead':
            //             return 'info';
            //         case 'Ongoing':
            //             return 'warning';
            //         case 'Closed':
            //             return 'success';
            //     }
            // }
            formatCurrency(val) {
                const formatter = new Intl.NumberFormat('id-ID', {
                    style: 'currency',
                    currency: 'IDR',

                    // These options are needed to round to whole numbers if that's what you want.
                    //minimumFractionDigits: 0, // (this suffices for whole numbers, but will print 2500.10 as $2,500.1)
                    //maximumFractionDigits: 0, // (causes 2500.99 to be printed as $2,501)
                });
                return formatter.format(val);
            }
        }
    }
</script>
<style scoped>
.harga {
    margin-top: 1.5rem;
    font-family: "Montserrat", sans-serif;
    font-size: 0.875rem;
}
.footer-link {
    margin-top: 1rem;
}
.footer-link li {
    margin-bottom: 1rem;
}
.bg-grey {
    background-color: #eaeaea;
}
</style>

<style>
/* .barang .slick-slide {
    margin: 1rem 1rem;
} */
.custom-arrow {
    display: flex;
    justify-content: center;
    align-items: center;
    z-index: 100;
    width: fit-content !important;
    height: fit-content !important;
}
.custom-arrow p {
    font-size: 28px;
    padding: 1.5rem 1rem !important;
    box-shadow: 3px 3px 8px rgba(0,0,0,0.25);
    border-radius: 50%;
}
.slick-next::before, .slick-prev::before {
    content: '' !important;
}
</style>