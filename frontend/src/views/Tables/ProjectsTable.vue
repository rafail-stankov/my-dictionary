<template>
  <div class="card shadow"
       :class="type === 'dark' ? 'bg-default': ''">
    <div class="card-header border-0"
         :class="type === 'dark' ? 'bg-transparent': ''">
      <div class="row align-items-center">
        <div class="col">
          <h3 class="mb-0" :class="type === 'dark' ? 'text-white': ''">
            {{name}}
          </h3>
        </div>
        <div class="col text-right">
          <base-button type="primary" size="sm">See all</base-button>
        </div>
      </div>
    </div>

    <div class="table-responsive big-enough">
      <base-table class="table align-items-center table-flush"
                  :class="type === 'dark' ? 'table-dark': ''"
                  :thead-classes="type === 'dark' ? 'thead-dark': 'thead-light'"
                  tbody-classes="list"
                  :data="tableData.slice(this.from, this.to)">
        <template slot="columns">
          <th>Dictionary</th>
          <th>Number of words</th>
          <th>Foreign language</th>
          <th>Familiar language</th>
          <th>Last updated on</th>
          <th>Labels</th>
          <th>Completion</th>
          <th></th>
        </template>

        <template slot-scope="{row}">
          <th scope="row">
            <div class="media align-items-center">
              <div class="icon-shape">
                <i class="ni ni-book-bookmark text-dark"></i>
              </div>
              <div class="media-body">
                <span class="name mb-0 text-sm">{{row.name}}</span>
              </div>
            </div>
          </th>
          <td>
            {{row.number_of_words}}
          </td>
          <td>
            <img alt="Image placeholder" class="square-image-nm" :src="getImgUrl(row.main_language_abbreviation)">
          </td>
          <td>
            <img alt="Image placeholder" class="square-image-nm" :src="getImgUrl(row.secondary_language_abbreviation)">
          </td>
          <td>
            {{row.updated_at}}
          </td>
          <td>
            <div class="avatar-group">
              <a v-for="(label, index) in row.labels.slice(0, 5)" :key="index" href="#" class="avatar avatar-sm rounded-circle" data-toggle="tooltip" data-original-title="Jessica Doe" :style="'background-color:' + label.colour">
                <span>{{getAbbreviation(label.name)}}</span>
              </a>
              <a v-if="row.labels.length > 5" href="#" class="avatar avatar-sm rounded-circle" data-toggle="tooltip" data-original-title="Jessica Doe" style="background-color:#989898">
                <span>..</span>
              </a>
            </div>
          </td>

          <td>
            <div class="d-flex align-items-center">
              <span class="completion mr-2">{{row.completion}}%</span>
              <div>
                <base-progress :type="colorForCompletion(row.completion)"
                               :show-percentage="false"
                               class="pt-0"
                               :value="row.completion"/>
              </div>
            </div>
          </td>

          <td class="text-right">
            <base-dropdown class="dropdown"
                           position="right">
              <a slot="title" class="btn btn-sm btn-icon-only text-light" role="button" data-toggle="dropdown" aria-haspopup="true" aria-expanded="false">
                <i class="fas fa-ellipsis-v"></i>
              </a>

              <template>
                <a class="dropdown-item" href="#">Inspect</a>
                <a class="dropdown-item" href="#">Edit</a>
                <a class="dropdown-item" href="#">Delete</a>
              </template>
            </base-dropdown>
          </td>

        </template>

      </base-table>
    </div>

    <div class="card-footer d-flex justify-content-end"
         :class="type === 'dark' ? 'bg-transparent': ''">
      <base-pagination :perPage="this.perPage" :total="tableData.length" v-on:input="changePage($event)"></base-pagination>
    </div>

  </div>
</template>
<script>
  export default {
    name: 'projects-table',
    props: {
      type: {
        type: String
      },
      title: String,
      perPage: {
        type: Number,
        default: 3
      }
    },
    data() {
      return {
        name: 'Your dictionaries',
        from: 0,
        to: 1,
        tableData: [
          {
            name: 'Swedish-English dict',
            number_of_words: 236,
            labels: [
              {
                id: 13,
                colour: 'red',
                name: "Noun"
              },
              {
                id: 17,
                colour: '#0080FF',
                name: "Verb"
              },
              {
                id: 25,
                colour: '#228B22',
                name: "Adjective"
              },
              {
                id: 37,
                colour: '#008080',
                name: "Adverb"
              },
              {
                id: 38,
                colour: '#0FF080',
                name: "Adverb"
              },
              {
                id: 41,
                colour: '#8B4513',
                name: "Pronoun"
              }
            ],
            main_language_abbreviation: 'se',
            secondary_language_abbreviation: 'en',
            updated_at: '06.11.2020',
            completion: 23
          },
          {
            name: 'Spanish-English dict',
            number_of_words: 357,
            labels: [
              {
                id: 26,
                colour: '#228B22',
                name: "Adjective"
              },
              {
                id: 35,
                colour: '#008080',
                name: "Adverb"
              }
            ],
            main_language_abbreviation: 'es',
            secondary_language_abbreviation: 'en',
            updated_at: '08.09.2017',
            completion: 44
          },
          {
            name: 'German-English dict',
            number_of_words: 350,
            labels: [
              {
                id: 26,
                colour: '#228B22',
                name: "Adjective"
              },
              {
                id: 35,
                colour: '#008080',
                name: "Adverb"
              }
            ],
            main_language_abbreviation: 'de',
            secondary_language_abbreviation: 'en',
            updated_at: '17.06.2016',
            completion: 83
          }
        ]
      }
    },
    methods:{
      getImgUrl: function(abbreviation) {
        var images = require.context('../../assets/images', false, /\.png$/)
        return images('./' + abbreviation + ".png")
      },
      colorForCompletion: function(number){
        if(number >= 0 && number <= 20){
          return "red";
        } else if(number <= 40){
          return "orange";
        } else if(number <= 60){
          return "yellow";
        } else if(number <= 80){
          return "green";
        } else if(number <= 100){
          return "blue";
        } else {
          return "black";
        }
      },
      getAbbreviation: function(name){
        if(name.length > 0){
          return name[0].toUpperCase();
        } else {
          return "";
        }
      },
      changePage(p){
        this.from = (p - 1) * this.perPage;
        this.to =  p * this.perPage;
      }
    }
  }
</script>
<style>
</style>
