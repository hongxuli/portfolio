<template>
  <div class="projects-Main">
    <div class="projects-Top">
      <header class="projects-Header">
        <nuxt-link :to="localePath('index')" class="projects-Home">Home</nuxt-link>
        <nuxt-link
          :to="localePath('projects', isEnPage ? 'zh' : 'en')"
          class="projects-LangSwitch"
        >{{ isEnPage ? '中文' : 'English' }}</nuxt-link>
      </header>
      <div class="projects-Intro">
        <h1 v-t="'projectIntro[0]'" />
      </div>
    </div>
    <ul class="projects-Projects">
      <li v-for="p in projects" :key="p.id">
        <project-card :project="p" />
      </li>
    </ul>
  </div>
</template>

<script>
import ProjectCard from '@/components/ProjectCard.vue'
import projects from '@/projects'

export default {
  components: {
    ProjectCard
  },
  head() {
    return {
      title: 'Projects'
    }
  },
  data() {
    return {
      projects
    }
  },
  computed: {
    isEnPage() {
      return this.$route.name.endsWith('en')
    }
  }
}
</script>

<style lang="scss">
.projects-Main {
  height: 100%;
  background: #f9f9f9;
}

$top-projects-spacing: 200px;
$intro-font-color: #fff;

.projects-Top {
  position: relative;
  padding: 20px 20px $top-projects-spacing;
  color: $intro-font-color;

  &::before {
    content: '';
    position: absolute;
    top: 0;
    bottom: 0;
    left: 0;
    right: 0;
    margin: auto;
    background-image: linear-gradient(315deg, #00838f 0%, #b2ebf2 74%);
    transform: skewY(-4deg);
    transform-origin: top left;
  }
}

.projects-Header {
  position: relative;
  display: flex;
  justify-content: space-between;
}

.projects-Home {
  font-weight: bold;
  color: inherit;
}

.projects-LangSwitch {
  text-decoration: none;
  width: 5em;
  height: 1.5em;
  line-height: 1.5em;
  text-align: center;
  border: 1px solid $intro-font-color;
  border-radius: 4px;
  color: $intro-font-color;
  transition: all 0.4s;

  &:hover {
    text-decoration: none;
    color: #333;
    background: $intro-font-color;
  }
}

.projects-Intro {
  position: relative;
  text-align: center;
  color: $intro-font-color;
}

.projects-Projects {
  position: relative;
  margin: (40px-$top-projects-spacing) 0 0;
  padding: 0 20px;
  display: flex;
  flex-direction: column;
  align-items: center;

  > li {
    list-style-type: none;
  }
}

html[lang^='zh'] {
  .projects-Intro {
    h1 {
      letter-spacing: 2px;
    }

    p {
      font-size: smaller;
    }
  }
}
</style>
