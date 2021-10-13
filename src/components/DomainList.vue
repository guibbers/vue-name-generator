<template>
  <div>
    <div id="main">
      <div class="container">
        <div class="row">
          <div class="col-md">
            <AppItemList
              title="Prefixos"
              :items="prefixes"
              @addItem="addPrefix"
              @deleteItem="deletePrefix"
            ></AppItemList>
          </div>
          <div class="col-md">
            <AppItemList
              title="Sufixos"
              :items="sufixes"
              @addItem="addSufix"
              @deleteItem="deleteSufix"
            ></AppItemList>
          </div>
        </div>
        <br />
        <h5>
          Domínios: <span>{{ this.domains.length }}</span>
        </h5>
        <div class="card">
          <div class="card-body">
            <ul class="list-group">
              <li
                class="list-group-item"
                v-for="domain in domains"
                :key="domain.name"
              >
                <div class="row">
                  <div class="col-md text-start">{{ domain.name }}</div>
                  <div class="col-md text-end">
                    <a
                      class="btn btn-primary"
                      :href="domain.checkout"
                      target="blank"
                    >
                      <span class="fa fa-shopping-cart"></span>
                    </a>
                  </div>
                </div>
              </li>
            </ul>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import 'bootstrap/dist/css/bootstrap.css'
import 'font-awesome/css/font-awesome.css'
import AppItemList from './AppItemList.vue'

export default {
  name: 'Home',
  components: {
    AppItemList,
  },
  data() {
    return {
      prefixes: ['Air', 'Jet', 'Flight'],
      sufixes: ['Hub', 'Station', 'Mart'],
      prefix: '',
      sufix: '',
    }
  },

  methods: {
    addPrefix(prefix) {
      this.prefixes.push(prefix)
      this.prefix = ''
    },
    deletePrefix(prefix) {
      this.prefixes.splice(this.prefixes.indexOf(prefix), 1)
    },
    addSufix(sufix) {
      this.sufixes.push(sufix)
      this.sufix = ''
    },
    deleteSufix(sufix) {
      this.sufixes.splice(this.sufixes.indexOf(sufix), 1)
    },
  },

  computed: {
    domains() {
      const domains = []
      for (const prefix of this.prefixes) {
        for (const sufix of this.sufixes) {
          const name = prefix + sufix
          const url = name.toLowerCase()
          const checkout = `https://checkout.hostgator.com.br/?a=add&sld=${url}&tld=.com.br`
          domains.push({ name, checkout })
        }
      }
      return domains
    },
  },
}
</script>
