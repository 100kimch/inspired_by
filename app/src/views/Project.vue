<template>
  <v-container class="pt-0">
    <custom-appbar id="app-bar" :topic="topic" />
    <div id="contents-box">
      <v-layout
        id="card-contents"
        class="d-flex justify-space-between flex-wrap overflow-y-auto pa-3"
      >
        <v-row>
          <v-col class="col-title pb-0" cols="12" md="8">
            <div class="head-content">
              <span id="circle" ref="circle"></span>
              <span>
                <h2 class="project-type">Github Project</h2>
                <h1 class="main-title">Explore, and Do.</h1>
                <p>
                  This project is an web application for private blogging.
                  <br />
                  There is a wish to design my own contents in my own layout just like a magazine.
                  MIT License is applied so all users can use and enjoy this project. {{line_pos_y}}, {{line_width}}
                </p>
                <v-btn text color="primary">
                  <v-icon left>mdi-arrow-right</v-icon>See Wiki
                </v-btn>
                <v-btn text color="primary">
                  <v-icon left>mdi-github-face</v-icon>Go to github
                </v-btn>
              </span>
            </div>
          </v-col>
          <v-col cols="12" md="4">
            <v-card>
              <v-parallax
                style="{'margin-top': -150px}"
                height="700"
                src="../assets/sample_project.jpeg"
              ></v-parallax>
            </v-card>
          </v-col>
        </v-row>
        <v-row class="horizontal-line"></v-row>
        <v-row class="subheader-box">
          <v-col class="pt-0 mt-0 pr-0">
            <div class="leftside edge reversed"></div>
            <div id="title-subheader">
              <span>Summary</span>
            </div>
            <div class="rightside edge reversed"></div>
          </v-col>
        </v-row>
        <v-row class="summary-box">
          <v-col class="px-5">
            <v-expansion-panels>
              <v-expansion-panel v-for="(message, i) in messages" :key="i" hide-actions>
                <v-expansion-panel-header>
                  <v-row align="center" class="spacer" no-gutters>
                    <v-col cols="4" sm="2" md="1">
                      <v-avatar size="36px">
                        <img
                          v-if="message.avatar"
                          alt="Avatar"
                          src="https://avatars0.githubusercontent.com/u/9064066?v=4&s=460"
                        />
                        <v-icon v-else :color="message.color" v-text="message.icon"></v-icon>
                      </v-avatar>
                    </v-col>

                    <v-col class="hidden-xs-only" sm="5" md="3">
                      <strong v-html="message.name"></strong>
                      <span v-if="message.total" class="grey--text">&nbsp;({{ message.total }})</span>
                    </v-col>

                    <v-col class="text-no-wrap" cols="5" sm="3">
                      <strong v-html="message.title"></strong>
                    </v-col>
                  </v-row>
                </v-expansion-panel-header>

                <v-expansion-panel-content>
                  <v-divider></v-divider>
                  <v-card-text v-text="lorem"></v-card-text>
                </v-expansion-panel-content>
              </v-expansion-panel>
            </v-expansion-panels>
          </v-col>
        </v-row>
        <v-row class="subheader-box">
          <v-col class="pt-0 mt-0 pr-0" cols="12">
            <div class="leftside edge"></div>
            <div id="title-subheader">
              <span>Wiki</span>
            </div>
            <div class="rightside edge"></div>
          </v-col>
        </v-row>
        <v-row class="py-0 px-5 content-box">
          <v-card class="ma-0 py-2 px-5">
            <v-row>
              <v-col cols="12" md="9">
                <vue-markdown>{{ content }}</vue-markdown>
              </v-col>
            </v-row>
          </v-card>
        </v-row>
        <v-row class="subheader-box">
          <v-col class="pt-0 mt-0 pr-0">
            <div class="leftside edge reversed"></div>
            <div id="title-subheader">
              <span>Issues</span>
            </div>
            <div class="rightside edge reversed"></div>
          </v-col>
        </v-row>
        <v-row class="copyright-box align-center mb-3">
          <v-card flat class="ma-1 pa-0 mt-0">
            <v-card-text class="px-3 py-1">2020 ⓒ KJHRicky</v-card-text>
          </v-card>
        </v-row>
      </v-layout>
    </div>
  </v-container>
</template>

<script>
export default {
  name: "HelloWorld",
  data: () => ({
    line_width: 100,
    line_pos_y: 0,
    messages: [
      {
        avatar: 'https://avatars0.githubusercontent.com/u/9064066?v=4&s=460',
        name: 'John Leider',
        title: 'Welcome to Vuetify.js!',
        excerpt: 'Thank you for joining our community...',
      },
      {
        color: 'red',
        icon: 'people',
        name: 'Social',
        new: 1,
        total: 3,
        title: 'Twitter',
      },
      {
        color: 'teal',
        icon: 'local_offer',
        name: 'Promos',
        new: 2,
        total: 4,
        title: 'Shop your way',
        exceprt: 'New deals available, Join Today',
      },
    ],
    lorem: 'Lorem ipsum dolor sit amet, at aliquam vivendum vel, everti delicatissimi cu eos. Dico iuvaret debitis mel an, et cum zril menandri. Eum in consul legimus accusam. Ea dico abhorreant duo, quo illum minimum incorrupte no, nostro voluptaria sea eu. Suas eligendi ius at, at nemore equidem est. Sed in error hendrerit, in consul constituam cum.',
    content: `
# Setting up a frontend web app

- Author: Kim Jihyeong(KJHRicky@gmail.com)
- Written in Nov 20, 2019

## Overview

This document gives a way to make a frontend web application with Vue. The steps below are exactly same as "inspired_by" blog.

## Create a vue project with vue-cli

> For information on how to use Vue CLI 3, visit [official documentation](https://cli.vuejs.org/guide/)

- What I chose:

## Install vuetify

- They say:

> Vuetify is a Vue UI Library with beautifully handcrafted Material Components. No design skills required — everything you need to create amazing applications is at your fingertips.

        `
  }),
  created () {
    for (let i in this.topics) {
      this.topics[i]["top"] = this.randomPosY() + "vh";
      this.topics[i]["left"] = this.randomPosX() + "vw";
    }
  },
  mounted () {
    this.line_pos_y = this.$refs['circle'].offsetTop
    this.line_width = this.$refs['circle'].offsetLeft
    console.log('circle: ', this.line_width, this.line_pos_y)
  },
  computed: {
    topic () {
      return this.$store.getters.getTopic;
    },
  },
  methods: {
  }
};
</script>

<style lang="scss" scoped>
.container {
  padding-top: 0 !important;
  #contents-box {
    #card-contents {
      .col-title {
        margin-top: 360px;
        .head-content {
          display: flex;
          #circle {
            width: 3rem;
            height: 3rem;
            border-radius: 50%;
            border: 2px solid rgba(255, 255, 255, 0.13);
            margin-top: 2.25em;
            margin-left: 0.5rem;
            margin-right: 1rem;
            &:before {
              content: "";
              display: block;
              width: 1.7em;
              height: 1.7em;
              margin: 0.5em;
              border-radius: 50%;
              background: rgba(255, 255, 255, 0.5);
            }
          }
          span:last-child {
            flex: 1;
          }

          .project-type {
            text-transform: uppercase;
            font-size: 1em;
            padding-left: 0.5em;
            margin-bottom: -0.75em;
          }
          .main-title {
            font-size: 4rem;
          }

          p {
            padding-right: 3rem;
          }
        }
      }
      .horizontal-line {
        width: 100%;
        height: 300px;
        border-left: 2px solid rgba(255, 255, 255, 0.12);
        margin-left: 2em;
        margin-top: -300px;
      }
      .subheader-box {
        width: 100%;
        .col {
          display: flex;
          margin-top: -2em;
          margin-bottom: 1.1em;
          #title-subheader {
            flex: 1;
            text-align: center;
            padding-top: 0;
            border-bottom: 2px solid rgba(255, 255, 255, 0.12);
            span {
              position: relative;
              top: 1.2em;
              background: #424242;
              border-radius: 0.5em;
              color: #999;
              font-size: medium;
              padding: 0.25em 0.5em;
            }
          }
          .edge {
            display: block;
            width: 2em;
            height: 2em;
            // margin-top: -0.9em;
            // margin-bottom: -2em;
            border: 2px solid rgba(255, 255, 255, 0.12);
            &.leftside {
              position: relative;
              margin-left: 2em;
            }
            &.rightside {
              position: relative;
            }
            &.leftside:not(.reversed) {
              top: calc(2em - 2px);
              border-bottom: none;
              border-right: none;
              border-top-left-radius: 2em;
            }
            &.rightside:not(.reversed) {
              top: 0;
              border-top: none;
              border-left: none;
              border-bottom-right-radius: 2em;
            }
            &.reversed.leftside {
              top: 0;
              border-top: none;
              border-right: none;
              border-bottom-left-radius: 2em;
            }
            &.reversed.rightside {
              top: calc(2em - 2px);
              border-bottom: none;
              border-left: none;
              border-top-right-radius: 2em;
            }
          }
        }
      }
      .summary-box {
        margin-left: 2em;
        border-right: 2px solid rgba(255, 255, 255, 0.12);
      }
      .content-box {
        margin-left: 2em;
        border-left: 2px solid rgba(255, 255, 255, 0.12);
        .v-card {
          background-color: rgba(100, 100, 100, 0.3);
        }
      }
      .copyright-box {
        display: flex;
        align-items: right;
        flex-direction: row-reverse;
      }
    }
  }
}
</style>

<style lang="scss">
.v-expansion-panel {
  background-color: rgba(100, 100, 100, 0.3) !important;
}
</style>