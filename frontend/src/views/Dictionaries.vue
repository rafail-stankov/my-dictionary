<template>
    <div>
        <base-header type="gradient-success" class="pb-6 pb-8 pt-5 pt-md-8">
            <!-- Card stats -->
            <div class="row">
                <div class="col-xl-6 col-lg-6">
                    <stats-card title="Create a new dictionary"
                    type="gradient-orange"
                    icon="ni ni-book-bookmark text-purple"
                    class="mb-4 mb-xl-0">

                    <template slot="footer">
                      <a href="#" data-toggle="tooltip" data-original-title="Ryan Tompson">
                        <img alt="Image placeholder" class="square-image-lg" style="margin-top:10px;margin-right:5px" src="@/assets/images/en.png">
                      </a>
                      <a href="#" data-toggle="tooltip" data-original-title="Ryan Tompson">
                        <img alt="Image placeholder" class="square-image-lg" style="margin-top:10px;margin-right:5px" src="@/assets/images/de.png">
                      </a>
                      <a href="#" data-toggle="tooltip" data-original-title="Ryan Tompson">
                        <img alt="Image placeholder" class="square-image-lg" style="margin-top:10px;margin-right:5px" src="@/assets/images/fr.png">
                      </a>
                      <a href="#" data-toggle="tooltip" data-original-title="Ryan Tompson">
                        <img alt="Image placeholder" class="square-image-lg" style="margin-top:10px;margin-right:5px" src="@/assets/images/es.png">
                      </a>
                      <a href="#" data-toggle="tooltip" data-original-title="Ryan Tompson">
                        <img alt="Image placeholder" class="square-image-lg" style="margin-top:10px;margin-right:5px" src="@/assets/images/ru.png">
                      </a>
                      <a href="#" data-toggle="tooltip" data-original-title="Ryan Tompson">
                        <img alt="Image placeholder" class="square-image-lg" style="margin-top:10px;margin-right:5px" src="@/assets/images/ita.png">
                      </a>
                      <a href="#" data-toggle="tooltip" data-original-title="Ryan Tompson">
                        <img alt="Image placeholder" class="square-image-lg" style="margin-top:10px;margin-right:5px" src="@/assets/images/tu.png">
                      </a>
                      <a href="#" data-toggle="tooltip" data-original-title="Ryan Tompson">
                        <img alt="Image placeholder" class="square-image-lg" style="margin-top:10px;margin-right:5px" src="@/assets/images/cn.png">
                      </a>
                      <a href="#" data-toggle="tooltip" data-original-title="Ryan Tompson">
                        <img alt="Image placeholder" class="square-image-lg" style="margin-top:10px;margin-right:5px" src="@/assets/images/jp.png">
                      </a>
                      <a href="#" data-toggle="tooltip" data-original-title="Ryan Tompson">
                        <img alt="Image placeholder" class="square-image-lg" style="margin-top:10px;margin-right:5px" src="@/assets/images/se.png">
                      </a>
                      <!-- <a href="#" data-toggle="tooltip" data-original-title="Ryan Tompson">
                        <img alt="Image placeholder" class="square-image-lg" style="margin-top:10px;margin-right:5px" src="@/assets/images/bg.png">
                      </a> -->
                    </template>
                  </stats-card>
                </div>
                <div class="col-xl-6 col-lg-6">
                    <stats-card title="Explore dictionaries"
                                type="gradient-red"
                                subTitle="Suggested for you:"
                                icon="ni ni-world text-dark"
                                class="mb-4 mb-xl-0">

                        <template slot="footer">
                            <span class="text-nowrap">1. Dictionary name 35</span>
                            <span class="text-yellow mr-2"> <i class="fas fa-star"></i></span><br />
                            <span class="text-nowrap">2. Dictionary name 18</span>
                            <span class="text-yellow mr-2"> <i class="fas fa-star"></i></span><br />
                            <span class="text-nowrap">3. Dictionary name 15</span>
                            <span class="text-yellow mr-2"> <i class="fas fa-star"></i></span>
                        </template>
                    </stats-card>
                </div>
            </div>
        </base-header>

        <div class="container-fluid mt--7">
            <div class="row">
                <div class="col">
                    <projects-table title="Light Table"></projects-table>
                </div>
            </div>
            <!-- <div class="row mt-5">
                <div class="col">
                    <projects-table type="dark" title="Dark Table"></projects-table>
                </div>
            </div> -->
        </div>

    </div>
</template>
<script>
  import ProjectsTable from './Tables/ProjectsTable'
  export default {
    name: 'tables',
    components: {
      ProjectsTable
    }
  };
</script>
<style></style>
