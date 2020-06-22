<template>
  <div class="w-full flex overflow-hidden relative md:pt-12" id="press">
    <h2 class="text-3xl md:text-4xl font-bold font-display absolute top-1">As mentioned by..</h2>

    <a
      :href="activePress.source"
      target="_blank"
      class="w-3/4 md:w-1/3 mt-20 mb-2 md:mb-10 m-auto flex justify-center items-center"
    >
      <img class="m-auto" :src="getImg(activePress.logo)" />
    </a>
  </div>
</template>

<script>
import "swiper/dist/css/swiper.css";
import { swiper, swiperSlide } from "vue-awesome-swiper";

export default {
  data() {
    return {
      activePress: null,
      press: [
        {
          title: "DIY and Open Source care solutions",
          outlet: "IlSole",
          date: "7 May 2017",
          source:
            "http://nova.ilsole24ore.com/progetti/soluzioni-di-cura-in-co-design/",
          logo: "ilsole24ore.png",
          excerpt:
            "Whether it is a ramp for disabled people or self-produced insulin, OpenCare's projects arise from collaboration between users and innovators"
        },
        {
          title: "DIY and Open Source care solutions",
          outlet: "Nesta",
          date: "11 April 2016",
          source: "http://www.nesta.org.uk/blog/era-development-mutants",
          logo: "nesta.png",
          excerpt:
            "Social movements led by self-organising citizens are becoming the cutting edge of development. Establishing effective partnerships with them requires abandoning much of the implicit paternalism that informs development work"
        },
        {
          title:
            "Eleven tips for councils on thinking creatively about adult social care",
          outlet: "The Guardian",
          date: "28 April 2014",
          source:
            "https://www.theguardian.com/local-government-network/2014/apr/28/eleven-tips-councils-thinking-creatively-adult-social-care",
          logo: "guardian.jpg",
          excerpt:
            "They have brought together a whole range of people mainly (but not all!) young and radical. They are doing some incredible work there. Am sorely tempted to head off there and alter the age demographic."
        },
        {
          title:
            "Can Monasteries Be a Model for Reclaiming Tech Culture for Good?",
          outlet: "The Nation",
          date: "27 August 2014",
          source:
            "https://www.thenation.com/article/can-monasteries-be-model-reclaiming-tech-culture-good/",
          logo: "nation.png",
          excerpt:
            "What united [Edgeryders] was not a political ideology, but the dead-end conditions of austerity and the hope of figuring out better ways forward."
        },
        {
          title:
            "Eleven tips for councils on thinking creatively about adult social care",
          outlet: "The New Yorker",
          date: "27 April 2015",
          source:
            "https://www.newyorker.com/magazine/2015/04/27/a-cave-with-a-view",
          logo: "newyorker.jpg",
          excerpt:
            "a group of self-described 'civic hackers' who run a 'social clinic' that embeds 'skilled individuals within communities that could benefit from their presence'."
        },
        {
          title: "When hacktivists live like monks",
          outlet: "Krautreporter",
          date: "12 November 2014",
          source:
            "https://krautreporter.de/111--wenn-hacktivisten-wie-monche-leben",
          logo: "krautreporter.png",
          excerpt:
            "..steps towards solving the major problems plaguing small towns such as Matera: massive land run-off, reduction of social services in the wake of European austerity measures, and not least unused housing stock."
        },
        {
          title: "Mutiny at UnMonastery, coworking in the land of Edgeryders",
          outlet: "Mutinerie",
          date: "11 November 2013",
          source:
            "http://magazine.mutinerie.org/edgeryders-unmonastery-coworking/",
          logo: "mutinerie.png",
          excerpt:
            "..an agile organization of individuals pooling know-how and professional networks at the service of social innovation."
        },
        {
          title:
            "Care by communities: non-zero sum provision of health and social care",
          outlet: "Re:publica",
          date: "4 May 2016",
          source:
            "https://16.re-publica.de/16/session/care-communities-non-zero-sum-provision-health-and-social-care",
          logo: "republica.png",
          excerpt:
            "We explore amazing care services that communities are providing - right now - to people that the state and private business have let down."
        },
        {
          title: "The unMonastery: a commune for the internet age",
          outlet: "Dazed",
          date: "25 November 2014",
          source:
            "http://www.dazeddigital.com/artsandculture/article/22717/1/the-unmonastery-a-commune-for-the-internet-age",
          logo: "dazed.png",
          excerpt:
            "Edgeryders built an Internet commune in Matera, a city similar to Petra in Jordan. They are both among the oldest inhabited settlements in the world."
        },
        {
          title:
            "UNDP Innovation Facility driving multiple projects in Indonesia through broad partnerships",
          outlet: "OpenGov",
          date: "18 July 2017",
          source:
            "http://www.opengovasia.com/articles/7815-undp-innovation-facility-driving-multiple-projects-in-indonesia-through-broad-partnerships",
          logo: "opengov.png",
          excerpt:
            "Edgeryders is a leading innovation partner of UNDP for testing new ways of working."
        },
        {
          title:
            "'No patriarchy. No hierarchy. No God.' - unMonastery is a monastery for tech utopians",
          outlet: "Wired",
          date: "29 January 2015",
          source:
            "https://www.wired.de/collection/life/das-kommt-heraus-wenn-tech-utopisten-ein-kloster-grunden",
          logo: "wired.png",
          excerpt: ""
        },
        {
          title: "New Thinker's Dream Government",
          outlet: "Di",
          date: "10 April 2014",
          source:
            "http://www.di.se/artiklar/2014/4/10/nytankarens-dromregering/",
          logo: "di.png",
          excerpt:
            "Our co-founder Nadia EL-Imam was named Minister of Labour in an ideal government for Sweden in the country's leading financial newspaper."
        },
        {
          title: "La Politica Tecnologica",
          outlet: "HuffPost",
          date: "4 June 2013",
          source:
            "http://www.huffingtonpost.it/andrea-latino/la-politica-tecnologica_b_3382521.html",
          logo: "huffpost.jpg",
          excerpt:
            "Now imagine those data available to ministries, entrusted to qualified young people of our best faculties, and listening to citizens through massive open collaboration, on the model of the European Edgeryders project."
        }
      ],
      slideOptions: {
        effect: "fade",
        autoplay: {
          delay: 2000
        },
        slidesPerView: 1,
        slidesPerColumn: 1,
        slidesPerGroup: 1,
        spaceBetween: 30,
        slidesPerColumnFill: "row",

        breakpoints: {
          640: {
            slidesPerView: 1,
            slidesPerColumn: 1,
            slidesPerGroup: 1,
            spaceBetween: 120,
            centeredSlides: true,
            spaceBetween: 30,
            slidesPerColumnFill: "row"
          }
        }
      }
    };
  },
  methods: {
    getImg(value) {
      return require("../assets/press/" + value);
      // The path could be '../assets/img.png', etc., which depends on where your vue file is
    }
  },
  components: {
    swiper,
    swiperSlide
  },
  mounted: function() {
    this.activePress = this.press[0];
    var counter = 0;
    setInterval(
      function() {
        if (counter == this.press.length - 1) {
          counter = 0;
        } else {
          counter = counter + 1;
        }
        this.activePress = this.press[counter];
      }.bind(this),
      2500
    );
  },
  props: ["data"]
};
</script>

<style type="text/css" lang="scss">
#press {
  height: 400px;
  overflow: hidden;
  text-align: center;
  display: flex;
  justify-content: center;
  a {
  }
}
#press {
  .mention {
    display: flex;
    justify-content: center;
    align-items: center;
    width: 400px;
    height: 300px;
    border-right: 1px solid #ddd;
    img {
      width: 70%;
      margin: 0px auto;
    }
    &#Di,
    &#OpenGov {
      img {
        width: 35%;
      }
    }
    &#Nesta {
      img {
        width: 55%;
      }
    }
    &#IlSole {
      img {
        width: 65%;
      }
    }
  }
  h3 {
    font-size: 1.8em !important;
    margin: 20px 0 60px;
  }
  .hooper {
    height: 200px !important;
    margin-top: 30px;
    width: 80% !important;
    margin: 0 auto !important;
  }
  .press_slide {
    .mention {
      height: 200px;
    }
  }

}

@media (max-width: 860px) {
  #press {
    margin-bottom: 0 !important;
    padding-bottom: 20px !important;
    padding-top: 20px !important;
height: 300px;
    h1 {
      font-size: 1.6em !important;
    }
    .mention {
      border-right: none !important;
      width: 100%;
      img {
        width: 100%;
      }
    }
    .hooper {
      width: 100% !important;
    }
  }
}
</style>