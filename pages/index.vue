<template>
  <section class="container">
    <div>

      <h1 class="title">
        csibekelteto
      </h1>
      <input type="file" @change="processFile($event)">
      <!-- <input type="file" @change="processFile($event)"> -->
      <h2 class="subtitle">
        Nuxt.js project
      </h2>

    </div>
  </section>
</template>

<script>
import _ from 'lodash'
import axios from 'axios'
import Fuse from 'fuse.js'

export default {
  data: function () {
    return {
      fileinput: 'nothing'
    }
  },
  watch: {
    fileinput: function () {
      var fileinput = this.fileinput.split('\n')
      console.log(fileinput)

      var keys = fileinput[0].split('\t')

      console.log('kulcsok: ', keys)

      var rv = {}
      for (var i = 0; i < fileinput.length; ++i) {
        rv[i] = fileinput[i]
      }

      console.log(rv)
    }
  },
  methods: {
    processFile (event) {
      console.log(event)
      var fajl = event.target.files[0]
      var reader = new FileReader()
      var vm = this
      reader.onload = (e) => {
        vm.fileinput = reader.result
      }
      reader.readAsText(fajl)
    }

  },
  created () {
    axios.get(`http://myviapan.com/api/api.php?type=a&ceg=md&kir=2&rnd=${Math.random()}`)
      .then((response) => {
        console.log('ITT JON AZ EN RESZEM!!!')
        console.log(response.data)
        var t = response.data
        // itt kell dolgozni
        // var obj = deepFind(value, data, options);
        // var obj = deepFindAll(value, data, options);

        var szukitendolista = []
        for (var i = 0; i < _.size(t); i++) {
          // console.log(t[i])
          szukitendolista.push(t[i])
        }
        console.log('az a szukitendo lista: ', szukitendolista)
        var keysofmine = _.keys(szukitendolista[0])
        // var keresettelem
        console.log('the keys', keysofmine)
        var l = [
          {
            title: "Old Man's War",
            author: {
              firstName: 'John',
              lastName: 'Scalzi'
            }
          },
          {
            title: 'The Lock Artist',
            author: {
              firstName: 'Steve',
              lastName: 'Hamilton'
            }
          },
          {
            title: 'HTML5',
            author: {
              firstName: 'Remy',
              lastName: 'Sharp'
            }
          },
          {
            title: 'Right Ho Jeeves',
            author: {
              firstName: 'P.D',
              lastName: 'Woodhouse'
            }
          },
          {
            title: 'The Code of the Wooster',
            author: {
              firstName: 'P.D',
              lastName: 'Woodhouse'
            }
          },
          {
            title: 'Thank You Jeeves',
            author: {
              firstName: 'P.D',
              lastName: 'Woodhouse'
            }
          },
          {
            title: 'The DaVinci Code',
            author: {
              firstName: 'Dan',
              lastName: 'Brown'
            }
          },
          {
            title: 'Angels & Demons',
            author: {
              firstName: 'Dan',
              lastName: 'Brown'
            }
          },
          {
            title: 'The Silmarillion',
            author: {
              firstName: 'J.R.R',
              lastName: 'Tolkien'
            }
          },
          {
            title: 'Syrup',
            author: {
              firstName: 'Max',
              lastName: 'Barry'
            }
          },
          {
            title: 'The Lost Symbol',
            author: {
              firstName: 'Dan',
              lastName: 'Brown'
            }
          },
          {
            title: 'The Book of Lies',
            author: {
              firstName: 'Brad',
              lastName: 'Meltzer'
            }
          },
          {
            title: 'Lamb',
            author: {
              firstName: 'Christopher',
              lastName: 'Moore'
            }
          },
          {
            title: 'Fool',
            author: {
              firstName: 'Christopher',
              lastName: 'Moore'
            }
          },
          {
            title: 'Incompetence',
            author: {
              firstName: 'Rob',
              lastName: 'Grant'
            }
          },
          {
            title: 'Fat',
            author: {
              firstName: 'Rob',
              lastName: 'Grant'
            }
          },
          {
            title: 'Colony',
            author: {
              firstName: 'Rob',
              lastName: 'Grant'
            }
          },
          {
            title: 'Backwards, Red Dwarf',
            author: {
              firstName: 'Rob',
              lastName: 'Grant'
            }
          },
          {
            title: 'The Grand Design',
            author: {
              firstName: 'Stephen',
              lastName: 'Hawking'
            }
          },
          {
            title: 'The Book of Samson',
            author: {
              firstName: 'David',
              lastName: 'Maine'
            }
          },
          {
            title: 'The Preservationist',
            author: {
              firstName: 'David',
              lastName: 'Maine'
            }
          },
          {
            title: 'Fallen',
            author: {
              firstName: 'David',
              lastName: 'Maine'
            }
          },
          {
            title: 'Monster 1959',
            author: {
              firstName: 'David',
              lastName: 'Maine'
            }
          }
        ]
        console.log(l)

        var options = {
          shouldSort: true,
          threshold: 0.1,
          location: 0,
          distance: 100,
          maxPatternLength: 32,
          minMatchCharLength: 1,
          keys: keysofmine
        }
        var fuse = new Fuse(szukitendolista, options) // "list" is the item array
        var result = fuse.search('lektronika')

        console.log('[fuse] - result', result)

        // const keresendo_szavak =
        // [  "Z",
        //   "Elektronika",
        // ]
        //
        // var szukitett_lista = [];
        // var aktualis_talalatok;
        // var db;
        //
        // for (var i = 0; i < keresendo_szavak.length; i++) {
        //     keresettelem = keresendo_szavak[i];
        //     console.log("Most keresett szo: ", keresettelem);
        //     console.log("Ebben a listaban keresek most: ",szukitendolista);
        //
        //     for (var i = 0; i < szukitett_lista.length; i++) {
        //       szukitett_lista[i]
        //     }
        //     console.log("Aktualis talalati lista: ",aktualis_talalatok);
        //
        // }
        //
        // console.log("Vegso talalati lista: ",aktualis_talalatok);
      }).catch((error) => {
        console.error(error)
      })
  }
}
</script>

<style>
.container {
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
}

.title {
  font-family: "Quicksand", "Source Sans Pro", -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, "Helvetica Neue", Arial, sans-serif; /* 1 */
  display: block;
  font-weight: 300;
  font-size: 100px;
  color: #35495e;
  letter-spacing: 1px;
}

.subtitle {
  font-weight: 300;
  font-size: 42px;
  color: #526488;
  word-spacing: 5px;
  padding-bottom: 15px;
}

.links {
  padding-top: 15px;
}
</style>
