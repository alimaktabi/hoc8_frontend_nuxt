<template>
  <div class="banner">
    <h1>
      <v-icon size="60px" color="white">mdi-help-circle</v-icon>
      سوالات متداول
      <v-icon size="60px" color="white">mdi-help-circle</v-icon>
    </h1>
    <v-expansion-panels accordion class="accordion">
      <v-expansion-panel v-for="question in questions">
        <v-expansion-panel-header>{{
          question.title
        }}</v-expansion-panel-header>
        <v-expansion-panel-content class="panelContent">
          {{ question.content }}
        </v-expansion-panel-content>
      </v-expansion-panel>
    </v-expansion-panels>
  </div>
</template>

<script>
export default {
  name: "Questions",
  data() {
    return {
      questions: [
        {
          title: " زنگ برنامه نویسی(Hour of Code) چیست؟ ",
          content:
            "\n" +
            "Hour of Code یا زنگ برنامه‌نویسی یک رویداد جهانی هست که توسط Code.org ایجاد شده و با هدف آشنایی دانش‌آموزان با علوم کامپیوتر و گسترش مشارکت در این زمینه، هرساله در هفتۀ جهانی آموزش علوم کامپیوتر برگزار می‌شود. این رویداد در تلاش است تا با از بین بردن باورهای غلط نشان دهد که هر کسی، با هر سن، جنسیت و پیش‌زمینه‌ای می‌تواند به یادگیری‌ علوم کامپیوتر و برنامه نویسی بپردازد.\n",
        },
        {
          title: "چرا برنامه نویسی؟",
          content:
            "یادگیری برنامه‌نویسی می‌تواند طرز تفکر منطقی، خلاقیت و همچنین ذهنیت حل‌ مسئلهٔ ما را تقویت کند؛ مهارت‌هایی که نه‌ تنها در زمینه کاری به ما کمک می‌کنند بلکه در زندگی و هنگام مواجهه با مسائل مختلف نیز مفید هستند. برنامه‌نویسی به ما کمک می‌کند که مشکلات را از زاویهٔ جدیدی ببینیم، با استفاده از خلاقیت خود برای مشکلات دنیای واقعی راه‌حل‌های نوآورانه ارائه دهیم و جهان پیرامون خود را به مکان بهتری تبدیل کنیم.\n",
        },
        {
          title: "چطور میتونم داخل همایش شرکت کنم؟",
          content:
            "به راحتی! کافیه در سایت ثبت‌نام کنید و منتظر باشید تا برای شرکت در همایش بهتون خبر بدیم!\nتوی همین سایت، بالا سمت چپ، گزینه ثبت‌نام رو انتخاب کنید. بعد از کامل کردن هر مرحله، به مرحله بعد برید و در نهایت پرداخت رو انجام بدین. تبریک میگم، شما با موفقیت ثبت‌نام شدین!\n",
        },
        {
          title: "توی همایش چه چیزهایی یاد میگیرم؟ ",
          content:
            "هدف از این همایش، آشنایی شما با مفاهیم اولیه برنامه‌نویسی از طریق آموزش‌های جذاب با مباحثی مثل تفکر الگوریتمی و مهارت حل مسئله است.",
        },
        {
          title: "همایش مناسب چه افرادیه؟",
          content:
            "همه دانش‌آموزانی که دوست دارند با برنامه‌نویسی آشنا شده و وارد این دنیای جذاب بشوند!",
        },
        {
          title: "همایش به صورت حضوری برگزار میشه؟",
          content:
            "خیر! امسال علاوه بر کلاس های حضوری، کلاس‌ها به صورت آنلاین هم برگزار می‌شوند.",
        },
        {
          title: "مدت زمان همایش چقدره و چه روزهایی برگزار میشه؟",
          content:
            "هر گروه از شما دانش‌آموزان ۲ روز به صورت حضوری - مجازی به دانشگاه میاین و آموزش می‌بینین. علاوه بر اون، ۴ روز دیگه هم براتون ویدیوهایی به صورت مجازی قرار میدیم که با مباحث جالبی آشنا بشین و لذت ببرین. در انتها هم توی مراسم جشن اختتامیه در دانشگاه، در خدمت همهٔ شما دانش‌آموزان عزیز خواهیم بود. :)",
        },
        {
          title: "آیا ظرفیت ثبت نام محدوده؟ ",
          content:
            "بله ! پس هر چه زودتر ثبت نام کنید، توی همایش منتظرتون هستیم :)",
        },
      ],
    };
  },
};
</script>

<style scoped>
.banner {
  background: linear-gradient(104.71deg, #00adaa 11.26%, #00928f 90.55%);
  position: relative;
  padding: 110px 0;
}

.accordion-button::after {
  margin-right: auto;
  margin-left: 0 !important;
}

h1 {
  color: white;
  display: flex;
  flex-direction: row;
  justify-content: center;
  align-items: center;
  gap: 20px;
  margin-bottom: 60px;
}

.v-expansion-panels {
  width: 920px;
  height: 568px;
  background: #fefefe;
  box-shadow: 0px 4px 4px rgba(0, 0, 0, 0.25);
  border-radius: 15px;
}

.v-expansion-panel-header {
  color: #004948;
}

.panelContent {
  color: #004948;
}

.accordion {
  max-width: calc(100% - 20px);
  margin-right: 10px;
}

@media screen and (min-width: 1000px) {
  .banner {
    width: 100%;
    height: 684px;
    padding: 110px;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
  }
}
</style>
