<template>
  <div id="page-box">
    <v-container id="contents-box" class="pt-0">
      <custom-appbar id="app-bar" :topic="topic" />
      <v-row id="head-banner">
        <v-col cols="12" class="pa-0">
          <div class="border-box">
            <v-carousel class="mb-5" :show-arrows="false" hide-delimiters :height="carouselHeight">
              <!-- <v-carousel-item v-for="(item,i) in items" :key="i" :src="item.src"></v-carousel-item> -->
              <v-carousel-item>
                <v-row class="overflow-hidden" :height="isCarouselOpen ? 0 : carouselHeight">
                  <v-col cols="12" sm="8" class="px-5 serif">
                    <div class="d-inline-block float-left" style="width: 6em; height: 100%;"></div>
                    <div>
                      <h1 class="align-self-end font-weight-medium">See Chromized livestream</h1>
                      <p>see livestream that are chromized livestream</p>
                      <p>
                        <v-btn
                          class="ma-0"
                          outlined
                          color="white"
                          @click="expandCarousel()"
                        >Turn on livestream</v-btn>
                      </p>
                    </div>
                  </v-col>
                  <v-col cols="12" sm="4"></v-col>
                </v-row>
                <v-row
                  class="overflow-hidden text-center"
                  :height="isCarouselOpen ? 0 : carouselHeight"
                >
                  <v-col cols="1"></v-col>
                  <v-col cols="5">
                    <video ref="video" id="video" height="280px" autoplay></video>
                    <h3 class="text-center serif font-weight-light">Original</h3>
                  </v-col>
                  <v-col cols="5">
                    <v-card outlined flat class="mx-auto" width="373px" height="280px"></v-card>
                    <h3 class="text-center serif font-weight-light">Filtered</h3>
                  </v-col>
                  <v-col cols="2"></v-col>
                </v-row>
                <v-row>
                  <v-col cols="4">
                    <div>
                      <button id="snap" v-on:click="capture()">Snap Photo</button>
                    </div>
                    <canvas ref="videoCanvas" id="videoCanvas" width="640" height="480"></canvas>
                    <ul>
                      <li :key="c" v-for="c in videoCaptures">
                        <img v-bind:src="c" height="50" />
                      </li>
                    </ul>
                  </v-col>
                </v-row>
              </v-carousel-item>
            </v-carousel>
          </div>
        </v-col>
      </v-row>
      <custom-subheader title="Inspirations" indent />
      <v-row class="bubble-box">
        <v-col id="category-box" cols="12" sm="4">
          <v-select :items="sortType" label="Bubbles sorted by" solo flat hide-details></v-select>
          <div class="timeline-box">
            <v-timeline dense>
              <v-timeline-item
                :key="key"
                :color="key % 2 == 0 ? 'pink' : 'teal lighten-3'"
                class="py-5"
                v-for="(category, key) in categories"
                small
              >
                <strong>{{ category }}</strong>
                <p>Lorem ipsum dolor sit amet.</p>
              </v-timeline-item>
            </v-timeline>
          </div>
        </v-col>
        <v-col id="bubble-contents-box" cols="12" sm="8">
          <v-sheet class="overflow-y-auto text-center">
            <div class="bubble-effector" :ref="'bubble-effector'"></div>
            <v-card
              class="inspiration-card pa-0"
              :class="['ma-' + content.level]"
              :key="content.id"
              :style="{
                'max-width': content.level * 2 + 4 + 'em',
                'max-height': content.level * 2 + 4 + 'em'
              }"
              color="#aaaaaa33"
              dark
              ripple
              v-for="content in contents"
              @click="content.minimized = !content.minimized"
            >
              <v-card-text
                class="keyword headline font-weight-bold px-0 py-5 my-5"
                :class="{ minimized: content.minimized }"
                :style="{
                  'line-height': content.level * 1.3 + 'em'
                }"
              >
                {{
                content.description.split(" ")[
                Math.floor(Math.random() * 20, 20)
                ]
                }}
              </v-card-text>

              <v-card-text class="headline font-weight-bold pa-0">{{ content.description }}</v-card-text>

              <v-card-actions>
                <v-list-item class="grow">
                  <!-- <v-list-item-avatar color="grey darken-3">
              <v-img
                class="elevation-6"
                src="https://avataaars.io/?avatarStyle=Transparent&topType=ShortHairShortCurly&accessoriesType=Prescription02&hairColor=Black&facialHairType=Blank&clotheType=Hoodie&clotheColor=White&eyeType=Default&eyebrowType=DefaultNatural&mouthType=Default&skinColor=Light"
              ></v-img>
                  </v-list-item-avatar>-->

                  <v-list-item-content>
                    <v-list-item-title>2019-11-28</v-list-item-title>
                  </v-list-item-content>

                  <v-row align="center" justify="end">
                    <v-btn text color="primary">More</v-btn>
                  </v-row>
                </v-list-item>
              </v-card-actions>
            </v-card>
          </v-sheet>
        </v-col>
      </v-row>
      <custom-subheader title="Recent Issues" indent reversed />
      <v-row class="issue-box pb-0">
        <v-col class="pa-0">
          <v-item-group class="pa-5">
            <v-card :key="key" v-for="key in [1, 2, 3]" class="mb-4">
              <v-row class="px-5">
                <v-col cols="12" sm="4">
                  <img width="100%" src="https://picsum.photos/200/300?grayscale" />
                  <!-- <video
                      width="100%"
                      src="../assets/result.mp4"
                      controls
                      autoplay
                      loop
                  ></video>-->
                </v-col>
                <v-col cols="12" sm="8">
                  <v-subheader>
                    <h5 class="mr-3">github</h5>
                    <h3>Lorem ipsum dolor sit amet.</h3>
                  </v-subheader>

                  <v-divider></v-divider>
                  <v-card-text>
                    Lorem ipsum dolor, sit amet consectetur adipisicing elit.
                    Enim reiciendis recusandae eaque, facere nesciunt quibusdam
                    suscipit ipsam nisi sequi explicabo ducimus itaque, illo
                    harum cumque repellat inventore aperiam unde incidunt!
                  </v-card-text>
                  <v-divider></v-divider>

                  <v-row>
                    <v-col cols="12">
                      <v-btn text color="primary" @click="routeTo('/project/inspired-by')">More</v-btn>
                    </v-col>
                  </v-row>
                </v-col>
              </v-row>
            </v-card>
            <v-card
              :id="'post-' + key"
              :ref="'post-' + key"
              :key="key"
              v-for="key in [4, 5, 6, 7, 8, 9]"
              class="mb-4"
            >
              <v-row class="px-5">
                <v-col cols="12" sm="4">
                  <img width="100%" src="https://picsum.photos/200/300?grayscale" />
                </v-col>
                <v-col cols="12" sm="8">
                  <v-subheader>
                    <h5 class="mr-3">post</h5>
                    <h3>Difference between backtracking and DFS</h3>
                  </v-subheader>

                  <v-divider></v-divider>
                  <v-card-text>
                    Lorem ipsum dolor, sit amet consectetur adipisicing elit.
                    Enim reiciendis recusandae eaque, facere nesciunt quibusdam
                    suscipit ipsam nisi sequi explicabo ducimus itaque, illo
                    harum cumque repellat inventore aperiam unde incidunt!
                  </v-card-text>
                  <v-divider></v-divider>

                  <v-row>
                    <v-col cols="12">
                      <v-btn text color="primary" @click="routeTo('./inspired-by')">More</v-btn>
                      <v-btn text v-scroll-to="'#post-' + key" @click="openPost(key)">See detail</v-btn>
                    </v-col>
                  </v-row>
                </v-col>
              </v-row>
            </v-card>
            <v-card flat color="transparent" class="py-3 text-center">
              <v-btn
                text
                color="grey"
                :disabled="contentLoading"
                :loading="contentLoading"
                @click="loadMoreContents"
              >
                <v-icon left>mdi-refresh</v-icon>
                <h3>load more...</h3>
              </v-btn>
            </v-card>
          </v-item-group>
        </v-col>
      </v-row>
      <v-row class="copyright-box align-center mb-3">
        <v-card flat class="ma-1 pa-0 mt-0">
          <v-card-text class="px-3 py-1">2020 ⓒ KJHRicky</v-card-text>
        </v-card>
      </v-row>
    </v-container>
    <v-container v-if="!show">
      <v-lazy :options="{ threshold: 0.5 }" min-width="100" transition="loader">
        <v-row>
          <v-skeleton-loader
            :loading="nextPageLoading"
            transition="page-move"
            type="article"
            width="100%"
          >
            <v-card>
              <v-card-title>Title</v-card-title>
              <v-card-text>Card Text</v-card-text>
              <v-card-text>Card Text</v-card-text>
              <v-card-text>Card Text</v-card-text>
            </v-card>
          </v-skeleton-loader>
        </v-row>
      </v-lazy>
    </v-container>
    <transition name="post-fade" mode="out-in">
      <div v-if="isPostOpening" id="post-card">
        <router-view name="postcard"></router-view>
      </div>
    </transition>
    <div id="scrim" v-if="isPostOpening" @click="openPost()" />
  </div>
</template>

<script>
import gql from "graphql-tag";
import { RecentRepo, RecentRepo2, Topics } from "../queries/repo";
import * as easings from "vuetify/es5/services/goto/easing-patterns";
import vuePlayer from "@algoz098/vue-player";
import debounce from "lodash/debounce";

export default {
  name: "Topic",
  components: {
    vuePlayer
  },
  apollo: {
    clients: {
      query () {
        return Topics;
      },
      update: data => data
    }
  },
  data: () => ({
    nextPageLoading: true,
    isCarouselOpen: false,
    carouselHeight: 150,
    sortType: ["Recent", "Keywords", "Views"],
    categories: [
      "2019-04-21",
      "2019-05-02",
      "2019-07-02",
      "2019-07-07",
      "2019-08-02",
      "2019-09-17"
    ],
    contentLoading: false,
    isPostOpening: false,
    selectedPostRef: null,
    scrollAtPost: 0,
    debouncedScroller: null,
    isScrollEventRunning: false,
    isVideoPlaying: false,
    video: {},
    videoCanvas: {},
    videoCaptures: [],
    contents: [
      {
        id: "1",
        title: "테스트",
        description:
          "'Turns out semicolon- less style is easier and safer in TS because most gotcha edge cases are type invalid as well.'",
        minimized: true,
        level: 2
      },
      {
        id: "2",
        title: "테스트",
        description:
          "'Turns out semicolon- less style is easier and safer in TS because most gotcha edge cases are type invalid as well.'",
        minimized: true,
        level: 5
      },
      {
        id: "3",
        title: "테스트",
        description:
          "'Turns out semicolon - less style is easier and safer in TS because most gotcha edge cases are type invalid as well.'",
        minimized: true,
        level: 4
      },
      {
        id: "4",
        title: "테스트",
        description:
          "'Turns out semicolon- less style is easier and safer in TS because most gotcha edge cases are type invalid as well.'",
        minimized: true,
        level: 1
      },
      {
        id: "5",
        title: "테스트",
        description:
          "'Turns out semicolon- less style is easier and safer in TS because most gotcha edge cases are type invalid as well.'",
        minimized: true,
        level: 3
      },
      {
        id: "6",
        title: "테스트",
        description:
          "'Turns out semicolon- less style is easier and safer in TS because most gotcha edge cases are type invalid as well.'",
        minimized: true,
        level: 4
      },
      {
        id: "7",
        title: "테스트",
        description:
          "'Turns out semicolon- less style is easier and safer in TS because most gotcha edge cases are type invalid as well.'",
        minimized: true,
        level: 2
      },
      {
        id: "8",
        title: "테스트",
        description:
          "'Turns out semicolon- less style is easier and safer in TS because most gotcha edge cases are type invalid as well.'",
        minimized: true,
        level: 5
      },
      {
        id: "9",
        title: "테스트",
        description:
          "'Turns out semicolon- less style is easier and safer in TS because most gotcha edge cases are type invalid as well.'",
        minimized: true,
        level: 2
      }
    ]
  }),
  computed: {
    topic () {
      return this.$store.getters.getTopic;
    },
    show () {
      return this.$store.getters.getShow;
    },
    sampleText () {
      console.log("client", this.clients);
      // if (this.client.viewer.properties[0].name != '') {
      //   return this.client.viewer.properties[0].name
      // }
      if (this.clients) return this.clients;
      return "";
    },
    isLoggedIn () {
      return this.$store.getters.getLoginStatus;
    },
  },
  mounted () {
    console.log(this.sample);
    this.video = this.$refs.video;

    // if (navigator.mediaDevices && navigator.mediaDevices.getUserMedia) {
    //   navigator.mediaDevices.getUserMedia({ video: true }).then(stream => {
    //     console.log(stream);
    //     // this.video.src = window.URL.createObjectURL(stream);
    //     this.video.src = HTMLMediaElement.srcObject = stream;
    //     this.video.play();
    //   });
    // }

    // function hasGetUserMedia () {
    //   return !!(navigator.mediaDevices && navigator.mediaDevices.getUserMedia);
    // }

    // if (hasGetUserMedia()) {
    //   // Good to go!
    // } else {
    //   alert("getUserMedia() is not supported by your browser");
    // }
    setTimeout(() => {
      // console.log(this.$refs["bubble-effector"]);
      this.$refs["bubble-effector"].classList.toggle("decreasing");
    }, 1000);
  },
  destroyed () {
    if (this.debouncedScroller) {
      window.removeEventListener("scroll", this.debouncedScroller);
    }
  },
  methods: {
    expandTopic () {
      this.expand = !this.expand;
    },
    expandCarousel () {
      this.isCarouselOpen = !this.isCarouselOpen;
      if (this.isCarouselOpen) {
        this.carouselHeight = 500;
        this.isVideoPlaying = true;
      } else {
        this.carouselHeight = 150;
        this.isVideoPlaying = false;
      }
      this.playVideo();
    },
    capture () {
      this.videoCanvas = this.$refs.videoCanvas;
      var videoCanvas = this.videoCanvas
        .getContext("2d")
        .drawImage(this.video, 0, 0, 640, 480);
      this.videoCaptures.push(videoCanvas.toDataURL("image/png"));
      // this.videoCaptures.push(videoCanvas.toDataURL("image/webp"));
    },
    playVideo () {
      navigator.mediaDevices
        .getUserMedia({ video: this.isVideoPlaying })
        .then(stream => {
          console.log(stream, this.$refs.video);
          this.video.srcObject = stream;
        });
    },
    openPost (key = null) {
      // if (!this.isLoggedIn) {
      //   this.$store.commit("setPopupLogin", true);
      //   return;
      // }
      if (key) this.selectedPostRef = this.$refs["post-" + key][0];
      // console.log('clientWidth:', this.selectedPostRef.$el.clientWidth)

      this.selectedPostRef.$el.classList.toggle("active");
      this.isPostOpening = !this.isPostOpening;

      if (this.isPostOpening) {
        setTimeout(() => {
          this.scrollAtPost = window.scrollY;
          this.debouncedScroller = debounce(this.handleScroll, 30);
          window.addEventListener("scroll", this.debouncedScroller);
        }, 1000);
        this.$router.push({ name: 'post', params: { post: 'testing' } });
        // this.$router.push({ name: 'postpage', params: { post: 'testpage' } });
      } else {
        window.removeEventListener("scroll", this.debouncedScroller);
        this.debouncedScroller = null;
        this.$router.back();
      }

    },
    handleScroll (e) {
      if (this.isScrollEventRunning) return;
      this.isScrollEventRunning = true;

      setTimeout(() => {
        if (Math.abs(window.scrollY - this.scrollAtPost) > 0) {
          window.scrollTo({
            top: this.scrollAtPost,
            left: 0,
            behavior: "smooth"
          });
        }
      }, 500);

      setTimeout(() => {
        this.isScrollEventRunning = false;
      }, 1000);
    },
    routeTo (path) {
      this.$router.push({ path: path });
    },
    loadMoreContents () {
      this.contentLoading = true;
    }
  }
};
</script>

<style lang="scss">
#page-box {
  // transform: translateY(-50vh);
  #contents-box {
    .serif {
      font-family: "Times New Roman", Times, serif !important;
    }
    & > .row:first-child {
      padding-top: 150px;
    }
    #head-banner {
      .col {
        padding-top: 0;
        padding-bottom: 0;
        .border-box {
          border-right: 2px solid rgba(255, 255, 255, 0.12);
          padding: 10em 0 1em 0;
          .v-carousel {
            img {
              position: absolute;
              top: -4em;
            }
          }
        }
      }
    }
    .bubble-box {
      padding-bottom: 0;
      margin-bottom: 0;
      overflow-x: hidden;
      #category-box {
        display: flex;
        flex-direction: column;
        padding-bottom: 0;
        max-height: 500px;
        overflow-x: hidden;
        .v-input {
          flex: none;
          .v-input__slot {
            background-color: rgba(100, 100, 100, 0.5);
          }
        }
        .timeline-box {
          display: flex;
          flex-direction: column;
          flex: 1;
          min-width: 30vw;
          overflow-y: scroll;
          .v-timeline {
            flex: 1;
          }
        }
      }
      #bubble-contents-box {
        padding: 0;
        max-height: 500px;
        .v-sheet {
          height: 100%;
          overflow: scroll;
          padding: 1em 0 1em 3em;
          background-color: transparent;
          // background-color: rgba(100, 100, 100, 0.4);
          .bubble-effector {
            width: 100%;
            height: 100%;
            transition: height 5s ease-out;
            &.decreasing {
              height: 0;
            }
          }
          .inspiration-card {
            display: inline-block;
            overflow: hidden;
            transition: max-width 1s, max-height 1s, margin 1s, padding 1s,
              border-radius 0.5s;
            text-overflow: ellipsis;
            max-width: 20em;
            max-height: 20em;
            border-radius: 50% !important;
            align-self: center;
            &.minimized {
              text-align: center;
              max-width: 7em;
              max-height: 7em;
            }
            .keyword {
              overflow: hidden;
              transition: max-width 1s, max-height 1s, padding 1s;
              max-width: 0;
              max-height: 0;
              padding: 0;
              &.minimized {
                max-width: 20em;
                min-height: 7em;
                max-height: 7.5em;
                line-height: 5.5em;
                // padding-bottom: 7em;
              }
              &:not(.minimized) {
                margin: 0 !important;
                padding: 0 !important;
              }
            }
          }
        }
      }
    }
    .issue-box {
      padding-left: 1.5em;
      .v-item-group {
        border-right: 2px solid rgba(255, 255, 255, 0.12);
        .v-card {
          // background-color: rgba(100, 100, 100, 0.5);
          min-height: 0;
          background-color: rgba(100, 100, 100, 0.3);
          font-size: initial;
          transition: color 0.5s, background-color 0.5s, min-height 1s;
          .v-subheader,
          .v-card__text {
            transition: font-size 0.5s;
            transition-delay: 1s;
            overflow: hidden;
          }
          img {
            object-fit: cover;
            max-height: 14em;
            transition: max-height 1s;
          }
          &.active {
            background-color: rgb(200, 200, 200);
            color: black;
            min-height: 80vh;
            max-height: 80vh;
            z-index: 10;
            overflow-y: scroll;
            img {
              max-height: 30em;
            }
            .v-subheader {
              color: black;
              font-size: x-large;
            }
            .v-card__text {
              display: none;
              // padding-top: 0;
              // padding-bottom: 0;
              // height: 0;
              // font-size: larger;
            }
            .v-btn {
              display: none;
              color: black;
            }
          }
        }
      }
    }
    .copyright-box {
      display: flex;
      align-items: right;
      flex-direction: row-reverse;
    }
  }
  #scrim {
    position: fixed;
    top: 0;
    left: 0;
    width: 100vw;
    height: 100vh;
    background-color: black;
    opacity: 0.5;
    z-index: 5;
  }
  #skeleton-loader {
    position: relative;
  }
  #post-card {
    position: fixed;
    // top: 100px;
    top: 0;
    left: 0;
    width: 100%;
    height: 80vh;
    z-index: 15;
  }
}
</style>

<style lang="scss" scoped>
.edge.leftside {
  margin-left: 2.95em !important;
}
</style>
