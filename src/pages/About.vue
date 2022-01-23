<template>
  <Layout>
    <!-- Page Header-->
    <header
      class="masthead"
      :style="`backgroundImage: url('/uploads/snow_df7b13c958.jpg')`"
    >
      <div class="container position-relative px-4 px-lg-5">
        <div class="row gx-4 gx-lg-5 justify-content-center">
          <div class="col-md-10 col-lg-8 col-xl-7">
            <div class="page-heading">
              <h1>About Me</h1>
              <span class="subheading">This is what I do.</span>
            </div>
          </div>
        </div>
      </div>
    </header>
    <!-- Main Content-->
    <main class="mb-4">
      <div class="container px-4 px-lg-5">
        <div class="row gx-4 gx-lg-5 justify-content-center">
          <div class="col-md-10 col-lg-8 col-xl-7">
            <p>
              An idea maker, a visionary, a creative genius — Ismael's
              speciality is turning nothing into something. He’s got a knack for
              taking an idea, giving it a foundation, then building on it to
              create a relevant experience for the public.
            </p>
          </div>
        </div>
      </div>
    </main>
  </Layout>
</template>

<script>
export default {
  name: "AboutPage",
  metaInfo: {
    title: "About Me",
  },
};
</script>
