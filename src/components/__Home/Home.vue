<template src="./Home.html"></template>
<script>
  import axios from 'axios';

  const API_URL = 'http://words.bighugelabs.com/api/2/abb4ea52ee15dfd20ed5bb3ed79d7138/';
  const TYPE = 'json';

  export default {
    name: 'Home',
    data() {
      return {
        title: 'Synonymy',
        word: null,
        synonyms: null,
        wordTypes: null,
        loading: false,
        responseObject: null,
      };
    },
    methods: {
      getSynonyms() {
        this.synonyms = []; // Clear old data.
        // Call API and get synonym
        this.loading = true; // Set loaded on.
        console.log(this.word);
        this.getSynsFromAPI()
        .then((response) => {
            this.responseObject = response.data;
            console.dir(this.responseObject);

            this.wordTypes = Object.getOwnPropertyNames(response.data);

            this.wordTypes.forEach((element) => {
              console.log(element);
              console.log(this.responseObject[element]);
              // let synArray = this.responseObject[element].syn;
              // console.log(synArray.join(' '));
              // this.synonyms.push.apply(synArray);
            });

            // if (this.responseObject.hasOwnProperty('noun')) {
            //     this.synonyms = this.responseObject.noun.syn;
            // } else {
            //     this.synonyms = null;
            // }
        })
        .catch((exception) => {
            console.dir(exception);
        })
        .then(() => {
            console.log('Finished API Call');
            this.loading = false;
        });
        console.dir(this.synonyms);
      },

      getSynsFromAPI() {
        return axios({
          method: 'get',
          url: API_URL + this.word + '/' + TYPE,
        });
      },
    },
  };

</script>
<style lang="scss" scoped src="./Home.scss">


</style>
