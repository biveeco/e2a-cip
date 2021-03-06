<template>
  <article>
    <header
      :class="[
        space.paddingHorizontal,
        space.paddingVerticalNarrow,
        color.well,
        border.bottom,
        base.header
      ]"
    >
      <BaseGutterWrapper
        :class="base.leftPane"
        gutterY="xnarrow"
        gutterX="xnarrow"
      >
        <BaseHeading
          :class="display.inlineBlock"
          :centered="false"
          scale="zeta"
          color="dark"
          weight="regular"
          sub
          >{{ $t("home.chooseLanguage") }}</BaseHeading
        >
        <!-- Language selector -->
        <LanguageSwitcher />
      </BaseGutterWrapper>
      <!-- EIPs -->
      <BaseGutterWrapper
        :class="base.rightPane"
        gutterY="xnarrow"
        gutterX="xnarrow"
      >
        <BaseGutterWrapper gutterX="xnarrow" gutterY="xnarrow">
          <BaseButtonLink
            :to="this.$t('nav.userGuidePDF')"
            :router="false"
            :label="this.$t('nav.userGuide')"
            :target="this.checkElectron() ? '_self' : '_blank'"
            role="default"
            size="small"
          />
        </BaseGutterWrapper>
        <BaseGutterWrapper
          :class="[space.marginLeftNarrow]"
          gutterX="xnarrow"
          gutterY="xnarrow"
        >
          <BaseButtonLink
            :to="this.$t('nav.eipPdf')"
            :router="false"
            :label="this.$t('nav.learnMore')"
            :target="this.checkElectron() ? '_self' : '_blank'"
            role="default"
            size="small"
          />
        </BaseGutterWrapper>
      </BaseGutterWrapper>
    </header>

    <BaseWidthWrapper
      :class="[
        space.paddingVerticalWide,
        space.paddingHorizontal,
        border.bottom
      ]"
    >
      <BaseGutterWrapper :class="base.logoGrid">
        <div :class="base.logo">
          <img
            src="@/assets/images/logos/usaid-lockup.svg"
            alt="USAID and E2A"
          />
        </div>
        <div :class="base.logoSmall">
          <img src="@/assets/images/logos/pathfinder.png" alt="Pathfinder" />
        </div>
        <div :class="base.logoSmall">
          <img src="@/assets/images/logos/ouaga.png" alt="OP" />
        </div>
      </BaseGutterWrapper>
    </BaseWidthWrapper>

    <!-- Intro -->
    <BasePageIntro
      :title="$t('home.title')"
      :subtitle="$t('home.subtitle')"
      :blurb="$t('home.intro')"
    />

    <!-- How it works -->
    <BaseSectionWrapper>
      <BaseWidthWrapper width="wide">
        <BasePageIntro
          :title="$t('home.stepsTitle')"
          :subtitle="$t('home.stepsIntro')"
        />
      </BaseWidthWrapper>
      <BaseWidthWrapper :class="space.paddingTop" width="xwide">
        <BaseStepList :steps="steps" size="small" />
      </BaseWidthWrapper>
    </BaseSectionWrapper>

    <!-- Get started! -->
    <BaseSectionWrapper :class="type.center" el="div" border>
      <BaseButtonLink
        :to="{ name: 'plan' }"
        :label="$t('home.getStartedButton').toUpperCase()"
        size="large"
        role="primary"
      />
      <div>
        <ClearItems :clear-type="['All']" :class="space.marginTop" />
      </div>
    </BaseSectionWrapper>

    <!-- Offline versions -->
    <BaseSectionWrapper v-if="!electron" :class="color.well" el="div" border>
      <BaseHeading :level="2" centered>{{
        $t("home.downloadTitle")
      }}</BaseHeading>
      <BaseWidthWrapper :class="space.paddingTop">
        <BaseBodyText
          :content="$t('home.downloadBlurb')"
          :class="base.centeredSubheads"
        />
        <BaseGutterWrapper
          :class="[space.paddingTop, type.center]"
          gutterX="xnarrow"
          gutterY="xnarrow"
        >
          <li :class="base.gutterItem">
            <BaseButtonLink
              :to="$t('home.downloadMacUrl')"
              :label="$t('home.downloadMac')"
              :router="false"
            />
          </li>
          <li :class="base.gutterItem">
            <BaseButtonLink
              :to="$t('home.downloadWindowsPortableUrl')"
              :label="$t('home.downloadWindowsPortable')"
              :router="false"
            />
          </li>
        </BaseGutterWrapper>
      </BaseWidthWrapper>
    </BaseSectionWrapper>

    <!-- Acknowledgements -->
    <BaseSectionWrapper border>
      <BaseHeading :level="2" scale="gamma">{{
        $t("home.acknowldgementTitle")
      }}</BaseHeading>
      <BaseWidthWrapper :class="space.paddingTop">
        <BaseBodyText
          :content="$t('home.acknowledgementText')"
          :class="base.centeredSubheads"
          size="zeta"
        />
      </BaseWidthWrapper>
    </BaseSectionWrapper>
  </article>
</template>

<script>
import i18n from "@/i18n.js";
import LanguageSwitcher from "@/components/LanguageSwitcher.vue";
import BasePageIntro from "@/components/BasePageIntro.vue";
import BaseWidthWrapper from "@/components/BaseWidthWrapper.vue";
import BaseSectionWrapper from "@/components/BaseSectionWrapper.vue";
import BaseHeading from "@/components/BaseHeading.vue";
import BaseBodyText from "@/components/BaseBodyText.vue";
import BaseGutterWrapper from "@/components/BaseGutterWrapper.vue";
import BaseStepList from "@/components/BaseStepList.vue";
import BaseButtonLink from "@/components/BaseButtonLink.vue";
import ClearItems from "@/components/ClearItems.vue";
import { dataMethods } from "@/components/mixins/dataMethods";
import { initData } from "@/components/mixins/initData.js";

export default {
  name: "Home",
  components: {
    LanguageSwitcher,
    BasePageIntro,
    BaseSectionWrapper,
    BaseWidthWrapper,
    BaseHeading,
    BaseBodyText,
    BaseGutterWrapper,
    BaseStepList,
    BaseButtonLink,
    ClearItems
  },
  mixins: [dataMethods, initData],
  data() {
    return {
      electron: this.checkElectron()
    };
  },
  computed: {
    steps() {
      return Object.values(i18n.messages[i18n.locale].home.steps).map(
        (step, index) => {
          return {
            title: this.$t(`home.steps.step${index + 1}.title`),
            blurb: this.$t(`home.steps.step${index + 1}.blurb`)
          };
        }
      );
    }
  }
};
</script>

<style src="styles/spacing.scss" lang="scss" module="space"></style>
<style src="styles/borders.scss" lang="scss" module="border"></style>
<style src="styles/type.scss" lang="scss" module="type"></style>
<style src="styles/color.scss" lang="scss" module="color"></style>
<style src="styles/display.scss" lang="scss" module="display"></style>

<style lang="scss" module="base">
@import "~styleConfig/breakpoints";
@import "~styleConfig/scale";
@import "~styleConfig/type";
@import "~styleConfig/spacing";

.header {
  display: flex;
}

.leftPane {
  width: 50%;
  flex: 1;
}

.rightPane {
  width: 50%;
  flex: 1;

  align-items: center;
  justify-content: flex-end;
  display: inline-flex;
}

.logoGrid {
  text-align: center;
}

.logo {
  display: inline-block;
  max-width: 36rem;
  vertical-align: middle;

  @include media(">small") {
    min-width: 30rem;
  }

  // for IE
  > img[src$=".svg"] {
    width: 100%;
    height: 100%;
  }
}

.logoSmall {
  composes: logo;
  max-width: 16em;

  @include media(">small") {
    min-width: 13rem;
  }
}

.centeredSubheads {
  // center all heading elements
  $list: ();
  @each $i in [1, 2, 3, 4, 5, 6] {
    $list: append($list, unquote("h#{$i}"), "comma");
  }

  #{$list} {
    text-align: center;
  }
}

.gutterItem {
  display: inline-block;
}
</style>
