<template>
  <div class="container flow flex crew">
    <h1 class="numbered-title"><span>02</span> Meet your Crew</h1>
    <div class="content">
      <div v-if="member" class="img-container flex">
        <img class="member-picture" :src="member['webp-image'].guid" alt="" />
      </div>
      <div class="dot-indicators flex">
        <button
          v-for="(item, index) in crew"
          :key="index"
          @click="setMember(index)"
        ></button>
      </div>
      <div class="container flex member-info" v-if="member">
        <div class="uppercase ff-serif member-role">{{ member['role'] }}</div>
        <div class="uppercase ff-serif fs-700 member-name">
          {{ member['crew-name'] }}
        </div>
        <p class="text-accent">{{ member.bio }}</p>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      crew: [],
      active: 0,
    }
  },
  computed: {
    member() {
      return this.crew[this.crew.length - 1 - this.active]
    },
  },
  methods: {
    async loadData() {
      const response = await fetch(
        'https://space.wp.seiwald.hak-stjo.schulwebspace.at/wp-json/wp/v2/crew'
      )
      this.crew = await response.json()
    },
    setMember(value) {
      this.active = value
    },
  },
  mounted() {
    this.loadData()
    document.body.style.backgroundImage = "url('background-crew-mobile.jpg')"
  },
}
</script>

<style scoped>
.crew {
  flex-direction: column;
  align-items: center;
}
.member-info {
  flex-direction: column;
  align-items: center;
  text-align: center;
}
img {
  height: 223px;
}
.member-role {
  font-size: 16px;
  color: hsl(var(--clr-white) / 0.25);
}
.member-name {
  font-size: 24px;
}

.img-container {
  width: 90vw;
  border-bottom: 2px solid hsl(var(--clr-white) / 0.25);
  justify-content: center;
}

.numbered-title {
  font-size: 16px;
}

.content {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 3rem;
}

.text-accent {
  font-size: 15px;
  line-height: 25px;
}

@media screen and (min-width: 480px) {
  .content {
    flex-direction: column-reverse;
    gap: 2rem;
  }

  .img-container {
    height: 400px;
    flex-direction: column;
    justify-content: flex-end;
    align-items: center;
  }

  .member-picture {
    height: 100%;
  }

  .member-role {
    font-size: 24px;
    line-height: 28px;
  }

  .member-name {
    font-size: 40px;
    line-height: 46px;
  }

  .text-accent {
    font-size: 16px;
    line-height: 28px;
  }

  .numbered-title {
    margin-top: 2rem;
    font-size: 20px;
    line-height: 24px;
    /* identical to box height */
    letter-spacing: 3.375px;
    align-self: flex-start;
  }
}
</style>
