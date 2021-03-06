<template>
  <div>
    <section class="lc-container-0">
      <div class="lc-container-1">
        <div class="lc-container-2">
          <header-flag />
        </div>
      </div>
    </section>

    <section class="lc-container-0 lc-header lc-mobile-hide">
      <div class="lc-container-1">
        <div class="underlay gray" />
        <div class="lc-container-2">
          <site-header :isShowAccountButton="true" />
        </div>
      </div>
    </section>

    <hero-video />

    <section class="lc-container-0">
      <div class="lc-container-1">
        <div class="lc-container-2">
          <div class="lc-container-3">
            <div class="social-links-container-mobile lc-tablet-pc-hide lc-padding-vertical-8">
              <platform-icon-bar />
            </div>
          </div>
        </div>
      </div>
    </section>

    <cta-section />

    <likecoin-stack class="lc-margin-top-32" />

    <road-map class="lc-margin-top-48" />

    <token-distribution class="lc-margin-top-48" />

    <early-adopters class="lc-margin-top-48" />

    <press-coverage class="lc-margin-top-48" />

    <advisors class="lc-margin-top-48" />

    <early-supporters class="lc-margin-top-48" />

    <team class="lc-margin-top-48" />

    <section class="lc-container-0">
      <div class="lc-container-1">
        <div class="lc-container-2">
          <div class="lc-container-3">
            <div class="social-links-container-mobile lc-tablet-pc-hide lc-padding-vertical-12">
              <platform-icon-bar />
            </div>
          </div>
        </div>
      </div>
    </section>

    <cta-section class="bottom" />

    <section class="lc-container-0 lc-community lc-mobile-hide">
      <div class="lc-container-1">
        <div class="lc-container-2">
          <div class="lc-container-3">

            <div class="lc-community-content lc-padding-top-24 lc-margin-bottom-64">
              <div class="platforms">
                <span>{{ $t('Home.Community.title') }}</span>
                <platform-icon-bar />
              </div>
              <div class="faq">
                <a
                  ref="noopener"
                  :href="$t('Home.Community.button.faqLink')"
                  class="lc-color-like-green lc-underline lc-font-size-20"
                  target="_blank"
                >
                  {{ $t('Home.Community.button.faq') }}
                </a>
              </div>
            </div>

          </div>
        </div>
      </div>
    </section>

  </div>
</template>


<script>
/* global fbq */
import { mapGetters } from 'vuex';

import MaterialButton from '~/components/MaterialButton';
import SiteHeader from '~/components/header/HeaderWithMenuButton';
import PlatformIconBar from '~/components/PlatformIconBar';

import Advisors from '~/components/about/Advisors';
import CTASection from '~/components/about/CTASection';
import Carousel from '~/components/about/Carousel';
import HeroVideo from '~/components/about/HeroVideo';
import HeaderFlag from '~/components/about/Flag';
import EarlyAdopters from '~/components/about/EarlyAdopters';
import EarlySupporters from '~/components/about/EarlySupporters';
import PressCoverage from '~/components/about/PressCoverage';
import LikecoinStack from '~/components/about/Stack';
import RoadMap from '~/components/about/RoadMap';
import Team from '~/components/about/Team';
import TokenDistribution from '~/components/about/TokenDistribution';

const images = require.context('../../assets/home');
const imgUrl = path => images(`./${path}`);

export default {
  name: 'home',
  layout: 'index',
  components: {
    Advisors,
    Carousel,
    'cta-section': CTASection,
    EarlyAdopters,
    EarlySupporters,
    HeaderFlag,
    HeroVideo,
    MaterialButton,
    PlatformIconBar,
    PressCoverage,
    LikecoinStack,
    RoadMap,
    SiteHeader,
    Team,
    TokenDistribution,
  },
  computed: {
    ...mapGetters([
      'getUserInfo',
      'getUserIsRegistered',
    ]),
  },
  head() {
    return {
      title: this.$t('Home.Flag.title'),
      meta: [
        {
          hid: 'description',
          name: 'description',
          content: this.$t('Home.Flag.content'),
        },
        {
          hid: 'og_description',
          property: 'og:description',
          content: this.$t('Home.Flag.content'),
        },
        {
          hid: 'og_image',
          property: 'og:image',
          content: 'https://like.co/images/og/sale.png',
        },
      ],
    };
  },
  mounted() {
    fbq('track', 'ViewContent');

    const { hash } = document.location;
    if (hash) {
      const element = document.querySelector(hash);
      if (element) element.scrollIntoView();
    }
  },
  methods: {
    imgUrl,
  },
};
</script>


<style lang="scss" scoped>
@import "~assets/variables";

$carousel-height: 488px;

.lc-community {
  font-size: 20px;

  .lc-community-content {
    display: flex;
    flex-direction: row;

    > div {
      display: flex;
      align-items: center;
      flex-direction: row;

      &.platforms {
        flex: 2;

        > span {
          margin-right: 16px;
        }
      }

      &.faq {
        flex: 1;
        justify-content: center;
      }
    }
  }
}

.cta-section.bottom {
  @media (min-width: 600px) {
    margin-top: 64px;
  }
}

.social-links-container-mobile {
  display: flex;
  justify-content: center;
}

</style>
