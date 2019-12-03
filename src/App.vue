<template>
  <div id="app">
    <div class="text-center">
      <h1>NameGator <i class="far fa-thumbs-up"></i></h1>
      <h6 class="text-secundary">
        Gerador de Nomes
      </h6>
    </div>
    <div id="content">
      <div class="container">

        <div class="row">

          <div class="col-md">
            <h5>Prefixos <span class="badge badge-info">{{ prefixes.length }}</span></h5>
            <div class="card">
              <div class="card-body">
                <ul class="list-group">
                  <li class="list-group-item" v-for="prefix in prefixes" v-bind:key="prefix">
                    <div class="row">
                      <div class="col-md">
                        {{ prefix }}
                      </div>
                      <div class="col-md text-right">
                        <button class="btn btn-danger" v-on:click="deletePrefix(prefix)"><i class="fa fa-trash fa-xs"></i></button>
                      </div>
                    </div>
                    
                  </li>
                </ul>
                <br>

                <div class="input-group">
                  <input type="text" class="form-control" v-model="prefix" v-on:keyup.enter="addPrefix(prefix)" placeholder="Digite o prefixo">
                  <div class="input-group-append">
                    <button class="btn btn-info" v-on:click="addPrefix(prefix)"><i class="fa fa-plus"></i></button>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="col-md">
            <h5>Sufixos <span class="badge badge-info">{{ sufixes.length }}</span></h5>
            <div class="card">
              <div class="card-body">
                <ul class="list-group">
                  <li class="list-group-item" v-for="sufix in sufixes" v-bind:key="sufix">
                    <div class="row">
                      <div class="col-md">
                        {{ sufix }}
                      </div>
                      <div class="col-md text-right">
                        <button class="btn btn-danger" v-on:click="deleteSufix(sufix)"><i class="fa fa-trash fa-xs"></i></button>
                      </div>
                    </div>
                  </li>
                </ul>
                <br>
                <div class="input-group">
                  <input type="text" class="form-control" v-model="sufix" v-on:keyup.enter="addSufix(sufix)" placeholder="Digite o sufixo">
                  <div class="input-group-append">
                    <button class="btn btn-info" v-on:click="addSufix(sufix)"><i class="fa fa-plus"></i></button>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>
        
        <br>

        <h5>Domínios <span class="badge badge-info">{{ domains.length }}</span></h5>
        <div class="row">
          <div class="col-md">
            <div class="card">
              <div class="card-body">
                <ul class="list-group">
                  <li class="list-group-item" v-for="domain in domains" v-bind:key="domain">
                    {{ domain }}
                  </li>
                </ul>
              </div>
            </div>
          </div>          
        </div>
        
      </div>
    </div>
  </div>
</template>

<script>
import "bootstrap/dist/css/bootstrap.css";
import "@fortawesome/fontawesome-free/css/all.css";

export default {
  name: 'app',
  data: ()=> {
    return {
      prefix: "",
      sufix: "",
      prefixes: ["Air", "Jet", "Flight"],
      sufixes: ["Hub", "Station", "Mart"],
      domains: ["AirHub", "AirStation", "AirMart", "JetHub", "JetStation", "JetMart", "FlightHub", "FlightStation", "FlightMart"]
    }
  },
  methods: {
    addPrefix(prefix) {
      this.prefixes.push(prefix);
      this.prefix = "";
      this.generateDomains();
    },
    addSufix(sufix) {
      this.sufixes.push(sufix);
      this.sufix = "";
      this.generateDomains();
    },
    generateDomains() {
      this.domains = [];
      for(const prefix of this.prefixes) {
        for(const sufix of this.sufixes) {
          this.domains.push(prefix + sufix);
        }

      }
    },
    deletePrefix(prefix) {
      this.prefixes.splice(this.prefixes.indexOf(prefix), 1);
      this.generateDomains();
    },
    deleteSufix(sufix) {
      this.sufixes.splice(this.sufixes.indexOf(sufix), 1);
      this.generateDomains();
    }
  },
  components: {
    
  }
}
</script>

<style>
#app {
  margin-top: 30px;
  margin-bottom: 30px;
}

#content {
  background-color: #F1F1F1;
  padding-top: 30px;
  padding-bottom: 30px;
}
</style>